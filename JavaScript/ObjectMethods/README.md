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

<br />

## `Object.getOwnPropertyDescriptor()`

`Object.getOwnPropertyDescriptor()` 是用來取得物件上指定 property 的描述符 (descriptor) 的靜態方法。透過這個方法可以瞭解物件 property 的特性，例如：value、是否可列舉 (enumerable)、是否可寫入 (writable)、是否可設定 (configurable)，以及 getter 和 setter 函式。

基本語法：

```
Object.getOwnPropertyDescriptor(obj, prop)
```

- obj：想要取得 property 描述符的物件。

- prop：想要查詢的 property 名稱 (key)，必須是字串或符號 (symbol)。

範例：

```
const person = {
    name: 'Charmy',
    age: 27
};

const descriptor = Object.getOwnPropertyDescriptor(person, 'name');
console.log(descriptor);
// {
//     "value": "Charmy",
//     "writable": true,
//     "enumerable": true,
//     "configurable": true
// }
```

在這個範例中，使用 `Object.getOwnPropertyDescriptor()` 取得了 person 物件中 name property 的描述符。這個描述符是一個物件，包含了 name property 的所有特性。

### 描述符內容

`Object.getOwnPropertyDescriptor()` 回傳的描述符物件可以包含以下屬性

- value：property 的值。

- writable：布林值，表示 property 的值是否可以被修改。

- enumerable：布林值，表示 property 是否可以在迴圈中被列舉出來。

- configurable：布林值，表示 property 是否可以被刪除或重新定義。

- get：一個函式，作為 property 的 getter，在讀取該 property 時會被呼叫。

- set：一個函式，作為 property 的 setter，在設定該 property 時會被呼叫。

    getter 和 setter 範例

    ```
	const person = {
	    firstName: 'Charmy',
	    lastName: 'Tseng',
	    get fullName() {
	        return `${this.firstName} ${this.lastName}`;
	    }
	};
	
	const descriptor = Object.getOwnPropertyDescriptor(person, 'fullName');
	console.log(descriptor);
	// {
	//     configurable:  true
	//     enumerable : true
	//     get: ƒ fullName()
	//     set : undefined
	// }
	```
	
	在這個範例中，取得了 person 物件中 fullName property 的描述符，可以看到包含了 get 函式，並且 set 是 undefined，表示沒有設定 setter。

### 注意事項

- `Object.getOwnPropertyDescriptor()` 只會回傳物件自身的 property 描述符，不會查詢原型鏈上的 property。

- 如果指定的 property 不存在於物件中，則會回傳 undefined。

### 用途

- 可以用來檢查物件 property 的特性，例如：在進行物件封裝或操作 property 時確認可寫入性或可列舉性。

- 在進行物件的深度操作時，結合 `Object.defineProperty()` 來修改物件 property 的特性

### 總結

`Object.getOwnPropertyDescriptor()` 可以更深入瞭解物件中 property 的特性，適合用在需要精確控制或檢查物件 property 的情況。

<br />

## `Object.getOwnPropertyDescriptors()`

`Object.getOwnPropertyDescriptors()` 是一個用來取得物件所有自身 property 的描述符 (descriptor) 的靜態方法。`Object.getOwnPropertyDescriptors()` 會回傳一個包含每個 property 描述符的物件，這樣可以獲取所有 property 的細節。

`Object.getOwnPropertyDescriptors()` 與 `Object.getOwnPropertyDescriptor()` 類似，但後者只能針對單一 property，而 `Object.getOwnPropertyDescriptors()` 則能一次取回全部自身 property 的描述符。

基本語法：

```
Object.getOwnPropertyDescriptors(obj)
```

- obj：想要取得 property 描述符的目標物件。

範例：

```
const person = {
    name: 'Charmy',
    age: 27,
    get fullName() {
        return `${this.name} Tseng`;
    }
};

const descriptors = Object.getOwnPropertyDescriptors(person);
console.log(descriptors);
// {
//     "name": {
//         "value": "Charmy",
//         "writable": true,
//         "enumerable": true,
//         "configurable": true
//     },
//     "age": {
//         "value": 27,
//         "writable": true,
//         "enumerable": true,
//         "configurable": true
//     },
//     "fullName": {
//         "enumerable": true,
//         "configurable": true
//     }
//  }
```

