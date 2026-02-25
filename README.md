<p align="center">
    <a href="./LEAME.md">Spanish / Español</a>
</p

---

# Skill Assessment: Laravel Package & Architecture

---

## This assessment must be completed independently and without AI assistance of any kind. Any submission that appears AI-generated will be rejected without further review.

---

# Objective

We are evaluating:

* Package architecture discipline
* Laravel ecosystem fluency
* Algorithm implementation ability
* Infrastructure automation
* Attention to detail

This is not a CRUD exercise.

---

# Critical Submission Rules (Auto-Fail Conditions)

You will be automatically disqualified if:

* You submit a full Laravel application instead of a package
* Your repository includes unnecessary Laravel boilerplate
* You use AI tools
* The Docker environment does not run with `docker-compose up`
* The binary search is not implemented manually
* You use quote IDs as array keys instead of sequential indexes

No partial credit for ignoring constraints.

---

# The Task

Build a Laravel Package that integrates with:

[https://dummyjson.com/quotes](https://dummyjson.com/quotes)

The package must:

* Fetch quotes
* Cache them
* Enforce rate limits
* Provide a Vue.js UI
* Be runnable via Docker without manual setup

---

# Step 1 – Package Architecture

Follow Laravel package standards:

* Service Provider
* Facade
* Config publishing
* Route registration inside the package
* Vendor publishing support

Bonus: Saloon or other modern ecosystem tools allowed.

Repository must contain:

* src/
* config/
* routes/
* resources/
* tests/
* docker-compose.yml
* Dockerfile

No Laravel application structure allowed.

---

# Step 2 – API Service & Rate Limiting

Create a service that:

* Allows configuration of:

  * base_url
  * request_limit
  * time_window

If the rate limit is exceeded:

* Throw RateLimitExceededException
* Do NOT sleep/wait

Rate limit persistence must use Laravel cache.

The service must never block execution.

---

# Step 3 – Algorithm Requirement (Binary Search)

You must implement:

getQuote(int $id)

Storage Requirements:

* Cached as flat PHP array
* Sequential integer keys only (0,1,2…)
* Sorted by quote id
* Do NOT use quote ID as array key

Retrieval Logic:

1. Load entire array
2. Perform manual Binary Search
3. If found → return
4. If not found:

   * Fetch from API
   * Insert into array
   * Re-sort
   * Update cache
   * Return result

Using collection helpers instead of binary search = fail.

We are evaluating algorithm discipline.

---

# Step 4 – Console Command

Command:
php artisan quotes:batch-import {count}

Requirements:

* Must retry automatically if rate limit hit
* Must sleep only inside the command layer
* Must ensure uniqueness by ID
* Must provide real-time CLI feedback

This tests exception handling + control flow logic.

---

# Step 5 – Vue.js UI

Requirements:

* Vue 3
* Composition API
* TypeScript

Features:

* Paginated list
* Single quote by ID (must call backend binary search)

Integration:

* Route registered by package
* Vite builds to /dist inside package
* Assets publishable via vendor:publish

No external SPA scaffold allowed.

---

# Step 6 – Docker

The evaluator must be able to:

git clone
docker-compose up
Visit localhost:8080/quotes-ui

The container must:

1. Install fresh Laravel app
2. Install your package via composer path repo
3. Run migrations if needed
4. Be fully functional

No manual steps allowed.

If Docker does not work → fail.

---

# Step 7 – Testing

Use PestPHP.

Required:

Unit Test:

* Binary Search in isolation

Feature Tests:

* API endpoints
* Console command
* Rate limit simulation via mocking

phpunit.xml must include:
TEST_MODE=interactive

If missing → fail.

---

# Deliverables

Public GitHub repository.

README must include:

* Installation
* Docker instructions
* Rate limiting explanation
* “Development Process” section explaining architectural decisions

---

> [!WARNING]
> **Read Carefully:** Failure to adhere to these constraints will result in immediate disqualification.
> 1. **Structure:** The repository must contain **only** the Laravel Package code. Do not commit a full Laravel Application.
> 2. **No AI:** This task must be completed entirely without AI assistants (Copilot, ChatGPT, etc.).
> 3. **Completeness:** All requirements must be functional within the provided Docker environment.

---

# Reasorces

<a href="https://github.com/FmTod/">Guidelines</a>
<a href="https://forms.gle/gSqn6SE3Wa65b3bS7">Questionnaire</a>

---

# Good luck!


<img src="https://raw.githubusercontent.com/FmTod2/skill-assessment/7ff556c2bb35948c7ee4e23667191ed05d8f88f3/assets/company.svg" width="300" alt="MyListerHub" style="padding-bottom: 2px;">


