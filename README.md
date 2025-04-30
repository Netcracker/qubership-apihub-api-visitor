# Qubership APIHUB API Visitor
## Overview
API Visitor is designed for secure and structured processing of Open API specifications using the `Visitor` pattern. It provides type-safe traversal of complex API schemes, including detecting self-references and preventing infinite recursion.

## Features
- **Type-safe traversal:** The module provides mechanisms for safe traversal and transformation of OpenAPI documents with full TypeScript support.
- **Self-link processing:** Detects and marks self-links in schemas using the unique `valueAlreadyVisited` flag, preventing endless recursion.
- **Visitor Pattern:** Uses the visitor pattern to bypass and transform API specification elements, making it easier to analyze and modify the API structure.
- **Multiple distribution** formats: Supports CommonJS, ES modules, and integration with TypeScript projects, providing flexibility in use.

## Self loops

![](docs/img/self-loops.png)

The Visitor API automatically identifies and marks self-references in schemas using a reliable mechanism for detecting and processing self-reference cycles during schema traversal. The mechanism is designed to prevent infinite recursion when traversing objects that may contain circular references (direct or indirect), for example, in the OpenAPI specifications.

### How the work
Cycle detection is performed by tracking already visited objects using two key elements:
- The `valueAlreadyVisited` flag. Passed to the user's callbacks. Indicates that the current element has already been visited before, and therefore further traversal should be stopped.
- A set of `visitedObjects`. It is stored in the internal state of the crawler. It is used to store links to objects that have already been visited. If an object occurs repeatedly, it is considered that a cycle has been found.

### Behaviour
- Each time an object is visited, a check is performed to see if it has already been visited.
- If the object is found in `visitedObjects`, the `valueAlreadyVisited = true` flag is set.
- The user can use this flag to avoid repeated traversal and stop recursion.
- Thus, the traversal correctly handles both direct and indirect circular references.

### Usage
Cycle detection is used:
- to prevent endless crawling;
- to report cyclic dependencies in API schemas, if necessary for analysis or validation.