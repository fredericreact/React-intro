# Récap

Faisons un petit point.

---

## Programmation fonctionnelle
<!-- .slide: data-background="#e98c36" -->



### [`.forEach()`](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Objets_globaux/Array/forEach)

Exécute une fonction pour chaque élément du tableau.
<!-- .element: class="fragment" -->

```js
var numbers = [1, 2, 3, 4, 5, 6];

// Affiche chaque nombre
numbers.forEach(function(number) {
  console.log('Le nombre est : ' + number);
});
```
<!-- .element: class="fragment" -->



### [`.map()`](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Objets_globaux/Array/map)

Renvoie un nouveau tableau modifié / transposé.
<!-- .element: class="fragment" -->

```js
var numbers = [1, 2, 3, 4, 5, 6];

// [1, 4, 9, 16, 25, 36]
var squares = numbers.map(function(number) {
  return number * number;
});
```
<!-- .element: class="fragment" -->



### [`.filter()`](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Objets_globaux/Array/filter)

Renvoie un nouveau tableau avec les éléments correspondants.
<!-- .element: class="fragment" -->

```js
var numbers = [1, 2, 3, 4, 5, 6];

// [2, 4, 6]
var evenNumbers = numbers.filter(function(number) {
  return number % 2 === 0;
});
```
<!-- .element: class="fragment" -->



### [`.find()`](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Objets_globaux/Array/find)

Renvoie le premier élément qui respecte la condition.
<!-- .element: class="fragment" -->

```js
var numbers = [1, 2, 3, 4, 5, 6];

// 3
var numberSupTwo = numbers.find(function(number) {
  return number > 2;
});
```
<!-- .element: class="fragment" -->



### Je savais déjà faire...

Tout ça, on pouvait le faire avec un `for`
		
- For, c'est plus rapide ! <!-- .element: class="fragment" -->
- For, c'est plus compatible ! <!-- .element: class="fragment" -->

Mais... <!-- .element: class="fragment" -->
		
- C'est moins lisible <!-- .element: class="fragment" -->
- C'est moins modulaire <!-- .element: class="fragment" -->



## Autres rappels



### Problème de portée

`var` : portée globale au contexte d'exécution.

```js
var names = ['Riri', 'Fifi', 'Loulou'];
var len = names.length;

for(var index = 0; index < len; index++) {
  setTimeout(function() {
    console.log('Hello ' + names[index]);
  }, 1000 * index);
}

// L'index est déjà passé à 4 ! Cela affiche donc :
// 0ms: Hello undefined
// 1000ms: Hello undefined
// 2000ms: Hello undefined
```
<!-- .element: class="fragment" -->



#### Solutions

- `.forEach()` - fonction : nouvelle portée de variable.
- IIFE ou fonction séparée - valeur copiée dans une nouvelle portée.
- `let` - portée limitée au bloc.

Avec `.forEach()`
<!-- .element: class="fragment" -->

```js
var names = ['Riri', 'Fifi', 'Loulou'];

names.forEach(function(name, index) {
  setTimeout(function() {
    console.log('Hello ' + name);
  }, 1000 * index);
});

// 0ms: Hello Riri
// 1000ms: Hello Fifi
// 2000ms: Hello Loulou
```
<!-- .element: class="fragment" -->



### Callback

Une approche généraliste

```js
function handleFormSubmit(event) {
  event.preventDefault();
  // ...
}

form.addEventListener('submit', handleFormSubmit);
```

---

## Programmation déclarative
<!-- .slide: data-background="#e98c36" -->



### Paradigme Déclaratif

On veut limiter/cacher le code _plomberie_.

On automatise tout ce qui peut l'être (merci les fonctions & callbacks).

On se concentre sur le résultat, on laisse la machine travailler / optimiser.



### Applications réactives & déclaratives

- On s'appuie sur des données (état / state) <!-- .element: class="fragment" -->
- Une logique de rendu initial propre… <!-- .element: class="fragment" -->
- On écoute les événements / interactions… <!-- .element: class="fragment" -->
- Dès qu'une donnée change, on redessine toute l'application ! <!-- .element: class="fragment" -->



### Quid des performances ?

- C'est pas important… <!-- .element: class="fragment" -->
- Bon, si, un peu… Mais on va déléguer… <!-- .element: class="fragment" -->
- React et son virtualdom ! <!-- .element: class="fragment" -->

---

## JavaScript - ECMAScript
<!-- .slide: data-background="#e98c36" -->



### ES2015+ ou ES6+

ECMAScript à partir de 2015 / de la version 6

> On a vu quelques nouveautés de syntaxe 

**A ne pas utiliser en production !** <!-- .element: class="fragment" -->

A moins de transpiler le code avec babel <!-- .element: class="fragment small" -->

Ce qu'on va faire aujourd'hui :) <!-- .element: class="fragment small" -->




### Exemples

<ul>
  <li><code>let</code> : portée se limitant au bloc</li>
  <li class="fragment"><code>const</code> : référence constante limitée au bloc</li>
  <li class="fragment"><code>() => {}</code> : fonctions flechées</li>
  <li class="fragment"><code>`Hello ${name}`</code> : littéraux de gabarits</li>
  <li class="fragment"><code>(...args) => {}</code> : paramètre du reste</li>
  <li class="fragment"><code>{ data }</code> = <code>{ data: data }</code> : propriété raccourcie</li>
</ul>



### Destructuration 1/3

Destructurer ou "éclater" un objet.

