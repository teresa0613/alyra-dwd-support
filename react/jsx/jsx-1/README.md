# JSX (1)

> Mais en quoi, `React.createElement` nous facilite la vie ? ... on dirait le contraire... ?

Si vous vous posez cette question, je pense que c'est un réflexe tout à fait légitime. Créer les structures plus complexes demande beaucoup de code. De plus, ce code n'est pas très lisible.

Heureusement, **JSX** nous vient à la rescousse !

**JSX** est une extension syntaxique de JavaScript, créée par des dévelopeurs de React et recommandée par React. Comme indiqué dans la documentation : _fondamentalement, JSX fournit juste du sucre syntaxique pour la fonction `React.createElement`_. Pourtant c'est un vrai _game changer_ pour nous, les développeurs.

Regardons le code qui nous génère le petite mémo sur les pandas roux.

```javascript
const rootElement = document.getElementById("root")
const imgSrc =
  "https://images.unsplash.com/photo-1500812013460-8ab63ad969a7?ixlib=rb-1.2.1&q=80&fm=jpg&crop=entropy&cs=tinysrgb&w=400&fit=max&ixid=eyJhcHBfaWQiOjE0NTg5fQ"

const h2El = React.createElement("h2", null, "Secrets des pandas roux")
const imgEl = React.createElement("img", {
  src: imgSrc,
  alt: "Panda roux sur une branche.",
  className: "img-fluid mb-3",
})
const pEl = React.createElement(
  "p",
  null,
  "Le saviez-vous ? Le petit panda est un carnivore, qui ne mange jamais de la viande."
)
const article = React.createElement(
  "article",
  {
    className: "mt-5 p-3 text-center shadow",
  },
  h2El,
  imgEl,
  pEl
)

ReactDOM.render(article, rootElement)
```

Voici, le même code re-écrit avec JSX :

```javascript
const rootElement = document.getElementById("root");
const imgSrc =
  "https://images.unsplash.com/photo-1500812013460-8ab63ad969a7?ixlib=rb-1.2.1&q=80&fm=jpg&crop=entropy&cs=tinysrgb&w=400&fit=max&ixid=eyJhcHBfaWQiOjE0NTg5fQ";

const article = (
  <article className="mt-5 p-3 text-center shadow">
    <h2>Secrets des pandas roux</h2>
    <img src={imgSrc} alt="Panda roux sur une branche." className="img-fluid mb-3">
    <p>Le saviez-vous ? Le petit panda est un carnivore, qui ne mange jamais de la viande.</p>
  </article>
)

ReactDOM.render(article, rootElement);
```

C'est un peu comme si on écrivait du HTML directement dans JavaScript ! 🤩 Voici quelques exemples supplémentaires :

```javascript
const element = <p></p>
/*
// avant :
const element = React.createElement("p")
*/
```

---

```javascript
const element = <p>Bonjour</p>
/*
// avant :
const element = React.createElement(
  "p",
  null,
  "Bonjour !"
)
*/
```

---

```javascript
const element = <h1 lang="en">Hello World!</h1>
/*
// avant
const element = React.createElement(
  "h1",
  {lang: "en"},
  "Hello World!"
)
*/
```

```javascript
const element = <p>Bonjour</p>
/*
// avant :
const element = React.createElement(
  "p",
  null,
  "Bonjour !"
)
*/
```

---

## BABEL

Vous vous rappelez de Sass ?  
Nous avons dit que Sass est une extension de CSS. Le navigateur ne comprend pas Sass. Le code Sass doit passer par le compilateur et être transformé en CSS. C'est pareil pour JSX, les navigateurs ne comprennent pas cette syntaxe. Comme pour Sass, nous devons utiliser un compilateur. Afin de compiler JSX en JavaScript allons utiliser [**babel**](https://babeljs.io).

### Comment utiliser Babel ?

