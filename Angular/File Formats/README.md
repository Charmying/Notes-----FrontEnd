# Angular 檔案類型

在 Angular 中，`.component`、`.service` 和 `.route` 等檔案是開發過程中的核心結構之一，這些檔案類型和結構對於維護和組織程式碼非常重要，每一個都有其特定的用途。以下是針對這些檔案的介紹，以及其他常見的檔案和功能。

<br />

## .component 檔

用途： Component 是 Angular 應用程式的基本構建塊。每個組件負責管理應用程式中特定的視圖和相關的功能。

- `.component.ts`

    功能： 定義組件的類別和功能，包括資料綁定、事件處理等。

    內容： 包含 TypeScript 類別，裝飾器 `@Component` 用來指定組件的元資料，例如：模板 (template)、樣式 (css/scss)等。

- `.component.html`

    功能： 定義組件的模板，描述該組件在瀏覽器中如何呈現。

    內容： 除了包含 HTML 語法，也可能包含 Angular 的模板語法，例如：`*ngIf`、`*ngFor` 等。

- `.component.css/scss`

    功能： 定義組件專用的樣式。

    內容： 包含 CSS 或 SCSS 樣式，這些樣式通常只影響該組件本身。

- `.component.spec.ts`

    測試檔案

    用途： 包含單元測試程式碼，用於測試組件、服務等的功能。

    內容： 使用測試框架 (例如：Jasmine) 編寫的測試用例

TypeScript 檔案範例：

```
import { Component } from '@angular/core';

@Component({
  selector: 'app-example',
  standalone: true,
  templateUrl: './example.component.html',
  styleUrl: './example.component.scss',
  imports: []
})

export class ExampleComponent {
  title = 'Hello World';
}
```

Angular 組件通過 `.html`、`.scss`、`.ts` 結合起來 (不一定需要 `.spec`)，形成了一個完整的功能模塊。組件的設計理念是將應用程式分解成小型、可重用的部分，提高開發效率和程式碼的可維護性。

<br />

## .service 檔

用途： service 用於封裝和共享應用程式中的功能和操作，例如：資料獲取、業務處理等，並將這些功能操作與視圖 (組件) 分離。service 有助於保持組件的簡潔，促進程式碼的可重用性和可測試性。

- `.service.ts`

    功能：定義 service 的類別和相關方法。
    
    內容：包含帶有 @Injectable 裝飾器的 TypeScript 類別，該裝飾器允許 service 被 inject 到其他 component 或 service 中。

    ```
    // example.service.ts

    import { Injectable } from '@angular/core';
    import { HttpClient } from '@angular/common/http';

    @Injectable({
        providedIn: 'root'
    })

    export class ExampleService {
        constructor(private http: HttpClient) {}

        getData() {
            return this.http.get('https://api.example.com/data');
        }
    }
    ```
    
    - `@Injectable` 裝飾器用於標記這是一個 service，並告訴 Angular 可以被注入到其他組件或 service 中。

        `providedIn: 'root'` 表示該 service 在應用程式的根層級可用，也就是說，可以在應用程式的任何部分都可以被注入。

    - `HttpClient` 是 Angular 的內建 service，用於發送 HTTP 請求。這裡 `ExampleService` 使用 `HttpClient` 來向 API 發送 GET 請求並獲取資料。

Angular service 的設計理念是將應用程式的業務流程與視圖分離，從而提高程式碼的可重用性和可測試性。service 可以輕鬆被不同的組件共享，使其適合處理應用程式中的跨組件應用。

<br />

## .route 檔

用途： route 檔案定義應用程式的路由 (routing) 配置，決定不同的 URL 對應哪個組件，實現單頁應用程式 (SPA) 的導航。

- `.route.ts` 或 `app-routing.module.ts`

    功能： 定義路由陣列，設定路由路徑、對應的 component 和其他路由選項。

    內容： 包含路由配置，使用 Angular 的 RouterModule 進行導入和導出。

