# undefined

## [](#mf-authentication-service-wrapper)Custom Authentication service

Custom authentication service can be configured and provided. It can be achieved by setting AUTH\_SERVICE and AUTH\_SERVICE\_CUSTOM\_URL in enviroment configuration.

**Module federation** is used to load implementation of custom authentication factory which can handle authentication and authorization of the application.

## [](#%5Fconfiguration%5Fin%5Fenvironment)Configuration in Environment:

* `AUTH_SERVICE` \- Set this to 'custom' to enable custom authentication service
* `AUTH_SERVICE_CUSTOM_URL` \- URL to load custom authentication service factory via **module federation**. The module federation remote should expose a factory function that returns an implementation of the **authentication service factory**.
