# Module Federation

OneCX is a platform composed of many independently developed applications, each built, versioned, and deployed on its own schedule. This page is a technology-agnostic overview of **module federation** — the mechanism that makes that composition possible — and the role it plays in OneCX; it does not cover how to configure it for a specific application, which is described in [Expose a Remote Module](../setup/required/expose-remote-module.html) and [Configure Remote Package Sharing](../setup/required/configure-remote-package-sharing.html).

## [](#what-is-module-federation)What is module federation

Module federation is a pattern for loading JavaScript code across independently built and deployed bundles at runtime, rather than at build time. A conventional web application is compiled as a single bundle: every module it depends on is known and linked when the application is built. Module federation removes that constraint — a bundle (a **host**) can load modules exposed by another, separately built bundle (a **remote**) over the network when the application actually runs, without either bundle having been compiled against the other’s source.

This is what allows OneCX’s UI to be assembled from applications that are developed by different teams, in different repositories, and released independently of one another and of the shell itself, while still appearing to the user as a single, seamless application.

The concept originates from [Webpack’s Module Federation](https://webpack.js.org/concepts/module-federation/) and has since been adopted more broadly, including implementations such as [Module Federation (the framework-agnostic runtime and tooling that OneCX’s recommended setup builds on)](https://module-federation.io/) and, for Angular applications that do not use Webpack, [Native Federation](https://www.angulararchitects.io/en/blog/dynamic-module-federation-with-angular/). All of these share the same underlying idea — hosts loading remotely-exposed modules at runtime — even though their configuration and build tooling differ.

## [](#module-federations-role-in-onecx)Module federation’s role in OneCX

In OneCX, the **shell** is the host and every other application is a remote. At startup, and as the user navigates, the shell uses module federation to fetch and load the code for whichever application or component needs to be displayed, straight from that application’s own deployment — the shell never bundles application code itself. This is what OneCX means by a **microfrontend**: an application that is developed and deployed as an independent unit, but is loaded and composed into the shell’s UI at runtime via module federation.

Module federation is the mechanism behind two distinct kinds of composition in OneCX:

* **Loading a microfrontend module** — when the user navigates to a route owned by an application, the shell resolves the route to that application’s module federation configuration and loads the corresponding module on demand.
* **Loading a remote component** — when a page needs to embed a piece of UI owned by a **different** application (a Slot Component), the shell loads that component the same way, via module federation, rather than the embedding application bundling it.

Because each application publishes its own module federation configuration independently, teams can release a new version of their application at any time without rebuilding or redeploying the shell, or any other application.

## [](#sharing-dependencies-at-runtime)Sharing dependencies at runtime

Loading every application’s code independently would be wasteful if each one also shipped its own copy of every shared library (the framework itself, the OneCX platform libraries, and so on). Module federation addresses this with **shared dependencies**: a host and its remotes can negotiate, at runtime, to reuse a single instance of a matching dependency instead of each loading their own. In OneCX, this is what allows many independently built applications to share a single instance of Angular or React, `rxjs`, and the OneCX platform packages, rather than loading a duplicate copy per application.

This negotiation is governed by **share scopes** — named groupings that determine which applications' shared dependencies are eligible to be reused by which other applications. Configuring an application’s share scope, and which dependencies it shares into that scope, is covered in [Configure Remote Package Sharing](../setup/required/configure-remote-package-sharing.html).

## [](#related)Related

* [Expose a Remote Module](../setup/required/expose-remote-module.html) — the practical, per-technology how-to for exposing an application to the shell via module federation.
* [Configure Remote Package Sharing](../setup/required/configure-remote-package-sharing.html) — the practical how-to for configuring share scopes and shared dependencies.
* [Module Federation in OneCX](../module-federation/index.html) — deep internal reference covering preloaders, dependency sharing, and slot components in implementation detail.
* [Webpack Module Federation](https://webpack.js.org/concepts/module-federation/) and [Module Federation](https://module-federation.io/) — external documentation for the underlying technology.