在這個範例中，使用 `Object.getOwnPropertyDescriptors()` 來取得 person 物件所有自身 property 的描述符，包含 name、age 和 fullName。每個 property 的特性 (例如：writable、enumerable、configurable) 都在描述符中詳細列出。

### 描述符內容

`Object.getOwnPropertyDescriptors()` 回傳的每個 property 描述符，可能包含以下屬性

- value：property 的值。

- writable：布林值，表示 property 的值是否可被修改。

- enumerable：布林值，表示 property 是否可被迴圈列舉。

- configurable：布林值，表示 property 是否可被刪除或重新定義。

- get：property 的 getter 函式（如果有的話）。

- set：property 的 setter 函式（如果有的話）。

### 注意事項

- `Object.getOwnPropertyDescriptors()` 只會回傳物件自身的 property 描述符，不會包含繼承自原型鏈的 property。

- 如果某個 property 沒有描述符，該 property 不會出現在回傳的物件中。

### 用途

通常用於結合 `Object.defineProperties()`，當想要複製或 clone 物件時，保留原物件的 property 特性很重要。`Object.getOwnPropertyDescriptors()` 可以精確取得每個 property 的描述符，然後通過 `Object.defineProperties()` 設置在新物件上。

用於物件複製的範例

```
const clone = Object.defineProperties({}, Object.getOwnPropertyDescriptors(person));
console.log(clone);   // 與 `person` 物件相同的屬性與屬性特性
```

### 總結

`Object.getOwnPropertyDescriptors()` 是用來檢視和操作物件所有自身的 property 描述符的方法，尤其在進行物件 clone 或需要複製物件特性，可以讓物件操作變得更加精確。

<br />

## `Object.getPrototypeOf()`

`Object.getPrototypeOf()` 是一個用來取得指定物件的原型 (prototype) 的靜態方法。原型是指物件繼承的方法和屬性所在的物件，這是 JavaScript 繼承機制的基礎。如果物件是透過某個構造函數 (constructor) 或使用 `Object.create()` 建立的，Object.getPrototypeOf() 就能回傳該物件的原型。

基本語法：

```
Object.getPrototypeOf(obj)
```

- obj：想要查詢原型的物件。

範例：

```
const person = {
    greet() {
        console.log('Hello!');
    }
};

const student = Object.create(person);
console.log(Object.getPrototypeOf(student) === person);   // true
```

在這個範例中，使用 `Object.create(person)` 建立了 student 物件，並且繼承了 person 的原型。透過 `Object.getPrototypeOf(student)` 可以確認 student 的原型是否為 person。

### 常見用途

- 確認物件的原型：可以用來檢查某個物件是否繼承自另一個物件，特別是在進行物件設計時有助於確認繼承鏈。

- 繼承控制：了解物件的原型可以更清楚掌握物件在原型鏈上的行為，確保繼承的功能正確。

### 注意事項

- 如果傳入的是一個使用 `Object.create(null)` 創建的物件，那麼 `Object.getPrototypeOf()` 會回傳 null，因為這類物件沒有原型。

    ```
    const obj = Object.create(null);
    console.log(Object.getPrototypeOf(obj));   // null
    ```

- 對於標準物件，`Object.getPrototypeOf()` 會回傳該物件的內部 [[Prototype]]。如果物件是透過類別 (class) 或建構子 (constructor) 建立的，那原型會是 constructor.prototype。

### 與 `__proto__` 的區別

在 JavaScript 中，`__proto__` 也是一種可以直接存取物件的原型。但這是一個非標準的方式，且不推薦在現代 JavaScript 中使用。相比之下，`Object.getPrototypeOf()` 是標準且更安全的選擇。

### 應用場景

- 繼承判斷：假設在調試階段想知道某個物件的繼承關係，可以使用 Object.getPrototypeOf() 來快速確認物件的原型。

- 優化性能：瞭解物件原型有助於掌握物件的屬性和方法是從哪裡繼承而來。

### 總結

`Object.getPrototypeOf()` 是一個非常實用的工具，能夠在處理 JavaScript 的原型繼承時檢視和操作物件的繼承結構。

<br />

## `Object.setPrototypeOf()`

