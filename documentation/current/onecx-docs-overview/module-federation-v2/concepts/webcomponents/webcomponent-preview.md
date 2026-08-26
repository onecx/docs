# undefined

## [](#webcomponents-preview)Web Components Preview

Web Components are used in OneCX context for dynamic content creation. OneCX platform uses Web Components technologies to bound UI components to HTML elements. OneCX platform will use information from the Application Store to determine what HTML elements have to be rendered to allow certain modules and Remote Components to be bound to page content.

With Webcomponent expose method, the OneCX platform is only loading the code required for Microfrontend’s content into the Shell UI memory and creating a "host" element for Remote Components or modules to attach to using Web Components. The Microfrontend’s exposed content is partially responsible for the content creation. Microfrontends have to adapt exposed modules and components, so they are using Web Components Custom Elements.

### [](#%5Fkey%5Fconcepts)Key concepts

* [Custom Elements](custom-elements.html)
* [Webcomponent Expose Method Requirements](expose-method-requirements.html)
