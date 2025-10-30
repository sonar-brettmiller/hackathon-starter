# SonarCloud Integration

This directory contains the GitHub Actions workflow for SonarCloud code quality analysis.

## Setup Instructions

### 1. Configure SonarCloud Token

You must add the `SONAR_TOKEN` secret to your GitHub repository:

1. Go to [SonarCloud](https://sonarcloud.io)
2. Navigate to your account settings → Security
3. Generate a new token
4. Go to your GitHub repository → Settings → Secrets and variables → Actions
5. Click "New repository secret"
6. Name: `SONAR_TOKEN`
7. Value: Paste the token from SonarCloud
8. Click "Add secret"

### 2. Verify Coverage Generation

Ensure your `package.json` includes coverage generation:

```json
{
  "scripts": {
    "test": "c8 mocha test/**/*.test.js",
    "test:coverage": "c8 --reporter=lcov --reporter=text mocha test/**/*.test.js"
  }
}
```

### 3. Trigger Analysis

The workflow runs automatically on:
- Push to `main` or `develop` branches
- Pull requests to these branches

### 4. View Results

View analysis results at: https://sonarcloud.io/project/overview?id=hackathon-starter

## Troubleshooting

- **No coverage report**: Ensure tests run successfully and generate `coverage/lcov.info`
- **Authentication errors**: Verify `SONAR_TOKEN` secret is configured correctly
- **Quality gate failures**: Review issues in SonarCloud dashboard and fix code quality issues