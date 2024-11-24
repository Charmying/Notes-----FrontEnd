# JavaScript Object Methods

以下是 JavaScript 的 Object Methods 整理。

<br />

## Object Property

在提到 Object Methods 之前，可以先對 Object Property 有基本的認識。

在 JavaScript 中，物件的 property (屬性) 可以有不同的屬性設定，這些設定決定了 property 在特定操作中的行為。

### value

- value 用來設定 property 的值。

- 預設值是 undefined，可以透過這個屬性設定 property 的初始值。

    ```
    let obj = {};
    Object.defineProperty(obj, 'name', {
        value: 'Charmy'
    });

    console.log(obj.name);   // Charmy
    ```

### enumerable (列舉)

- enumerable 指的是 property 是否可以在迴圈 (例如：for...in) 中被遍歷出來。

- 當 property 的 enumerable 設為 true 時，這個 property 就會在迴圈中被列舉出來。

- 若設為 false，則這個 property 不會被 for...in 等迴圈列出。

    ```
    let obj = {};

    Object.defineProperty(obj, 'hidden', {
        value: 'secret',
        enumerable: false
    });

    for (let key in obj) {
        console.log(key);   // 不會輸出 'hidden'
    }
    ```

### writable (修改)

- writable 指的是 property 的值是否可以被重新賦值。

- 當 property 的 writable 設為 true 時，就可以修改該 property 的值。

- 若設為 false，則該 property 的值是唯讀的，無法被改變。

    ```
    let person = {};

    Object.defineProperty(person, 'name', {
        value: 'Charmy',
        writable: false
    });

    person.name = 'Tina';   // 嘗試修改值，但不會成功
    console.log(person.name);   // Charmy
    ```

### configurable (刪除)

- configurable 指的是 property 是否可以被刪除或重新定義。

- 當 property 的 configurable 設為 true 時，就可以使用 delete 運算子刪除這個 property，或者重新定義屬性描述符。

- 若設為 false，則無法刪除該 property，也無法修改屬性設定。

    ```
    let member = {};

    Object.defineProperty(member, 'name', {
        value: 'Charmy',
        configurable: false
    });

    delete member.name;   // 嘗試刪除 name，但不會成功
    console.log(member.name);   // Charmy
    ```

### get 和 set

- get 和 set 屬性用來定義 getter 和 setter 函式，讓 property 可以透過存取器 (accessor) 方法來取得或設定值。

- 這兩個方法提供了更靈活的方式來控制 property 的讀取和賦值行為。

    get

    - get 是一個函式，當讀取 property 的值時會被呼叫。

    - 如果沒有設定 get，則預設值為 undefined。

        ```
        let person = {
            firstName: 'Charmy',
            lastName: 'Tseng'
        };

        Object.defineProperty(person, 'fullName', {
            get: function() {
                return this.firstName + ' ' + this.lastName;
            }
        });

        console.log(person.fullName);   // Charmy Tseng
        ```

    set

    - set 是一個函式，當設定 property 的值時會被呼叫。

    - 如果沒有設定 set，則預設值為 undefined。

        ```
        let person = {
            firstName: 'Charmy',
            lastName: 'Tseng'
        };

        Object.defineProperty(person, 'fullName', {
            set: function(name) {
                let parts = name.split(' ');
                this.firstName = parts[0];
                this.lastName = parts[1];
            }
        });

        person.fullName = 'Tina Ho';

        console.log(person.firstName);   // Tina
        console.log(person.lastName);   // Ho
        ```

    當使用 get 和 set 屬性時，不能同時使用 value、writable 屬性。如果 get 或 set 其中一個被設定，value 和 writable 就會被忽略。

    ```
    let obj = {};

    Object.defineProperty(obj, 'number', {
        value: 10,
        get: function() { return 20; }
    });

    console.log(obj.number);   // 產生報錯，因為同時設定了 `value` 和 `get`
    ```

<br />

## `Object.defineProperty()`

`Object.defineProperty()` 是可以用來精確新增或修改物件中 property 的方法。透過這個方法可以定義 property 的屬性，像是能否被列舉 (enumerable)、能否被修改 (writable)、以及能否被刪除 (configurable)。這樣能更細緻的操控物件。

基本語法：

```
Object.defineProperty(obj, prop, descriptor)
```

- obj：想要新增或修改 property 的物件。

- prop：想要定義或修改的 property 名稱 (key 值)。

- descriptor：用來描述 property 行為的物件

    - value：property 的值，預設是 undefined。

    - enumerable：設定 property 是否可以被列舉，預設是 false。

    - writable：設定 property 是否可以被修改，預設是 false。

    - configurable：設定 property 是否可以被刪除或再次修改描述符，預設是 false。

    - get 和 set：定義 getter 和 setter 方法，讓 property 的值可以透過存取器方法來取得或設定。

範例：

```
let person = {};

Object.defineProperty(person, 'name', {
    value: 'Charmy',
    writable: false,
    enumerable: true,
    configurable: false
});

console.log(person.name);   // Charmy

person.name = 'Tina';   // 嘗試修改 name 但不會成功，因為 writable 是 false
console.log(person.name);   // Charmy
```

