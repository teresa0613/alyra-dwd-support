# DOM - Document Object Model

## document.documentElement -> html

```html
<html lang="fr"></html>
```

```javascript
document.documentElement // correspond au html
document.documentElement.lang // 'fr'
```

## document.body -> body

```javascript
document.body.style.background = "red"
```

## document.getElementById()

`document.getElementById('id-name')` retourne l'élément ou `null`

On peut avoir le même résultat avec la méthode plus générique `document.querySelector('#id-name')`, dans ce cas il faut ajouter le symbol "#"

`getElementById()` s'applique uniquement sur `document`

```javascript
document.getElementById("cookie-info").remove()
document.getElementById("#pub").remove()
```

## document.querySelector(), element.querySelector()

Utilise les même selecteurs que css.  
Trouve un élément, premier que correspond au sélecteur.

```javascript
const cookie = document.querySelector("#cookie-info")
cookie.querySelector("span").remove()
```

## document.querySelectorAll('selector')

Le résultat est une NodeList, une structure semblable à l'array.
Si aucun élément ne correspond pas au selecteur, le résultat est une liste vide []
On peut la parcourrir avec la boucle `for of`, la méthode `.forEach()` (et avec la boucle for classique)

```javascript
const allButtons = document.querySelectorAll("button")
for (let button of allButtons) {
  button.disabled = true
}
```

```javascript
const allButtons = document.querySelectorAll("button")
allButtons.forEach((btn) => {
  btn.disabled = true
})
```

## document.getElementsByTagName('tag')

```javascript
const allParagraphs = document.getElementsByTagName("p")
```

## document.getElementsByClassName('.class-name')

```javascript
const allParagraphs = document.getElementsByClassName(".hidden")
```

# Attributes

## standard attributes

Standard HTML attributs peuvent être utiliser "directement" en tant que une propriété d'un élément

```javascript
document.documentElement.lang
document.body.class
const el = document.querySelector("p")
el.id
```

## class

Au lieu de propriété `class` nous avons `className` et `classList`

```html
<body class="bg-dark container"></body>
```

```javascript
document.body.class // undefined
document.body.className // "bg-dark container"
document.body.classList.length // 2
document.body.classList.contains("bg-dark") // true
document.body.classList.add("text-white")
document.body.classList.remove("container")
```

[Plus d'information ici - MDN](https://developer.mozilla.org/fr/docs/Web/API/Element/classList)

## non-standard attributes

Pour non-standard attributs (crée par utilisateur) nous devons utiliser les méthodes `hasAttribute(), setAttribute(), getAttribute(), removeAttribute()`.
Elles fonctionnent aussi pour des attributs standard.

```html
<body author="Franck"></body>
```

```javascript
document.body.hasAttribute("author") // true
document.body.author // undefined
document.body.getAttribute("author") // 'Franck'
document.body.setAttribute("author", "Paulina")
document.body.getAttribute("author") // 'Paulina'
document.body.removeAttribute("author")
```

Attention, ceci n'est pas une bonne pratique. Les attributs personnalisés devraient toujous commancer par `data-`. Dans ce cas là ils sont accèssible via la propriété `dataset`

```html
<body data-author="Franck"></body>
```

```javascript
document.body.hasAttribute("data-author") // true
document.body[data - author] // undefined
document.body.dataset.author // 'Franck'
document.body.dataset.author = "Maxime"
document.body.getAttribute("data-author") // 'Maxime'
document.body.setAttribute("data-author", "Paulina")
document.body.getAttribute("data-author") // 'Paulina'
document.body.removeAttribute("data-author")
// ou
delete document.body.dataset.author
```

# Modification du document

## element.textContent

```javascript
const tagline = document.querySelector("#tagline")
const hellos = ["Salut", "Hello", "Cześć", "Hola"]
const randomHelloIndex = Math.floor(Math.random() * hellos.length)
tagline.textContent = hellos[randomHelloIndex]
```

## element.innerHTML

```javascript
const tagline = document.querySelector("#tagline")
const hellos = ["Salut", "Hello", "Cześć", "Hola"]
const randomHelloIndex = Math.floor(Math.random() * hellos.length)
tagline.innerHTML = `<strong>${hellos[randomHelloIndex]}</strong>`
```

## document.createElement(), before, after, prepend/append

```javascript
const 'cookieInfo' = document.createElement("p")
p.textContent = "Ce site n'utilise pas des cookies."
document.body.append(cookieInfo)
```

![](https://assets.codepen.io/4515922/beforeprepend.png)

https://codepen.io/alyra/pen/GRoLXBj

## insertAdjacentHTML

```javascript
const 'cookieInfo' = `<p>Ce site n'utilise pas des cookies.</p>`
document.body.insertAdjacentHTML('afterend', cookieInfo)
```

![](https://assets.codepen.io/4515922/insert.png)

https://codepen.io/alyra/pen/ZEQZMqq

## element.addEventListener

`el.addEventListener(event, eventHandler)`

`eventHandler` est une fonction callback

```javascript
const myButton = document.querySelector("#my-button")
myButton.addEventListener("click", (event) => {
  alert("button clicked !!!")
  console.log(event)
})
```

On peut profiter de l'intéractivité des éléments de formulaires. On peut les utiliser en dehors d'élément `form`. Le type d'event qu'on utilise souvent avec `input` et `select` et `change`

https://codepen.io/alyra/pen/LYGoobE

```html
<label for="mode">Mode sombre</label>
  <input type="checkbox" id="mode">
</label>
```

```javascript
const modeInput = document.getElementById("mode")
modeInput.addEventListener("change", function (event) {
  if (modeInput.checked) {
    // if (this.checked)
    // if (event.currentTarget.checked)
    // if (event.target.checked)
    alert("Mode sombre")
  } else {
    alert("Mode claire")
  }
})
```

```javascript
const modeInput = document.getElementById("mode")
modeInput.addEventListener("change", () => {
  document.body.classList.toggle("bg-dark")
  document.body.classList.toggle("text-white")
})
```

https://codepen.io/alyra/pen/vYLwyJx

[Bonus - exemple avec localStorage](https://codepen.io/alyra/pen/wvMZVqo)

---

[alyra-dom repo](https://github.com/pehaa/alyra-dom)

---

## Exercices

- [Dom - top5](https://codepen.io/alyra/pen/dyGLgoX) | [solution](https://codepen.io/alyra/pen/20c665db9b2bf35ce56635b71b37e5bd)
- [Dom - top5 + attributs](https://codepen.io/alyra/pen/dyGLgpp) | [solution](https://codepen.io/alyra/pen/2dcf464398e04c4a07a2fab6d80b8df8)
- [Dom - top5 + attributs](https://codepen.io/alyra/pen/jOWReMe) | [solution](https://codepen.io/alyra/pen/1e6aaae79019f03cbde8b95bc7432e13)
- [Lorem Ipsum](https://codepen.io/alyra/pen/mdVYMje) | [solution](https://codepen.io/alyra/pen/556c09a96bbc23c76c05760805f18a3d)
- [Dom veilles 1](https://codepen.io/alyra/pen/XWXwaeY) | [solution](https://codepen.io/alyra/pen/663748fcb0a8c328ad24d8b996e29392)
- [Dom veilles 2](https://codepen.io/alyra/pen/abdryWa) | [solution](https://codepen.io/alyra/pen/b4bb65ef7816f7675cb3629dee091c2d)
- [Date du jour](https://codepen.io/alyra/pen/mdVYMpJ) | [solution](https://codepen.io/alyra/pen/23049d07c690bcc660a40cbbf751ac7e)
