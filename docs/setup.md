---
sidebar_position: 2
---

# Notre première application

:::caution Pré requis
Avant de commencer, assurons nous d'avoir les éléments suivants:

- [Node.js](https://nodejs.org/en/download/) 14 ou plus
- [NPM](https://www.npmjs.com/) 7 ou plus.
- Un éditeur de code ([VSCode](https://code.visualstudio.com/) par exemple)

:::

## Initialiser l'application

💿 **Créer l'application**

Pour créer une application Remix, nous allons pour utiliser la commande `npx create-remix@latest`. Pour ce workshop, nous allons nous baser sur un template.

```bash
npx create-remix@latest ./my-playlists --template https://github.com/jrakotoharisoa/remix-workshop/tree/starter
```

Voyons ce qui a été généré :

```bash
my-playlists
├── README.md
├── app
│   ├── repositories/
│   ├── routes/
│   ├── styles/
│   ├── ui/
│   ├── utils/
│   ├── entry.client.tsx
│   ├── entry.server.tsx
│   └── root.tsx
├── package-lock.json
├── package.json
├── public
│   └── favicon.ico
├── prisma/
├── remix.config.js
├── remix.env.d.ts
└── tsconfig.json

```

- **app/** : Répertoire dans lequel se trouve le code de notre application Remix
- **app/entry.client.tsx** : Fichier contenant le premier élément de votre JavaScript qui sera exécuté lorsque l'application se chargera dans le navigateur. C'est dans ce fichier que se passe l'hydratation de nos composants React.
- **app/entry.server.tsx** : Fichier contenant la première partie de votre JavaScript qui s'exécutera lorsqu'une requête atteindra votre serveur. Remix s'occupe de récupérer toutes les données nécessaires et vous êtes responsable de renvoyer la réponse. C'est dans ce fichier que Remix rend notre application React côté serveur sous forme de chaîne de caractère ou de flux afin de l'envoyer comme réponse au navigateur.
- **app/root.tsx** : Composant racine de l'application où se trouve la balise `<html>`
- **app/routes** : Répertoire dans lequel vos routes vont être définies. Remix utilise les fichiers dans ce répertoire pour créer les URLs des routes de votre application
- **public/** : Répertoire dans lequel se retrouve les différentes ressources statiques de votre application
- **remix.config.js** : Remix dispose d'un tas d'options de configuration que vous pouvez définir dans ce fichier

💿 **Lancer le serveur de développement**

```bash
cd my-playlists
npm run dev
```

💿 **Ouvrir [http://localhost:3000](http://localhost:3000) dans votre navigateur**

:::info 🚀 Vous êtes prêt à démarrer !

Passons à l'étape suivante pour créer la première page de votre application.
:::
