# Terres Hostiles Réel

Jeu de survie en solo, jouable dans le navigateur, contenu dans **un seul fichier HTML**. Pas de build, pas de serveur, pas de dépendance à installer : on ouvre `index.html` et on joue.

Vous êtes seul, dans un milieu hostile. Chaque jour, vous disposez de quelques points d'action ; chaque nuit, le froid, la chaleur ou l'humidité vous coûtent de la santé, la faim et la soif progressent. Il faut tenir jusqu'au dernier jour, ou allumer assez de signaux pour être secouru.

L'interface est en français.

## Lancer le jeu

- **En local :** téléchargez `index.html` et ouvrez-le dans un navigateur récent (Chrome, Firefox, Safari, Edge, mobile compris).
- **Sur GitHub Pages :** activez Pages sur la branche principale, le jeu est servi tel quel.

Le jeu fonctionne hors ligne. Seules les polices (Google Fonts) viennent du réseau ; sans connexion, le navigateur utilise ses polices par défaut.

## Aperçu du jeu

| | |
|---|---|
| **Mode** | Solo, tour par tour |
| **Durée d'une partie** | 8, 12 ou 16 jours, ou illimitée |
| **Environnements** | 11 : désert, océan, forêt, glacier, montagne, marais, jungle, savane, steppe, canyons, fjords |
| **Difficultés** | Randonneur, Survivaliste, Extrême, Enfer |
| **Modes** | Partie libre, scénarios, défi du jour |
| **Sauvegarde** | Automatique dans le navigateur (5 parties), export et import par code |

### Un tour de jeu

Chaque jour commence par 4 points d'action (PA), moins si vous êtes fatigué, blessé ou si la météo s'en mêle. Vous pouvez :

- **Explorer** (tirer des cartes : objets, nourriture, rencontres, aléas) ;
- **Collecter** du bois, de la pierre, des fibres, de l'eau, des vivres, des plantes ;
- **Fabriquer** des outils, des vêtements, un abri, un feu ;
- **Construire** un habitat (2 PA) ;
- **Se reposer**, **préparer des remèdes**, **calmer son esprit**, **signaler** votre position.

Équiper, manger, boire et se soigner sont gratuits. La nuit tombe quand vous terminez la journée : dégâts de stress, faim, soif, blessures, rencontres nocturnes.

### Systèmes

- **Corps :** température centrale (hypothermie, coup de chaleur), poids, énergie, blessures (saignement, fracture, infection, gastro).
- **Esprit :** peur qui paralyse, moral, conscience après vos choix.
- **Météo et saisons :** prévision du lendemain, huit jours par saison, effets propres à chaque milieu.
- **Rencontres :** prédateurs, proies, aléas, visiteurs, **Habitants** du lieu qui peuvent devenir alliés ou ennemis selon votre réputation.
- **Plantes et remèdes :** recettes à apprendre (visiteurs, Habitants, parchemins), plantes à trouver, remèdes à préparer.
- **Compétences :** feu, abri, eau, nourriture, premiers secours, signalisation, qui progressent avec la pratique.
- **Secours :** chaque signal allumé augmente vos chances d'être repéré ; un signal suffisant déclenche une veille de secours quotidienne.

### Mécaniques de gestion

| Action | Coût | Effet |
|---|---|---|
| **Cacher une carte** | 1 PA | Met un objet ou un matériau à l'abri des vols, pillages et pertes de nuit. Capacité : 2 + niveau d'habitat. Pas de vivres périssables. |
| **Renforcer l'abri** | 1 PA, 2 matériaux | Jusqu'à 2 niveaux, chacun retire 1 point de stress de nuit. Les tempêtes en abîment. |
| **Veiller** | 1 PA, énergie −2 | Aucune surprise nocturne ; avec un feu, 1 point de stress de moins. |
| **Entretenir le feu** | 1 PA, 1 Bois, outil à feu | Foyer de 3 nuits, compte comme feu et épargne l'usure de l'outil. |
| **À l'affût** | 1 PA, énergie −1, canne ou arme | Pêche ou chasse immédiate. À la chasse, une bête blessée peut contre-attaquer : on l'achève ou on lâche prise. |
| **Fumer les prises** | 1 PA, Fumoir, feu | Transforme jusqu'à 4 Poissons ou Gibiers frais en vivres fumés qui ne pourrissent pas. |

### Aides en jeu

- Un bouton **Aide** (règles, glossaire, stratégie) et un bouton **Point** (situation et priorités).
- Un mode **formateur** qui affiche des conseils selon le milieu et vos dernières actions.
- Des **pastilles vertes** signalent ce qui est disponible maintenant dans les menus et sur les cartes.
- Un **bilan** de fin de partie avec points forts, points faibles et conseils.
- Un **registre** local des parties terminées, classées par points (jours tenus, difficulté, secours).

## Accessibilité et mobile

- Pensé d'abord pour le téléphone : zones tactiles d'au moins 44 px, pas de zoom intempestif sur iOS.
- Fenêtres modales avec piège de focus, fermeture par la touche Échap, retour du focus à la fermeture.
- Pastilles et jauges avec libellés lisibles par les lecteurs d'écran, thèmes clair et sombre.
- Son et ambiance synthétisés dans le navigateur, avec bouton Son/Muet.

## Sauvegardes et données

Tout reste dans le navigateur (`localStorage`) : parties, scores, réglages. Rien n'est envoyé à un serveur.

- Les sauvegardes sont **versionnées** et **assainies** au chargement : un fichier modifié ou corrompu ne peut pas casser le jeu (valeurs bornées, cartes reconstruites depuis le catalogue).
- L'**export** produit un code texte, l'**import** le vérifie avant de l'accepter.
- Le **défi du jour** est identique pour tout le monde : même paquet, même météo.

## Structure du dépôt

```
index.html          le jeu complet (HTML, CSS, JavaScript)
sim.js              simulateur d'équilibrage et tests, hors du jeu
ia-simulateur.js    petite IA de test utilisée par sim.js
README.md           ce fichier
```

Le jeu n'a aucune dépendance. Le simulateur demande seulement Node.js.

## Simulateur et tests

`sim.js` charge le script du jeu dans un contexte Node, sans navigateur, et fait jouer un bot sur toutes les combinaisons. Il vérifie notamment :

- que 330 parties s'exécutent sans erreur dans les 11 environnements ;
- la cohérence de la température selon la météo ;
- l'aller-retour des sauvegardes et le rejet d'imports piégés ;
- le défi du jour déterministe ;
- le taux de survie par environnement et par difficulté (repère d'équilibrage ; le bot est plus faible qu'un joueur humain) ;
- le rendu de chaque écran.

```bash
node sim.js
```

`index.html`, `sim.js` et `ia-simulateur.js` doivent se trouver dans le même dossier.

## Contribuer

Le jeu tient dans un seul fichier, il suffit d'éditer `index.html`. Quelques repères :

- les cartes sont dans le tableau `DEFS` ; les environnements dans `ENVS` ; les recettes dans `RECIPES` et `REMEDES` ;
- la difficulté se règle dans la table `DIFF` ;
- `endDay` et `nightEvents` décrivent la nuit ; `stressNight` calcule le stress ;
- les sauvegardes passent par `makeRec` (écriture) et `cleanSave` (lecture assainie) : tout nouveau champ de joueur doit être ajouté aux deux, avec des bornes.

Après une modification, lancez `node sim.js` : le jeu doit afficher `fails 0` et `problems 0`.

## Licence

À préciser par l'auteur avant publication (MIT, CC BY-NC, tous droits réservés…).
