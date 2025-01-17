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