<br />

### `.route.ts` 和 `app-routing.module.ts` 的差異

- `.route.ts`

    比較簡單且常見的一種路由設定方式，通常是在專案中單獨的檔案內設定路由規則。

    通常適用於使用獨立元件 (Standalone Components)，可以在這個檔案中直接定義路由陣列，並在根組件中使用 `RouterModule.forRoot(routes)` 或 `RouterModule.forChild(routes)` 來進行配置。

    比較適合單一檔案配置，讓路由更集中、更簡潔。

    ```
    // app.routes.ts

    import { Routes } from '@angular/router';
    import { HomeComponent } from './home/home.component';
    import { AboutComponent } from './about/about.component';

    export const routes: Routes = [
        { path: '', component: HomeComponent },
        { path: 'about', component: AboutComponent },
    ];
    ```
    
    ```
    // app.component.ts

    import { Component } from '@angular/core';
    import { RouterOutlet } from '@angular/router';

    @Component({
        selector: 'app-root',
        standalone: true,
        imports: [ RouterOutlet ],
        templateUrl: './app.component.html',
        styleUrl: './app.component.scss'
    })

    export class AppComponent {}
    ```
    
    ```
    <!-- app.component.html -->

    <router-outlet />
    ```

- `app-routing.module.ts`

    Angular 傳統的路由配置方式，通常是為了較大的專案而設計的。

    路由配置會放在 AppRoutingModule 模組中，並使用 `@NgModule` 來管理和匯出路由設定。

    適合於非獨立元件 (使用模組系統的元件)，並且容易擴展和管理較大規模的專案。

    ```
    // app-routing.module.ts

    import { NgModule } from '@angular/core';
    import { RouterModule, Routes } from '@angular/router';
    import { HomeComponent } from './home/home.component';
    import { AboutComponent } from './about/about.component';

    const routes: Routes = [
        { path: '', component: HomeComponent },
        { path: 'about', component: AboutComponent },
        { path: '**', redirectTo: '' },   // 未匹配的路由導向至首頁
    ];

    @NgModule({
        imports: [ RouterModule.forRoot(routes) ],
        exports: [ RouterModule ]
    })

    export class AppRoutingModule {}
    ```
    
    - `RouterModule.forRoot(routes)`：用於設定應用程式的主要路由配置。

    - `path` 是 URL 路徑，component 是該路徑對應的組件。

    - `**` 表示所有未匹配的路徑，這裡配置為重新導向至首頁。
    
    ```
    // app.module.ts
    
    import { NgModule } from '@angular/core';
    import { BrowserModule } from '@angular/platform-browser';
    import { AppRoutingModule } from './app-routing.module';
    import { AppComponent } from './app.component';
    import { HomeComponent } from './home/home.component';
    import { AboutComponent } from './about/about.component';

    @NgModule({
        declarations: [
            AppComponent,
            HomeComponent,
            AboutComponent
        ],
        imports: [
            BrowserModule,
            AppRoutingModule
        ],
        providers: [],
        bootstrap: [ AppComponent ]
    })

    export class AppModule {}
    ```

<br />

## .module 檔

用途： Module 用於組織應用程式中的相關部分，將應用程式的功能分組，以便管理和加載。Module 通常包含 組件 (component)、指令 (directive)、管道 (pipe) 和服務 (service) 等，並組合成一個功能性單元。