## `Object.defineProperties()`

`Object.defineProperties()` 是用來一次定義或修改多個物件屬性的靜態方法。`Object.defineProperties()` 可以更細緻控制屬性的描述符，例如：可寫性 (writable)、可列舉性 (enumerable) 和可配置性 (configurable)，並且可以同時設定多個屬性。

基本語法：

```
Object.defineProperties(obj, props)
```

- obj：想要定義或修改屬性的目標物件。

- props：一個物件，包含要定義或修改的屬性及其描述符。

範例：

```
const person = {};

Object.defineProperties(person, {
    name: {
    	value: 'Charmy',
    	writable: true,
    	enumerable: true,
    	configurable: true
    },
    age: {
    	value: 27,
    	writable: false,
    	enumerable: true,
    	configurable: false
    }
});

console.log(person.name);   // Charmy
console.log(person.age);   // 27

person.name = 'Tina';   // 修改成功
console.log(person.name);   // Tina

person.age = 100;   // 修改失敗，age 仍然是 27
console.log(person.age);   // 27

delete person.name;   // 刪除成功
console.log(person.name);   // undefined

delete person.age;   // 刪除失敗，因為 age 的 configurable 設定為 false
console.log(person.age);   // 27
```

在這個範例中，使用 `Object.defineProperties()` 來定義 person 物件的兩個屬性 name 和 age。name 是可寫的，而 age 則是不可寫的，這樣就可以在不影響物件結構的情況下，精細控制各個屬性的行為。

### 應用場景

- 定義多個屬性：當需要一次性定義或修改多個屬性時，使用 `Object.defineProperties()` 可以提高效率，讓程式碼更簡潔。

- 控制屬性行為：如果需要對屬性的可寫性、可列舉性和可配置性進行精細控制，這個方法非常合適。

- 創建不可變物件：可以用來創建具有特定屬性設置的物件，特別是在需要維護某些屬性不被修改或刪除的情況下。

### 注意事項

- 描述符必須正確：當定義屬性時，必須提供正確的描述符屬性 (例如：value、writable、enumerable 和 configurable)。如果缺少必要的屬性，會導致錯誤。

- 不能定義已有屬性：如果嘗試用 `Object.defineProperties()` 定義已經存在的屬性，但沒有提供 `configurable: true` 的描述符，則會拋出錯誤。

- 物件必須可擴展：在使用此方法之前，確保物件沒有被封閉或凍結，否則會無法新增屬性。

### 與 `Object.defineProperty()` 的區別

`Object.defineProperty()` 用來定義或修改單一屬性，而 `Object.defineProperties()` 可以同時處理多個屬性。

### 總結

`Object.defineProperties()` 是一個功能強大的方法，能夠一次性定義多個屬性並精確控制其行為。當需要對物件的屬性進行細緻的管理時，這個方法可以更有效達成目標。

<br />

## `Object.hasOwnProperty()`

`Object.hasOwnProperty()` 是用來檢查物件是否擁有指定名稱 (key) 的自身 property 的方法，也就是說，`Object.hasOwnProperty()` 會判斷該 property 是否存在於物件本身，而不是從原型鏈 (prototype chain) 繼承而來的。

`Object.hasOwnProperty()` 可以幫助在遍歷物件的時候，避免意外存取到繼承自原型的 property。

基本語法：

```
obj.hasOwnProperty(prop)
```

- obj：想要檢查的物件。

- prop：想要檢查的 property 名稱 (key)，必須是字串或符號 (symbol)。

範例：

```
const person = {
    name: 'Charmy',
    age: 27
};

console.log(person.hasOwnProperty('name'));   // true
console.log(person.hasOwnProperty('toString'));   // false
```

在這個範例中，`person.hasOwnProperty('name')` 回傳 true 是因為 name 是 person 物件自身的 property，而 `person.hasOwnProperty('toString')` 回傳 false 是因為 toString 是從 Object 原型繼承而來的 property，不是 person 自身的。

### 注意事項

- `hasOwnProperty()` 只會檢查物件自身的 property，不會檢查原型鏈上的 property。

- 在遍歷物件的時候，例如：使用 for...in 迴圈，通常會搭配 `hasOwnProperty()` 來確保只操作物件自身的 property，而不會誤操作到繼承的 property。

    搭配 for...in 迴圈範例：

    ```
    const person = {
        name: 'Charmy',
        age: 27
    };

    for (let key in person) {
        if (person.hasOwnProperty(key)) {
            console.log(key + ': ' + person[key]);
        }
    }

	// name: Charmy
	// age: 27
    ```

    在這個範例中，使用 for...in 迴圈遍歷 person 物件，並搭配 `hasOwnProperty()` 來確保只列出 person 自身的 property。

### 總結

`Object.hasOwnProperty()` 在需要確認物件中是否包含特定 property，或者在遍歷物件時避免操作到繼承的 property。
