# Note de veille

## Source 1 Vercel et Express

La documentation Vercel indique qu'une application Express peut être déployée sans configuration complexe : Vercel la fait fonctionner comme une fonction Node.js unique et détecte automatiquement le projet dans les cas pris en charge.

Impact pour Lanterne : conserver une exportation de l'application Express avec `module.exports = app`, garder un point d'entrée clair et éviter une configuration `vercel.json` plus complexe que nécessaire.

Source : [How to ship an Express app on Vercel](https://vercel.com/kb/guide/ship-a-express-app-on-vercel), consultée le 23/09/2026.

## Source 2 Dépendances Node.js sur Vercel

La documentation du runtime Node.js précise que Vercel choisit le gestionnaire de paquets à partir du fichier de verrouillage présent : `pnpm-lock.yaml` entraîne l'utilisation de pnpm, tandis que `package-lock.json` entraîne l'utilisation de npm.

Impact pour Lanterne : ne pas mélanger les gestionnaires de paquets. le projet doit conserver son lockfile et documenter la commande correspondante.

Source : [Using the Node.js Runtime with Vercel Functions](https://vercel.com/docs/functions/runtimes/node-js), consultée le 23/09/2026

## Source 3 Cycle de vie Node.js

La page officielle Node.js recommande d'utiliser une version Active LTS ou Maintenance LTS en production. À la date de cette correction, Node.js 24 est indiqué comme LTS et Node.js 26 comme Current.

Impact pour Laterne : fixer Node.js 24 dans `.nvmrc` et vérifier que la version local et la version utilisée par Vercel restent cohérentes.

Source : [Node.js Releases](https://nodejs.org/en/about/previous-releases), consultée le 23/09/2026