# JavaScript Number Methods

以下是 JavaScript 的 Number Methods 簡單整理。

<br />

## Number.isNaN()

用於判斷一個值是否為 NaN。`Number.isNaN()` 比全域的 `isNaN()` 更精確，因為 `Number.isNaN()` 只會在傳入的參數是 NaN 時才返回 true，全域的 `isNaN()` 則會將參數強制轉換為數字類型，再進行判斷。

```
console.log(Number.isNaN(NaN));   // true
console.log(Number.isNaN("hello"));   // false
console.log(Number.isNaN(123));   // false
```

<br />

## Number.isFinite()

檢查一個數字是否是有限的 (不是 Infinity 或 -Infinity，也不是 NaN)。

```
console.log(Number.isFinite(123));   // true
console.log(Number.isFinite(Infinity));   // false
console.log(Number.isFinite(NaN));   // false
```

<br />

## Number.isInteger()

檢查一個數字是否為整數。

```
console.log(Number.isInteger(4));   // true
console.log(Number.isInteger(4.5));   // false
```

<br />

## Number.parseFloat()

將字符串解析為浮點數。

```
console.log(Number.parseFloat("3.14"));   // 3.14
console.log(Number.parseFloat("3.14abc"));   // 3.14
```

<br />

## Number.parseInt()

將字符串解析為整數，並可選擇指定基數 (radix)。

```
console.log(Number.parseInt("123"));   // 123
console.log(Number.parseInt("123abc"));   // 123
console.log(Number.parseInt("10", 2));   // 2 (二進位)
```

<br />

## Number.isSafeInteger()

檢查一個數字是否為安全整數。安全整數是指在 JavaScript 中可精確表示的整數範圍內的整數 (在 -(2^53 - 1) 和 2^53 - 1 之間的整數)。

```
console.log(Number.isSafeInteger(10));   // true
console.log(Number.isSafeInteger(Math.pow(2, 53)));   // false
```

<br />

## Number.MAX_VALUE()

表示 JavaScript 可表示的最大數值。

```
console.log(Number.MAX_VALUE);   // 1.7976931348623157e+308
```

<br />

## Number.MIN_VALUE()

表示 JavaScript 可表示的最小正數值 (接近 0，但不是 0)。

```
console.log(Number.MIN_VALUE);   // 5e-324
```

<br />

## Number.NEGATIVE_INFINITY

表示負無窮大。

```
console.log(Number.NEGATIVE_INFINITY);   // -Infinity
```

<br />

## Number.POSITIVE_INFINITY

表示正無窮大。

```
console.log(Number.POSITIVE_INFINITY);   // Infinity
```

<br />

## Number.prototype.toFixed()

將數字格式化為固定小數位數的字符串。

```
console.log((123.456).toFixed(2));   // 123.46
```
