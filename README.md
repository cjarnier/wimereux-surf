# Prévisions de surf — Côte d'Opale

Notation des sessions de **surf** à **Wimereux** et à
**Calais**, calculée toutes les 3 heures par GitHub Actions et publiée sur une
page consultable au téléphone, avec des alertes quand une bonne session se
profile.

Les deux spots ne se ressemblent pas et sont paramétrés séparément :

| | Wimereux | Calais | Siouville |
|---|---|---|---|
| Bouée de référence | Hastings (CEFAS) | Sandettie | aucune : modèle au large de la Hague |
| La plage regarde vers | l'ouest-nord-ouest | le nord | l'ouest |
| Fenêtre de houle | 200-270° | 300-60° | 225-315° |
| Optimum de marée (surf) | 1 h après la PM | 1 h 30 avant la PM | 2 h avant ou après la PM |
| Période de houle visée | 5,5 à 7,5 s | 4,5 à 6,5 s | 7 à 11 s |
| Port de marée | Boulogne-sur-Mer | Calais | Diélette |
| Taille où la plage sature | — | — | note en baisse de 2 à 3 m |
| Trajet depuis chez toi (Wimille) | 10 min | 35 min | 4 h 45 |
| Alertes | oui | oui | non, page seulement |

## Comment la note est construite

**Principe commun.** Chaque note est une *moyenne géométrique* de sous-notes
sur 5. Contrairement à une moyenne ordinaire, un critère mauvais n'y est pas
compensé par les autres : une houle parfaite ne sauve pas un vent pourri. Tous
les barèmes sont continus, sans marche où deux centimètres ou un degré
feraient basculer la note. Le seul véto restant est l'orage, parce qu'il
relève de la sécurité : risque élevé, note nulle ; risque modéré, note
plafonnée à 2,5.

**Surf** = houle (poids 0,5) × vent (0,3) × marée (0,2).

