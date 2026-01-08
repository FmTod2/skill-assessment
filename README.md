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

# Skill Assessment: Laravel Package & Architecture

## Objective

To assess your ability to design a modular, scalable Laravel package. We are looking for **clean architecture**, **ecosystem familiarity**, **algorithmic problem solving**, and **infrastructure automation**.

## The Task

Develop a Laravel package that interacts with the `https://dummyjson.com/quotes` API. The package must serve as a bridge to fetch, cache, and display quotes via a Vue.js UI, while strictly adhering to rate limits.

## Submission Constraints

> [!WARNING]
> **Read Carefully:** Failure to adhere to these constraints will result in immediate disqualification.
> 1. **Structure:** The repository must contain **only** the Laravel Package code. Do not commit a full Laravel Application.
> 2. **No AI:** This task must be completed entirely without AI assistants (Copilot, ChatGPT, etc.).
> 3. **Completeness:** All requirements must be functional within the provided Docker environment.

## Requirements

### 1. Package Architecture

* Follow standard Laravel package conventions (Service Provider, Facades, Config Publishing).
* **Bonus:** Use of modern ecosystem libraries (e.g., **Saloon** for API integrations) is permitted and encouraged.

### 2. API Service & Rate Limiting

* Create a service class to communicate with `https://dummyjson.com/quotes`.
* **Configuration:** Users must be able to define the `base_url`, `request_limit` (e.g., 5), and `time_window` (e.g., 30 seconds) via a published config file.
* **Constraint:** The Service **must not** sleep/wait. If the rate limit is exceeded, it must throw a custom `RateLimitExceededException`.
* **Persistence:** Use a cache driver to store hit counts so limits persist across requests.

### 3. Caching & Algorithmic Constraint

* **Constraint:** You must implement a custom caching strategy for `getQuote(int $id)`.
* **Storage:** Store fetched quotes in the cache as a **flat, numerically indexed array** sorted by ID (e.g., `[{id: 1...}, {id: 5...}]`). Do **not** use the ID as the array key.
* **Retrieval:** When `getQuote($id)` is called:
    1. Retrieve the full list from the cache.
    2. **Implement a Binary Search algorithm** to find the quote with the matching ID.
    3. If found, return it.
    4. If not found, fetch from API, re-sort the list, update the cache, and return.


* *Note: We are aware this is not the most efficient PHP strategy. We are testing your ability to implement algorithms and manipulate data structures.*

### 4. Smart Import Command (Problem Solving)

* Create a command: `php artisan quotes:batch-import {count}`.
* **Goal:** Fetch `{count}` *unique* quotes and store them in the cache.
* **Logic:**
    * The command must catch the `RateLimitExceededException` from your service and **sleep/wait** until the window resets, then retry automatically.
    * It must ensure uniqueness (discard duplicates found in the API that already exist in cache).
    * Provide real-time terminal feedback (e.g., "Fetched 5/20... Limit hit, waiting 30s...").



### 5. Vue.js User Interface

* Build a UI using **Vue.js (Composition API + TypeScript)**.
* **Features:**
    * View all quotes (Paginated).
    * View a single quote by ID (must use the backend Binary Search logic).


* **Integration:**
* Register a web route (e.g., `/quotes-ui`) in the package to serve the SPA.
* Configure Vite to build assets into a `dist/` folder within the package.
* Ensure assets can be published to a host app via `vendor:publish`.



### 6. Infrastructure (Docker)

* **Requirement:** The repository must be clean (package files only), but you must provide a `docker-compose.yml` (and `Dockerfile`) that builds a functional test environment.
* **The Build Process:**
    * The container should automatically install a fresh Laravel application.
    * It should copy your package code into the container.
    * It should link/install the package into the fresh Laravel app (e.g., using Composer `path` repositories).


* **Goal:** The evaluator should be able to clone your repo, run `docker-compose up`, visit `localhost:8080/quotes-ui`, and see the working application without manual installation steps.

### 7. Testing

* **Unit Tests:** Test the Binary Search algorithm in isolation.
* **Feature Tests:** Test the API endpoints and the Console Command (mocking the API to simulate rate limits).
* **Tool:** Tests must be written using **PestPHP**.

## Deliverables

1. Public Git Repository Link.
2. `README.md` with:
* Installation guide.
* Explanation of your Rate Limiting strategy.
* Instructions to run the Docker environment.

Good luck!
