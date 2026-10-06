# Plan de tests

Un cas de test par ligne.
La colonne « Vérifié par » contient `Test automatisé` ou `À la main`.

| N° | Action | Résultat attendu | Vérifié par |
|----|--------|------------------|-------------|
| 1  | Appeler `ajouterTache([], 'Lire')` | La liste contient 1 tâche, dont le titre est « Lire » | Test automatisé |
| 2  | Appeler `supprimerTache` sur une liste contenant « Lire », avec le titre « Lire » | La liste renvoyée est vide | Test automatisé |
| 3  | Appeler `compterTaches` sur une liste contenant 1 tâche | La fonction renvoie 1 | Test automatisé |
| 4  | Ouvrir la page, taper « Lire » dans le champ et cliquer sur « Ajouter » | « Lire » apparaît dans la liste, le champ se vide et le compteur passe de « Nombre de tâches : 0 » à « Nombre de tâches : 1 » | À la main |
| 5  | Cliquer sur le bouton « Supprimer » à côté de la tâche « Lire » | La tâche disparaît de la liste et le compteur revient à « Nombre de tâches : 0 » | À la main |
