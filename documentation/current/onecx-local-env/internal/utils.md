# Utilities used in OneCX Local Environment

## [](#additional-started-services)Additional Started Services

In addition to the original OneCX products, some open-source tools are also used and launched.

### [](#keycloak)Keycloak

[Keycloak](https://www.keycloak.org/) is an open-source software for Identity and Access Management (IAM) that provides features like single sign-on (SSO), user authentication, and authorization for modern applications and services.

There is an OneCX realm which contains all configurations needed by OneCX like users, roles, clients etc.

* <http://keycloak-app/admin/master/console/#/onecx>
* Username: **admin**
* Password: **admin**

![screenshot successful keycloak onecx](../_images/screenshot_successful-keycloak-onecx.png) 

Figure 1\. Keycloak running on localhost

### [](#pgadmin)pgAdmin

[pgAdmin](https://www.pgadmin.org/) is a popular, open-source administration and development platform for [PostgreSQL](https://www.postgresql.org/) databases.

| |  This service is optional, as it is not strictly necessary for OneCX to function. For a better user experience, use a native client directly on your computer. |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |

* <http://pgadmin/>
* Username: **user@1000kit.org**
* Password: **admin**

![screenshot successful pgadmin](../_images/screenshot_successful-pgadmin.png) 

Figure 2\. pgAdmin running on localhost

### [](#traefik)Traefik

Traefik is required for routing within Docker Compose networks as well as to and from networks outside this network.

* [Use Traefik for routing Microfrontends](../scripts/toggle-mfes.html#routing-and-prioritize)
* <http://traefik:8082/dashboard/>

![screenshot successful traefik](../_images/screenshot_successful-traefik.png) 

Figure 3\. Traefik Dashboard
