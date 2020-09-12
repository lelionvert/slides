---
title: Quickie scopes, closures and this
revealOptions:
	verticalSeparator: '\s----\s'
---

# Quickie scopes, closures and this

---

## `var`, `let`, `const`

There's no reason to use `var`.

You should use `let` and `const`

(and try to stick with `const`)

---

## Scopes

Blocks create new scopes

(simple braces, for and while loops, try/catch statements)

```javascript
it("Blocks create new scopes", function() {
  {
    const a = 0;
  }
  expect(() => a).toThrow();
});
```

----

...except with `var`

----

Functions create new scopes

```javascript
it("Functions create new scopes", function() {
  function doSomething() {
    const a = 0;
    return;
  }
  doSomething();
  expect(() => a).toThrow();
});
```

----

A child scope has access to its parent's scope

```javascript
it("A child scope has access to its parents scope", function() {
  const a = 0;
  function doSomething() {
    expect(a).toEqual(0);
    return;
  }
  doSomething();
});
```

----

Shadowing is possible

```javascript
it("Shadowing is possible", function() {
  const a = 0;
  function doSomething() {
    const a = 1;
    return;
  }
  doSomething();
  expect(a).toEqual(0);
});
```

---

## Closures

----

1. Functions car return functions;

2. A child scope has access to its parent's scope.

----

A closure is a function with its scope

(called "lexical scope")

```javascript
it("A simple closure", function() {
  function times(i) {
    return function(n) {
      return i * n;
    };
  }
  const times2 = times(2);
  expect(times2(2)).toEqual(4);
});
```

---

## `this` (from 😱 to 😎)

----

You can write code using `this` or not using `this` 😂

----

`this` refers to the current object

```javascript
it("this refers to the current object", function() {
  const square = {
    size: 6,
    computeSurface: function() {
      return this.size ** 2;
    }
  };
  expect(square.size).toEqual(6);
  expect(square.computeSurface()).toEqual(36);
});
```

----

Functions being objects, `this` also make sense in the case of functions...

```javascript
it("Should allow creating objects with constructor functions", function() {
  function Square(size) {
    this.size = size;
    this.computeSurface = function() {
      return this.size ** 2;
    };
  }
  const square = new Square(6);
  expect(square.size).toEqual(6);
  expect(square.computeSurface()).toEqual(36);
});
```

----

...or should I say classes

```javascript
it("Should allow creating classes", function() {
  class Square {
    constructor(size) {
      this.size = size;
    }
    computeSurface() {
      return this.size ** 2;
    }
  }
  const square = new Square(6);
  expect(square.size).toEqual(6);
  expect(square.computeSurface()).toEqual(36);
});
```

----

But `this` goes with some pitfalls

```javascript
it("this should be undefined", function() {
  class Square {
    constructor(size) {
      this.size = size;
    }
    computeSurface() {
      return this.size ** 2;
    }
  }

  const square = new Square(6);
  const computeSurface = square.computeSurface;
  expect(computeSurface).toThrowError("Cannot read property 'size' of undefined");
});
```

----

Why? Because the value of `this` is determined by the call site

----

`.bind()` to the rescue

```javascript
it("this should be defined again!", function() {
  class Square {
    constructor(size) {
      this.size = size;
    }
    computeSurface() {
      return this.size ** 2;
    }
  }

  const square = new Square(6);
  const boundComputeSurface = square.computeSurface.bind(square);
  expect(boundComputeSurface()).toEqual(36);
});
```

----

Or `.call()` if you prefer

```javascript
it("this should be defined", function() {
  class Square {
    constructor(size) {
      this.size = size;
    }
    computePerimeter() {
      return this.size * 4;
    }
  }
  const square = new Square(6);
  const computePerimeter = square.computePerimeter;
  const diamond = {
    size: 10
  };
  expect(computePerimeter.call(diamond)).toEqual(40);
});
```

----

Here fat arrow functions are helpful as well

```javascript
it("this should be defined again!", function() {
  class Square {
    constructor(size) {
      this.size = size;
    }
    computeSurface = () => this.size ** 2;
  }
  
  const square = new Square(6);
  const computeSurface = square.computeSurface;
  expect(computeSurface()).toEqual(36);
});
```
