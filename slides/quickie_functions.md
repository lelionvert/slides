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

note:
TODO pour plus tard, peut-être que cette partie on devrait commencer par des fonctions sans arguments
Et faire une section dédiée aux arguments / paramètres puis enchaîner sur function anonyme et la suite

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

----

### Question 

#### Est-ce que ce code est valide ? 

```javascript
it("Does it work ?", () => {
  expect(increment(0)).toEqual(1);
  const increment = function(n) {
    return n + 1;
  };
});
```

note:
Une expression de fonction est hissée, mais une déclaration de variable ne l'est pas 

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

- on a enlevé le mot clé `function`
- on a ajouté la fat arrow `=>` entre l'argument et le block d'instructions

----

#### Arguments / Paramètres

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

#### Default parameters

```javascript
it("should take default parameter", () => {
  const hello = (name="world") => `Hello ${name} !`;

  expect(hello()).toEqual("Hello world !");
  expect(hello("dev")).toEqual("Hello dev !");
});
```

----

#### Rest parameters

```javascript
it("should take rest parameters", () => {
  const concat = (glue, ...parts) => parts.join(glue);

  expect(concat("&", "Pepper", "Carrot")).toEqual("Pepper&Carrot");
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

<div class="fragment" data-fragment-index="1">
Object

```javascript
it("should allow to return object", () => {
  // const euro = euro => ({ euro: euro });
  const euro = euro => ({ euro });
  expect(euro(42)).toEqual({ euro: 42 });
});
```
</div>

note:
pour un objet, on ne peut pas seulement mettre des accolades, sinon ça ferait un block d'instructions, dans ce cas, il faut entourer les accolades avec des parenthèses

---

## Fonctions de première classe / Function as First Class Citizen

note:
Un langage a des fonctions dites de premières classes s'ils traitent les fonctions comme des entités de premières classes, càd elles peuvent être traitées comme n'importe quelle variable

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

----

### Fonction d'ordre supérieur / Higher order function

```javascript
it("should be possible to have higher order function", () => {
  function higherOrderFunction(anyFunction) {
    return function callTwice(n) {
      return anyFunction(anyFunction(n));
    };
  }
  const incrementTwice = higherOrderFunction(n => n + 1);
  expect(incrementTwice(1)).toEqual(3);
});
```

note:
Si une fonction prend en argument une fonction ou retourne une fonction, c'est une fonction d'ordre supérieure
Faire un lien avec la slide de composition d'après. On a anyFunction(anyFunction(n)), c'est de la composition

---

## Composition

----

### Diviser pour conquérir, 
### mais assembler pour conduire 

note:
on assemble des fonctions plus simples pour faire des fonctions plus compliquées 
ça nous permet d'écrire des petites fonctions qui ne font qu'une seule chose (reuse ++ et maintenabilité ++)

----

```javascript
it("should be possible to compose functions", () => {
  const increment = n => n + 1;
  const powerTwo = n => n ** 2;
  
  const powerTwoAndIncrement = n => increment(powerTwo(n))

  expect(powerTwoAndIncrement(2)).toEqual(5);
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
