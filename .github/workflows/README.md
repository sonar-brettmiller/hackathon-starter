# SonarCloud Integration

This directory contains the GitHub Actions workflow for SonarCloud code quality analysis.

## Setup Instructions

### 1. Configure SonarCloud Token

1. Go to [SonarCloud](https://sonarcloud.io)
2. Navigate to your organization: `sonar-brettmiller`
3. Go to **My Account** > **Security** > **Generate Tokens**
4. Generate a new token with a descriptive name (e.g., `hackathon-starter-github-actions`)
5. Copy the generated token

### 2. Add Secret to GitHub Repository

1. Go to your GitHub repository: `https://github.com/sonar-brettmiller/hackathon-starter`
2. Navigate to **Settings** > **Secrets and variables** > **Actions**
3. Click **New repository secret**
4. Name: `SONAR_TOKEN`
5. Value: Paste the token from SonarCloud
6. Click **Add secret**

### 3. Update package.json Test Script

Ensure your `package.json` test script includes coverage generation:

```json
{
  "scripts": {
    "test": "c8 --reporter=lcov --reporter=text mocha test --exit"
  }
}
```

### 4. Trigger Initial Scan

1. Commit and push the workflow files:
   ```bash
   git add .github/workflows/sonarcloud.yml sonar-project.properties
   git commit -m "Add SonarCloud integration"
   git push origin main
   ```

2. The workflow will automatically run on push to `main`, `master`, or `develop` branches
3. It will also run on all pull requests

### 5. View Results

- Check workflow execution: `https://github.com/sonar-brettmiller/hackathon-starter/actions`
- View SonarCloud dashboard: `https://sonarcloud.io/dashboard?id=hackathon-starter`

## Workflow Features

- **Automatic Triggers**: Runs on push to main branches and all PRs
- **Node.js 22.16.0**: Matches your project's Node.js version
- **Dependency Caching**: Uses npm cache for faster builds
- **SASS Compilation**: Runs `npm run scss` before tests
- **Test Coverage**: Executes `npm test` with c8 coverage
- **Quality Gate**: Enforces quality standards with automatic checks
- **Continue on Error**: Tests continue even if some fail to ensure SonarCloud receives partial results

## Troubleshooting

### Coverage Not Showing

- Verify coverage report is generated at `tmp/coverage/lcov.info` or `coverage/lcov.info`
- Check test script includes c8 with lcov reporter
- Review SonarCloud logs in GitHub Actions for coverage parsing errors

### Quality Gate Failing

- Review quality gate settings in SonarCloud project settings
- Check for new bugs, vulnerabilities, or code smells
- Review coverage thresholds and adjust if needed

### Workflow Not Running

- Verify SONAR_TOKEN secret is properly configured
- Check workflow file syntax is valid YAML
- Ensure branch names match trigger configuration

## Configuration Files

- **`.github/workflows/sonarcloud.yml`**: GitHub Actions workflow definition
- **`sonar-project.properties`**: SonarQube scanner configuration

## Support

For issues or questions:
- SonarCloud Documentation: https://docs.sonarcloud.io/
- GitHub Actions Documentation: https://docs.github.com/en/actions