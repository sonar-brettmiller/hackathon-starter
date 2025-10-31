# GitHub Actions Workflows

## SonarCloud Analysis

This workflow performs automated code quality analysis using SonarCloud.

### Setup Instructions

1. **Add SONAR_TOKEN Secret**:
   - Go to your SonarCloud account (https://sonarcloud.io)
   - Navigate to My Account > Security > Generate Tokens
   - Generate a new token with a descriptive name (e.g., "hackathon-starter-github-actions")
   - Copy the token value
   - Go to your GitHub repository Settings > Secrets and variables > Actions
   - Click "New repository secret"
   - Name: `SONAR_TOKEN`
   - Value: Paste the token from SonarCloud
   - Click "Add secret"

2. **Configure SonarCloud Project**:
   - Go to SonarCloud and import your GitHub repository
   - Set the organization to: `sonar-brettmiller`
   - Set the project key to: `hackathon-starter`
   - Disable automatic analysis (we use GitHub Actions instead)

3. **Verify Test Coverage**:
   - Ensure your `package.json` includes the test script with c8 coverage:
     ```json
     "test": "c8 --reporter=lcov --reporter=text mocha test --exit"
     ```
   - The coverage report will be generated at `tmp/coverage/lcov.info`

4. **Trigger Workflow**:
   - Push changes to `main` or `develop` branches
   - Create a pull request targeting these branches
   - The workflow will run automatically

### Workflow Features

- **Automatic Triggers**: Runs on push and pull requests to main/develop branches
- **Node.js Setup**: Uses Node.js 22.16.0 as specified in project requirements
- **Dependency Caching**: Caches npm dependencies for faster builds
- **Test Execution**: Runs tests with coverage collection using c8
- **Code Analysis**: Performs comprehensive code quality analysis with SonarCloud
- **Quality Gate**: Validates code against configured quality standards

### Troubleshooting

- **Missing SONAR_TOKEN**: Ensure the secret is properly configured in GitHub repository settings
- **Coverage not appearing**: Verify test script generates lcov.info in tmp/coverage directory
- **Quality Gate failures**: Review SonarCloud dashboard for specific issues
- **Node.js version mismatch**: Workflow uses Node.js 22.16.0 as specified