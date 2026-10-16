# Pong — jeu web

Un Pong jouable directement dans le navigateur, en un seul fichier `index.html`.
Aucune dépendance, aucun build : on ouvre la page et on joue.

## Jouer

- En ligne : https://davidfafnirforge.github.io/pong-web/
- En local : télécharger `index.html` et l'ouvrir dans un navigateur,
  ou lancer `python3 -m http.server 8000` puis aller sur <http://localhost:8000>.

## Commandes

| Touche | Action |
| --- | --- |
| `W` / `S` | Déplacer la raquette du joueur 1 (à gauche) |
| `↑` / `↓` | Déplacer la raquette du joueur 2 en mode 2 joueurs |
| `2` | Basculer entre 1 joueur (contre l'IA) et 2 joueurs |
| `P` | Pause / reprendre |
| `M` | Couper / remettre le son |
| `R` | Réinitialiser la partie |
| `Espace` | Servir, ou rejouer après une partie terminée |

Sur mobile ou tablette : toucher l'écran pour servir, puis faire glisser le doigt
pour déplacer la raquette (la moitié gauche pilote le joueur 1, la moitié droite
le joueur 2 en mode 2 joueurs).

## Règles

- Premier à **7 points** gagne. Un point est marqué quand la balle sort du terrain.
- La balle accélère légèrement à chaque renvoi de raquette (plafonnée).
- L'angle de renvoi dépend de l'endroit où la balle touche la raquette.
- **La balle change de couleur à chaque touche** : rebond sur une raquette ou sur
  un mur. Les teintes sont générées par pas d'or (~137,5° sur le cercle
  chromatique), donc deux couleurs consécutives ne sont jamais identiques.

## Mode démo automatique (tests)

La page expose un point d'entrée `window.__pong` utilisé par les tests de
vérification. En réglant `state.manual = true`, la physique n'est plus avancée par
la boucle d'animation et peut être pilotée image par image :

```js
const g = window.__pong;
g.state.manual = true;
g.resetMatch();
g.serve();
const hueAvant = g.state.hue;
for (let i = 0; i < 120; i++) g.update(1 / 60);
console.log(g.state.ball.x, g.state.hue !== hueAvant);
```

## Licence

MIT — voir `LICENSE`.