- *Houle* : jusqu'à 3 points de hauteur et 2 de période, plus ou moins un
  demi-point selon le type de déferlement (nombre d'Iribarren) et selon la
  part d'énergie portée par la houle longue ; le tout multiplié par la
  fenêtre de direction, qui s'éteint progressivement sur 15° au lieu de
  couper net.
- *Vent* : projeté sur l'axe de la plage, il passe continûment d'une courbe
  « offshore » à une courbe « onshore » selon l'angle ; les rafales retirent
  jusqu'à un point et demi.
- *Marée* : position dans le cycle × stabilité de la zone de déferlement
  (vitesse à laquelle le bord de l'eau se déplace sur l'estran).
- *Petits jours* : sous 0,70 m, la houle reçoit un plancher modeste (1 point
  à 0,45 m, 1,6 à 0,70 m), et le poids du vent passe progressivement de 30 à
  45 % — sur une petite mer, c'est la propreté du plan d'eau qui décide.
  Résultat : 0,45 m à 5 s ressort autour de 2,5 par temps calme, de quoi
  aller jeter un œil, mais retombe vers 1 dès que l'onshore s'en mêle. Rien
  sous 0,30 m. Sous un point de houle, la note globale s'efface
  proportionnellement, pour éviter les sauts près de zéro.
- Le RTR (marnage rapporté à la houle) est affiché mais n'entre plus dans la
  note : il dépend du coefficient, comme la stabilité, et le compter deux fois
  pénalisait doublement les vives-eaux.

**Sessions chantier.** Une mer formée (au moins ~0,9 m) mais hachée par le
vent n'est pas une belle session, mais elle se surfe en shortboard si on est
motivé. Au-delà de 0,8 m, la note de vent reçoit un plancher qui monte avec
la hauteur (1,5 à 1 m, 1,8 dès 1,4 m) : ces journées remontent vers 2,3-2,9
au lieu de 1,5-2, sans rivaliser avec une vraie bonne session. Le plancher
s'efface entre 22 et 30 nœuds de vent : au-delà, c'est une machine à laver.
Les heures chantier sont hachurées sur la page et ont leurs propres alertes
(`PLANCHER_VENT_CHANTIER`, `HOULE_CHANTIER_M`, `VENT_CHANTIER`,
`VENT_MAX_CHANTIER_KT`).

**Planche conseillée.** Pour chaque heure, les deux planches du quiver les
mieux adaptées, la meilleure d'abord. Chaque planche a une note d'adéquation
sur 5, somme de trois termes réglés dans `PLANCHES` :

- une courbe selon la *hauteur* : le mini-mal 7'4 domine sous 0,5 m, le fish
  5'6 de 0,5 à 1,2 m, la Rocket 5'9 au-delà ;
- un bonus ou malus selon la *période* : une mer courte et molle favorise le
  volume, une mer plus longue et creuse favorise la Rocket ;
- un terme *clapot*, actif seulement quand la mer est formée (de 0,7 à
  1,1 m) et désordonnée (note de vent basse) : la Rocket, qui se canarde
  facilement, y gagne jusqu'à 1,5 point, le fish y perd un point.

Quelques repères : 0,4 m à 5 s par temps calme → mini-mal ; 0,6 à 1 m propre
→ fish ; 1 m à 6 s avec 18 nœuds d'onshore → Rocket ; 1,2 m à 8 s propre →
Rocket, fish en second. Le tableau affiche la taille (7'4, 5'6, 5'9) faute de
place ; le nom complet est dans l'infobulle et le résumé.

**Équipement.** Chaque créneau indique l'épaisseur de combinaison et les
accessoires conseillés. On part de la température de l'eau (au large du
spot), refroidie de 0,25 °C par degré d'écart quand l'air ressenti est plus
froid que l'eau (3 °C au plus) et de 0,1 °C par nœud de vent au-delà de 12
(2 °C au plus). La température effective donne : 3/2 dès 16 °C, 4/3 dès 13,
5/4 dès 10, 6/5 en dessous ; chaussons sous 13 °C, gants sous 11, cagoule
sous 9. Le résumé du jour est prudent : il retient l'eau la plus froide,
l'air ressenti le plus froid et le vent le plus fort de la journée.

**Sessions.** On note des heures, mais on surfe des sessions : la « meilleure
session » est la meilleure fenêtre de deux heures consécutives de jour.

**Fiabilité.** Chaque note porte une confiance entre 0 et 1, qui baisse avec
l'échéance et quand les modèles se contredisent. Sur la page, les carrés
d'une prévision peu fiable sont plus pâles.

## Mise en route

1. **Crée un dépôt public** sur GitHub et pousse ces fichiers dedans.
   Le dépôt doit être public : GitHub Pages sur dépôt privé est réservé aux
   comptes payants. Aucune donnée sensible n'y circule — la clé d'API reste
   dans les secrets, seul le résultat calculé est publié.

2. **Récupère une clé api-maree.fr** (gratuit) sur https://api-maree.fr/,
   puis dans le dépôt : *Settings → Secrets and variables → Actions →
   New repository secret*, nom `API_MAREE_KEY`.

3. **Vérifie les identifiants des sites de marée.** Appelle une fois
   `https://api-maree.fr/sites?key=TA_CLE` et cherche les points les plus
   proches de chaque spot. Si ce ne sont pas `boulogne-sur-mer` et `calais`,
   ajoute des *variables* (et non des secrets) nommées `SITE_MAREE_WIMEREUX`,
   `SITE_MAREE_CALAIS` et `SITE_MAREE_SIOUVILLE`.

4. **Active Pages** : *Settings → Pages → Source : Deploy from a branch →
   Branch `main`, dossier `/docs`*. La page sera sur
   `https://TON-COMPTE.github.io/NOM-DU-DEPOT/`.

5. **Lance une première fois à la main** : onglet *Actions → Prévisions
   Wimereux → Run workflow*. Sans ça, `docs/data.json` n'existe pas encore et
   la page affichera un message d'erreur.

6. **Sur l'iPhone** : ouvre la page dans Safari, *Partager → Sur l'écran
   d'accueil*. **Sur le Mac** (macOS Sonoma ou plus récent) : dans Safari,
   *Fichier → Ajouter au Dock*. Elle s'ouvre ensuite comme une application.

## Réglages

Tout se règle en tête de `previsions.py`. Le dictionnaire `SPOTS` contient ce
qui distingue les deux spots :

| Clé | Rôle |
|---|---|
| `point_houle`, `point_vent` | points de calcul — à garder figés |
| `direction_houle`, `marge_direction` | fenêtre de houle et largeur de son extinction |
| `pic_maree_h` | optimum de marée surf, en heures par rapport à la PM ; une liste pour plusieurs optimums |
| `axe_offshore_surf` | direction de vent idéale pour le surf, issue de l'expérience |
| `trajet_min` | temps pour être à l'eau, utilisé par les alertes |
| `alertes` | `False` pour un spot affiché sur la page sans jamais notifier (Siouville) |
| `seuils_houle` | barème de houle propre au spot ; `h_trop` (facultatif) fait baisser la note quand la plage sature |
| `pente_haute`, `pente_basse` | profil de plage, pilote Iribarren et la translation — **estimations** |

Réglages communs :

| Constante | Rôle |
|---|---|
| `POIDS_SURF`, `POIDS_MAREE` | poids des moyennes géométriques |
| `POIDS_SURF_PETIT`, `HAUTEUR_PETIT_JOUR`, `PETITE_HOULE` | réglage des petits jours glassy |
| `VENT_OFFSHORE`, `VENT_ONSHORE` | courbes de note de vent surf selon la force |
| `PLANCHES` | ton quiver : nom, libellé court, volume (pour mémoire), courbes `hauteur` et `periode`, coefficient `clapot` |
| `HAUTEUR_CLAPOT` | hauteurs entre lesquelles le clapot commence à peser sur le choix de planche |
| `COMBINAISONS`, `CHAUSSONS`, `GANTS`, `SEUIL_CAGOULE` | barème d'équipement selon la température effective |
| `DUREE_SESSION_H` | durée d'une session, 2 h par défaut |
| `FIABILITE_ECHEANCE` | baisse de confiance avec l'échéance |
| `CALIBRATION_HOULE` | facteur correctif de hauteur |
| `CAPE_*`, `LI_*` | seuils de risque orageux |

Les courbes s'écrivent comme des listes de points `(valeur, note)` reliés par
des segments : pour déplacer un seuil, on déplace un point.

## La bouée d'Ambleteuse

La bouée houlographe de Géodunes, mouillée au large d'Ambleteuse à quelques
kilomètres au nord de Wimereux, est lue à chaque calcul. Sa dernière mesure
s'affiche en haut de la page de Wimereux (« En ce moment »), avec la source.

Chaque mesure est aussi archivée dans `observations/ambleteuse.csv`, à côté de
ce que le modèle prévoyait pour la même heure : hauteur, période, direction,
température de l'eau et vent. C'est la base de la calibration à venir — dans
quelques semaines, ce fichier dira de combien le modèle se trompe devant chez
toi, et dans quelles conditions. Une même heure n'est archivée qu'une fois.

Si la bouée est muette (maintenance, perte de signal), l'outil continue sans
elle.

### Alerte « bonne surprise »

À chaque calcul, la mesure de la bouée est notée avec le barème surf : la houle
mesurée remplace la houle prévue, le vent, la marée et le risque d'orage restent
ceux de l'heure. Si cette note mesurée atteint 3,5 et dépasse d'au moins un
point la note que la prévision donnait pour la même heure, une notification
part en priorité haute : les conditions sont meilleures que prévu, maintenant.

Elle ne part que pour une mesure de moins de deux heures, de jour, et une seule
fois par épisode (pas de nouvelle alerte de ce type pendant six heures). Les
seuils se règlent en tête d'`alerter.py` (`SEUIL_SURPRISE`, `ECART_SURPRISE`).

Le calcul tourne toutes les trois heures : l'alerte peut donc arriver jusqu'à
trois heures après le début de l'embellie.

## Le journal

Tous les réglages ci-dessus sont des hypothèses raisonnables, pas des mesures.
Le journal est ce qui les rendra justes.

### Remplir

Le plus simple : le bloc **Noter une session ou une observation** en bas de
la page. Il prépare la ligne, la copie, et ouvre `journal.csv` en édition sur
GitHub ; il ne reste qu'à coller à la fin du fichier et valider.

Format d'une ligne :

```
date,heure,spot,discipline,type,conditions,session,planche,commentaire
2026-09-27,16,wimereux,surf,session,4,3,Fish 5'6,belles séries mais du monde
2026-09-28,11,calais,surf,observation,2,,,trop haché pas sorti
```

- `discipline` : toujours `surf` (colonne gardée pour la compatibilité).
- `type` : `session` si tu étais à l'eau, `observation` si tu as seulement
  regardé la mer.
- `conditions` : la qualité de la mer et du vent, de 1 à 5. C'est **elle**
  qu'on compare à la note calculée.
- `planche` : la planche utilisée, pour une session seulement.
- `session` : ton plaisir, de 1 à 5, vide pour une observation. Il dépend
  aussi de la fatigue, du monde à l'eau et du matériel ; il est conservé mais
  jamais comparé au modèle.

**Note aussi les jours où tu n'y vas pas.** Tu iras surtout quand la
prévision est bonne : sans observations, tu n'apprendrais que les erreurs par
excès d'optimisme, jamais les bonnes journées que le calcul a ratées. Depuis
Wimereux, un coup d'œil à la mer suffit.

Les lignes à l'ancien format (`date,heure,spot,note,commentaire`) restent
lues : la note unique vaut alors pour les conditions et la session.

### Analyser

```
python3 analyser.py
python3 analyser.py --spot calais
```

Le script affiche l'écart entre conditions observées
et note calculée, compte les bonnes conditions ratées et les fausses
promesses, classe les critères selon leur lien avec les conditions observées,
montre comment la prévision se dégrade avec son ancienneté, et dresse un
bilan par planche : dans quelle houle tu l'as prise, ce que tu en as pensé,
et combien de fois elle correspondait au conseil. C'est ce bilan qui servira
à recaler les courbes de `PLANCHES`. En dessous
d'une douzaine d'entrées, les corrélations sont du bruit, et le script le
dit.

Règle d'or : ajuster peu de paramètres, les plus influents d'abord. Avec une
vingtaine de réglages et quelques dizaines d'entrées, tout retoucher revient à
caler l'outil sur du bruit.

## Attribution

Données de marée fournies par api-maree.fr sous licence CC BY, calculées à
partir de composantes harmoniques Ifremer / PREVIMER, elles-mêmes sous licence
CC BY. Houle, vent, courant et indices convectifs : Open-Meteo (modèles DWD
EWAM et GWAM pour la houle).

## Modèles de vent

Le vent vient de deux modèles à haute résolution, moyennés quand ils sont
disponibles tous les deux :

- **AROME HD** (Météo-France), environ 1,5 km, jusqu'à ~42 h ;
- **UKV** (Met Office), 2 km, jusqu'à ~48 h, réputé sur la Manche.

Au-delà de deux jours, le global du Met Office (10 km, 7 jours) prend le
relais : même physique que l'UKV, donc une prévision cohérente. Le Met Office
fait tourner l'UKV jusqu'à 120 h, mais Open-Meteo n'en redistribue que 48.
ARPEGE puis le choix automatique d'Open-Meteo servent de secours ultimes. Le modèle utilisé s'affiche dans l'infobulle de chaque case de
vent, et un cadre pointillé signale un désaccord d'au moins 5 nœuds.

Le vent est calculé un peu au large (`point_vent` dans `SPOTS`) : posé sur le
trait de côte, une maille de 1,5 à 2 km mélange terre et mer, et la rugosité
du sol freine artificiellement le vent.

Pour privilégier un seul modèle, ajoute la variable de dépôt `MODE_VENT` avec
`arome` ou `ukv` (par défaut : `moyenne`), et ajoute-la à la section `env`
de l'étape « Calculer les notes » du workflow.

## Recevoir une notification

Le workflow prévient par **ntfy** : gratuit, sans compte, l'application
reçoit la notification directement.

1. Installe *ntfy* depuis l'App Store (ou le Play Store). Sur iPhone, les
   notifications arrivent aussi sur l'Apple Watch.
2. Choisis un sujet à toi, long et impossible à deviner. Génère-le plutôt
   que de l'inventer :
   `python3 -c "import secrets; print('opale-' + secrets.token_hex(6))"`.
   Toute personne connaissant ce mot peut lire tes notifications — et en
   envoyer —, alors ne le publie nulle part.
3. Dans l'application, abonne-toi à ce sujet.
4. Dans le dépôt, *Settings → Secrets and variables → Actions → Secrets*,
   crée `NTFY_TOPIC` avec ce même mot.

Seuils, en *variables* du dépôt (pas en secrets) : `SEUIL_ALERTE`, 3 par
défaut, et `SEUIL_CHANTIER`, 2,3 par défaut, pour les sessions chantier. Ces
dernières arrivent sous l'étiquette « chantier », jamais en priorité haute,
et se taisent les jours où une vraie session dépasse déjà le seuil surf.

`alerter.py` raisonne par meilleure session de chaque jour, et envoie quatre
sortes de lignes :

- **NOUVEAU** — une journée passe au-dessus du seuil ;
- **MIEUX** — une session déjà annoncée gagne au moins 0,75 point ;
- **ANNULÉ** — une session annoncée retombe nettement sous le seuil ;
- **MAINTENANT** — une bonne session commence dans les trois heures, compte
  tenu du trajet (`trajet_min`). Celle-ci sonne en priorité haute.

Il retient ce qui a déjà été annoncé dans `etat_alertes.json`, pour ne pas
répéter la même alerte huit fois par jour. Sans le secret `NTFY_TOPIC`,
l'étape est simplement ignorée. Pour voir ce qui partirait sans rien envoyer
ni rien mémoriser :

```
python3 alerter.py --seuil 3 --seuil-chantier 2.3 --essai
```

### Par courriel plutôt que par notification

Si tu préfères un mail, l'astuce sans service tiers consiste à faire créer une
*issue* par le workflow : GitHub envoie nativement un courriel pour chaque
issue ouverte sur un dépôt que tu surveilles. Remplace l'étape « Notifier »
par un appel à `gh issue create` avec le contenu de `message.txt`. Le revers
est que l'onglet Issues se remplit et qu'il faut les refermer.

## Sécurité

Le risque d'orage est un véto : une heure classée « élevé » est notée zéro
quelles que soient les conditions par ailleurs, et les deux heures voisines
passent au moins en « modéré ». Sur l'eau, la règle reste de sortir dès le
premier coup de tonnerre et d'attendre trente minutes après le dernier.
