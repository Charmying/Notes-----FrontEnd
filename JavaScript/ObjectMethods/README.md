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
