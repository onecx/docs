# OneCX Announcement Management

![overview](_images/overview.png) 

Figure 1\. Announcement UI

## [](#overview)Overview

The Announcement Management feature is designed to facilitate the dissemination of important information across a platform. It supports various types of announcements, such as system maintenance notifications, general information, and achievements. This feature ensures that users are always informed about critical updates and events. Key Features includes:

**Platform-Wide Announcements**:

* System Maintenance: Allows administrators to post announcements about system maintenance, ensuring users are aware of any scheduled downtimes or updates.
* General Information: Provides a channel for sharing other important information, such as policy changes or new feature releases.
* Achievements: Highlights significant achievements or milestones, fostering a sense of community and engagement.

**Workspace-Specific Announcements**:

* Targeted Messaging: Enables the placement of announcements for specific workspaces, ensuring that relevant information reaches the appropriate audience.
* Flexible Distribution: Supports sending announcements to all workspaces simultaneously, making it easy to communicate platform-wide updates.

**Application-Specific Announcements**:

* Dedicated Announcements: Allows for the creation of announcements specific to individual applications, ensuring users of those apps receive pertinent information.

**Important Announcements**:

* High Visibility: Important announcements, such as system maintenance notifications, are displayed prominently in a micro frontend and visualized by the shell on any page of the portal. This ensures that critical information is always visible to users.

**Administrative Controls**:

* Easy Management: Provides administrators with tools to create, edit, and manage announcements efficiently.
* Scheduling: Allows for the scheduling of announcements to be posted at specific times, ensuring timely communication.

## [](#benefits)Benefits

* Enhanced Communication: Ensures that important information is effectively communicated to all users, reducing confusion and improving awareness.
* Targeted Messaging: Allows for targeted announcements, ensuring that users receive information relevant to their specific workspaces or applications.
* High Visibility: Important announcements are prominently displayed, ensuring that critical updates are not missed.
* Administrative Efficiency: Streamlines the process of managing announcements, saving time and resources for administrators.

## [](#ui-examples)UI Examples

![announcement configuration](_images/announcement_configuration.png) 

Figure 2\. Announcement configuration

## [](#licence)Licence

This software is licensed under the Apache License, Version 2.0\. You may obtain a copy of the license in the corresponding LICENSE file or visit the [Apache website](https://www.apache.org/licenses/LICENSE-2.0) for more information.

## [](#contributing)Contributing

We welcome contributions from the community. If you would like to contribute to the development of OneCX Announcement Management Software, please follow our contribution guidelines (tbd).

## [](#issue-tracking)Issue Tracking

All OneCX Announcement Management issues are tracked and maintained at the [issue tracking tool](https://xyz.com).

## [](#structure-overview)Structure Overview

OneCX Announcement Management Software is a comprehensive solution for managing Announcement items in a user-friendly and efficient manner. It is a solution that consists of three main components: a backend service, a user interface and a backend-for-frontend (BFF) layer.

The three components of OneCX Announcement Management Software are as follows:

1. Announcement Management User Interface (UI) The user interface component is based on Angular, a popular JavaScript framework for building dynamic web applications. It offers a user-friendly and intuitive interface for interacting with the Announcement management system. Users can perform actions such as searching and editing of Announcement items.
2. Announcement Management Backend for Frontend (BFF) The BFF layer acts as an intermediary between the frontend user interface and the backend service. It handles tasks such as data aggregation, transformation, and composition to provide an optimized API for the UI. The BFF layer is designed to enhance performance and simplify the integration of the frontend with the backend service.
3. Announcement Management Backend Service (SVC) This component provides the core functionality. It handles tasks such as storage, retrieval and editing of Announcement items. The backend is built cloud native using Quarkus.

Interfaces are based on the TM-Forum standard [TMF 667](https://github.com/tmforum-apis/TMF667%5FDocument).

## [](#getting-started)Getting Started

To get started with OneCX Announcement Management Software, please refer to the following installation and setup instructions specific to each component:

* [OneCX Announcement Management UI (User Interface) - Getting Started](https://onecx.github.io/docs/onecx-announcement/current/onecx-announcement-ui/index.html)
* [OneCX Announcement Management BFF (Backend for Frontend) - Getting Started](https://onecx.github.io/docs/onecx-announcement/current/onecx-announcement-bff/index.html)
* [OneCX Announcement Management SVC (Backend) - Getting Started](https://onecx.github.io/docs/onecx-announcement/current/onecx-announcement-svc/index.html)

For detailed usage instructions and API documentation, please refer to the respective documentation files for each component.

## [](#roadmap)Roadmap

tbd
