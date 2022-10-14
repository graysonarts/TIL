---
tags: [ dev/javascript/typescript, dev/javascript/typescript, dev/functional ]
date: 2022-08-29
title: Type Predicates in Typescript
---

 it’s SUPER helpful when iterating through lists of types that are `x | undefined` and you want to filter out all the `undefined`.
 
 Documentation is in the [Typescript Handbook: Narrowing](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#using-type-predicates) but it looks like this:

```typescript
type T = number | undefined;

const values: T[] = [ 1, 2, 3, undefined, 4, 5 ];
const numbersOnly: number[] = values
   .filter((x): x is number => Boolean(x));

// 1, 2, 3, 4, 5
```


That `x is number` is a type predicate and it asserts that every value that matches the filter will be a `number` type.