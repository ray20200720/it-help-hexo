---
title: Hello, JavaScript!
---

今天發現了學習JavaScript很好的網站,網站名稱是[Hello, JavaScript!](https://courses.cs.northwestern.edu/394/guides/intro-js.php).在此記錄一下

## Function calls

```js
Math.hypot(3, 4)
Math.hypot(5, 12)
Math.hypot(3, 4, 5)
```

## Function definitions

``` js
const circum = (r) => 2 * r * Math.PI;

circum(30)
```

The general form of a function definition is

``` js
const function-name = (list-of-variable-names) => expression;
```

Here's a function that returns the average of three numbers:

``` js
const ave3 = (x, y, z) => (x + y + z) / 3;

ave3(10, 32, 18)
```

## Function blocks


``` js
const triangleArea = (a, b, c) => {
    const s = (a + b + c) / 2;
    return Math.sqrt(s * (s - a) * (s - b) * (s - c));
};

triangleArea(3, 4, 5)
```

The general form of a function block is

``` js
const function-name = (parameter-list) => {
  statement;
  statement;
  ...
  return expression;
}
```