`Object.setPrototypeOf()` 是一個用來設定指定物件的原型 (prototype) 的靜態方法。透過這個方法可以動態修改物件的原型，進而改變物件的繼承鏈和其行為。物件的原型決定了能夠繼承哪些屬性和方法，因此 `
Object.setPrototypeOf()` 可以更靈活控制物件的繼承關係。

基本語法：

```
Object.setPrototypeOf(obj, proto)
```

- obj：想要修改原型的目標物件。

- proto：作為新原型的物件。如果傳入 null，那麼物件將不再有任何原型。

範例：

```
const animal = {
    speak() {
        console.log('Animal makes a sound.');
    }
};

const dog = {
    bark() {
        console.log('Dog barks.');
    }
};

// 將 dog 的原型設為 animal，讓 dog 繼承 animal 的屬性和方法
Object.setPrototypeOf(dog, animal);

dog.bark();   // Dog barks.
dog.speak();   // Animal makes a sound.
```

在這個範例中，使用 `Object.setPrototypeOf()` 將 dog 的原型設置為 animal，因此 dog 不僅可以使用自己的 bark 方法，還可以繼承並使用 animal 的 speak 方法。

### 注意事項

- 性能影響：頻繁使用 `Object.setPrototypeOf()` 來修改物件的原型會對性能造成影響，特別是在高效能要求的應用程式中，因為這會破壞 JavaScript 引擎對物件的優化。通常在創建物件時就應該確定好原型，而非在運行時頻繁修改。

- 設為 null 的後果：如果將一個物件的原型設為 null，那麼該物件將不會繼承任何來自 `Object.prototype` 的屬性和方法，例如：toString() 或 hasOwnProperty()。

    範例

    ```
    const obj = {};
    Object.setPrototypeOf(obj, null);
    console.log(obj.toString);   // undefined
    ```

- 不推薦在物件上反覆更改原型：最好在物件創建時通過 `Object.create()` 指定原型，而不是後期使用 `Object.setPrototypeOf()` 進行修改，這樣可以保持程式碼的清晰和效能。

### 常見用途

- 動態改變繼承鏈：在某些情況下，可能需要根據不同的需求動態改變物件的繼承鏈，這時就可以使用 `Object.setPrototypeOf()`。例如：可能需要讓一個物件在執行過程中具備不同的行為或屬性。

- 模擬繼承行為：如果想要實現類似於傳統物件導向中的繼承機制，使用 `Object.setPrototypeOf()` 可以讓物件繼承另一個物件的屬性和方法，達到模擬類別繼承的效果。

    動態更改原型的範例

    ```
    const car = {
        drive() {
            console.log('Car is driving.');
        }
    };

    const airplane = {
        fly() {
            console.log('Airplane is flying.');
        }
    };

    const vehicle = {};

    Object.setPrototypeOf(vehicle, car);
    vehicle.drive();   // Car is driving.

    Object.setPrototypeOf(vehicle, airplane);
    vehicle.fly();   // Airplane is flying.
    ```

    在這個範例中，動態改變了 vehicle 的原型，先繼承 car，後來又繼承 airplane，使其行為發生了變化。

### 總結

`Object.setPrototypeOf()` 能夠靈活設定或更改物件的原型，進而影響該物件的繼承關係和行為。雖然這個方法非常強大，但由於會對性能造成影響，應在必要時使用，並避免頻繁修改物件的原型。

<br />

## `Object.prototype.toString()`

`Object.prototype.toString()` 是 JavaScript 中每個物件都有的預設方法，這個方法會回傳一個表示物件類型的字串。`Object.prototype.toString()` 是用來檢查物件的具體類型的，特別是當需要精確區分物件類型時 (例如：區分陣列、日期、正規表達式等)，會比 typeof 更加準確。

基本語法：

```
obj.toString()
```

- obj：想要檢查的物件。

預設情況下，當直接呼叫物件的 `toString()` 方法時，會回傳類似 [object Object] 這樣的字串，表示這是一個普通的物件。但如果物件是其他內建類型，像是陣列或日期，結果會有所不同。

範例：

```
const obj = {};
console.log(obj.toString());    // [object Object]

const arr = [];
console.log(arr.toString());    // 空白，因為 Array 的 toString() 會輸出元素

console.log(Object.prototype.toString.call(arr));    // [object Array]，精確顯示陣列類型
```

