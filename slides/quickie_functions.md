---
title: Quickie Functions
revealOptions:
    verticalSeparator: '\s----\s'
---
# Quickie Functions

---

## Prérequis

- Aucun

---

## Définition

<div class="fragment" data-fragment-index="1">

Une fonction est une **portion de code** :

- qui _doit_ **être déclarée**
- qui _peut_ **être nommée**
- qui _peut_ contenir une **suite d'instructions**
- qui _peut_ **être appelée** après avoir été déclarée
- qui _peut_ **prendre des arguments**
- qui _peut_ **retourner une valeur**

</div>

note:
est-ce que quelqu'un peut essayer de donner une définition de ce qu'est une fonction ?

---

## `function` keyword

----

### Déclaration

```javascript
it("should allow using functions", () => {
  function increment(n) {
    return n + 1;
  }
  expect(increment(0)).toEqual(1);
});
```

note:

- ligne 2 : une fonction est déclarée
- ligne 2 : elle est nommée `increment`
- ligne 3 : elle a une instruction qui est une addition
- ligne 5 : elle est appelé
- ligne 2 : elle prend un argument nommé `n`
- ligne 3 : elle retourne le résultat de sa dernière instruction

----

#### Hissage / Hoisting

```javascript
it("Function declarations are hoisted", () => {
  expect(increment(0)).toEqual(1);
  function increment(n) {
    return n + 1;
  }
});
```

note:
les fonctions déclarées avec le mot clé `function` sont "hissées" lors de la compilation du fichier et peuvent donc être appelées avant d'être déclarées

----

#### Fonction Anonyme / Anonymous Function

```javascript
it("Function declarations can be anonymous", () => {
  const increment = function(n) {
    return n + 1;
  };
  expect(increment(0)).toEqual(1);
});
```

note:
les fonctions peuvent ne pas avoir de nom, on appelle ça une fonction anonyme

dans ce cas, la variable a un nom mais pas la fonction

---

## Fonctions fléchées / Arrow functions

note:
les fonctions fléchées sont une syntaxe alternative au mot clé `function`

dans la plupart des cas, c'est complètement équivalent

----

### Déclaration

```javascript
it("should allow using arrow functions", () => {
  const increment = (n) => {
    return n + 1;
  };
  expect(increment(0)).toEqual(1);
});
```

note:
par rapport à l'exemple précédent :

- on a enlever le clé `function`
- on a enlever ajouté la fat arrow `=>` entre l'argument et le block d'instructions

----

#### Arguments

##### Arguments multiple

```javascript
it("should allow to have several arguments", () => {
  const add = (n, k) => {
    return n + k;
  };
  expect(add(0, 1)).toEqual(1);
});
```

##### Simplification avec 1 argument

```javascript
it("should allow to omit braces", () => {
  const increment = n => {
    return n + 1;
  };
  expect(increment(0)).toEqual(1);
});
```

----

#### Instructions

##### Instructions multiple

```javascript
it("should contain multiple instructions", () => {
  const increment = n => {
    const x = n - 1;
    return x + 2;
  };
  expect(increment(0)).toEqual(1);
});
```

----

##### Simplification avec 1 instruction

Instruction simple

```javascript
it("should allow to omit braces and return", () => {
  const increment = n => n + 1;
  expect(increment(0)).toEqual(1);
});
it("should allow to return array", () => {
  const initArrayWith = n => [n];
  expect(initArrayWith(42)).toEqual([42]);
});
```

Object
<!-- .element: class="fragment" data-fragment-index="1" -->

```javascript
it("should allow to return object", () => {
  // const euro = euro => ({ euro: euro });
  const euro = euro => ({ euro });
  expect(euro(42)).toEqual({ euro: 42 });
});
```
<!-- .element: class="fragment" data-fragment-index="2" -->

note:
pour un objet, on ne peut pas seulement mettre des accolades, sinon ça ferait un block d'instructions, dans ce cas, il faut entourer les accolades avec des parenthèses

---

## Fonctions de première classe / First Class Citizen

note:
les fonctions sont de première classe, elles peuvent être traitées comme n'importe quelle variable

----

### Assign

```javascript
it("should allow to assign a function to a variable", () => {
  const increment = function(n) {
    return n + 1;
  };
  expect(increment(0)).toEqual(1);
});
```

----

### Argument / Callback

```javascript
it("should allow to pass a function as a callback", () => {
  function increment(n, callback) {
    const result = n + 1;
    callback(result);
    return result;
  }
  const callback = jest.fn();
  increment(0, callback);
  expect(callback).toHaveBeenCalledWith(1);
});
```

----

### Return

```javascript
it("should allow to return a function", () => {
  function toPower(exponent) {
    return function(n) {
      return n ** exponent;
    };
  }
  const toPower2 = toPower(2);
  expect(toPower2(3)).toEqual(9);
});
```

---

## Parameters

----

### Default parameters

```javascript
it("should take default parameter", () => {
  const hello = (name="world") => `Hello ${name} !`;
  expect(hello()).toEqual("Hello world !");
  expect(hello("dev")).toEqual("Hello dev !");
});
```

----

### Rest parameters

```javascript
it("should take rest parameters", () => {
  const concat = (glue, ...parts) => parts.join(glue);
  expect(concat("&", "Pepper", "Carrot")).toEqual("Pepper&Carrot");
});
```

---

## IIFE

Immediately Invoked Function Expression

```javascript
it("Function declarations can be immediately invoked", () => {
  const increment = (function(n) {
    return n + 1;
  })(0);
  expect(increment).toEqual(1);
});
```

note:
il est possible d'éxécuter une fonction directement après sa déclaration

généralement, ce sont des fonctions anonymes

ce n'est pas souvent utilisé mais ça peut etre utile pour certains besoins spécifiques avancés

---

## Références

- [Exemple](https://github.com/lelionvert/js-intro/tree/master/Functions)
- [Fonction](https://developer.mozilla.org/fr/docs/Glossaire/Fonction)
- [Hoisting](https://developer.mozilla.org/fr/docs/Glossaire/Hoisting)
- [First Class Citizen](https://developer.mozilla.org/fr/docs/Glossaire/Fonction_de_premi%C3%A8re_classe)
- [IIFE](https://developer.mozilla.org/fr/docs/Glossaire/IIFE)
