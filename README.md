<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400"></a></p>

<p align="center"><a href="https://github.com/FmTod/">Guidelines</a></p>

<p align="center"><a href="https://forms.gle/gSqn6SE3Wa65b3bS7">Questionnaire</a></p>

<p align="center"><a href="./LEAME.md">Spanish / Español</a></p>

## Skill Assessment

The challenge is to create a Laravel package that handles fetching quotes from an external API. This will involve connecting to an API, basic package structure, exposing an API within the package, and writing tests.

The API we want you to connect to is [https://dummyjson.com/docs/quotes](https://dummyjson.com/docs/quotes). All the logic related to fetching and manipulating quotes from this API must be encapsulated within a composer package.

### Attention Programmers

Please read the following instructions carefully before beginning the skill test:

1. **Repository**:
The project must be contained in the provided repository. You will be working within the `./packages/quotes` directory.

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

## The package must have the following features

1. A facade that fetches a specified number of random quotes from the API.
2. Implement rate limiting for API requests to prevent abuse. The API should be limited to 30 requests per minute by default but should be customizable via a configuration file within the package.
3. An API route should be registered within the package to fetch a specified number of random quotes. This route should accept a `limit` query parameter.
4. An API route should be registered within the package to fetch "favorite" quotes. For the purpose of this assessment, you can simulate this functionality (e.g., by returning a predefined array or using a simple in-memory store). In a real application, this would likely involve database interaction.
5. An API route should be registered within the package to "delete" a quote from favorites. Similar to the previous point, you can simulate this. This route should accept a quote identifier.
6. All API routes registered by the package should be configurable from the main Laravel application (prefix, middleware). This should be achieved through the package's configuration file.
7. All the above features are to be tested with Feature tests located within the package's `tests` directory.

### Extra Credit

* Implement a caching mechanism for fetched quotes to reduce API calls.
* Allow users to configure the base URL of the dummyjson API through the package's configuration.
* Provide clear and concise documentation within the package's README file.

## Developer

Name: `<your name>` <br/>
Email: `<your email>`<br/>

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
