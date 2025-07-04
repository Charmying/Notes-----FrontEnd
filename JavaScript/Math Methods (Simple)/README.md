# JavaScript Math Methods

以下是 JavaScript 的 Math Methods 整理。

<br />

## Math.random()

返回一個 0 到 1 之間的隨機數，不包含 1。`Math.random()` 常用來生成隨機數或進行隨機選取。

```
console.log(Math.random());   // 0.123456789
```

<br />

## Math.round(x)

將數字四捨五入到最接近的整數。小數部分小於 0.5 則向下取整數，大於等於 0.5 則向上取整數。

```
console.log(Math.round(5.4));   // 5
console.log(Math.round(5.5));   // 6
```

<br />

## Math.floor(x)

將數字向下取整數，也就是取最接近的、比該數字小的整數。

```
console.log(Math.floor(4.9));   // 4
console.log(Math.floor(-3.1));   // -4
```

<br />

## Math.ceil(x)

將數字向上取整數，也就是取最接近的、比該數字大的整數。

```
console.log(Math.ceil(4.2));   // 5
console.log(Math.ceil(-7.8));   // -7
```

<br />

## Math.trunc(x)

去除數字的小數部分，僅返回整數部分。

```
console.log(Math.trunc(4.9));   // 4
console.log(Math.trunc(-4.9));   // -4
```

<br />

## Math.abs(x)

返回一個數的絕對值，也就是該數在數線上距離零的距離，無論是正數還是負數。

```
console.log(Math.abs(-5));   // 5
console.log(Math.abs(3.5));   // 3.5
```

<br />

## Math.sign(x)

返回一個數字的符號，若是正數返回 1，負數返回 -1，0 返回 0。

```
console.log(Math.sign(10));   // 1
console.log(Math.sign(-3));   // -1
console.log(Math.sign(0));   // 0
```

<br />

## Math.max(...values)

返回一組數字中的最大值。可以接受多個參數。

```
console.log(Math.max(1, 5, 3, 9));   // 9
console.log(Math.max(-1, -5, -3));   // -1
```

<br />

## Math.min(...values)

返回一組數字中的最小值。可以接受多個參數。

```
console.log(Math.min(1, 5, 3, 9));   // 1
console.log(Math.min(-1, -5, -3));   // -5
```

<br />

## Math.pow(base, exponent)

計算 base 的 exponent 次方，也就是 base 的冪次。

```
console.log(Math.pow(2, 3));   // 8
console.log(Math.pow(5, 2));   // 25
```

<br />

## Math.sqrt(x)

計算數字的平方根。

```
console.log(Math.sqrt(9));   // 3
console.log(Math.sqrt(16));   // 4
```

<br />

## Math.cbrt(x)

計算數字的立方根。

```
console.log(Math.cbrt(8));   // 2
console.log(Math.cbrt(27));   // 3
```

<br />

## Math.log(x)

計算數字的自然對數 (以 e 為底)。

```
console.log(Math.log(1));   // 0
console.log(Math.log(Math.E));   // 1
```

<br />

## Math.log10(x)

計算數字的以 10 為底的對數。

```
console.log(Math.log10(100));   // 2
console.log(Math.log10(1000));   // 3
```

<br />

## Math.log2(x)

計算數字的以 2 為底的對數。

```
console.log(Math.log2(8));   // 3
console.log(Math.log2(16));   // 4
```

<br />

## Math.exp(x)

計算 e 的 x 次方。

```
console.log(Math.exp(1));   // 2.718281828459045 (即 e)
console.log(Math.exp(2));   // 7.389056098930649
```

<br />

## Math.sin(x)

計算數字 (以弧度表示) 的正弦值。

```
console.log(Math.sin(Math.PI / 2));   // 1
console.log(Math.sin(0));   // 0
```

<br />

## Math.cos(x)

計算數字 (以弧度表示) 的餘弦值。

```
console.log(Math.cos(Math.PI));   // -1
console.log(Math.cos(0));   // 1
```

<br />

## Math.tan(x)

計算數字 (以弧度表示) 的正切值。

```
console.log(Math.tan(Math.PI / 4));   // 0.9999999999999999
console.log(Math.tan(0));   // 0
```

<br />

## Math.asin(x)

計算數字的反正弦值，結果以弧度表示，輸入的值必須在 -1 到 1 之間。

```
console.log(Math.asin(1));   // 1.5707963267948966 (即 π/2)
console.log(Math.asin(0));   // 0
```

<br />

## Math.acos(x)

計算數字的反餘弦值，結果以弧度表示，輸入的值必須在 -1 到 1 之間。

```
console.log(Math.acos(1));   // 0
console.log(Math.acos(0));   // 1.5707963267948966 (即 π/2)
```

<br />

## Math.atan(x)

計算數字的反正切值，結果以弧度表示。

```
console.log(Math.atan(1));   // 0.7853981633974483
console.log(Math.atan(0));   // 0
```

<br />

## Math.atan2(y, x)

計算 y/x 的反正切值，返回的值以弧度表示。因為有兩個參數，能確定結果位於哪個象限。

```
console.log(Math.atan2(1, 1));   // 0.7853981633974483 (π/4)
console.log(Math.atan2(1, -1));   // 2.356194490192345 (3π/4)
```

<br />

## Math.hypot(...values)

計算一組數字的平方和的平方根。

```
console.log(Math.hypot(3, 4));   // 5
console.log(Math.hypot(5, 12));   // 13
console.log(Math.hypot(1, 2, 3, 4));   // 5.477225575051661
```

<br />

## Math.clz32(x)

計算 32 位元無符號整數的前導零的數量。

```
console.log(Math.clz32(1));   // 31
console.log(Math.clz32(16));   // 27
```

<br />

## Math.imul(a, b)

進行 32 位元整數相乘，返回結果的低 32 位。

```
console.log(Math.imul(2, 4));   // 8
console.log(Math.imul(-1, 8));   // -8
```

<br />

## Math.fround(x)

返回最接近的 32 位元單精度浮點數表示。

```
console.log(Math.fround(5.5));   // 5.5
console.log(Math.fround(0.1));   // 0.10000000149011612
```

## Math.expm1(x)

計算 `e^x - 1` 的值，精度比 `Math.exp(x) - 1` 更高。

```
console.log(Math.expm1(1));   // 1.718281828459045
console.log(Math.expm1(0));   // 0
```
