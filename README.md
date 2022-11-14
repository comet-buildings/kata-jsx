# KATA - JSX

En React, nous avons l'habitude d'écrire nos vues avec en JSX mais que ce cache t-il derrière cela ?

## TL;DR

```tsx
// Le JSX dans vos fichiers tsx...
<div>hello</div>;

// ... est tranformé en :
React.createElement("div", null, "hello");
```

Le code JSX n'est donc rien d'autre que du sucre syntaxique pour l'appel de la fonction `React.createElement`.
`

## But du KATA

L'idée de ce KATA est de re-coder notre propre fonction `createElement` et de l'utiliser à la place `React.createElement` afin de générer directement des éléments du DOM.

Cette fonction doit prendre en premier argument le nom du tag de l'élément, en second argument les propriétés et enfin le contenu de l'élément.

```ts
type CreateElement = (
  type: string,
  props: Record<string, string | number> | null = null,
  ...children: (HTMLElement | string | number)[]
) => HTMLElement;
```

# TODO

1- Pour commencer simple, créons une fonction nous retournant l'object ci-dessous lors de l'utilisation de l'expression `<Top value={42} />`.

```typescript
// Resultat de <Top value={42} />
{
  type: "Top";
  value: 42;
}
```

2- Jouons maintenant avec le dom pour que l'expression JSX ci-dessous nous génére l'élément du DOM correspondant

```typescript
const element: HTMLElement = (
  <div id="myId">
    <span>hello</span>
  </div>
);
```

# Note

## How magic happens

Le code JSX est interprété par le compilateur (dans notre cas ici `babel`). Mais pour cela il doit se trouver dans des fichiers avec l'extention `.tsx` ou `.jsx`.

Pour que babel avec le plugin `@babel/plugin-transform-react-jsx` puisse utiliser une autre fonction que `React.createElement` il suffit d'ajouter le commentaire `/** @jsx maFonction */` et de déclarer ou d'importer `maFonction` juste après.

## Test

Pour les tests, on peut facilement tester des interactions avec le DOM en définissant le `testEnvironment` à `jsdom` dans la config `jest`.

## Docs

[Intro à JSX](https://fr.reactjs.org/docs/introducing-jsx.html)

[DOM Document API](https://developer.mozilla.org/fr/docs/Web/API/Document)
