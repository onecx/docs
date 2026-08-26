# Set up a OneCX Local Environment

This guide provides instructions for setting up and installing **onecx-local-env**, the local development environment for OneCX. Once setup is done the environment can be started, see [Run OneCX](run-onecx.html).

If you want to setup a development environment for writing OneCX documentation, please refer to the [OneCX Docs: Setting up](../onecx-docs-doc/setup.html) guide instead.

## [](#prerequisites)Prerequisites

### [](#operating-systems)Operating Systems

**onecx-local-env** fully supports Linux, macOS and Windows 10/11 via WSL2.

Linux & macOS

Linux and macOS are natively supported operating systems for **onecx-local-env** and do not require any operating-system-specific adjustments. Users of these operating systems can safely proceed to the next section of this guide.

Windows

To run **onecx-local-env** on Windows, Windows Subsystem for Linux version 2 (WSL2) must be installed and configured on the system. To check if WSL2 is currently installed, open PowerShell or a command prompt and run the following command:

```powershell
wsl -l -v
```

This command lists all installed WSL distributions along with their version numbers. To run **onecx-local-env**, at least one distribution must be installed and its version **must be 2**.

In case of errors, no output, or no WSL2 distributions listed, WSL2 is either not installed or not properly configured. Official guidance on installing and configuring WSL2 can be found here:

1. [Install WSL (learn.microsoft.com)](https://learn.microsoft.com/en-us/windows/wsl/install)
2. [Set up the Linux Distribution](wsl2.html)

| |  Checkpoint At this point, users should have verified that their operating system is supported and, if using Windows, that WSL2 is properly installed and configured. |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

| |  If you are using Windows and WSL, you should install and use your **entire development environment** in WSL. This includes cloning Git repositories and installing tools like Docker, Git, and jq.Connect your development environment, such as Visual Studio Code, to WSL and install its extensions/plugins in WSL as well. Avoid working on your WSL files from Windows, i.e. via mount paths like /mnt/c/…​.This can lead to file permission issues and unexpected behavior when running scripts and Docker containers. |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

### [](#programs)Programs

**onecx-local-env** requires the direct installation of some programs on the operating system. This list reflects only the essential necessary programs, additional tools may be required for specific use cases.

Docker & Docker Compose

To ensure that all used features work correctly, it is recommended to use **Docker Compose** version **v2.20.0** or higher. When using older versions, some functions may not work as expected.

The functionality of **onecx-local-env** has been tested with the following versions:

| Docker         | **28.1.1** ⇒ [instructions to install Docker](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository) |
| -------------- | -------------------------------------------------------------------------------------------------------------------------- |
| Docker Compose | **2.35.1** ⇒ [Instructions to install Docker Compose](https://docs.docker.com/compose/install/)                            |

| curl    | Import OneCX data ⇒ [Instructions to install curl](https://curl.se/download.html)                                                                                                                             |
| ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| git     | Various actions such as cloning the **onecx-local-env** repository and following the installation instructions ⇒ [Instructions to install git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) |
| jq      | Import OneCX data ⇒ [Instructions to install jq](https://stedolan.github.io/jq/download/)                                                                                                                     |
| node.js | Working on local microfrontends and import OneCX data, version >= 20 ⇒ [Instructions to install node.js](https://nodejs.org/en/download/)                                                                     |

## [](#onecx-installation)OneCX Installation

### [](#cloning-the-repository)Cloning the repository

Before starting the installation, the **onecx-local-env** repository needs to be cloned into a folder on the local machine/inside WSL2\. This can be done using the following command:

```bash
git clone https://github.com/onecx/onecx-local-env.git
```

| |  Checkpoint At this point, the **onecx-local-env** repository should be cloned and all necessary scripts should have execute permissions. To verify: Confirm all **.sh** scripts have execute permissions (indicated by an **x** in the permission string). If any scripts are missing execute permissions, run chmod +x <file name>. |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### [](#changing-the-hosts-file)Changing the hosts file

In order to expose multiple services on the same local port, OneCX Local Environment uses the Traefik reverse proxy. Traefik routes requests to the appropriate services based on the requested hostname.

To ensure that all relevant hostnames used by OneCX are correctly routed to the local machine, the system **hosts** file needs to be modified to include entries for all OneCX services.

Hosts file locations

| Windows | c:\\Windows\\System32\\drivers\\etc\\hosts |
| ------- | ------------------------------------------ |
| Linux   | /etc/hosts                                 |
| macOS   | /etc/hosts                                 |

Click here to view entries to be added to the **hosts** file 

```text
# OneCX - utilities
127.0.0.1 traefik
127.0.0.1 postgresdb
127.0.0.1 pgadmin
127.0.0.1 keycloak-app
127.0.0.1 rustfs
127.0.0.1 rustfs-console
# OneCX - local services
127.0.0.1 sonar

# OneCX - product services
127.0.0.1 onecx-ai-provider-runtime
127.0.0.1 onecx-ai-provider-bff
127.0.0.1 onecx-ai-provider-svc
127.0.0.1 onecx-announcement-bff
127.0.0.1 onecx-announcement-svc
127.0.0.1 onecx-bookmark-svc
127.0.0.1 onecx-bookmark-bff
127.0.0.1 onecx-chat-bff
127.0.0.1 onecx-chat-svc
127.0.0.1 onecx-document-svc
127.0.0.1 onecx-document-bff
127.0.0.1 onecx-file-storage-svc
127.0.0.1 onecx-help-svc
127.0.0.1 onecx-help-bff
127.0.0.1 onecx-iam-bff
127.0.0.1 onecx-iam-svc
127.0.0.1 onecx-notification-svc
127.0.0.1 onecx-notification-bff
127.0.0.1 onecx-notification-bff-2
127.0.0.1 onecx-parameter-svc
127.0.0.1 onecx-parameter-bff
127.0.0.1 onecx-permission-svc
127.0.0.1 onecx-permission-bff
127.0.0.1 onecx-product-store-svc
127.0.0.1 onecx-product-store-bff
127.0.0.1 onecx-search-config-svc
127.0.0.1 onecx-search-config-bff
127.0.0.1 onecx-shell-bff
127.0.0.1 onecx-tenant-svc
127.0.0.1 onecx-tenant-bff
127.0.0.1 onecx-theme-svc
127.0.0.1 onecx-theme-bff
127.0.0.1 onecx-welcome-svc
127.0.0.1 onecx-welcome-bff
127.0.0.1 onecx-workspace-svc
127.0.0.1 onecx-workspace-bff
127.0.0.1 onecx-user-profile-avatar-svc
127.0.0.1 onecx-user-profile-svc
127.0.0.1 onecx-user-profile-bff
```

| |  If you are using Windows with WSL, ensure that changes to the Windows Hosts file are correctly propagated to WSL. By default, and unless disabled via the generateHosts option (see [WSL network settings](https://learn.microsoft.com/en-us/windows/wsl/wsl-config#network-settings)), WSL automatically generates its Hosts file based on the contents of the Windows Hosts file. If this does not happen, or if automatic Hosts file generation has been disabled, you can manually update the WSL Hosts file by modifying the Linux Hosts file at the path described above. |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## [](#next-step)Next Step

After completing the steps outlined in this guide, **onecx-local-env** is now ready to run OneCX locally. Check the instructions on how to start, access, and stop the local environment in the [Run OneCX](run-onecx.html) guide.
