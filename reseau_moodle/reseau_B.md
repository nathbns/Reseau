# Architecture en couches

Transmission de l'information, c'est quoi une liaison? Les supports de transmission?

## Transmission de l'information:

- 2 grandes catégories de transmission:
  - (données multimédias (son, image, vidéo))
  - données discret et finis (ex: un fichier de n'imp type):
    - ce fichier a un debut et une fin, il peut facilement etre traduit en séquence binaire.
  - données continues: correspond a la variation continu d'un phéno physique comme la voix, temp, lumière, etc...

Quel que soit le type de données, on doit se ramener à une séquence binaire avant de générer un signal adapté au support de transmission.
Et donc à l'inverse quand un support reçoit la séquence binaire il doit faire la conversion inverser pour avoir le signal analogique.
Op donnée -> seq binaire ==> Codage
op seq binaire -> donnée ==> Decodage

### Techniques de transmission:

![Techniques de transmission 1 et 2](public/signal.png)

#### (Figure 1) Méthode "transmission en bande de base":

La carte réseau utilise un codeur et un decodeur. Permettant la traduction la seq binaire en un signal qui circule sur le cable Ethernet.
La carte reseau peut transmettre le signal electrique sur un support en cuivre. Méthode relativement simple.

#### (Figure 2) Méthode "transmission par modulation du signal analogique sur la liaison":

Transmettre un signal analogique modulé sur a la liaison. (utilisée pour transmettre des signaux sans fil à des fréquences diff).
avtg: transmettre +sieurs signaux dans un meme espace grace a des fréquences diff. Couvre plus grand distance (+km).

#### liaison

1 carte reseau ---------- liaison ---------- 1 carte reseau

On a bien une carte reseau de chaque coté de la liaison. Et un support de transmission entre les deux.
En gros la carte reseau prend un seq binaire (provenant de l'app, ou équipement) et génère le signal adapté au support de transmission.

### Supports de transmission:

- cable en cuivre (connecteur RJ45 === port Ethernet):
  - distance: paire torsader < cable coaxial (meilleur débit)
- fibre optique:
  - transmission d'onde lumineuse (30km de porté sans répéteur, encore meilleur débit)
- antennes: reseau sans fil (WIFI, reseau mobile, reseau tv, radio)
- satelite:
  - debit élevé / latence très faible
  - cout élevé

Ils peuvent tous subir des interférences pendant leurs transmission provoquant des erreurs.
Erreur == quand un bit change de valeur pendant la transmission.

**Dans un reseau**:

- Équipement terminaux (ordi, imprimante) != Équipement intermédiaire (routeurs, commutateurs, borne WIFI, pare-feu, répéteurs)
- Les différents supports de transmissions (liaison sans-fil, filaire local (LAN), longue distance (WAN), fibre optique, satellite).

### Modes de transmissions:

**full-duplex**: deux cartes reseau peuvent envoyer et recevoir des signaux simultanément. (reseau sans-fil / filaire).
**simplex**: ne permet l'envoi de signaux que dans un seul sens. (antennes de radio et de television, pas capable de transmettre des données).
**half-duplex**: possible d'envoyer **ou** de recevoir des signaux mais pas simultanément.
**liaison point-à-point**: il n'y a que 2 cartes reseau qui communiquent entre elles sur une seule et meme liaison.
**liaison multipoints**: plusieurs carte reseau qui communiquent sur le meme support de transmission. (+sieurs ordi sur borne WIFI).

- 2 problématique de la **liaison multipoints**:
  - nécessaire d'attribuer des adresses uniques aux différentes cartes reseau pour identifier les équipements qui communiquent entre eux
    et savoir quelle carte reseau émet le signal et quelle carte reseau doit en etre destinataire.
  - il faut gérer le partage du support de transmission, qui a le droit d'émettre.

### Différentes topologies de liaison:

**Topologies**:

- **le bus**: consiste à une liaison multipoints avec plusieurs ordinateurs ou cartes reseau, toutes relié par un unique support de liaison, le **bus central**.
- **en étoile**: équipement central, auquel sont reliées les cartes reseau. (utilisé pour les reseau locaux, ex: box, wifi)
- problème commun aux deux de dessus: si l'équipement intermédiaire tombe en panne, plus de reseau.
- **en anneau**: chaque équipement est relié à deux autres équipements, le précédent et le suivant.
- **maillée**:
  - chaque équipements est relié à +sieurs autres.
  - on a donc +sieurs chemin possible entre deux équipements.
  - en cas de panne on a des alternatives de chemin.
  - souvent utilisé en reseau, pour avoir de la redondance et de la tolérance à la panne.
  - cout élevé
  - si chaque équipement relié à **tous** les autres alors => **topologie maillée totale**. O(n^2) si n équipements.

## Les architectures protocolaires:

ex: Archi TCP/IP fait fonctionner internet.

### Architectures en couche et encapsulation:

**modèle de référence OSI (Open Systems Interconnexion)**: rassemble dans une seule archi, toutes les bases présentes dans tous les reseau.
**architecture protocolaire**:

- les protocoles applicatifs: definit pour chaque appli, comment elle doit échanger des données.
- les protocoles de transport: permet de définir comment transporter l'info d'un émetteur à un récepteur.
- les protocoles de liaison: proche du matériel et servent à transmettre un signal sur une liaison de transmission.
- Tous exec, dans l'app, le syst. exploit. et la carte reseau.

### Protocole:
