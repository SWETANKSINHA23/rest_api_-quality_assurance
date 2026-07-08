# REST API Quality Assurance

![Postman](https://img.shields.io/badge/tested%20with-postman-FF6C37.svg)
![Newman](https://img.shields.io/badge/cli-newman-darkgreen)
![GitHub Actions](https://img.shields.io/badge/ci%2Fcd-github%20actions-2088FF.svg)
![License](https://img.shields.io/badge/license-ISC-blue)

---

## What is this project?

This is an API testing project I built to test a public REST API called JSONPlaceholder. The idea is simple - I wanted to cover all the basic HTTP operations (GET, POST, PUT, PATCH, DELETE) with proper test assertions, handle edge cases like invalid requests, and have everything run automatically through a CI/CD pipeline without me having to trigger it manually.

The tests are written inside Postman and executed via Newman on the command line. GitHub Actions takes care of running them on every push or pull request.
