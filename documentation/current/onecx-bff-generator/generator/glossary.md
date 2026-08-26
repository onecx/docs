# Glossary

A collection of essential terms and concepts in the context of the **OneCX BFF Generator**.

## [](#backend-for-frontend)Backend For Frontend Service (BFF)

A Backend for Frontend (BFF) is a backend service tailored to a specific frontend application. It acts as an API layer between the frontend and backend services and adapts backend APIs to frontend requirements.

## [](#permission)Permission

Permissions are a way **to control access** to certain features or actions within an application. They allow you to define who can perform specific actions based on their roles or other criteria. By configuring **permissions**, you can ensure that only authorized users can access sensitive data or perform critical operations, enhancing the security and integrity of your application.  
The **permissions** are defined in the `values.yaml` file of the [Helm](https://helm.sh/) chart. This file contains a section for permissions where you can specify the actions that users can perform on different entities.  
The `values.yaml` file is used by the OneCX permission operator during deployment to create the necessary permissions in the [Permission Management](../../onecx-permission/index.html).
