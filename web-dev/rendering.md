# Rendering

## SSG

Serve pre-generated HTML files directly to the client.

### Build

Requires you to build the project first before deploying. SSG processes the content files, applies the templates, and generates static HTML files. The result is a set of static HTML files and associated assets in a designated output directory.

### Deployment

The static files can be deployed to any web server or Content Delivery Network (CDN), which serves them directly to users without the need for server-side processing.

## CSR

In CSR, the server sends a minimal HTML page to the client, along with JavaScript files. The JavaScript is then executed by the browser to fetch additional data and dynamically update the content of the web page.

### Initial Request

When a user navigates to a web page, the browser makes an initial request to the server.

The server responds with an HTML file that contains minimal content, typically just a single div element with an id where the application will be mounted, and links to JavaScript files.

### Loading JavaScript

The browser parses the HTML and makes additional requests for the linked JavaScript files. Once the JavaScript files are downloaded, the browser executes them.

### Fetching Data

The JavaScript code (often using frameworks/libraries like React, Vue, or Angular) takes over and initializes the application. It may make further requests (usually via APIs) to fetch data required to render the content.

### Rendering Content

The JavaScript code processes the fetched data and updates the DOM (Document Object Model) to display the content dynamically. This can include rendering entire pages or just updating parts of the page as needed.

### User Interaction

CSR allows for highly interactive applications. When the user interacts with the page (e.g., clicks a button, submits a form), the JavaScript can handle these events and update the content without requiring a full page reload.

### Benefits

#### Improved User Experience

Faster interactions after the initial load because updates are handled dynamically. Also can do client-side routing.

### Drawbacks of Using CSR

#### Initial Load Time

The initial load can be slower because the browser has to download and execute JavaScript before displaying the content.

#### SEO

Search engines might struggle to index content rendered by JavaScript.

## SSR

SSG but js evaluated on the server and sent to client. Need a server to handle the routes.

## Client-Side Routing

JavaScript libraries and frameworks (e.g., React Router for React, Vue Router for Vue, Angular Router for Angular) provide client-side routing capabilities, which gives a single page application feel (SPA).

These routers intercept navigation events (e.g., clicking on links) and prevent the browser from making a full page request (the default behavior) to the server. Instead, the router updates the URL and modifies the DOM to display the new view (SPA).

JavaScript frameworks use a virtual DOM (e.g., React) or efficient DOM diffing algorithms (e.g., Vue) to determine the minimal set of changes needed to update the actual DOM. This results in fast and efficient updates, minimizing reflows and repaints in the browser.