- `.module.ts`

    功能： 定義一個 Angular 模組，指定其包含的組件、指令、Pipe，以及導入的其他模組。

    內容： 包含帶有 `@NgModule` 裝飾器的類別，定義模組的元數據。

    `@NgModule` 裝飾器：用於配置模組的元數據，包括組件、服務、指令和 Pipe 等的註冊。

    ```
    // app.module.ts

    import { BrowserModule } from '@angular/platform-browser';
    import { NgModule } from '@angular/core';
    import { AppComponent } from './app.component';
    import { ExampleComponent } from './example/example.component';

    @NgModule({
        declarations: [
            AppComponent,
            ExampleComponent
        ],
        imports: [
            BrowserModule
        ],
        providers: [],
        bootstrap: [ AppComponent ]
    })

    export class AppModule {}
    ```

    - `declarations`：指定該模組包含的組件、指令和管道。這裡註冊了 `AppComponent` 和 `ExampleComponent`。

    - `imports`：指定該模組依賴的其他模組。這裡導入了 `BrowserModule`，這是所有 Angular 應用程式的必需模組。

    - `providers`：指定服務提供者，通常用於註冊全局服務。

    - `bootstrap`：指定應用程式的根組件，這個組件是應用程式啟動時顯示的第一個組件。

Module 是 Angular 應用程式的基本結構單位，通過將組件、service 和其他功能組織在一起，幫助管理複雜的應用程式結構。

<br />

## .model 檔

用途： Model 用於定義應用程式中使用的資料結構和類型，提供強類型支持。

- `.model.ts`

    功能： 定義資料模型的介面或類別。

    內容： 包含 TypeScript 介面或類別，描述資料的結構和屬性。

    ```
    // user.model.ts

    export interface User {
        id: number;
        name: string;
        email: string;
    }
    ```

.model 檔為應用程式提供了資料結構的清晰定義，能夠幫助開發人員管理和操作資料，提高程式碼的可讀性和可維護性。

<br />

## .pipe 檔

用途： Pipe (管道) 用於轉換和格式化資料，使其在 template 中更方便呈現預想的樣式。

- `.pipe.ts`

    功能： 定義一個 Pipe 的類別和轉換行為。

    內容： 包含帶有 `@Pipe` 裝飾器的類別，實現 transform 方法來處理輸入值。

    ```
    // capitalize.pipe.ts

    import { Pipe, PipeTransform } from '@angular/core';

    @Pipe({
        name: 'capitalize'
    })

    export class CapitalizePipe implements PipeTransform {
        transform(value: string): string {
            return value.charAt(0).toUpperCase() + value.slice(1);
        }
    }
    ```
    
    - `@Pipe` 裝飾器：用來定義 Pipe，包含 name 屬性，用於指定 Pipe 的名稱。這個名稱會在模板中使用。

    - `PipeTransform` 介面：要求 Pipe 實現 `transform` 方法，用於實際的資料轉換。

    - `transform` 方法：接受一個輸入值，並返回轉換後的值。這裡將字串的首字母轉為大寫，其餘字母轉為小寫。

    完成 `capitalize.pipe.ts` 後，在想要使用的 Component 中引入 `CapitalizePipe`。
    
    ```
    // example.component.ts

    import { Component } from '@angular/core';

    @Component({
        selector: 'app-example',
        standalone: true,
        templateUrl: './example.component.html',
        styleUrl: './example.component.scss',
        imports: []
    })

    export class ExampleComponent {}
    ```

    ```
    <!-- example.component.html -->
    
    <h1>{{ 'hello world' | capitalize }}</h1>
    ```

<br />

## .enum 檔

用途： Enum (枚舉) 用於定義一組有命名的常數，增強程式碼的可讀性和可維護性。

- `.enum.ts`

    功能： 定義枚舉類型。

    內容： 包含 TypeScript 枚舉。
    
    ```
    // user-role.enum.ts

    export enum UserRole {
        Admin = 'ADMIN',
        User = 'USER',
        Guest = 'GUEST'
    }
    ```

.enum 檔能夠幫助使用命名的常數來提高程式碼的可讀性，避免寫死 (hard-coding)，並且讓程式碼更具可維護性。

<br />

## .environment 檔

用途： 定義不同環境 (例如：開發、測試、生產) 下的配置，例如：API 路徑、調試選項等。