1. Vous pouvez essayer le fonctionnement de babel directement en ligne avec cette [**demo**](https://babeljs.io/en/repl#?browsers=&build=&builtIns=false&spec=false&loose=false&code_lz=MYewdgzgLgBApgGzgWzmWBeGAeAFgRgD4AJRBEGAdRACcEATbAegMKA&debug=false&forceAllTransforms=false&shippedProposals=false&circleciRepo=&evaluate=false&fileSize=false&timeTravel=false&sourceType=module&lineWrap=true&presets=react&prettier=false&targets=&version=7.7.4&externalPlugins=) qui fait partie du site web officiel.

2. Afin d'ajouter babel dans un de vos projets, vous pouvez opter pour la solution babel _standalone_. Vous devez alors inclure le fichier source de babel, disponible par exemple ici `https://unpkg.com/@babel/standalone/babel.js`. Ensuite dans le script dans lequel vous souhaitez activer babel, ajoutez l'attribut `type="text/babel"`. Voici un exemple :

```html
<div id="root"></div>
<script src="https://unpkg.com/react/umd/react.development.js"></script>
<script src="https://unpkg.com/react-dom/umd/react-dom.development.js"></script>
<script src="https://unpkg.com/@babel/standalone/babel.js"></script>
<script type="text/babel">
  // vous pouvez profiter de jsx ici !!!
</script>
```

3. On aurait pu opter pour la solution précédente pour mettre en place babel dans nos pens sur CodePen. Mais ceci n'est pas nécessaire. En fait, babel est directement disponible dans CodePen. Pour l'activer, cliquez sur les réglages de JavaScript et choisissez Babel dans JavaScript Preprocessor.

https://wptemplates.pehaa.com/assets/alyra/babel.mp4

4. À un moment donné, nous allons commencer à utiliser [CRA](https://fr.reactjs.org/docs/create-a-new-react-app.html) - un _starter_ pour des applications web monopage recommandé par React - babel et toute la configuration seront inclus 💫.

## ReactDOM.render et JSX

On peut utiliser JSX directement avec `ReactDOM` :

```javascript
ReactDOM.render(<h1>Hello World</h1>, root)
```

## React sans JSX

JSX est juste une extension syntaxique, il n'est pas donc indispensable pour un projet React. Dans certain cas, on peut préférer pouvoir se passer d'un compilateur. Vous pouvez [en lire davantage dans cette article.](https://fr.reactjs.org/docs/react-without-jsx.html)

## Syntaxe JSX en détails (1)

### Toutes les balises sont obligatoirement fermées (xml-style)

Dans HTML on peut se permettre de ne pas fermer des balises auto-fermantes (_self-closing tags_), tel que `<input>` ou `<img src="img1.jpg" alt="">`.

Ceci n'est pas correct dans JSX, et provoquera une erreur.

La syntaxe correcte est `<input />` et `<img src="img1.jpg" alt="" />`.

### React.Fragment

```javascript
element = (
  <React.Fragment>
    <dt>JSX</dt>
    <dd>une extension syntaxique de JavaScript</dd>
  </React.Fragment>
)
```

ou plus simplement :

```javascript
element = (
  <>
    <dt>JSX</dt>
    <dd>une extension syntaxique de JavaScript</dd>
  </>
)
```

### Commentaires

```javascript
const element = <p>{/* je suis un commentaire  */}</p>
```

---

## Exercices

- [JSX p](https://codepen.io/alyra/pen/OJNbKMo) | [solution](https://codepen.io/alyra/pen/29e2be325c73498465349b7eb816d4b1)
- [JSX button](https://codepen.io/alyra/pen/MWybNyY) | [solution](https://codepen.io/alyra/pen/24c0e41e939ac4cc1773c654711bf2cd)
- [JSX h1](https://codepen.io/alyra/pen/wvGoVGR) | [solution](https://codepen.io/alyra/pen/aa7b96a373353287f147da0cf3937fb9?editors=1010)
- [JSX - header](https://codepen.io/alyra/pen/eYZdoWg) | [solution](https://codepen.io/alyra/pen/50bee6a7d1c810dfccba46d5e4dee82b)
- [JSX - input](https://codepen.io/alyra/pen/MWyoLrY) | [solution](https://codepen.io/alyra/pen/cf85be5c0ae3a664db66486387b908c5)
- [JSX - label + input](https://codepen.io/alyra/pen/GRZEzyG) | [solution](https://codepen.io/alyra/pen/3b5c8b252ef90a019d3db1c8990b6677)
- [JSX - style](https://codepen.io/alyra/pen/vYGJrLx) | [solution](https://codepen.io/alyra/pen/5882c4df35ceb675f3e246b2829bff4a)