在這個範例中，使用了 `Object.prototype.toString.call()` 來精確檢查 arr 是陣列類型。這是因為陣列的 toString() 方法被重寫了，會輸出其元素而不是物件類型，而透過 `Object.prototype.toString.call()` 可以得到具體的物件類型。

### 應用場景

- 檢查物件類型：`Object.prototype.toString()` 可以用來精確檢查物件的具體類型，特別是當 typeof 不夠準確時，例如：區分 Array、Date、RegExp 等特殊物件。

    ```
    console.log(Object.prototype.toString.call([]));   // [object Array]
    console.log(Object.prototype.toString.call(new Date()));   // [object Date]
    console.log(Object.prototype.toString.call(/regex/));   // [object RegExp]
    ```

- 解決 typeof 的局限：typeof 對於某些物件類型會返回不準確的結果，例如：陣列和物件都會被判斷為 object，而 `Object.prototype.toString()` 則能提供精確的類型資訊。

    ```
    console.log(typeof []);   // object
    console.log(Object.prototype.toString.call([]));   // [object Array]
    ```

- 自訂物件類型：可以自訂物件的 `toString()` 行為，使其回傳特定的類型資訊。

    ```
    const person = {
        name: 'Charmy',
        toString: function() {
            return '[object Person]';
        }
    };

    console.log(person.toString());   // [object Person]
    ```

### 注意事項

- 需使用 `call()` 或 `apply()`：當想檢查物件的具體類型時，應使用 `Object.prototype.toString.call(obj)`，而不是直接呼叫物件的 `toString()` 方法，這是因為某些內建物件 (例如：陣列) 已經重寫了這個方法。

- 不適合檢查基本數據類型：`Object.prototype.toString()` 更適合用來檢查物件類型，對於基本數據類型 (例如：number, string) 則不常用到，因為 typeof 對基本數據類型已經足夠。

<br />

## `Object.keys()`

`Object.keys()` 是用來取得物件中所有可列舉 (enumerable) 
的靜態方法。`Object.keys()` 會回傳一個包含物件自身所有可列舉 property 名稱 (key 值) 的陣列，這些 key 值是以字串的形式存在。

`Object.keys()` 只會取得物件本身的 property，不會包含從原型鏈 (prototype chain) 繼承而來的 property。

基本語法：

```
Object.keys(obj)
```

- obj：想要取得 key 值的物件。

範例：

```
const person = {
    name: 'Charmy',
    age: 27,
    city: 'Taichung'
};

const keys = Object.keys(person);
console.log(keys);   // ['name', 'age', 'city']
```

在這個範例中，Object.keys(person) 回傳了一個陣列，包含了 person 物件中所有可列舉的 key 值。

### 注意事項

- `Object.keys()` 只會回傳物件自身的可列舉 property，不包含從原型繼承的 property。

- 只會包含 enumerable 設定為 true 的 property。

- 回傳的 key 值順序與在物件中定義的順序一致。

### 總結

Object.keys() 在許多情況下都很實用，尤其是在想要遍歷一個物件，或者只是想知道物件中有哪些 property 時。

<br />

## `Object.values()`

`Object.values()` 是用來取得物件中所有 property 值 (value 值) 的靜態方法。`Object.values()` 會回傳一個包含物件自身所有可列舉 value 值的陣列。

`Object.values()` 只會取得物件本身的 value 值，不會包含從原型鏈 (prototype chain) 繼承而來的 property。

基本語法：

```
Object.values(obj)
```

- obj：想要取得 value 值的物件。

範例：

```
const person = {
    name: 'Charmy',
    age: 27,
    city: 'Taichung'
};

const values = Object.values(person);
console.log(values);   // ['Charmy', 27, 'Taichung']
```

在這個範例中，Object.values(person) 回傳了一個陣列，包含了 person 物件中所有可列舉的 value 值。

### 注意事項

- `Object.values()` 只會回傳物件自身的可列舉 value 值，不包含從原型繼承的 property。

- 回傳的 value 值的順序與物件中定義的順序一致。

### 總結

`Object.values()` 在需要處理物件的值或進行某些基於值的操作時會非常方便。

<br />

## `Object.entries()`

`Object.entries()` 是用來取得物件中所有可列舉 (enumerable) property 的鍵值對 (key-value pairs) 的靜態方法。`Object.entries()` 會回傳一個二維陣列 (array of arrays)，每個子陣列包含兩個元素：第一個元素是 property 的名稱 (key)，第二個元素是 property 的值 (value)。


