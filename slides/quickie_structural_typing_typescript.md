---
title: Quickie structural typing in TypeScript
revealOptions:
	verticalSeparator: '\s----\s'
---

# Quickie structural typing in TypeScript

---

## Nominal typing

A type is defined by its name.

----

In Java, this:

```Java
public class ProductId {
    private String id;

    public ProductId(String id) {
        this.id = id;
    }

    public String getId() {
        return this.id;
    }
}
```

----

...and this:

```Java
public class ClientId {
    private String id;

    public ClientId(String id) {
        this.id = id;
    }

    public String getId() {
        return this.id;
    }
}
```

----

...are two different things, because their names differ (`ProductId` vs. `ClientId`)

---

## Structural typing

A type is defined by its shape (the list of its attributes).

----

In TypeScript, this:

```typescript
interface ProductId {
    id: string;
}
```

and this:

```typescript
interface ClientId {
    id: string;
}
```

----

are the same thing, because their shape is the same:

```typescript
{
    id: string;
}
```

---

### Why structural typing?

"Because once compiled in JavaScript, there are no more types"

---

### Consequences

Some mistakes might not be spotted by the compiler:

```typescript
function getClient(clientId: ClientId): Client {
    ...
}

const productId: ProductId = {
    id: "4b86e42a-19e7-43b6-a9f5-249000d1f820"
}

const client = getClient(productId); // this won't fail
```

---

### How to mitigate that?

You could add a `type` field to emulate nominal typing:

```typescript
interface ProductId {
    type: "PRODUCT";
    id: string;
}

interface ClientId {
    type: "CLIENT";
    id: string;
}
```

---

## The final word

[https://www.typescriptlang.org/docs](https://www.typescriptlang.org/docs)
