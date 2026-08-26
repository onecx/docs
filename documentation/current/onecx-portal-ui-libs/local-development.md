# OneCX UI Libraries: Local Development

This guide explains how to set up a local development environment for testing changes to the libraries, located in the **onecx-portal-ui-libs** repository and integrating them in local applications and a local [OneCX Shell](../onecx-shell/index.html).

Before proceeding, make sure you have read the following documentation:

* [OneCX Local Environment](../onecx-local-env/index.html)

These resources provide essential background on setting up a local OneCX environment and running custom applications._This guide assumes you already know how to start OneCX locally and how to replace application images with local versions._

## [](#making-changes-to-the-libraries)Making changes to the libraries

To begin making changes and contributing to the libraries:

1. Fork the repository: <https://github.com/onecx/onecx-portal-ui-libs>  
**Important:** Do **not** just copy the `main` branch. You may need to work on other branches like `v5` to apply changes to older library versions.
2. Clone your fork to your local machine. The command below assumes that you named your fork `onecx-portal-ui-libs`:  
```bash  
git clone https://github.com/<YOUR_USER_NAME>/onecx-portal-ui-libs  
```
3. Navigate to the cloned repository directory and install dependencies:  
```bash  
cd onecx-portal-ui-libs && npm i  
```
4. Open the project in your preferred code editor (e.g., VSCode) and make your desired changes.

| |  Checkpoint At this point you should have…​ a fork of the onecx-portal-ui-libs repository in your GitHub account. a local clone of said fork on your machine. installed all dependencies using npm i. made some changes to the codebase. |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

## [](#testing-the-changes-locally)Testing the changes locally

To test your changes, the libraries must be built and copied into the `node_modules` folders of both the shell and the app(s) you want to test in.

While it’s technically possible to only copy the changes to the `node_modules` folders of the shell in certain situations, we recommend you always copy the changes to both shell and the app(s) to avoid issues during dependency sharing.

Complete the following steps to test your changes:

### [](#1-identify-relative-paths)1\. Identify Relative Paths

Before copying the built libraries, you first need to decide which application(s) you want to test the changes in. After deciding on the application(s), you need to determine the relative paths from the root of `onecx-portal-ui-libs` to both the application(s) and your local clone of `onecx-shell-ui`. The relative paths will be used later and might look something like this:

* For the app(s), e.g.:  
```none  
../../apps/my-cool-app  
```
* For your local clone of `onecx-shell-ui`, e.g.:  
```none  
../onecx-shell-ui  
```

### [](#2-create-copy-build-to-file)2\. Create `.copy-build-to` File

Create an empty file named `.copy-build-to` in the root of **onecx-portal-ui-libs**.  
This file will contain the paths to the **node\_modules** folders that the build output should be copied to.

The file can contain multiple paths, one per line. Each path must be relative to the root of **onecx-portal-ui-libs** and must point to the **@onecx** folder inside the **node\_modules** folder of the target project.  
For now, leave the file empty. You will add the paths in the next step.

### [](#3-add-paths-to-copy-build-to)3\. Add Paths to `.copy-build-to`

Use the relative paths from step 1 and follow these patterns:

#### [](#for-apps-non-shell)For Apps (non-shell)

Append `/node_modules/@onecx` to the app path.

Example:

```none
../../apps/my-cool-app/node_modules/@onecx
```

**Note:** Do **not** add a trailing `/`.

#### [](#for-shell)For Shell

Identify the library version you’re testing:

* **v5.x.x** → changes made on `v5` or branches based on `v5`
* **v6.x.x** → changes made on `main` or branches based on `main`

##### [](#v5-x-x)v5.x.x

Copy only to the Angular 18 pre-loader by appending `/pre_loaders/angular-18/node_modules/@onecx` to the shell path.

Example

```none
../onecx-shell-ui/pre_loaders/angular-18/node_modules/@onecx
```

##### [](#v6-x-x)v6.x.x

Copy to both Angular 19 pre-loader and shell’s root `node_modules` by appending `/pre_loaders/angular-19/node_modules/@onecx` and `/node_modules/@onecx` to the shell path.

Example

```none
../onecx-shell-ui/pre_loaders/angular-19/node_modules/@onecx
../onecx-shell-ui/node_modules/@onecx
```

**Note:** Similar to apps, do **not** add a trailing `/` to any of the paths.

| |  Checkpoint At this point, your .copy-build-to file should contain two or more paths (shell + at least one app), each on a new line, pointing to the @onecx folder inside the node\_modules folder of the target projects (apps and/or shell). The file might look something like this: ../../apps/my-cool-app/node\_modules/@onecx ../onecx-shell-ui/pre\_loaders/angular-19/node\_modules/@onecx ../onecx-shell-ui/node\_modules/@onecx |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### [](#4-build-and-copy-libraries)4\. Build and Copy Libraries

Once you have correctly set up the `.copy-build-to` file, you are ready to build and copy the libraries to the specified paths.

Before building, make sure to remove potentially outdated cached builds by running:

```bash
rm -rf dist .nx/cache
```

Afterwards, build and copy the libraries by running:

```bash
npm run build-copy
```

| |  Checkpoint At this point, you should see terminal output indicating that the libraries have been built and copied to the specified paths. If you encounter any errors, refer to any error messages and ensure that the paths in the .copy-build-to file are correct. |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### [](#5-prepare-apps-and-shell-for-local-testing)5\. Prepare Apps and Shell for Local Testing

Before running the shell and app(s) with the locally built libraries, you need to make some adjustments to ensure the local versions are used correctly:

1. Open the `package.json` files of each app, pre-loader, and shell that libraries were copied to.
2. Increase the version numbers of all OneCX packages to simulate a version update.  
| |  Ideally, you should use the version number your changes will be released in. Any version number higher than the current one should, however, work. Make sure to use the same version number for all OneCX packages within the project starting with 6. for v6.x.x or 5. for v5.x.x. |  
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
3. **Do not** run `npm install` after changing the version numbers.
4. Before running the app(s) (non-shell) delete any build caches to ensure a clean build environment. Delete build caches:  
```bash  
rm -rf dist .nx/cache .angular  
```
5. Before running the shell delete the build caches of both the respective pre-loader (18 or 19) and the shell itself to ensure a clean build environment. Example for v6.x.x (Angular 19):  
```bash  
rm -rf pre_loaders/angular-19/dist pre_loaders/angular-19/.nx/cache dist .nx/cache  
```

| |  Checkpoint At this point, you should have updated the version numbers in the package.json files of the shell and app(s) where the libraries were copied to. Additionally, you should have deleted any build caches to ensure a clean build environment. |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### [](#6-run-onecx-shell-and-apps)6\. Run OneCX Shell and App(s)

After completing the previous steps, you are now ready to run OneCX Shell and the app(s) with your local library changes.

To do so, follow the documentation on [running custom applications locally](../onecx-docs-start/first-app/running%5Fcustom%5Fapps%5Foverview.html).

| |  The steps for running the shell should match the steps for running existing OneCX core apps. |
| ----------------------------------------------------------------------------------------------- |
