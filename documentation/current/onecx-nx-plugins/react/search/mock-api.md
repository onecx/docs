# Map the API and Prepare Mock Data

The React search page fetches its data through a generated `<Resource>Api`, called from the `use<Resource>Search` hook. This page describes how to map the search criteria to the API request, how the search endpoint is defined in the OpenAPI file, and how to provide mock data while no real backend is available.

## [](#action-s2)ACTION S2 - Map criteria to the search request

The hook contains a colocated query function that calls the generated API service. Adjust the mapping so that the criteria object matches the generated `Search<Resource>Request`.

| Directory | src/hooks/use<Resource>Search |
| --------- | ----------------------------- |
| File      | use<Resource>Search.ts        |

ACTION S2 in `use<Resource>Search.ts` 

```typescript
const fetch<Resource>SearchResults = async (
  <resource>Service: <Resource>Api,
  criteria: <Resource>SearchCriteria
): Promise<<Resource>SearchRow[]> => {
  // ACTION S2: map the criteria to the generated search request
  const response = await <resource>Service.search<Resource>Items({
    ...criteria,
    pageNumber: 0,
    pageSize: 100,
  } as any);
  return ((response.data as any).stream ?? []) as <Resource>SearchRow[];
};
```

Replace the spread `...criteria` with an explicit mapping to the fields of your `Search<Resource>Request`, and remove the `as any` casts once the request type matches.

## [](#generated-openapi-endpoint)Generated OpenAPI Endpoint

During generation, a search endpoint is added to the BFF OpenAPI specification. Adapt the request/response schemas to your entity, then regenerate the typed API client.

| Directory | src/assets/api   |
| --------- | ---------------- |
| File      | openapi-bff.yaml |

Generated search endpoint (excerpt) 

```yaml
  /<resource>s/search:
    post:
      operationId: search<Resource>Items
      requestBody:
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Search<Resource>Request'
      responses:
        '200':
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Search<Resource>Response'
```

Add your entity properties to the `Search<Resource>Request` (criteria) and to the `<Resource>` schema (result row).

| |  After adjusting the OpenAPI specification, regenerate the typed API client so the changes are reflected in <Resource>Api. |
| ---------------------------------------------------------------------------------------------------------------------------- |

Generate the API client code

```bash
npm run apigen
```

## [](#mock-server-with-node-js)Mock Server with Node.js

While no real backend is available, you can provide simulated data with a small [Node.js](https://nodejs.org/en) server. This example assumes an entity called "**Book**" and serves data on the `/books/search` endpoint. Save the file e.g. as `bookstore-mock-server.js`.

Simulated data example via node mock server 

```javascript
const bodyParser = require("body-parser");
const express = require("express");
const { v4 } = require("uuid");
const app = express();
app.use(express.json());
const data = {
  books: [],
};
const bookTypes = ["CRIME", "DRAMA", "FANTASY", "PROSE", "SCIENCE"];
const apiNames = ["books"];

const generateBooks = (count) => {
  let results = [];
  for (let i = 0; i < count; i++) {
    results.push({
      creationDate: "2024-04-12T06:08:27.806Z",
      creationUser: "anonymous",
      modificationDate: "2024-04-12T06:08:40.312Z",
      modificationUser: "anonymous",
      modificationCount: "0",
      id: i,
      bookTitle: "Big Bang and Black Holes - " + i,
      bookType: bookTypes[i % bookTypes.length],
      bookAuthor: "Stephan Hawking",
      bookIsbn: "978-3-99-123456-" + i,
      bookPrice: "12,80",
      bookPublisher: 'World Scientific',
      bookPublishedDate: new Date(Date.now() + 2 * 24 * 60 * 60 * 1000).toISOString()
    });
  }
  data.books = results;
  return { number: 0, size: 100, totalElements: results.length, totalPages: 1, stream: results };
};

// Book Endpoints
app.post("/books/search", (req, res) => {
  const bookTitle = req.body.bookTitle;

  res.send(
    generateBooks(23)
  );
});


app.get(`/books/:id`, (req, res) => {
  res.send({
    resource: {
      creationDate: "2026-02-12T05:08:08.080Z",
      creationUser: "anonymous",
      modificationDate: "2026-02-12T05:18:18.888Z",
      modificationUser: "anonymous",
      modificationCount: "0",
      id: req.params.id,
      bookTitle: "Big Bang and Black Holes - " + req.params.id,
      bookType: bookTypes[req.params.id % bookTypes.length],
      bookAuthor: "Stephan Hawking",
      bookIsbn: "978-3-99-123456-" + req.params.id,
      bookPrice: "12,80",
      bookPublisher: 'World Scientific',
      bookPublishedDate: "1993-02-12T05:08:08.080Z",
    },
  });
});

// Generic Endpoints
for (const apiname of apiNames) {
  app.post(`/${apiname}/search`, (req, res) => {
    res.send({
      results: data[apiname],
      totalNumberOfResults: data[apiname].length,
    });
  });

  app.delete(`/${apiname}/:id`, (req, res) => {
    data[apiname] = data[apiname].filter((i) => i.id != req.params.id);
    res.status(204).send("Item deleted");
  });

  app.post(`/${apiname}/`, (req, res) => {
    let item = {
      id: v4(),
      ...req.body.resource,
    };
    data[apiname] = [...data[apiname], item];
    res.send({ resource: item });
  });

  app.put(`/${apiname}/:id`, (req, res) => {
    console.log(`data[${apiname}] length: `, data[apiname].length);
    console.log('req.params.id: ', req.params.id);

    let item = data[apiname].find((i) => i.id == req.params.id);

    if(!item) {
      res.status(404).send("Item not found");
      return;
    }
    console.log('current item: ', item);
    console.log('request item: ', req.body.resource);

    // update item
    item = {
      ...item,
      ...req.body.resource,
      ...{ modificationCount: (parseInt(item.modificationCount) + 1).toString() },
    };

    data[apiname] = data[apiname].map((_item) => {
      if (_item.id == item.id) {
        return item;
      } else {
        return _item;
      }
    });

    res.send({ resource: item });
  });

  app.get(`/${apiname}/:id`, (req, res) => {
    const result = {
      resource: data[apiname].find((i) => i.id == req.params.id),
    };
    res.send(result);
  });
}

app.listen(3000, () => console.log("Bookstore app is listening on port 3000."));
```

Start the server with the following command

```bash
node bookstore-mock-server.js
```

The server starts and listens for incoming requests on port 3000.

![react mock server running](react_mock_server_running.png) 

Figure 1\. Example output when the server is running and a request is made to the search endpoint

## [](#using-the-mock-api)Using the Mock API

Point your application’s BFF base URL to the mock server (e.g. `http://localhost:3000`) instead of the real backend, so the generated `<Resource>Api` calls the mock endpoints. Adjust the configured BFF/proxy target of your React UI app accordingly.
