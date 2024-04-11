<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400"></a></p>

<p align="center"><a href="https://github.com/FmTod/">Guidelines</a></p>

<p align="center"><a href="https://forms.gle/gSqn6SE3Wa65b3bS7">Questionnaire</a></p>

<p align="center"><a href="./LEAME.md">Spanish / Español</a></p>

# Quotes App

## Skill Assessment

The challenge will contain a few core features most applications have. These include connecting to an API, basic MVC, exposing an API, and finally, writing tests.

The API we want you to connect to is [https://dummyjson.com/docs/quotes](https://dummyjson.com/docs/quotes). All the logic related to fetching and manipulating quotes from this API should be encapsulated within a separate composer package located in `./packages/quotes`.

### Attention Programmers

Please read the following instructions carefully before beginning the skill test:

1. **Repository**:
The project must be contained in the same repository adn application, both frontend and backend.

2. **Complete All Tasks**:
Each task is crucial and must be fully completed. Partial completion will not be considered.

3. **Attention to Detail**:
Pay close attention to the specifications and requirements for each task. Accuracy and adherence to instructions are key.

4. **Quality of Work**:
We are looking for clean, efficient, and well-documented code. Quality is as important as completion.

5. **Bonus Features**:
Implementing additional features or enhancements not listed in the tasks will earn you extra points. Creativity and innovation are highly valued.

6. **Time Management**:
We do not expect all tasks to be completed in one sitting.

7. **Submission**:
Once you have completed all tasks, submit your work as instructed.

## The application must have the following features

1. User authentication and profile update page
2. A separate composer package located in `./packages/quotes` that handles all quote-related functionality:
    1. A facade that fetches a number of random quotes from the API
    2. Implement rate limiting for API requests to prevent abuse. The API should be limited to 30 requests per minutes by default but should be customizable from the main application
    3. An API route should be registered in the package to fetch a specified number of random quotes
    4. An API route should be registered in the package to fetch your favorites quotes
    5. An API route should be registered in the package to delete a quote from your favorites
    6. All API routes should be customizable from the main application (prefix, middleware, etc.)
    7. Above features are to be tested with Feature tests inside the package
3. Separate admin authentication for moderating saved user quotes and banning users
4. Frontend should be done with Vue.js and optionally Inertia.js
    1. Typescript should be used for any frontend functionality
    2. UI should be responsive
5. All API route should be secured with an user token
6. Above features are to be tested with Feature tests

### Extra Credit

* Use composition API and setup script for Vue components
* Use inertia to connect backend and frontend
* Provide a separate file with documentation

## Developer

Name: `<your name>` <br/>
Email: `<your email>`<br/>

## Instructions

### DO NOT START A NEW LARAVEL APP, USE THIS BOILERPLATE INSTEAD

### Cloning the repository

1. Create a bare clone of the repository. (This is temporary and will be removed so just do it wherever.)

    ```bash
    git clone --bare https://github.com/FmTod2/skill-assessment.git
    ```

2. Create a new repository on GitHub.

3. Mirror-push your bare clone to your new repository.<br/>_Replace &lt;username&gt; with your actual Github username in the url below._<br/>_Replace &lt;repository&gt; with the name of your new repository._

    ```shell
    cd skill-assessment-quotes.git
    git push --mirror https://github.com/<username>/<repository>.git
    ```

4. Delete the bare clone created in step 1.

    ```shell
    cd ..
    rm -rf skill-assessment-quotes.git
    ```

5. You can now clone your repository, where you are going to be working, on your machine (in my case in the code folder).

    ```shell
    cd ~/code
    git clone https://github.com/<username>/<repository>.git
    ```

## Getting Started

1. Create a copy of the `.env.example` file as `.env`

    ```bash
    cp .env.example .env
    ```

2. Install dependencies:

<details>
<summary> a. Docker (Recommended)</summary>

3. Install composer dependecies

    ```shell
    docker run --rm \
        -u "$(id -u):$(id -g)" \
        -v $(pwd):/var/www/html \
        -w /var/www/html \
        laravelsail/php81-composer:latest \
        composer install --ignore-platform-reqs
    ```

4. Start the container (Sail):

    ```shell
    ./vendor/bin/sail up -d
    ```

5. Generate a new secret key:

    ```shell
    ./vendor/bin/sail artisan key:generate
    ```

</details>

<details>
<summary>b. Without Docker (Not recommended)</summary>

3. Install all required dependencies

    ```bash
    composer install
    ```

4. Generate a new secret key:

    ```shell
    php artisan key:generate
    ```

</details>

> [!IMPORTANT]
> Docker is recommended as you have all the external dependecies needed are already present in the provided container. Without docker you may need to install some external dependencies like MySQL or some extra PHP extensions required by the project

## Your first commit (IMPORTANT)

1. Edit the README.md file and add your name and email.

    ```diff
    - Name: `<your name>` <br/>
    - Email: `<your email>` <br/>
    + Name: Jhon Doe <br/>
    + Email: jhondoe@exmaple.com <br/>
    ```

2. Submit your first commit with just the changes to the README.md file. Must be done before starting the assignment.

    ```shell
    git add README.md
    git commit -m "Initial commit"
    git push
    ```

## Executing Commands

<details>
<summary>Docker/Sail</summary>

### PHP Commands

```shell
./vendor/bin/sail php --version
 
./vendor/bin/sail php script.php
```

### Composer Commands

```shell
./vendor/bin/sail composer require laravel/sanctum
```

### Artisan Commands

```shell
./vendor/bin/sail artisan queue:work
```

### Node / NPM Commands

```shell
./vendor/bin/sail node --version
 
./vendor/bin/sail npm run dev
```

If you wish, you may use Yarn instead of NPM:

```shell
./vendor/bin/sail yarn
```

### Running Tests

```shell
./vendor/bin/sail test

./vendor/bin/sail test --group orders
```

</details>

<details>
<summary>Without Docker</summary>

### Artisan Commands

```shell
php artisan serve
php artisan list
```

### Node / NPM Commands

```shell
npm run dev
// or
npm run build
```

### Running Tests

```shell
composer test
```

</details>
