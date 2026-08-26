# OneCX Welcome Management

![overview](_images/overview.png) 

Figure 1\. Welcome UI

## [](#%5Foverview)Overview

The welcome dialogue feature is designed to enhance the user experience by providing a personalized and engaging entry point to the portal. It serves multiple purposes, including displaying important announcements, greeting the user, and showcasing customized images to make the starting page visually appealing. Key features include:

**Announcements Display**:

* Integration with Announcements Management Tool: The welcome dialogue pulls in the latest announcements or news from an integrated announcements management tool.
* Real-Time Updates: Ensures that users are always informed about the most recent and relevant information.

**Personalized Greeting**:

* User-Specific Welcome Message: Greets the logged-in user by name, creating a personalized experience.
* Dynamic Content: The greeting can include the current date, time, and other relevant user-specific information.

**Customized Images**:

* Visual Appeal: Displays attractive images that can be customized for each workspace.
* Administrative Control: Administrators have the ability to maintain and update these images, ensuring they are relevant and up-to-date.
* Workspace-Specific: Different workspaces can have unique sets of images, tailored to their specific themes or needs.

## [](#%5Fbenefits)Benefits

* Enhanced User Engagement: The personalized greeting and dynamic content make users feel welcomed and valued.
* Improved Communication: The announcements feature ensures that important information is effectively communicated to all users.
* Aesthetic Appeal: Customized images add a visual element that makes the portal more inviting and engaging.

## [](#%5Flicence)Licence

This software is licensed under the Apache License, Version 2.0\. You may obtain a copy of the license in the corresponding LICENSE file or visit the [Apache website](https://www.apache.org/licenses/LICENSE-2.0) for more information.

## [](#%5Fcontributing)Contributing

We welcome contributions from the community. If you would like to contribute to the development of OneCX Welcome Management Software, please follow our contribution guidelines (tbd).

## [](#%5Fissue%5Ftracking)Issue Tracking

All OneCX Welcome issues are tracked and maintained at the [issue tracking tool](https://xyz.com).

## [](#%5Fstructure%5Foverview)Structure Overview

OneCX Welcome Software is a comprehensive solution for managing Welcome screens in a user-friendly and efficient manner. It is a solution that consists of three main components: a backend service, a user interface and a backend-for-frontend (BFF) layer.

The three components of the OneCX Welcome Software are as follows:

1. Welcome User Interface (UI) The user interface component is based on Angular, a popular JavaScript framework for building dynamic web applications. It offers a user-friendly and intuitive interface for interacting with the Welcome system. Users can perform actions such as searching and editing of Welcome screens.
2. Welcome Backend for Frontend (BFF) The BFF layer acts as an intermediary between the frontend user interface and the backend service. It handles tasks such as data aggregation, transformation, and composition to provide an optimized API for the UI. The BFF layer is designed to enhance performance and simplify the integration of the frontend with the backend service.
3. Welcome Backend Service (SVC) This component provides the core functionality. It handles tasks such as storage, retrieval and editing of Welcome screens. The backend is built cloud native using Quarkus.

Interfaces are based on the TM-Forum standard [TMF 667](https://github.com/tmforum-apis/TMF667%5FDocument).

## [](#%5Fgetting%5Fstarted)Getting Started

To get started with OneCX Welcome Software, please refer to the following installation and setup instructions specific to each component:

* [OneCX Welcome UI (User Interface) - Getting Started](https://onecx.github.io/docs/onecx-welcome/current/onecx-welcome-ui/index.html)
* [OneCX Welcome BFF (Backend for Frontend) - Getting Started](https://onecx.github.io/docs/onecx-welcome/current/onecx-welcome-bff/index.html)
* [OneCX Welcome SVC (Backend) - Getting Started](https://onecx.github.io/docs/onecx-welcome/current/onecx-permission-svc/index.html)

For detailed usage instructions and API documentation, please refer to the respective documentation files for each component.

## [](#%5Froadmap)Roadmap

tbd
