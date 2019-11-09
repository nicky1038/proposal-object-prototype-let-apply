# Object.prototype.{let, apply}

Add `let` and `apply` methods to Object.prototype.

## Status

Author(s): Nikolay Kudryavtsev

Stage: -1

## Motivation

### Allow advanced chaining

```javascript
//instead of
const tempArr = inputArray
 .filter(predicate1)
 .map(transform);
 
const result = someArrayTransformationMethod(tempArr)
 .filter(predicate2);
 
 // do
 const result = inputAyray
  .filter(predicate1)
  .map(transform)
  .let(someArrayTransformationMethod)
  .filter(predicate2);
```

### Produce more readable code

Separating the object mutation logic into separate function (which is passed to `apply` method) reduces user's cognitive load when reading the code.
It's also possible for this function not to be an anonymous lambda but a stored/named one, and one can apply it to the object without losing chaining.

### Other notes

Proposed methods go very well with [optional chaining](https://github.com/tc39/proposal-optional-chaining) proposal.

## Description

These two methods are the same as `let` and `also` methods in Kotlin language.

###`let`

```typescript
// Typescript type definition
let<T : any, R>(this: T, transform: (t: T) => R): R
```

Takes a given `transform` function, applies it to the object on which `let` method was called, and returns the result if `transform` function.

###`apply`

```typescript
// Typescript type definition
apply<T : any, R>(this: T, action: (t: T) => void): T
```

Takes a given `transform` function, applies it to the object on which `let` method was called, and return this object.