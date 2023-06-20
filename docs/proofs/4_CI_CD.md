# Continuous Integration and Continuous Development <a name="continuous-integration-and-continuous-development"></a>

---

- [Continuous Integration and Continuous Development](#continuous-integration-and-continuous-development)
  - [Intro](#intro)
  - [Design and Implement](#design-and-implement)
  - [What is Continuous Integration and Development?](#what-is-continuous-integration-and-development)
  - [What does "CI/CD" encompass in terms of learning outcomes?](#what-does-cicd-encompass-in-terms-of-learning-outcomes)
  - [My Achievements](#my-achievements)
    - [Backend Testing](#backend-testing)
    - [Pipeline Setup](#pipeline-setup)

## Intro<a name="intro"></a>

*You design and implement a (semi)automated software release process that matches the needs of the project context.*

## Design and Implement<a name="design-and-implement"></a>

*You design a release process and implement a continuous integration and deployment solution (using e.g., GitLab CI and Docker).*

## What is Continuous Integration and Development?<a name="what-is-continuous-integration-and-development"></a>

Continuous Integration (CI) is a practice in software development where code changes are regularly merged into a common repository. CI aims to automate code integration from multiple developers, ensuring a smooth merge process and avoiding conflicts. A key part of this is setting up a CI pipeline that automatically builds and tests the code whenever changes are committed to the repository. This allows early detection of issues and ensures that the codebase is always in a deployable state.

Continuous Deployment (CD) extends CI by further automating the deployment of tested and approved code changes to production environments. With CD, every successful code change that passes through the CI pipeline is automatically deployed to staging or production environments. This reduces the manual effort required for releases and enables faster, more frequent releases. CD ensures a reliable and efficient delivery of new features and bug fixes to end-users.

## What does "CI/CD" encompass in terms of learning outcomes?<a name="what-does-cicd-encompass-in-terms-of-learning-outcomes"></a>

In terms of learning outcomes, "CI/CD" entails an understanding and proficiency in implementing Continuous Integration and Continuous Deployment practices. This includes knowing how to set up CI pipelines, automate code integration and build processes, write and run automated tests. It also involves understanding CD principles, automating deployment processes, managing environments, and ensuring a smooth software release. Mastery of CI/CD learning outcomes means being able to establish efficient and reliable software delivery pipelines, improving collaboration, code quality, and the speed of software deployment and delivery to end-users.

## My Achievements<a name="my-achievements"></a>

I will detail my achievements in two areas: [Backend Testing](#backend-testing) and [Pipeline Setup](#pipeline-setup).

### Backend Testing<a name="backend-testing"></a>

For more details, visit [code quality proof](./2 Software quality.md).

### Pipeline Setup<a name="pipeline-setup"></a>

To ensure that customers/users interact with working code, frequent code testing, integration, and deployment are necessary. Automated tests are the most effective way to guarantee this.

I used GitHub Actions to create an environment that executes these tests on every commit and merge request. These pipelines not only ensure code testing but also verify proper code build, enforce code style, and statically analyze code for imperfections that may be missed by the human eye.

Below is a pipeline I used for my project:

```yaml
# .github/workflows/main.yml
name: Node.js CI

on: [push]

jobs:
  build:

    runs-on: ubuntu-latest

    strategy:
      matrix:
        node-version: [12.x]

    steps:
    - uses: actions/checkout@v2
    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v1
      with:
        node-version: ${{ matrix.node-version }}
    - name: Install dependencies
      run: npm ci
    - name: Run tests
      run: npm test
    - name: Run SonarCloud analysis
      uses: sonarsource/sonarcloud-github-action@master
      env:
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
```
