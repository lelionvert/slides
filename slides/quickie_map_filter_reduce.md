---
revealOptions:
	verticalSeparator: '\s----\s'
---
# Quickie Map / Filter / Reduce

---

## Prérequis

- Function
  - lambda / arrow function notation
  - First Citizen
    - Callback
    - Return Function
  - Pure Function ?
- Immutabilité ?
- Curry ?

---

## Map

----

### Exemple

Faire du popcorn

[🌽, 🌽, 🌽] => [🍿, 🍿, 🍿]

note: par exemple, j'ai un conteneur avec des épis de maïs que je voudrais transformer en pop corn

----

### Définition

**`map`** permet de **transformer** un _ensemble de données_ dans un **autre _ensemble de données_** de **même taille**. <!-- .element: class="fragment" data-fragment-index="1" -->

**`map`** permet d'appliquer une **transformation** à chaque éléments d'un _ensemble de données_, résultant à un **autre _ensemble de données_** de **même taille**. <!-- .element: class="fragment" data-fragment-index="1" -->

note:
	est-ce que quelqu'un peut essayer de donner une définition à la fonction map ?
	reviewer : choisir une définition

----

### Fonction de transformation / Mapper

----

#### Exemple

Chauffer

(🌽) => 🍿

note: pour reprendre l'exemple, pour transformer du maïs en pop corn, il suffit d'avoir quelque chose permettant de le chauffer

----

#### Définition

Une **fonction** permet de **transformer** une **donnée** dans un **autre type de donnée**. <!-- .element: class="fragment" data-fragment-index="1" -->

note:
	est-ce que quelqu'un peut essayer de donner une définition à un mapper ?
	reviewer : est-ce que "Mapper" c'est le bon terme ?

----

### Démo

```typescript
const chauffer = (épiDeMaïs) => "🍿"

const conteneurDÉpisDeMaïs = ["🌽", "🌽", "🌽"]

const conteneurDePopCorn = conteneurDÉpisDeMaïs.map(chauffer)

expect(conteneurDePopCorn).toEqual(["🍿", "🍿", "🍿"])
expect(conteneurDÉpisDeMaïs).toEqual(["🌽", "🌽", "🌽"])
```

note: map renvoit un nouveau tableau et ne change pas celui sur lequel la transformation est appliquée comme le montre les `expect`

----

### Exemple

Mettre 2 à la puissance `n` une suite de nombres

[`number`, `number`, `number`] => [`number`, `number`, `number`]

note:
	nouvel exemple, cette fois-ci plus concret : avec des nombres
	on peut voir que le type de sorti PEUT etre le meme que le type d'entré

----

### Démo

```typescript
const power2 = (someNumber) => 2 ** someNumber

const numbers = [1, 2, 3]

const numbersPowered = numbers.map(power2)

expect(numbersPowered).toEqual([2, 4, 8])
expect(numbers).toEqual([1, 2, 3])
```

---

## Filtre / Filter

----

### Exemple

[🍒, 🍅, 🍏, 🍅, 🍏] => [🍅, 🍅]

note: je voudrais récupérer toutes les tomates qui sont dans mon bac à fruits

----

### Définition

**`filter`** permet de **sélectionner** (filtrer) un **sous-_ensemble de données_** parmit un _ensemble de données_. <!-- .element: class="fragment" data-fragment-index="1" -->

note:
	est-ce que quelqu'un peut essayer de donner une définition à la fonction filter ?

----

### Prédicat / Predicate

----

#### Exemple

Est-ce que ce fruit est une tomate ?

(🍒|🍅|🍏) => `boolean`

----

#### Définition

Un **prédicat** est une **fonction** qui **vérifie** une **condition**. <!-- .element: class="fragment" data-fragment-index="1" -->

note:
	est-ce que quelqu'un peut essayer de donner une définition à un prédicat ?

----

### Démo

```typescript
const estCeUneTomate = (fruit) => fruit === "🍅"

const conteneurDeFruits = ["🍒", "🍅", "🍏", "🍅", "🍏"]

const conteneurDeTomate = conteneurDeFruits.filter(estCeUneTomate)

expect(conteneurDeTomate).toEqual(["🍅", "🍅"])
expect(conteneurDeFruits).toEqual(["🍒", "🍅", "🍏", "🍅", "🍏"])
```

note:
	filter renvoit un nouveau tableau et ne change pas celui sur lequel le filter est appliqué comme le montre les `expect`

