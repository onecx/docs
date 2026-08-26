# Create an Entity Schema

What is an Entity Schema?

An entity schema defines the structure of an **entity/resource**, including its properties and their types. It is used to ensure that the data for the entity is consistent and follows a defined format. The schema definition follows the OpenAPI specification. This is the basis for processing feature data, e.g., for searching, displaying, and modifying it.  
At OneCX, we explicitly follow an **API-first approach**. In practice, this means that the [OpenAPI Specification](https://spec.openapis.org/oas/) file is created first, in which entities and the paths for requests/responses are described. The **OpenAPI** file serves as the basis for the implementation of the backend services and the frontend components.

Let’s begin by describing the entity that can be managed in the generated components. Starting this way makes the subsequent steps easier to understand.

## [](#action-e)ACTION E

Add Entity Schema

After creating the feature module and components, the next step is to define the entity schema in the **OpenAPI** file. This involves adding the base properties of the entity, which will be used to generate the API code for the frontend application.

### Template: Generated Entity Schema

| Directory | <root-of-ui-app>/src/assets/api |
| --------- | ------------------------------- |
| File      | openapi-bff.yaml                |

ACTION E in `openapi-bff.yaml` (excerpt) 

```yml
components:
  schemas:
    ...
    <resource/entity name>:
      type: object
      required:
        - 'id'
      properties:
        creationDate:
          $ref: '#/components/schemas/OffsetDateTime'
        creationUser:
          type: string
        modificationDate:
          $ref: '#/components/schemas/OffsetDateTime'
        modificationUser:
          type: string
        modificationCount:
          format: int32
          type: integer
        id:
          type: integer
        changeMe:
          type: string
        # "ACTION E: Add entity properties"
```

Where below **properties** the properties of the entity are listed.

---

### Example: Book Entity Schema

| Directory | bookstore/src/assets/api |
| --------- | ------------------------ |
| File      | openapi-bff.yaml         |

Example: Schema of Books in `openapi-bff.yaml` 

```yml
components:
  schemas:
    ...
    Book:
      type: object
      required:
        - 'id'
      properties:
        creationDate:
          $ref: '#/components/schemas/OffsetDateTime'
        creationUser:
          type: string
        modificationDate:
          $ref: '#/components/schemas/OffsetDateTime'
        modificationUser:
          type: string
        modificationCount:
          format: int32
          type: integer
        id:
          type: string
        bookType:
          $ref: '#/components/schemas/BookType'
        bookTitle:
          type: string
        bookAuthor:
          type: string
        bookIsbn:
          type: string
        bookPrice:
          type: number
          format: float
        bookPublisher:
          type: string
        bookPublishedDate:
          $ref: '#/components/schemas/OffsetDateTime'
    BookType:
      type: string
      enum: [ CRIME, DRAMA, FANTASY, PROSE, SCIENCE ]
```

Where properties with prefix **book** are added to the entity `Book` (replaced **changedMe**).

| |  Each time the **OpenAPI** file is changed, the API code needs to be updated to reflect these changes.To do this, run the the following command in the terminal with the root of the UI application as current working directory. |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Create API code after changing the OpenAPI file

```bash
npm run apigen
```

The result can be found in the generated API folder:  
`<root-of-ui-app>/src/app/shared/generated`.
