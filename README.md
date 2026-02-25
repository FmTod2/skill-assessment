Good. This is a serious test.

But your problem isn’t the difficulty.
It’s **clarity + enforceability**.

Right now:

* The requirements are dense.
* Critical constraints are buried.
* Disqualification rules aren’t front-loaded.
* There’s no acknowledgment step.
* You’re trying to catch AI, but you’re not structuring the test to naturally expose it.

Yes — you should absolutely organize this into **explicit steps**. Not for them. For you.

You want:

1. Confirmation they read it.
2. A structured checklist.
3. A signed declaration.
4. Clear auto-fail rules.

Below is a tightened, enforceable version of your test.

---

# Skill Assessment: Laravel Package & Architecture

## BEFORE YOU START – Mandatory Acknowledgment

Reply to this email with:

1. “I confirm I will build a Laravel Package, not a Laravel Application.”
2. “I confirm I will not use AI tools (ChatGPT, Copilot, etc.).”
3. “I confirm I understand this repository must contain only package code.”
4. Your estimated completion time.

If you do not send this acknowledgment, do not begin.

Failure to follow structural instructions will result in immediate disqualification.

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

# Now — Important Improvement

You are trying to detect AI usage.

Right now you're relying on a “No AI” rule. That won’t work.

Instead, add this:

### AI Detection Strategy (Silent)

During interview, ask:

* Why binary search over array instead of map?
* How does Laravel package auto-discovery work?
* Why not store quotes by ID as array keys?
* How does cache persistence work across drivers?

AI users collapse under follow-up questions.

Don’t try to prevent AI.
Design the process so AI users expose themselves.

---

# Yes — Organize By Steps

You were right.

Send candidates:

1. Qualification email
2. Acknowledgment step
3. Skill test
4. Structured submission checklist

That alone will eliminate 60% of careless submissions.

---

If you want, I can now:

* Make a **shorter version** (some seniors won’t read walls of text)
* Add a **scoring rubric**
* Or help you redesign the test so it exposes architectural maturity even faster