----

### Exemple

Filtrer les nombres pairs d'une suite de nombres

[`number`, `number`, `number`, `number`, `number`, `number`] => [`number`, `number`, `number`]

----

### Démo

```typescript
const isEven = (someNumber) => someNumber % 2 === 0

const numbers = [1, 2, 3, 4, 5, 6]

const evenNumbers = numbers.filter(isEven)

expect(evenNumbers).toEqual([2, 4, 6])
```

---

## Reduce

----

### Exemple

Assembler une salade

[🍅, 🍏, 🥬] => 🥗

----

### Définition

`reduce` permet de **réduire** (transformer) un _ensemble de données_ en une **autre donnée**. <!-- .element: class="fragment" data-fragment-index="1" -->

note:
	est-ce que quelqu'un peut essayer de donner une définition à la fonction reduce ?

----

### Fonction de réduction / Reducer

----

#### Exemple

(🥗, 🥬) => 🥗

----

#### Définition

Un **reducer** est une **fonction** prend un **accumulateur** et un **élément** et retourne un **accumulateur**. <!-- .element: class="fragment" data-fragment-index="1" -->

note:
	est-ce que quelqu'un peut essayer de donner une définition à un reducer ?

----

### Démo

```typescript
const assembler = (salade, ingrédient) => "🥗"

const ingrédients = ["🍅", "🍏", "🥬"]

const salade = ingrédients.reduce(assembler, "🥣")

expect(salade).toEqual("🥗")
expect(ingrédients).toEqual(["🍅", "🍏", "🥬"])
```

note:
	pour commencer la salade, il faut d'abord avoir un bol vide qui se remplira un peu plus à chaque itération

----

### Exemple

Faire le produit d'une suite de nombres

[`number`, `number`, `number`] => `number`

`number * number * number === number`

----

### Démo

```typescript
const multiply = (accumulator, item) => accumulator * item

const numbers = [2, 3, 4]

const product = numbers.reduce(multiply, 1)

expect(product).toEqual(24)
```

<!-- markdownlint-disable MD033 -->
<div class="fragment" data-fragment-index="1">

|                             accumulator | item |                                  result |
|----------------------------------------:|-----:|----------------------------------------:|
|                                       1 |    2 |     <span style="color: green">2</span> |
|     <span style="color: green">2</span> |    3 | <span style="color: royalblue">6</span> |
| <span style="color: royalblue">6</span> |    4 |                                      24 |

</div>
<!-- markdownlint-enable MD033 -->

note:
	le résultat du reducer est utilisé en tant qu'accumulateur pour l'iteration suivante
	c'est pour cette raison que nous sommes obligé de fournir une valeur initiale : pour la première itération

---

## Tout en meme

Il possible de chainer les traitements sur les _ensembles de données_

----

### Exemple de la salade composée

Faire une salade avec ce qu'il y a dans mon frigo

[🍅, 🥔, 🍏, 🍅, 🥔, 🍏, 🥬] => 🥗

----

### Démo

```typescript
const estCeUnePommeDeTerre = (ingrédient) => ingrédient === "🥔"
const inverser = (prédicat) => (élément) => !prédicat(élément)
const cuire = (ingrédient) => `${ingrédient} cuit`
const couper = (ingrédient) => `${ingrédient} coupé`
const assembler = (salade, ingrédient) => "🥗"

const ingrédients = ["🍅", "🥔", "🍏", "🍅", "🥔", "🍏", "🥬"]

const ingrédientsCuits = ingrédients.filter(estCeUnePommeDeTerre).map(cuire)
const ingrédientsCrus = ingrédients.filter(inverser(estCeUnePommeDeTerre))

const ingrédientsÀCouper = [
	...ingrédientsCrus,
	...ingrédientsCuits,
]

const ingrédientCoupés = ingrédientsÀCouper.map(couper)

const salade = ingrédientCoupés.reduce(assembler, "🥣")

expect(salade).toEqual("🥗")
```

note:
	les pommes de terre crues sont toxiques pour l'humain, il faut d'abord les cuire pour les mettre dans la salade
	un prédicat renvoit toujours un `boolean` donc on peut inverser un prédicat en inversant la valeur de retour
	`filter` renvoit un tableau, donc on peut chainer le `map`

---

## Références

[filter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)

[map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

[reduce](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce)
