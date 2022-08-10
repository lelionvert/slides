---
title: Quickie Pure Function
revealOptions:
    verticalSeparator: '\s----\s'
---
# Quickie Pure Function

---

## Prérequis

- [Function](./quickie_functions.md)

---

## Définitions

----

### Fonction Pure / Pure Function

<div class="fragment">

Une fonction pure est une fonction qui respecte 2 propriétés :

- qui _est_ une fonction **déterministe**
- qui _ne doit pas_ faire d'**effets de bord** / side effects

</div>

----

### Déterministe / Deterministic

<div class="fragment">

Une fonction détermiste a pour le _même argument_ **toujours** la _même_ valeur de _retour_

</div>

----

### Effets de Bord / Side Effects

<div class="fragment">

Une fonction fait un effet de bord lorsqu'elle **lit ou modifie** quelque chose qui est est en **dehors** de ses **paramètres**

</div>

----

## Transparence Référencielle / Referencial Transparency

La **transparence référencielle** permet de remplacer l'appel à une fonction par la valeur qu'elle retourne

----

```typescript
const add = (value1: number, value2: number): number =>
    value1 + value2

const a = add(3, 4)
// équivalent à
const a = 7
```

----

Une fonction pure permet de faire de la **transparence référencielle**

---

## Exemples

Est-ce que la fonction est pure ?

```typescript
const toto = () => 42
```

----

```typescript
const identity = x => x
```

----

```typescript
const add = (value1: number, value2: number): number =>
    value1 + value2
```

----

```typescript
const today = (): Date => new Date()
```

note:
    lit la date depuis le système

----

```typescript
fetch('http://perdu.com')
```

note:
    fait des I/O

----

```typescript
max(3, 12, 4)
```

----

```typescript
console.log('coucou')
```

----

```typescript
const addTo(array: number[], item: number): number[] => {
    array.push(item)
    return array
}
```

note:
    mute un argument

----

```typescript
const addTo(array: number[], item: number): number[] => {
    return array.concat(item)
}
```

----

```typescript
const fizzBuzz = (value: number): string => {
    switch (true) {
        case 0 == value % 15: return "FizzBuzz"
        case 0 == value %  5: return "Buzz"
        case 0 == value %  3: return "Fizz"
        default: return `${value}`
    }
}
```

----

```typescript
const getConfigPort = (): number => {
    return Number.parseInt(process.env.PORT)
}
```

note:
    lit une variable globale

---

## Code Smells

- I/O (Input / Ouput)
  - lire / écrire un fichier
  - faire une requete réseau
- fonction sans argument
  - qui ne retourne pas une valeur constante
- mutation d'un argument
- variable globale
- lecture d'une valeur cachée
  - date
  - random
- lancer une exception
