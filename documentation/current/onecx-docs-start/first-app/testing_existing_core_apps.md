# Testing Changes to Existing OneCX Core Apps

If you’ve modified an existing OneCX core app (e.g. OneCX Theme UI), you can test it using the same methods available for custom applications.

You can use the same options as described in [Running and Testing Applications](running%5Fcustom%5Fapps%5Foverview.html#running-and-testing-applications):

* You can follow the [automatic image build process](image%5Fbuild%5Fautomatic.html) and use the build context in `docker-compose.yaml` to build the image from your local application each time you run Docker Compose.
* You can follow the [manual image build process](image%5Fbuild%5Fmanual.html) to build a local image in the application and adjust the .env UI variable to use your local image.
* You can set up your application for hot reloading as described in [Hot Reload](enable%5Fhot%5Freload.html) for faster development and testing.
