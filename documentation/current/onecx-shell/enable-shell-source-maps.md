# Enable shell source maps

Shell v3 generates webpack source maps. This is useful for diagnostics and debugging, especially in development and lower environments.

## [](#importance-of-source-maps)Importance of source maps in shell

Since applications share common code and dependencies, it is very likely that issues in development will be related to the shared code by the shell. This is especially true for issues related to dependencies like Angular, RxJS, OneCX libraries, and other common code.

Enabling source maps in shell ensures that the shared code used by any application is also mapped, making it easier to identify and resolve issues that may arise in development.

## [](#how-to-enable)How to enable

To enable source maps for the shell, set the `SOURCE_MAPS_ACCESS_RULE` environment variable to `allow all;` in development environment or any other value that allows access to source maps as intended.

## [](#default-behavior)Default behavior

* default: `deny all;`By default, the `SOURCE_MAPS_ACCESS_RULE` is set to `deny all;`, which means that source maps are generated but not accessible.

## [](#recommendation)Recommendation

| |  Do not enable public source map access in production unless the security and operational implications have been thoroughly reviewed. |
| --------------------------------------------------------------------------------------------------------------------------------------- |

Recommended practice:

* enable source maps in development
* allow source maps only in trusted lower environments if needed
* keep production access disabled by default
