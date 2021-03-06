# Couleurs 🌈

CSS nous permet de colorier nos pages, en particulier avec des propriétés :  
`background-color`, `color`, `border`, `box-shadow`, `text-shadow`

Il y a plusieur possibilité pour décrire une couleur. Voici juste quelques possibilités de décrire la même nuance du rouge:
`red`,  
`#ff0000`,  
`#f00`,  
`rgb(255, 0, 0)`,  
`rgba(255, 0, 0, 0)`,  
`rgb(100%, 0, 0)`,  
`hsl(0, 100%, 50%)`

Nous allons maintenant déchiffrer tout cela.

1. La première possibilité est d'utiliser le nom de la couleur [keyword](https://developer.mozilla.org/fr/docs/Web/CSS/Type_color#Les_mots-cl%C3%A9s) (mot-clé) : `red`, `black`, `tomato`, `cornflowerblue`, ...., `transparent` et `currentColor`.

De cette façon nous pouvons décrire **147** couleurs différentes, sans compter `transparent` et `currentColor`

(voici un autre [site que les présente](http://www.colors.commutercreative.com/)).

Et si nous voulons aller au-déla ?

Chaque pixel sur l'écran est composé de trois petits points appelés luminophores entourés d'un masque noir.

Les trois luminophores distincts produisent respectivement de la lumière <span style="color:red;">rouge</span>, <span style="color:lime">verte</span> et <span style="color:blue;">bleue.</span>

Pour contrôler la couleur de chaque pixel sur l'écran, le système d'exploitation consacre une quantité de mémoire à chaque pixel.

Sur les premiers écrans en noir et blanc, pixel est allumé (1) ou éteint (0), un seul morceau de mémoire est affecté à chaque pixel - un bit de memoire.

Sur les écrans modernes 8 bits de mémoire sont affectés pour chaque couleurs (rouge, verte et bleue). Cela donne 2<sup>8</sup> = **256** valueurs possibles pour la couleur rouge, **256** pour la couleur verte et **256** pour la bleue, donc:

256 x 256 x 256 = **16 777 216** couleurs

- **rgb, rgba** (intensité du rouge (r), vert (g) et b (bleu) + opacité a (alpha)

[Playground - Couleurs RGB expliquées](https://cdpn.io/alyra/debug/b2c543699a8868342fb23ac6c9f6f73d)

```
p {
  color: rgb(255, 0, 0);
  background: rgb(255, 0, 0, 0.1);
}
```

- **code hexadecimal** (pareil que rgb, rgba mais en utilisant le système hexadécimal)

[Le fameux Quiz du Professeur Hervé B.\*](https://cdpn.io/alyra/debug/616e97467780239fc8927073fe284ec5)

- **hsl, hsla** Teinte h (hue), Saturation s, Luminosité (l)  
  [HSL Color Picker par Marton Borbely](https://codepen.io/HunorMarton/full/dvXVvQ)

Le format `hsl` est particulierement pratique pour gérér :

- les nuances et ombres (**juste le 3e paramètre change**):

```
/* Teinte de base */
background-color: hsl(14, 76%, 55%);

/* Plus foncée */
background-color: hsl(14, 76%, 75%);

/* Plus claire */
background-color: hsl(14, 76%, 35%);
```

- couleurs complémentaires (ajoter 180 - demi-tour au 1e paramètre):

```
/* Teinte de base */
color: hsl(14, 76%, 55%);

/* Couleur complémentaire */
color: hsl(194, 76%, 55%);
```

- couleurs complémentaires adjacentes (+/-120 au 1e paramètre):

```
/* Teinte de base */
color: hsl(14, 76%, 55%);

/* Couleur complémentaire adj. 1 */
color: hsl(134, 76%, 55%);

/* Couleur complémentaire adj. 1 */
color: hsl(254, 76%, 55%);
```

- couleurs similaires (analogous) (+/-30 au 1e paramètre):

```
/* Teinte de base */
color: hsl(14, 76%, 55%);

/* Couleur complémentaire adj. 1 */
color: hsl(44, 76%, 55%);

/* Couleur complémentaire adj. 1 */
color: hsl(74, 76%, 55%);
```

[HSL en action - 1](https://codepen.io/alyra/pen/RwrPBxB)
[HSL en action](https://cdpn.io/alyra/debug/LYpoYPY)

C'est déjà pas mal, et pourtant - des nouvelles couleurs arrivent - pour l'instant uniquement dans le navigateur Safari [CodePen](https://codepen.io/cssgrid/pen/KKpLBom)

[Contrast checker](https://webaim.org/resources/contrastchecker/)

## Background

[Playground - size/repeat/position](https://codepen.io/alyra/debug/ExPxpyw)
[Playground - linear-gradient](https://codepen.io/alyra/debug/bGEdmMM)

## Exercices

- [hsl colors](https://codepen.io/alyra/pen/JjGdBwM) | [solution](https://codepen.io/alyra/pen/24600deab70bf2bd797c1e39fbedec24)
