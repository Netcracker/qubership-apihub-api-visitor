# Qubership APIHUB API Visitor

The APIHUB API Visitor is designed for secure and structured processing of Open API specifications using the `Visitor` pattern. It provides type-safe traversal of complex API schemes, including detecting self-references and preventing infinite recursion.

## Features
- **Type-safe traversal:** The module provides mechanisms for safe traversal and transformation of OpenAPI documents with full TypeScript support.
- **Self-link processing:** Detects and marks self-links in schemas using the unique `valueAlreadyVisited` flag, preventing endless recursion.
- **Visitor Pattern:** Uses the visitor pattern to bypass and transform API specification elements, making it easier to analyze API structure.
- **Multiple distribution** formats: Supports CommonJS, ES modules, and integration with TypeScript projects, providing flexibility in use.

## Self loops
The APIHUB API Visitor automatically identifies and marks self-references in schemas using a reliable mechanism for detecting and processing self-reference cycles during schema traversal. The mechanism is designed to prevent infinite recursion when traversing objects that may contain circular references (direct or indirect).

## Usage
```ts
const walker = new OpenApiWalker();
const normalizedOpenApiDocument = { /* Normalized OpenAPI document */ };
walker.walkPathsOnNormalizedSource(normalizedOpenApiDocument, {
  // Handlers
  responseStart: ({ responseCode }) => {
    /* Do something */
    return true
  },
  responseEnd: () => {
    /* Do something */
  },
  mediaTypeStart: ({ mediaType }) => {
    /* Do something */
    return true
  },
  mediaTypeEnd: () => {
    /* Do something */
  },
  // Add other handlers as needed

}, { /* Options */ })
```


## Contributing
Please run the unit tests before submitting your PR: `npm test`. Hopefully your PR includes additional unit tests to illustrate your change/modification!