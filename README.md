<p align="center">
    <a href="https://mylisterhub.com" target="_blank">
        <img src="https://raw.githubusercontent.com/FmTod2/skill-assessment/7ff556c2bb35948c7ee4e23667191ed05d8f88f3/assets/logo.svg" width="75" alt="Logo" style="padding-right: 5px;">
        <img src="https://raw.githubusercontent.com/FmTod2/skill-assessment/7ff556c2bb35948c7ee4e23667191ed05d8f88f3/assets/company.svg" width="400" alt="MyListerHub" style="padding-bottom: 2px;">
    </a>
</p>

<p align="center">
    <a href="https://github.com/FmTod/">Guidelines</a>
</p>

<p align="center">
    <a href="https://forms.gle/gSqn6SE3Wa65b3bS7">Questionnaire</a>
</p>

<p align="center">
    <a href="./LEAME.md">Spanish / Español</a>
</p>

# Skill Assessment

Quotes API Interaction Package with Rate Limiting, Caching, and Vue.js UI

## Objective

To assess your ability to design, develop, test, and document a comprehensive Laravel package that consumes quote data from the `https://dummyjson.com/quotes` API, implements request rate limiting, utilizes local caching with efficient retrieval using binary search, and provides a pre-built, publishable UI built with Vue.js for interacting with the API.

## Task

Develop a Laravel package that simplifies interaction with the `https://dummyjson.com/quotes` public API. The package should include API interaction, rate limiting, caching, and a user interface built with Vue.js for displaying quotes. The UI's build artifacts should be publishable for customization.

**Time Allotment:** 8 - 12 hours

## Deliverables

* A Git repository link containing the complete Laravel package code.
* A `README.md` file in the package root directory with clear instructions for installation, configuration, basic usage, rate limiting, caching, and accessing/publishing the Vue.js UI.

## Requirements

1. **Package Structure:**
    * Follow standard Laravel package development conventions.
    * Include a service provider to register the package's functionality, routes, and publishable assets.
    * Include the necessary directory structure for your Vue.js application (e.g., `resources/js`, `resources/views`).

2. **API Client Service:**
    * Create a service within the package that handles the communication with the `https://dummyjson.com/quotes` API using Laravel's HTTP client.
    * This service should incorporate request rate limiting logic and local caching with binary search.

3. **Configuration:**
    * Provide a configuration file for the package (e.g., `config/quotes.php`).
    * The configuration file should allow users to define:
        * The base URL of the API (default to `https://dummyjson.com`).
        * The maximum number of requests allowed per time window (e.g., per minute).
        * The duration of the time window in seconds (e.g., 60 for one minute).

4. **API Interaction Methods:**
    * `getAllQuotes()`: Fetches all quotes from the `/quotes` endpoint.
    * `getRandomQuote()`: Fetches a single random quote from the `/quotes/random` endpoint.
    * `getQuote(int $id)`: Fetches a specific quote by its ID from the `/quotes/{id}` endpoint. This method should first check the local cache using binary search.

5. **Rate Limiting Implementation:**
    * Implement a mechanism to track the number of requests made to the API within the configured time window.
    * If the limit is exceeded, pause execution for a short period until the window resets and then retry the request.

6. **Local Caching with Efficient Retrieval:**
    * Implement a local caching mechanism (e.g., an array) to store fetched quotes.
    * The `getQuote(int $id)` method should first check this cache.
    * **If the quote with the given ID is found in the cache, retrieve it using binary search (assuming the cached data is sorted by ID) and return it without making an API call.**
    * If the quote is not in the cache, make an API call, store the fetched quote in the cache (ensuring the cache remains sorted by ID for binary search), and then return it.

7. **Vue.js User Interface:**
    * Build a user interface using Vue.js within your package. This UI should allow users to:
        * View all quotes (potentially with pagination).
        * View a random quote.
        * View a specific quote by ID.
    * This UI should make API requests to your package's backend to fetch the data.

8. **Package API Routes:**
    * Define API routes within your package (registered via the service provider, likely under a `/api/quotes` prefix) that your Vue.js application can consume. These routes should:
        * `/api/quotes`: Return all quotes.
        * `/api/quotes/random`: Return a random quote.
        * `/api/quotes/{id}`: Return a specific quote by ID.
    * Create controller(s) within your package to handle these API routes and interact with your API client service.

9. **Serving the Vue.js Application:**
    * Define a route in your package (e.g., `/quotes-ui`) that serves the main entry point of your Vue.js application. You will need to configure Vite within your package to build the Vue.js application into static assets.

10. **Publishable Assets:**
    * Configure your package's service provider to make the built Vue.js application assets (e.g., the `dist` folder containing JavaScript and CSS) publishable to the main Laravel application using the `php artisan vendor:publish`. The published assets should reside in a logical directory within the main application's `public` directory (e.g., `public/vendor/your-package-name`).

11. **Usage:**
    * Include instructions on how to install the package, configure it, and **how to access the pre-built Vue.js UI (the defined route, e.g., `/quotes-ui`).**
    * Provide clear instructions on **how to publish the Vue.js UI assets** if a developer wants to customize the frontend. Include steps on where the assets are published and how they can be modified.

12. **Testing:**
    * Include unit tests for the API client service.
    * Include basic feature tests for your package's API routes to ensure they return the correct data.

13. **Documentation:**
    * The `README.md` should include comprehensive documentation for all features, including clear instructions on accessing and publishing the Vue.js UI and any necessary build steps (e.g., running `npm install` and `npm run build` within the package's UI directory).

## Submission Instructions

1. Create a new private repository on a platform like GitHub, GitLab, or Bitbucket.
2. Develop the Laravel package according to the requirements outlined above.
3. Ensure all tests pass and the documentation is complete.
4. Grant access to your repository to the designated evaluator(s).
5. Submit the repository link to the designated evaluator(s).

Good luck!
