# undefined

### [](#%5Fwebcomponent%5Fexpose%5Fmethod%5Frequirements)Webcomponent Expose Method Requirements

To correctly use Webcomponent expose method, 2 requirements need to be fulfilled:

1. Database is correctly configured for module or Remote Component  
   1. **technology** set to **WebComponent**  
   2. **tag name** set to agreed **HTML element name**
2. Microfrontend is adapted to expose Web Components compliant content  
   1. desired component needs to be registered as Custom Element in the Custom Elements Registry  
   2. Angular issues are covered (use the `[@onecx/angular-webcomponents](#onecx/angular-webcomponents)` library to cover them by default)  
         1. multiple routers synchronization  
         2. ngZone sharing  
         3. platform sharing

| |  Database configuration is easy to set up using the Application Store Application. |
| ------------------------------------------------------------------------------------ |

| |  To ensure Microfrontend compliance with Web Components for Angular modules and Remote Components, it is recommended to use the **[@onecx/angular-webcomponents](#onecx/angular-webcomponents)** library. |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

__Table 1\. Navigation__
| [← Previous: Custom Elements](custom-elements.html) |
| --------------------------------------------------- |
