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