基本語法：

```
Object.entries(obj)
```

- obj：想要取得鍵值對的物件。

範例：

```
const person = {
  name: 'Alice',
  age: 30,
  city: 'Taipei'
};

const entries = Object.entries(person);
console.log(entries);   // [['name', 'Alice'], ['age', 30], ['city', 'Taipei']]
```

在這個範例中，`Object.entries(person)` 回傳了一個二維陣列，其中每個子陣列包含 person 物件中每個可列舉 property 的 key 和 value。

### 注意事項

- `Object.entries()` 只會回傳物件自身的可列舉 property，不包含從原型繼承的 property。

- 回傳的鍵值對順序與物件中定義的順序一致。

### 總結

`Object.entries()` 在想要遍歷物件的 key 和 value，或者想要將物件轉換為其他資料結構時。`Object.entries()` 能夠輕鬆處理物件的鍵值對，方便進行迴圈操作。

<br />

## `Object.fromEntries()`

`Object.fromEntries()` 是一個將鍵值對 (key-value pairs) 的陣列轉換成物件的靜態方法。當有一個由 [key, value] 形式的陣列組成的資料結構時，可以使用 `Object.fromEntries()` 將其轉換成物件，這個物件的屬性即為那些鍵值對。

基本語法：

```
Object.fromEntries(iterable)
```

- iterable：一個可迭代的資料結構，通常是由鍵值對 (例如：陣列) 組成的結構，例如：Map 或二維陣列。

範例：

```
const entries = [['name', 'Charmy'], ['age', 27], ['city', 'Taichung']];

const obj = Object.fromEntries(entries);
console.log(obj);   // { name: 'Alice', age: 30, city: 'Taipei' }
```

在這個範例中，entries 是一個二維陣列，每個子陣列都是一個鍵值對。透過 `Object.fromEntries()`，這些鍵值對被轉換成一個物件，物件中的屬性 name、age 和 city 對應到原陣列中的鍵值對。

### 應用場景

- 將 Map 轉換為物件：`Object.fromEntries()` 將 Map 資料結構轉換為普通物件。

    ```
    const map = new Map([['name', 'Charmy'], ['age', 27]]);
    onst obj = Object.fromEntries(map);
    console.log(obj);   // {name: 'Charmy', age: 27}
    ```

- 資料轉換：從某些 API 獲得的資料是陣列形式，需要將其轉換為物件時，就可以使用 `Object.fromEntries()`。

- 反轉 `Object.entries()`：`Object.entries()` 可以將物件轉換為鍵值對陣列，而 `Object.fromEntries()` 則是將這個過程反轉，將鍵值對陣列再轉換回物件。

    ```
    const obj = { name: 'Charmy', age: 27 };
    const entries = Object.entries(obj);
    const newObj = Object.fromEntries(entries);
    console.log(newObj);   // {name: 'Charmy', age: 27}
    ```

### 注意事項

- 無法處理重複鍵：如果鍵值對陣列中有重複的鍵，後面出現的鍵值對會覆蓋前面的值。

    ```
    const entries = [['name', 'Charmy'], ['name', 'Tina']];
    const obj = Object.fromEntries(entries);
    console.log(obj);   // {name: 'Tina'}
    ```

- 輸入格式必須正確：`Object.fromEntries()` 需要傳入的資料是鍵值對形式的可迭代結構，否則會報錯。

### 總結

`Object.fromEntries()` 適合將鍵值對陣列或 Map 結構轉換成物件，特別適合用在將資料從一種結構轉換為物件的情境下。`Object.fromEntries()` 能讓程式更加靈活，也能更輕鬆處理各種鍵值對資料。

<br />

## `Object.assign()`

`Object.assign()` 是用來將一個或多個來源物件 (source objects) 的所有可列舉 (enumerable) property 複製到目標物件 (target object) 的靜態方法。`Object.assign()` 會修改並回傳目標物件，使其可以輕鬆合併多個物件或拷貝物件的 property。

基本語法：

```
Object.assign(target, ...sources)
```

範例：

```
const target = { name: 'Charmy' };
const source = { age: 27, city: 'Taichung' };

const result = Object.assign(target, source);
console.log(result);   // {name: 'Charmy', age: 27, city: 'Taichung'}
console.log(target);   // {name: 'Charmy', age: 27, city: 'Taichung'}
```

