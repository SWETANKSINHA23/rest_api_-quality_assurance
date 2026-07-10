# REST API Quality Assurance

![Postman](https://img.shields.io/badge/tested%20with-postman-FF6C37.svg)
![Newman](https://img.shields.io/badge/cli-newman-darkgreen)
![GitHub Actions](https://img.shields.io/badge/ci%2Fcd-github%20actions-2088FF.svg)
![License](https://img.shields.io/badge/license-ISC-blue)

---

## What is this project?

This is an API testing project I built to test a public REST API called JSONPlaceholder. The idea is simple - I wanted to cover all the basic HTTP operations (GET, POST, PUT, PATCH, DELETE) with proper test assertions, handle edge cases like invalid requests, and have everything run automatically through a CI/CD pipeline without me having to trigger it manually.

The tests are written inside Postman and executed via Newman on the command line. GitHub Actions takes care of running them on every push or pull request.

---

## What does it test?

The API under test is [JSONPlaceholder](https://jsonplaceholder.typicode.com) - a free fake REST API commonly used for testing. I'm hitting the `/users` endpoint across 7 test cases:

| Method | Endpoint    | What it checks                                 | Expected Status |
| ------ | ----------- | ---------------------------------------------- | --------------- |
| GET    | /users/1    | Fetches a single user                          | 200             |
| GET    | /users      | Fetches all users, checks array is not empty   | 200             |
| GET    | /users/9999 | Handles non-existent user gracefully           | 404             |
| POST   | /users      | Creates a user, validates response body        | 201             |
| PUT    | /users/1    | Full update, checks updated name in response   | 200             |
| PATCH  | /users/1    | Partial update, checks updated job in response | 200             |
| DELETE | /users/1    | Deletes user, checks response is empty         | 200             |

---

## Key things I have covered

- Status code validation on every single request
- Response body validation - checking fields exist and have the right values
- Negative testing - what happens when you request something that does not exist
- Request chaining - the POST request saves the created user's ID into an environment variable so it can be reused in follow-up requests
- Auto-generated HTML test report after every run

---

## Tech Stack

- Postman - for writing and designing the test cases
- Newman - to run the Postman collection from the command line
- newman-reporter-htmlextra - generates a clean HTML report
- GitHub Actions - automates the whole test run on every push

---

## How to run it locally

Make sure you have Node.js 20+ installed, then:

```bash
git clone https://github.com/SWETANKSINHA23/rest_api_-quality_assurance
cd rest_api_-quality_assurance
npm install
npx newman run collections/api-tests.postman_collection.json --reporters cli,htmlextra --reporter-htmlextra-export reports/report.html
```

After the run, open `reports/report.html` in your browser to see the full test report with pass/fail counts, response times, and assertion details.

---

## CI/CD

Every push and pull request automatically triggers the test suite via GitHub Actions. The workflow installs dependencies, runs Newman, and uploads the HTML report as a downloadable artifact. You can check the results under the Actions tab in the repository.

Workflow config: `.github/workflows/api-tests.yml`
