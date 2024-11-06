# JavaScript Array Methods

以下是 JavaScript 的 Array Methods 整理。

<br />

## length property (length 屬性)

返回陣列的長度。

```
const arr = [1, 2, 3];

console.log(arr.length);   // 3
```

<br />

## push()

將元素添加到陣列的末尾。

```
const arr = [1, 2, 3];
arr.push(5);

console.log(arr);   // [1, 2, 3, 5]
```

<br />

## pop()

移除並返回陣列的最後一個元素。

```
const arr = [1, 2, 3];
const last = arr.pop();

console.log(last);   // 3
console.log(arr);   // [1, 2]
```

<br />

## shift()

移除並返回陣列的第一個元素。

```
const arr = [1, 2, 3];
const first = arr.shift();

console.log(first);   // 1
console.log(arr);   // [2, 3]
```

<br />

## unshift()

將元素添加到陣列的開頭。

```
const arr = [2, 3];
arr.unshift(1);

console.log(arr);   // [1, 2, 3]
```

<br />

## splice()

添加、移除或替換陣列中的元素。

```
const arr = [1, 2, 3, 4];
arr.splice(2, 1, 'a', 'b'); 

console.log(arr);   // [1, 2, 'a', 'b', 4]
```

<br />

## slice()

功返回一個新的陣列，包含從開始索引到結束索引 (不包含結束索引) 的部分元素。

```
const arr = [1, 2, 3, 4];
const newArr = arr.slice(1, 3);

console.log(newArr);   // [2, 3]
```

<br />

## concat()

合併兩個或多個陣列，返回一個新陣列。

```
const arr1 = [1, 2];
const arr2 = [3, 4];
const arr = arr1.concat(arr2);

console.log(arr);   // [1, 2, 3, 4]
```

<br />

## toString()

將陣列轉換為字串，元素之間以逗號分隔。

```
const arr = [1, 2, 3];
const str = arr.toString();

console.log(str);   // 1,2,3
```

<br />

## join()

將陣列轉換為字串，可以指定分隔符號。

```
const arr = [1, 2, 3];
const str = arr.join('-');

console.log(str);   // 1-2-3
```

<br />

## forEach()

為陣列中的每個元素執行一次提供的函式。

```
const arr = [1, 2, 3];
arr.forEach(element => {
  console.log(element);
});

// 1
// 2
// 3
```

<br />

## map()

創建一個新陣列，其元素是調用函式處理每個元素後的結果。

```
const arr = [1, 2, 3];
const newArr = arr.map(x => x * 2);

console.log(newArr);   // [2, 4, 6]
```

<br />

## filter()

創建一個新陣列，其結果是滿足條件的所有元素。

```
const arr = [1, 2, 3, 4];
const filteredArr = arr.filter(x => x > 2);

console.log(filteredArr);   // [3, 4]
```

<br />

## find()

返回符合條件的第一個元素，否則返回 undefined。

```
const arr = [1, 2, 3, 4];
const found = arr.find(x => x > 2);

console.log(found);  // 3
```

<br />

## findIndex()

返回符合條件的第一個元素的索引，否則返回 -1。

```
const arr = [1, 2, 3, 4];
const index = arr.findIndex(x => x > 2);

console.log(index);   // 2
```

<br />

## includes()

判斷陣列是否包含某個值，返回布林值。

```
const arr = [1, 2, 3];

console.log(arr.includes(2));   // true
console.log(arr.includes(4));   // false
```

<br />

## indexOf()

返回指定元素在陣列中的第一個索引，若未找到則返回 -1。

```
const arr = [1, 2, 3, 2];

console.log(arr.indexOf(2));   // 1
console.log(arr.indexOf(4));   // -1
```

<br />

## lastIndexOf()

返回指定元素在陣列中的最後一個索引，若未找到則返回 -1。

```
const arr = [1, 2, 3, 2];

console.log(arr.lastIndexOf(2));   // 3
console.log(arr.lastIndexOf(4));   // -1
```

<br />

## some()

判斷陣列中是否至少有一個元素滿足條件，返回布林值。

```
const arr = [1, 2, 3];
const hasEven = arr.some(x => x % 2 === 0);

console.log(hasEven);   // true
```

<br />

## every()

判斷陣列中的所有元素是否都滿足條件，返回布林值。

```
const arr = [1, 2, 3];
const allPositive = arr.every(x => x > 0);

console.log(allPositive);   // true
```

<br />

## reverse()

反轉陣列中元素的順序。

```
const arr = [1, 2, 3];
arr.reverse();

console.log(arr);   // [3, 2, 1]
```

<br />

## sort()

對陣列中的元素進行排序。

```
const arr = [3, 1, 2];
arr.sort();

console.log(arr);   // [1, 2, 3]
```

<br />

## fill()

用靜態值填充陣列中的元素。

```
const arr = [1, 2, 3];
arr.fill(0);

console.log(arr);   // [0, 0, 0]
```

<br />

## flat()

將多維陣列展平成一維陣列。

```
const arr = [1, [2, 3], [4, [5]]];
const flatArr = arr.flat(2);

console.log(flatArr);   // [1, 2, 3, 4, 5]
```

<br />

## flatMap()

先對陣列進行 map 操作，再將結果展平成一維陣列。

```
const arr = [1, 2, 3];
const flatMappedArr = arr.flatMap(x => [x, x * 2]);

console.log(flatMappedArr);   // [1, 2, 2, 4, 3, 6]
```

<br />

## isArray()

檢查給定的值是否為陣列，返回布林值。

```
console.log(Array.isArray([1, 2, 3]));   // true
console.log(Array.isArray('Hello'));   // false
```

<br />

## from()

將類陣列物件或可迭代物件轉換為陣列。

```
const str = 'Hello';
const arr = Array.from(str);

console.log(arr);   // ['H', 'e', 'l', 'l', 'o']
```

<br />

## entries()

返回一個新的陣列迭代器物件，包含鍵值對 (key-value pair)。

```
const arr = ['a', 'b', 'c'];
const iterator = arr.entries();
for (let [index, value] of iterator) {
  console.log(index, value);
}

// 0 'a'
// 0 'a'
// 2 'c'
```

<br />

## keys()

返回一個新的陣列迭代器物件，包含每個索引。

```
const arr = ['a', 'b', 'c'];
const iterator = arr.keys();
for (let key of iterator) {
  console.log(key);
}

// 0
// 1
// 2
```
