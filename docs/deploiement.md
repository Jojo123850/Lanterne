# Procédure de déploiement

## 1. Prérequis

- Node.js 24 LTS
- pnpm 11
- Un repository Github
- Un compte Vercel
- Le dossier du projet configuré comme répertoire racine du projet Vercel

La version Node.js doit être cohérente entre le développement local, le dépôt et Vercel.
Le fichier `.nvmrc` fixe Node.js 24 pour éviter un environnement implicite.

## 2. Installation locale

```text
git clone https://github.com/Errante-Creation/CP8-Lanterne-Correction
pnpm install ci
pnpm run check
pnpm test
```

Résultats attendus : 
```text
node --check api/index.js && node --check tests/api.test.js
API tests passed
```

## 3. Déploiement Vercel

Depuis la racine du projet : 

``` 
vercel link
> Create a new project
> Name : Nommez le projet ou appuyez sur entrer
> Connect this Git repository to automatically deploy changes on every push : N
> Code directory : Laisser par défaut
> Customize settings : N
```

Cela crée un nouveau project vide sur Vercel. 
Sélectionnez ce projet.
Vous devez configurer les variables d'environnement.
Menu `Environment variables` → `Add environment variable`
Choisir `Config` 
Ajouter les clés qui sont dans `.env.example`
Configurer la variable d'environnement en fonction de l'environnnement (production)
ensuite déployer avec `vercel`, cela vous permet de déployer la version en production (première version)

### Déployer la version de dev

1. Créer une branche develop : `git checkout -b develop`
2. Déployer avec `vercel`
3. Configurer les variables d'environnement pour la version Preview
4. Lancer un Redeploy sur la version Preview


## 4. Procédure de mise à jour

Pour publier une nouvelle version :

1. Passer sur la branche develop : `git switch develop`
2. Mettre à jour le projet
3. Mettre à jour les tests si le comportement change
4. Lancer `pnpm run check` et `pnpm test`
5. Créer un commit explicite
6. Déployer la preview : `vercel`
7. Vérifier les routes
8. Publier en production

### Publier en production

Pour publier en production :

1. Fusionner la branche develop avec la branche main
2. Lancer `vercel --prod`

## 5. Retour en arrière

En cas d'échec, sélectionner le déploiement précédent dans l'historique Vercel et le promouvoir en Production.