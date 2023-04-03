---
sidebar_position: 2
---

# Traitement des requêtes de mutations

Lorsqu'une requête de mutation est effectuée (méthodes `POST`, `PATCH`, `PUT` ou `DELETE`) sur notre route, la fonction `action` est appelé. Cette fonction est exécutée côté serveur uniquement.

Nous allons maintenant permettre la modification des playlists en traitant ces requêtes de mutation.

:::info Exercice

Créer une fonction `action` qui, lorsqu'elle est exécutée, ajoute la track identifiée par son `track_id` à la playlist.
:::

## Guide

💿 **Définir une fonction `action`**

<details>
  <summary>Voir une solution</summary>

```tsx title="app/routes/_layout.playlists.$id.(edit).tsx"
export const action = () => {};
```

</details>

💿 **Récupérer des données soumises**

La fonction `action` nous expose les mêmes paramètres que la fonction `loader` : `request` et` params`. On va pouvoir ainsi récupérer l'id de la playlist dans les paramètres de l'URL et l'id de la track à ajouter dans le form data de la requête.

Nous pourrons utiliser la methode [`formData()`](https://developer.mozilla.org/en-US/docs/Web/API/Request/formData) de la `request`

<details>
  <summary>Voir une solution</summary>

```tsx title="app/routes/_layout.playlists.$id.(edit).tsx"
// highlight-start
export const action = async ({ request, params: { id = "" } }: ActionArgs) => {
  // highlight-next-line
  const rawFormData = await request.formData();
  // highlight-end
};
```

</details>

💿 **Valider les données soumises**

Pour s'assurer que les données soumises sont valides, nous allons utiliser la librairie `zod`. Cette librairie nous permet de définir la structure d'un objet et de valider au runtime cette structure.

Cela nous permet en plus de la validation d'avoir par la suite des données correctement typées.

:::tip
Pour en savoir plus sur Zod [voir la docs](https://zod.dev/).
:::

<details>
  <summary>Voir une solution</summary>

```tsx title="app/routes/_layout.playlists.$id.(edit).tsx"
// highlight-start
const FormDataRequestSchema = z.object({
  track_id: z.string(),
});
// highlight-end

export const action = async ({ request, params: { id = "" } }: ActionArgs) => {
  const rawFormData = await request.formData();
  // highlight-next-line
  const formData = FormDataRequestSchema.parse(Object.fromEntries(rawFormData));

  return null;
};
```

</details>

💿 **Changer l'état du serveur**

`action` étant une fonction exécuté côté serveur uniquement, nous allons pouvoir ici appeler directement notre repository.

<details>
  <summary>Voir une solution</summary>

```tsx title="app/routes/_layout.playlists.$id.(edit).tsx"
export const action = async ({ request, params: { id = "" } }: ActionArgs) => {
  const rawFormData = await request.formData();
  const formData = FormDataRequestSchema.parse(Object.fromEntries(rawFormData));
  // highlight-next-line
  await playlists.addTrack(id, formData.track_id);
  // highlight-end
  return null;
};
```

</details>

:::info 👏 Nous pouvons maintenant modifier nos playlists en y ajoutant des tracks.

Ajoutons maintenant la possibilité de retirer des tracks de la playlist.
:::
