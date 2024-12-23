# GitHub Actions CI/CD Setup

## Overview

This project demonstrates how to set up a CI/CD pipeline using GitHub Actions. The pipeline includes running Cypress component tests on pull requests to the `develop` branch and deploying the application to Render when code is merged from `develop` to the `main` branch.

## Table of Contents

- [Overview](#overview)
- [User Story](#user-story)
- [Acceptance Criteria](#acceptance-criteria)
- [Project Structure](#project-structure)
- [Setup Instructions](#setup-instructions)
- [GitHub Actions Workflows](#github-actions-workflows)
  - [Cypress Tests Workflow](#cypress-tests-workflow)
  - [Deploy Workflow](#deploy-workflow)
- [Running the Application Locally](#running-the-application-locally)
- [Contributing](#contributing)
- [License](#license)

## User Story

```md
AS A developer looking to integrate a pipeline in a codebase for continuous integration and deployment, 
I WANT to create a GitHub Action that will follow best practices by running test cases when a Pull Request is made to the develop branch
SO THAT I can ensure that all code integrations are clean and pass the proper requirements.

AS A developer looking to deploy the application automatically to Render when code is merged from develop to main,
I WANT to create a GitHub Action that will run when the code is merged to main and automatically deploys to Render
SO THAT the application is constantly updated when major releases are made to the main branch.
```

## Acceptance Criteria

```md
GIVEN a fullstack application for a web developer,
WHEN I upload new features to the application
THEN I should be making Pull Requests to a develop branch first
WHEN I create a Pull Request to a develop branch
THEN I should be executing a GitHub Action that checks the Cypress component tests
WHEN I see that the tests pass on GitHub Action
THEN I should see those test results on GitHub Action and merge the code
WHEN I push the code from the develop branch to the main branch
THEN I should see that another GitHub Action triggers and should automatically deploy to Render
```

## Project Structure

```
Develop/
  .github/
    workflows/
      cypress-tests.yml
      deploy.yml
  client/
    .eslintrc.cjs
    .gitignore
    index.html
    package.json
    public/
    src/
      App.css
      App.tsx
      assets/
      components/
      main.tsx
      mocks/
      models/
      services/
    tsconfig.json
    tsconfig.node.json
    vite.config.ts
  cypress/
    component/
    fixtures/
    support/
    tsconfig.json
  cypress.config.ts
  package.json
  README.md
  server/
    .env.EXAMPLE
    package.json
    src/
    tsconfig.json
  tsconfig.json
  vite.config.ts
```

## Setup Instructions

1. **Clone the repository:**
   ```sh
   git clone https://github.com/<your-username>/<your-repo>.git
   cd <your-repo>
   ```

2. **Install dependencies:**
   ```sh
   npm install
   ```

3. **Create and switch to `develop` branch:**
   ```sh
   git checkout -b develop
   ```

4. **Push the `develop` branch to GitHub:**
   ```sh
   git push -u origin develop
   ```

5. **Set up GitHub Actions:**
   - Ensure the `.github/workflows` directory contains the `cypress-tests.yml` and `deploy.yml` files.

6. **Add secrets to GitHub:**
   - Go to your GitHub repository settings.
   - Add a new secret named `RENDER_DEPLOY_HOOK_URL` with your Render deploy hook URL.

## GitHub Actions Workflows

### Cypress Tests Workflow

This workflow runs Cypress component tests on pull requests to the `develop` branch.

```yaml
name: Cypress Tests

on:
  pull_request:
    branches:
      - develop

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '16'

      - name: Install dependencies
        run: npm install

      - name: Run Cypress tests
        run: npm run test-component
```

### Deploy Workflow

This workflow deploys the application to Render when code is merged to the `main` branch.

```yaml
name: Deploy to Render

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Deploy to Render
        run: |
          curl -X POST -H "Accept: application/json" -H "Authorization: Bearer ${{ secrets.RENDER_API_KEY }}" \
          -d '' https://api.render.com/deploy/srv-<your-service-id>
```

## Running the Application Locally

1. **Navigate to the Project Directory:**
   ```sh
   cd /c:/Users/Kimani/GitHub-Actions-CI-CD-Setup/Develop/client
   ```

2. **Install Dependencies:**
   ```sh
   npm install
   ```

3. **Start the Development Server:**
   ```sh
   npm run dev
   ```

4. **Open the Application in a Browser:**
   - Once the development server is running, open your browser and navigate to the URL provided by Vite (usually `http://localhost:3000`).
  
## contact 
Kimani 
- **Email:** kimanichambliss@gmail.com
- **GitHub:** https://github.com/ManiChams





## License

This project is licensed under the MIT License.