在這個範例中，`Object.assign()` 將 source 物件中的所有 property 複製到 target 物件，並回傳修改後的 target 物件。

### 注意事項

- `Object.assign()` 是淺拷貝 (shallow copy)，也就是說，如果來源物件中的 property 是物件或陣列等複雜資料類型，那麼拷貝的是引用，而不是值。

- 如果目標物件中已經存在與來源物件相同的 property 名稱 (key)，來源物件的 property 會覆蓋目標物件中的 property。

- 如果有多個來源物件具有相同的 property 名稱 (key)，靠後的來源物件會覆蓋靠前的。

    淺拷貝範例：
    
    ```
    const target = { name: 'Charmy', details: { age: 27 } };
    const source = { details: { city: 'Taichung' } };

    Object.assign(target, source);
    console.log(target);   // {"name": "Charmy", "details": {"city": "Taichung"}}
    ```

    在這個範例中，因為 `Object.assign() 是淺拷貝`，所以 details 這個物件的引用會被覆蓋，而不是合併。

### 總結

`Object.assign()` 是一個強大的方法，在需要合併物件、拷貝物件屬性，或為物件新增新的屬性時非常有用。

<br />

## `Object.is()`

`Object.is()` 是用來比較兩個值是否完全相等的靜態方法。`Object.is()` 的比較方式與嚴格相等運算子 `===` 類似，但在處理一些特殊情況時，`Object.is()` 有更嚴格的判斷標準。

基本語法：

```
Object.is(value1, value2)
```

- value1：第一個要比較的值。

- pvalue2：第二個要比較的值。

範例：

```
console.log(Object.is('hello', 'hello'));   // true
console.log(Object.is('hello', 'Hello'));   // false
console.log(Object.is({}, {}));   // false（不同的物件實例）
console.log(Object.is([], []));   // false（不同的陣列實例）
console.log(Object.is(NaN, NaN));   // true
console.log(Object.is('', ''));   // true
console.log(Object.is(1, 1));   // true
console.log(Object.is(0, 0));   // true
console.log(Object.is(0, -0));   // false
console.log(Object.is(+0, -0));   // false
console.log(Object.is(-0, -0));   // true
```

### `Object.is()` 與 `===` 的差異

`Object.is()` 與嚴格相等運算子 `===` 很相似，但有兩個特殊情況 `Object.is()` 與 `===` 不同

- NaN 比較： `===` 判斷 `NaN === NaN` 為 false，但 `Object.is(NaN, NaN)` 會回傳 true。

- 0 與 -0： `===` 判斷 `0 === -0` 為 true，但 `Object.is(0, -0)` 會回傳 false。

### 注意事項

- `Object.is()` 主要用於需要嚴格比較的情況，特別是在需要區分 NaN 或正負零的場合。

- 對於其他一般情況，`Object.is()` 與 `===` 的行為基本一致。

### 總結

`Object.is()` 是一個更精確的比較方法，特別適合用在需要區分 NaN、正零和負零的場合。

<br />

## `Object.create()`

`Object.create()` 是用來建立新物件的靜態方法。這個新物件的原型 (prototype) 可以自己指定，並且可以在建立時直接添加新的 property。透過 `Object.create()` 可以更靈活控制物件的繼承關係，特別是在需要建立具有特定原型的物件時。

基本語法：

```
Object.create(proto, propertiesObject)
```

- proto：新物件的原型，可以是另一個物件或 null。如果傳入 null，新物件將不會繼承任何東西。

- propertiesObject (可選)：一個用來定義新物件 property 的物件。這個物件的格式與 `Object.defineProperties()` 所使用的格式相同，可以設定 property 的描述符 (descriptor)。

範例：

```
const person = {
    greet() {
        console.log('Hello!');
    }
};

const member = Object.create(person);
member.name = 'Charmy';

member.greet();   // Hello!
console.log(member.name);   // Charmy
```

在這個範例中，使用 `Object.create(person)` 建立了一個新物件 member，並將 person 設為原型。由於 member 繼承自 person，因此可以呼叫 person 的 greet 方法。

### 使用 `propertiesObject`

