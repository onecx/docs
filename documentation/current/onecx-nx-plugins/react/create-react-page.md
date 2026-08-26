# Create a React Page

What is a Page?

A Component is a reusable building block of the user interface in a UI Application. It encapsulates the structure, behavior, and presentation of a specific part of the UI, allowing developers to create modular and maintainable applications.  
Components can represent anything from a simple button or form field to complex data-driven views.

Empty Page

The React page generator creates a minimal, ready-to-use page with a header and a content area. It is the right starting point for utility pages such as settings, about or dashboard pages that do not need search or API integration.

| |  This page describes the **React** page generator (react-page). For a data-driven search page, see [Create a React Search Page](create-react-search.html). |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------ |

## [](#generate-a-react-page)Generate a React Page

The current working directory must be the root of an existing OneCX React UI Application.

Create a React page with the following command

```bash
nx generate <namespace>/react-generator:react-page <feature>
```

with:

| _<namespace>_ | The base namespace of the project where the application is part of.For the OneCX, use @onecx.                                                            |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| _<feature>_   | The name of the feature to which the generated page or component is added.Passed as the first positional argument. E.g. book for a feature named "Book". |

Next, **you will be asked** for the page name and the page title.

| _pageName_      | The name of the page to generate.E.g. Book results in a BookPage component. Defaults to Page.                                                       |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| _pageTitle_     | The title rendered inside the generated page.E.g. Books. Defaults to Page Title.                                                                    |
| _\--standalone_ | Optional. If set, the generated page is not gated on a permission.Use this for standalone apps that do not run inside the OneCX permission context. |

The generator creates the page, registers it in the feature and adds a route, so it is reachable immediately.

### [](#generated-structure)Generated Structure

The generator creates the following files (exemplary for the **book** feature, page **Book**):

```text
src/pages/<feature>/<page>/
  <page>.page.tsx        # Page component (BookPage)
  <page>.page.test.tsx   # Jest/Testing Library tests

src/components/accelerator/   # Shared UI building blocks (generated only if not present)
```

In addition the generator:

* registers the page in the feature barrel `src/pages/<feature>/index.tsx`,
* adds a route for the page to `src/router.tsx`,
* merges the i18n templates (`HEADER`, `SUB_HEADER`, `ARIA_LABEL`) into the translation files,
* adds the `<PAGE>#VIEW` permission to `helm/values.yaml`.

### [](#key-naming-conventions)Key Naming Conventions

* `src/pages/<feature>/<page>`  
Directory for the page and its related files
* `<Page>Page`  
Name for the page component
* `<PAGE>`  
Prefix for the generated i18n translation keys

The generated page is gated on the `<PAGE>#VIEW` permission. Generate with `--standalone` to skip permission gating for standalone apps.

## [](#post-generation-steps)Post-Generation Steps

The page is intentionally minimal and contains **no `ACTION` markers**. Only a few light adjustments are typically needed:

1. Replace the three translation placeholders (`HEADER`, `SUB_HEADER`, `ARIA_LABEL`), which are generated as `ACTION: ADD TRANSLATION`.
2. Add your page content inside the `<Content>` area of `<page>.page.tsx`.
3. Ensure the `<PAGE>#VIEW` permission exists in your auth system (or use `--standalone`).

| Directory | src/pages/<feature>/<page> |
| --------- | -------------------------- |
| File      | <page>.page.tsx            |

Generated page component (excerpt) 

```tsx
export const <Page>Page: FC = () => {
  const { t } = useTranslation();

  return (
    <PortalPage
      permission="<PAGE>#VIEW"
      ariaLabel={t('<PAGE>.ARIA_LABEL')}
    >
      <PageHeader
        header={t('<PAGE>.HEADER')}
        subheader={t('<PAGE>.SUB_HEADER')}
      />

      <Content>
        <h1 className="m-0 p-0 text-xl font-bold"><page title></h1>
      </Content>
    </PortalPage>
  );
};
```

Add your page content inside the `<Content>` element.

## [](#example)Example

Create a **book** page inside the **book** feature, with the title "Books".  
Execute the following command with the **bookstore** application as current working directory.

Create a React Page for Books

```bash
nx generate @onecx/react-generator:react-page book
```

When prompted, enter `Book` as the page name and `Books` as the page title. The generator creates `BookPage` under `src/pages/book/book`, registers it and adds a route.

![react generated book page](react_generated_book_page.png) 

Figure 1\. Generated React page after integration into the application