```js
const data = {
  firstname: 'Parker',
  lastname: 'Lewis',
};

// Stockage de chaque valeur de l'objet data
const firstname = data.firstname; // 'Parker'
const lastname = data.lastname; // 'Lewis'

// Équivalent avec le destructuring
const { firstname, lastname } = data;

```



### Destructuration 2/3

Destructurer ou "éclater" un tableau.

```js
const students = ['Hannah', 'Coraline', 'Fred'];

// Stockage de chaque valeur du tableau students
const first = students[0]; // 'Hannah'
const second = students[1]; // 'Coraline'
const last = students[2]; // 'Fred'

// Équivalent avec le destructuring
const [first, second, last] = students;

```



### Destructuration 3/3

Destructurer ou "éclater" un objet dans les paramètres d'une fonction.

```js
// La fonction display va recevoir un objet
// on peut le destructurer directement
function display({ firstname, lastname }) {
  alert(`Bienvenue ${firstname} ${lastname} !`);
};

// Objet de données
const data = {
  firstname: 'Parker',
  lastname: 'Lewis',
};

// Exécution en passant data en argument
display(data);

```

---

## Les outils
<!-- .slide: data-background="#e98c36" -->



## npm

Gestionnaire de paquets

Un incontournable dans l'écosystème JS 
<!-- .element: class="fragment " -->



### Node Package Manager 1/3

Pour Node ? Oui, mais pas que !

`npm` s'appuie sur la plateforme https://www.npmjs.com/

- Multiples modules / packages pour le JavaScript en général.
- Pour le back et le front, par exemple `express` (back) et `react` (front)
- Même des outils annexes comme : `bulma`, `bootstrap`, etc...



### Node Package Manager 2/3

Quelques commandes à savoir

<ul>
  <li class="fragment"><code>npm init</code> : crée un fichier <code>package.json</code></li>
  <li class="fragment"><code>npm install</code> : installe les packages présents dans <code>package.json</code></li>
  <li class="fragment"><code>npm install react</code> : installe le package nommé "react"</li>
  <li class="fragment"><code>npm uninstall react</code> : désinstalle le package nommé "react"</li>
  <li class="fragment"><code>npm install react --save</code> : installe react et le rajoute aux dépendances dans package.json</li>
  <li class="fragment"><code>npm install webpack --save-dev</code> : installe "webpack" et le rajoute aux dépendances de dev dans package.json</li>
</ul>



### Node Package Manager 3/3

`yarn` : une version améliorée de `npm`

Plus rapide, plus secure, plus joli.

<ul>
  <li class="fragment"><code>yarn init</code> = <code>npm init</code></li>
  <li class="fragment"><code>yarn</code> = <code>npm install</code></li>
  <li class="fragment"><code>yarn add react</code> = <code>npm install react --save</code></li>
  <li class="fragment"><code>yarn remove react</code> = <code>npm uninstall react --save</code></li>
  <li class="fragment"><code>yarn add webpack --dev</code> = <code>npm install webpack --save-dev</code></li>
</ul>



## Webpack

Notre outil de build

Modularise, transpile et compresse notre code 
<!-- .element: class="fragment" -->

Gère tous les assets (JS, styles, images). 
<!-- .element: class="fragment" -->



## Babel

Transpile le code ES2015+ en code ES5

Via un module à rajouter, Babel transpile aussi le JSX
<!-- .element: class="fragment" -->



## ESLint

Un linter JavaScript éprouvé.



### Linter 1/2

Analyse le code, fournit des conseils et des bonnes pratiques, aide au formatage, ...

- Votre meilleur ami. <!-- .element: class="fragment" -->
- Vous pouvez comptez sur lui. <!-- .element: class="fragment" -->
- Parfois un peu agaçant car il a toujours raison :P <!-- .element: class="fragment" -->



### Linter 2/2

On va utiliser la configuration proposée par un acteur important de la communauté JS

**Airbnb**

---

## Rentrons dans le vif
<!-- .slide: data-background="#e98c36" -->



### Modules

Webpack va créer un module pour chaque fichier `.js` utilisés dans le dossier `src/` du projet.

- `import` : permet d'importer un module
- `export` ou `export default` : permet d'exporter une donnée



#### ES2015 modules (ESM) 1/3

`export` est utilisé lorsque l'on souhaite exporter plusieurs données.

On appelle ça des **exports nommés**. On exporte directement la variable.

```js
// src/maths/operations.js

// Export de sum
export const sum = (a, b) => a + b;
// Export de multiply
export const multiply = (a, b) => a * b;

```



#### ES2015 modules (ESM) 2/3

`export default` est utilisé lorsque l'on souhaite exporter une donnée en particulier.

On appelle ça un **export par défaut**. On exporte directement le contenu de la variable.

```js
// src/maths/index.js
const createSum = number1 => number2 => number1 + number2;
const addTwo = createSum(2);

export default addTwo;
```



#### ES2015 modules (ESM) 3/3

La phase d'importation diffère selon le type d'export.

```js
// Import de l'export par défaut de src/maths/index.js
import addTwo from 'src/maths';

// Import des exports de src/maths/operations.js
import { sum, multiply } from 'src/maths/operations';
```



### React & ReactDOM

```js
// Pour construire nos composants
import React from 'react';

// Pour rendre un composant dans le dom
import { render } from 'react-dom';
```



#### JSX

```js
// On importe ce dont on a besoin
import React from 'react';
import Screen from 'src/components/Screen';
import Chat from 'src/components/Chat';

// On fait notre cuisine
const Cockpit = () => (
  <div id="cockpit">
    <Chat />
    <Screen title="En route vers React" />
  </div>
);

// On exporte le composant
export default Cockpit;
```

---

# Allons coder !
