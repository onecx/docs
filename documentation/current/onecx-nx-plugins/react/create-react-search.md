# Create a React Search Page

What is a Page?

A Component is a reusable building block of the user interface in a UI Application. It encapsulates the structure, behavior, and presentation of a specific part of the UI, allowing developers to create modular and maintainable applications.  
Components can represent anything from a simple button or form field to complex data-driven views.

Search Page and Entity/Resource

The Search Page is a specific type of page that provides a user interface for searching and displaying results based on a certain entity or resource.  
The entity or resource represents the data model that the search page interacts with. Therefore, the resource is the base parameter for the generation of a React search page.

| |  This page describes the **React** search generator (react-search). For the Angular variant, see [Create a Search Component](../generator/create-search.html). |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## [](#generate-a-react-search-page)Generate a React Search Page

The current working directory must be the root of an existing OneCX React UI Application.

The generator presets the API class name to `<Resource>Api` used by the generated search page, derived from the feature name. This should correspond to the schema created in the OpenAPI file.

Create a React search page with the following command

```bash
nx generate <namespace>/react-generator:react-search <feature>
```

with:

| _<namespace>_ | The base namespace of the project where the application is part of.For the OneCX, use @onecx.                                                            |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| _<feature>_   | The name of the feature to which the generated page or component is added.Passed as the first positional argument. E.g. book for a feature named "Book". |

Next, **you will be asked** if you would like to customize the names for the generated API.

| _customizeNamingForAPI_ | Optional (interactive prompt). If you answer **Yes**, you can customize the resource and the generated API names (resource, search request and search response).If you answer **No**, the generator derives these names from the feature name (fastest path). |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

If you answer **No**, the generator derives the resource name (and the `Search<Resource>Request` / `Search<Resource>Response` names) from the feature name. This is the fastest way.  
If you answer **Yes**, you can specify a name for the resource/entity and the API request/response components. This can be helpful if you want to customize an existing API.

The generator creates a new search page within the specified feature and sets up the necessary structure and configurations.

![react generated feature book search book yes](react_generated_feature_book_search_book_yes.png) 

Figure 1\. Example: React search page for books - answering "Yes" to customize naming

### [](#generated-structure)Generated Structure

The generator creates the following files (exemplary for the **book** feature, resource **Book**):

```text
src/pages/<feature>/<resource>-search/
  <resource>-search.page.tsx        # Main search page component (BookSearchPage)
  <resource>-search.types.ts        # Search criteria, row + column definitions
  <resource>-search.page.spec.tsx   # Jest/Testing Library tests

src/components/<feature>/
  <resource>-search-header-section.component.tsx    # Search criteria input UI
  <resource>-search-results-section.component.tsx   # Results table / interactive data view

src/hooks/use<Resource>Search/
  use<Resource>Search.ts            # React Query search hook
  use<Resource>Search.spec.tsx      # Hook tests

src/components/accelerator/         # Shared UI building blocks (generated only once)
  PortalPage.tsx, PageHeader.tsx, SearchHeader.tsx,
  Content.tsx, ContentContainer.tsx, InteractiveDataView.tsx,
  usePermissions.tsx, index.ts
```

The `src/components/accelerator/` library is generated **only on the first run** of a React generator and reused by subsequent search and page generators.

### [](#key-naming-conventions)Key Naming Conventions

* `src/pages/<feature>/<resource>-search`  
Directory for the search page and its related files
* `<Resource>SearchPage`  
Name for the search page component
* `<Resource>Api`  
Name for the generated API class used by the search hook
* `use<Resource>Search`  
Name for the React Query search hook
* `<RESOURCE>_SEARCH`  
Prefix for the generated i18n translation keys

The generator also registers the page in the feature barrel `src/pages/<feature>/index.tsx`, adds the search endpoint to `src/assets/api/openapi-bff.yaml`, merges i18n templates and adds permissions to `helm/values.yaml`.

## [](#post-generation-steps)Post-Generation Steps

The next steps involve adapting the search page to your specific requirements. All parts that need to be adapted after the generation are described in the following sections.

1. [Configure Search Criteria](react-search/search-criteria.html)
2. [Configure Search Results](react-search/search-results.html)
3. [Configure Search Add-ons](react-search/search-add-ons.html)
4. [Configure Search Tests](react-search/search-tests.html)
5. [Map the API and Prepare Mock Data](react-search/mock-api.html)

All places that need to be adapted are marked with an action box like this one

```javascript
ACTION S<NUMBER>: <Short Description>
```

| |  Search in your IDE for the string **ACTION S** to quickly find all places that need to be adapted. |
| ----------------------------------------------------------------------------------------------------- |

## [](#example)Example

### [](#create-a-react-search-page)Create a React Search Page

Create a search page for books inside the **book** feature.  
Execute the following command with the **bookstore** application as current working directory.

Create a React Search Page for Books

```bash
nx generate @onecx/react-generator:react-search book
```

This command generates a new search page **book-search** within the **book** feature with the necessary structure and configurations. The generator presets the API class name to **BookApi** used by the generated search hook. This should correspond to the created schema in the OpenAPI file.

![react generated feature book search](react_generated_feature_book_search.png) 

Figure 2\. Excerpt of generated files and directories

### [](#configure-the-search)Configure the Search

The generated search page provides a basic structure for searching and displaying results based on the specified resource/entity.  
You can further configure the search criteria, search results, header actions and tests according to your specific requirements, following the [Post Generation Steps](#post-generation-steps).

### [](#start-backend-service)Start Backend Service

To have the search page working, you need a backend service running that provides the necessary API endpoints for the search functionality.  
In case you don’t have a real backend service available, you can prepare mock data and use it with the generated search page, see [Map the API and Prepare Mock Data](react-search/mock-api.html).

### [](#preview)Preview

![react generated book search component org](react_generated_book_search_component_org.png) 

Figure 3\. Search UI after integration into the application

![react generated book search component books](react_generated_book_search_component_books.png) 

Figure 4\. Search UI with adapted search and example data
