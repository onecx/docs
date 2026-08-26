# undefined

### [](#content-exposed-using-angular-method)Content Exposed Using Angular Method

| |  **It is NOT recommended** to use the Angular expose method. Doing so restrains the platform from using many frameworks with different versions, which means that all Microfrontends would need to use the same technology and version. |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

When exposing modules and Remote Components using the Angular method, there are two requirements:

1. Webpack configuration needs to expose the module or component file directly. It means that instead of pointing to a **main.ts** file that is bootstrapping the content, **module.ts** and **component.ts** files should be used directly.
2. The **main.ts** file of Microfrontend’s modules (content type) needs to bootstrap the module asynchronously.  
**main.ts** content should look similar to:  
```typescript  
import('./bootstrap').catch(err => console.error(err));  
```  
**bootstrap.ts** content should look similar to (or any custom bootstrap of your Microfrontend):  
```typescript  
import { AppModule } from './app/app.module';  
import { environment } from './environments/environment';  
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';  
import { enableProdMode } from '@angular/core';  
if (environment.production) {  
  enableProdMode();  
}  
platformBrowserDynamic().bootstrapModule(AppModule)  
  .catch(err => console.error(err));  
```

__Table 1\. Navigation__
| [← Previous: Microfrontend Content Bootstrapping Explained](bootstrapping-explained.html) | [Next: Content Exposed Using Webcomponent Method →](webcomponent-expose-method.html) |
| ----------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
