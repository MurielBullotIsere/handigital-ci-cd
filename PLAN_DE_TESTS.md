# Plan de tests

Un cas de test par ligne.
La colonne « Vérifié par » contient `Test automatisé` ou `À la main`.

| N° | Action | Résultat attendu | Vérifié par |
|----|--------|------------------|-------------|
| 1  | Appeler `ajouterTache([], 'Lire')` (ajouter une tâche)| La liste contient 1 tâche, dont le titre est « Lire » | Test automatisé |
| 2  | Appeler `supprimerTache([], 'Lire')` sur une liste contenant la tâche « Lire » (supprimer une tâche)| La liste renvoyée est vide | Test automatisé |
| 3  | Appeler `compterTaches` sur une liste contenant 1 tâche | La fonction renvoie 1 | Test automatisé |
| 4  | Appeler `compterTaches` sur une liste contenant 3 tâches | La fonction renvoie 3 | Test automatisé |
| 5  | Ouvrir la page d'accueil | Le titre s'affiche | Muriel |
| 6  | Ajouter la tâche « Lire » sur la page d'accueil | « Lire » apparaît dans la liste, le champ se vide et le compteur augmente de 1 | À la main |
| 7  | Supprimer une tâche qui se trouve dans la liste | La tâche disparaît de la liste et le compteur diminue de 1 | À la main |
