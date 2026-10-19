# Application-only Testing

If you’ve modified an existing OneCX application (e.g. OneCX Theme UI) and the change is confined to that app, no rebuild of the shell or the libraries is required.

## [](#testing-the-application)Testing the application

You can use the same options as described in [Running and Testing Applications](../../onecx-docs-start/first-app/running%5Fcustom%5Fapps%5Foverview.html#running-and-testing-applications):

* You can follow the [automatic image build process](../../onecx-docs-start/first-app/image%5Fbuild%5Fautomatic.html) and use the build context in `docker-compose.yaml` to build the image from your local application each time you run Docker Compose.
* You can follow the [manual image build process](../../onecx-docs-start/first-app/image%5Fbuild%5Fmanual.html) to build a local image in the application and adjust the .env UI variable to use your local image.
* You can set up your application for hot reloading as described in [Hot Reload](../../onecx-docs-start/first-app/enable%5Fhot%5Freload.html) for faster development and testing.

## [](#related)Related

* [Contribution & Testing](index.html) — the overview and the other verification tiers.
* [Local-only testing](local-only.html) — verifying a change with the library’s own unit tests and Storybook.
* [Integration testing](integration.html) — building the libraries locally and copying them into the shell and apps.
