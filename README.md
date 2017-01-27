# README


## Usage

### Graphique temporel

Les graphiques temporels permettent d'afficher en fonction du temps des données.

 * Horizontal Bar Chart
 * Area Chart

La base de données utilisée est dans db/

Attention, il est important de respecter certaines conventions pour le CSV :
  - Utiliser des séparateurs ','
  - La première colonne doit être nommée 'Date'
  - Le format de date de la première colonne doit être en format anglais (Ex: '12/31/2017', '31 dec. 2017', ...)

### Graphique statique

Contrairement aux graphiques temporels, les graphiques statiques associent une valeur à un tag.

  * Pie Chart

La base de données utilisée est dans db/

Attention, il est important de respecter certaines conventions pour le CSV :
  - Utiliser des séparateurs ','
  - Ne mettre que deux lignes, une pour le nom de la donnée et une autre pour ça valeur.


## Differences

La seule différence entre les charts 'multiBarChart' et 'stackedAreaChart' est à la ligne 39 lors de l'import du modèle.

