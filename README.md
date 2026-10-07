# Liste de tâches

Application d'exemple du module « CI/CD avec Jenkins ».  

## Commandes utiles

| Commande        | Ce qu'elle fait                 |
|-----------------|---------------------------------|
| `npm ci`        | Installe les dépendances        |
| `npm test`      | Lance les tests                 |
| `npm run dev`   | Affiche le site sur votre poste |
| `npm run build` | Crée le dossier `dist`          |

---


## 1. Le site
Adresse du site en ligne (Adresse de mon fichier sur Netlify) : https://snazzy-meerkat-870b3a.netlify.app/  

## 2. Démarrer Jenkins
```
docker run -d --name jenkins -p 8080:8080 -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts
```

Adress du navigateur : http://localhost:8080   

## 3. Configuration
`node22` : nom de l'outil Node.js déclaré dans Jenkins (Administrer Jenkins > Tools).  
`netlify-token` : le jeton d'accès personnel Netlify, qui autorise Jenkins à déployer le site.  
`netlify-site` : l'identifiant du site Netlify (Site ID), qui indique sur quel site déployer.  

## 4. Le pipeline
Le pipeline vérifie le dépôt toutes les 2 minutes et se lance automatiquement s'il détecte un nouveau commit. Il enchaîne 6 étapes :

1. **Installer** : installe les dépendances du projet avec `npm ci`.
2. **Tester** : lance les tests avec `npm run test:ci` et produit un rapport de résultats.
3. **Construire** : crée le dossier `dist` avec `npm run build` et l'archive dans Jenkins.
4. **Prévisualiser** : déploie le site sur une adresse de prévisualisation Netlify pour pouvoir le vérifier avant la mise en ligne.
5. **Valider** : met le pipeline en pause et attend qu'une personne clique sur « Mettre en ligne ? » pour continuer.
6. **Déployer** : met le site en ligne en production sur Netlify avec `npm run deploy`.

## 5. Mettre en ligne
1. Envoyer les modifications sur GitHub avec les 3 commandes :

```bash
   git add .
   git commit -m "Description de la modification"
   git push origin main
```

2. Attendre : Jenkins détecte le nouveau commit en 2 minutes au plus et lance le pipeline.  
3. Le build s'arrête à l'étape **Valider**.  
4. Dans Jenkins, ouvrir **Console Output** et chercher la ligne `draft URL`. Ouvrir cette adresse dans un nouvel onglet : c'est la prévisualisation du site.  
5. Sur la prévisualisation, vérifier les cas « à la main » (ou ceux nommés par le testeur) du fichier `PLAN_DE_TESTS.md`.  
6. Revenir dans Jenkins :
   - si tous les cas sont corrects, cliquer sur **Proceed** : le site est mis en ligne ;
   - sinon, cliquer sur **Abort** : le site principal ne change pas.  
7. Attendre la fin du build, puis recharger le site principal pour vérifier la nouvelle version.  

## 6. Revenir en arrière
Si la version en ligne a un défaut qui vient du dernier commit, on remet en ligne la version précédente.

1. Annuler le dernier commit et garder le message proposé :

```bash
   git revert HEAD
```

2. Envoyer ce nouveau commit sur GitHub :

```bash
   git push origin main
```

3. Attendre le pipeline. Il s'arrête à l'étape **Valider**.
4. Vérifier la prévisualisation, puis cliquer sur **Proceed** dans Jenkins.
5. Recharger le site principal : il est revenu à l'état précédent, avant le commit qui a causé le défaut.

`git revert HEAD` crée un nouveau commit qui annule le dernier. L'historique est donc conservé.