```
const person = {
    greet() {
        console.log('Hello!');
    }
};

const member = Object.create(person, {
    name: {
        value: 'Charmy',
        writable: true,
        enumerable: true,
        configurable: true
    }
});

console.log(member.name);   // Charmy
member.greet();   // Hello!
```

在這個範例中，使用 `propertiesObject` 參數來定義 member 的 name property，並指定描述符，這樣可以更精確控制 name property 的行為。

### 注意事項

- 如果 proto 傳入 null，新物件將沒有原型，因此不會繼承任何來自 Object 的方法，例如：`toString()`。

- `Object.create()` 提供了一種更加直接和清晰的方式來設定物件的原型，相比於使用建構子函式 (constructor function) 來說更為簡單。

### 應用場景

- 使用 `Object.create()` 可以用來建立物件之間的繼承關係，並且在建立物件時可以精確定義 property。

- 適合用於需要定制化物件原型的情況，例如：實作原型繼承 (prototypal inheritance)。

### 總結

`Object.create()` 可以精確控制物件的繼承結構，同時也可以在建立物件時設定其屬性。

<br />

## `Object.preventExtensions()`

`Object.preventExtensions()` 是一個用來阻止物件擴展的靜態方法，也就是說，對一個物件使用 `Object.preventExtensions()` 之後就無法再向該物件添加新的屬性。已經存在的屬性仍然可以修改或刪除，但不能再新增屬性。。

基本語法：

```
Object.preventExtensions(obj)
```

- obj：想要阻止擴展的物件。

這個方法會直接修改傳入的物件，使其無法再擴展，並且回傳該物件。

範例：

```
const person = {
    name: 'Charmy'
};

Object.preventExtensions(person);

person.age = 27;   // 新屬性無法被添加
console.log(person.age);   // undefined

person.name = 'Tina';   // 仍然可以修改現有屬性
console.log(person.name);   // Tina

delete person.name;   // 也可以刪除現有屬性
console.log(person.name);   // undefined
```

在這個範例中，當對 person 物件使用了 `Object.preventExtensions()` 之後，嘗試添加新屬性 age 會失敗，但仍然可以修改或刪除現有的屬性 name。

### 應用場景

- 防止對物件的意外擴展：在開發過程中，當希望某個物件結構保持穩定，不被不小心添加新的屬性時，可以使用 `Object.preventExtensions()` 來鎖定物件的結構。

- 強化物件的完整性：當物件的屬性應該保持固定而不應再增添時，`Object.preventExtensions()` 有助於提高程式的安全性和可靠性。

### 如何檢查物件是否可擴展

可以使用 `Object.isExtensible()` 來檢查一個物件是否還能擴展。

```
const person = { name: 'Charmy' };
console.log(Object.isExtensible(person));   // true

Object.preventExtensions(person);
console.log(Object.isExtensible(person));   // false
```

### 注意事項

- `Object.preventExtensions()` 只會阻止添加新屬性，並不會影響現有屬性的修改或刪除行為。

- 一旦使用了 `Object.preventExtensions()` 就無法撤銷這個操作。物件將永遠無法擴展。

- `Object.preventExtensions()` 不會影響物件的原型鏈，因此物件仍然可以透過原型繼承屬性和方法。

### 與 `Object.seal()` 和 `Object.freeze()` 的區別

- `Object.preventExtensions()` 只阻止新增屬性，但允許修改或刪除現有屬性。

- `Object.seal()` 不僅阻止新增屬性，也不允許刪除屬性，但仍允許修改屬性值。

- `Object.freeze()` 則是最嚴格的，既阻止新增屬性，也阻止修改和刪除屬性，完全凍結物件。

### 總結

`Object.preventExtensions()` 是一個有助於防止物件結構發生變化的工具。當希望物件保持原有的屬性並阻止新增屬性時，可以使用這個方法來確保物件的穩定性和完整性。

<br />

## `Object.seal()`

`Object.seal()` 是一個用來封閉物件的靜態方法。當對一個物件使用 `Object.seal()` 之後，這個物件就無法再新增或刪除屬性，現有的屬性仍然可以修改，但屬性的可配置性 (configurable) 會被設定為 false，也就是說，無法重新定義屬性或更改其屬性描述符。

基本語法：

```
Object.seal(obj)
```

- obj：想要封閉的物件。

這個方法會直接修改傳入的物件，使其無法新增或刪除屬性，並回傳該物件。