### `environment.ts` 和 `environment.prod.ts` 的差異

- `environment.ts`

    用途：用於開發環境，當在本地開發應用程式時，Angular 會使用這個檔案中的設定。

    設定內容：通常包含一些適用於開發環境的設定，例如：測試伺服器的 API URL、開發中使用的特殊功能開關等。

    ```
    export const environment = {
        production: false,
        apiUrl: 'http://localhost:3000/api',
        debugMode: true
    };
    ```
    
    - `production`：表示當前環境是否為生產環境，false 表示開發環境。

    - `apiUrl`：定義了 API 伺服器的 URL，在開發過程中用於連接到本地伺服器。

    - `featureFlag`：控制某些功能是否啟用，可以根據需要開啟或關閉特性。

- `environment.prod.ts`

    用途：用於生產環境，當要將應用程式部署到生產環境時，Angular 會使用這個檔案中的設定。

    設定內容：包含適用於生產環境的設定，例如：生產伺服器的 API URL、關閉開發中使用的特殊功能 (例如：除錯模式) 等。

    ```
    export const environment = {
        production: true,
        apiUrl: 'https://api.example.com',
        debugMode: false
    };
    ```
    
    - `production`：設定為 true 表示此檔案用於生產環境。

    - `apiUrl`：定義了生產環境的 API 伺服器 URL。

    - `featureFlag`：通常在生產環境中禁用某些功能。

### 使用方式

Angular 使用 `fileReplacements` 機制來根據環境自動替換 `environment.ts`。在 `angular.json` 中可以看到這個設定

```
"configurations": {
    "production": {
        "fileReplacements": [
            {
                "replace": "src/environments/environment.ts",
                "with": "src/environments/environment.prod.ts"
            }
        ],
        ...
    }
}
```

當使用 `ng build --prod` 進行專案編譯時，Angular 會自動將 `environment.ts` 替換為 `environment.prod.ts`。這樣可以確保應用程式在不同的環境中使用正確的設定。

## .directive 檔

用途： Directive 用於擴展或操縱 DOM 元素的行為。自定義指令可用於實現複雜的交互效果或重用的行為操作。

- `.directive.ts`

    功能： 定義一個指令的類別和相關操作。

    內容： 包含帶有 `@Directive` 裝飾器的類別，指定指令的選擇器和行為。

    ```
    // highlight.directive.ts

    import { Directive, ElementRef, HostListener } from '@angular/core';

    @Directive({
        selector: '[appHighlight]'
    })

    export class HighlightDirective {
        constructor(private el: ElementRef) {}

        @HostListener('mouseenter')
        onMouseEnter() {
            this.highlight('yellow');
        }

        @HostListener('mouseleave')
        onMouseLeave() {
            this.highlight(null);
        }

        private highlight(color: string) {
            this.el.nativeElement.style.backgroundColor = color;
        }
    }
    ```

<br />

## .guard 檔

用途： Guard (路由守衛) 用於控制路由存取和導航的權限，決定用戶是否可以導航到特定路由。

- `.guard.ts`

    功能： 定義路由守衛的類別和驗證邏輯。

    內容： 實現 Angular 的路由守衛介面，例如：CanActivate、CanDeactivate 等。


    ```
    // auth.guard.ts

    import { Injectable } from '@angular/core';
    import { CanActivate, Router } from '@angular/router';

    @Injectable({
        providedIn: 'root'
    })

    export class AuthGuard implements CanActivate {
        constructor(private router: Router) {}

        canActivate(): boolean {
            if (/* 檢查用戶是否已登入 */) {
                return true;
            } else {
                this.router.navigate(['/login']);
                return false;
            }
        }
    }
    ```

    - `CanActivate` 介面：用於檢查是否允許進入特定路由。
    
    - `canActivate` 方法：如果用戶未認證，重定向至登錄頁面，返回 false 表示不允許導航。

