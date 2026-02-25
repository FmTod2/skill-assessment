<p align="center">
    <a href="./LEAME.md">Spanish / Español</a>
</p

---

# Skill Assessment: Laravel Package & Architecture

---

## This assessment must be completed independently and without AI assistance of any kind. Any submission that appears AI-generated will be rejected without further review.

---

## Critical Submission Rules (Auto-Fail Conditions)

You will be automatically disqualified if:

* You submit a full Laravel application instead of a package
* Your repository includes unnecessary Laravel boilerplate
* You use AI tools
* The Docker environment does not run with `docker-compose up`
* The binary search is not implemented manually
* You use quote IDs as array keys instead of sequential indexes

No partial credit for ignoring constraints.

## Objective

To evaluate your ability to build a production-grade, modular Laravel package. We are looking for mastery in **package discovery**, **service orchestration**, **algorithmic efficiency**, and **infrastructure automation**.

---

# The Challenge

Develop a Laravel package that integrates with the [DummyJSON Quotes API](https://dummyjson.com/quotes). The package must provide a robust bridge for fetching, managing, and displaying quotes while maintaining strict performance and rate-limiting constraints.

## 1. Core Requirements

### A. Architectural Integrity

* **Standard Compliance:** The package must follow standard Laravel package conventions (Service Providers, Facades, Config, and Assets).
* **Isolation:** The repository must contain **only** the package source. Committing a full Laravel skeleton is an immediate disqualification.
* **External Tools:** Use of modern ecosystem tools (e.g., Saloon for API integration) is permitted if it demonstrates superior architectural choices.

### B. Rate Limiting & Resilience

* Implement a configurable rate-limiting service (limits per time window).
* The service must be **non-blocking**: if a limit is reached, it must throw a custom exception immediately rather than sleeping.
* Limit state must persist across requests using Laravel's Cache drivers.

### C. Data Management & Optimization

* **The Constraint:** To evaluate your data structure manipulation, you must store cached quotes as a **flat, index-sequential PHP array sorted by ID**.
* **The Logic:** You must implement a retrieval algorithm that utilizes the sorted nature of this array to find quotes with $O(\log n)$ time complexity.
* **Cache Management:** If a quote is missing, fetch it, merge it into the sorted structure, and persist it.

### D. Intelligent CLI

* Create a command `php artisan quotes:batch-import {count}`.
* The command must fetch the requested number of **unique** quotes.
* Unlike the service layer, the CLI **must** be resilient: catch rate-limit exceptions, wait for the window to reset, and resume until the target count is met.

## 2. Interface & Delivery

### E. Frontend Integration

* Provide a Vue.js 3 (Composition API + TypeScript) interface.
* **Features:** Paginated browsing and a "Find by ID" lookup (utilizing your optimized backend retrieval).
* **Build Pipeline:** Assets must be compiled within the package and made available to the host application via Laravel's asset publishing system.

### F. Automated Infrastructure (The "One-Command" Rule)

* Provide a `docker-compose.yml` that bootstraps a **test environment from scratch**.
* When run, the container must:
    1. Spin up a fresh Laravel instance.
    2. Mount/link your local package.
    3. Configure the environment and install dependencies.


* **Success Metric:** The evaluator runs `docker-compose up` and visits `localhost:8080` to find a fully working UI.

## 3. Quality Assurance

* **Testing:** Use **PestPHP**.
* **Coverage:** Include unit tests for your data retrieval algorithm and feature tests for the API/CLI layers (mocking external HTTP calls).

## 4. Deliverables

1. **Repository Link:** Public or accessible Git repo.
2. **README:** Documentation covering the following:
    1. Installation instructions
    2. Docker instructions
    3. Rate-limiting strategy
    4. Complexity analysis of your retrieval logic.
    5. Technical approach explanation

---

> [!CAUTION]
> **Read Carefully:** Failure to adhere to these constraints will result in immediate disqualification.
> 1. **Structure:** The repository must contain **only** the Laravel Package code. Do not commit a full Laravel Application.
> 2. **No AI:** This task must be completed entirely without AI assistants (Copilot, ChatGPT, etc.).
> 3. **Completeness:** All requirements must be functional within the provided Docker environment.

---

### Resources

- [Guidelines](https://github.com/FmTod/)
- [Questionnaire](https://forms.gle/gSqn6SE3Wa65b3bS7)

### Good luck!

<img src="https://raw.githubusercontent.com/FmTod2/skill-assessment/7ff556c2bb35948c7ee4e23667191ed05d8f88f3/assets/company.svg" width="300" alt="MyListerHub" style="padding-bottom: 2px;">
