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
