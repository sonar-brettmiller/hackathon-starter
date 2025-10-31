# SonarCloud Integration

This directory contains the GitHub Actions workflow for SonarCloud code quality analysis.

## Setup Instructions

### 1. Configure SonarCloud Token

1. Go to [SonarCloud Security Settings](https://sonarcloud.io/account/security/)
2. Generate a new token with a descriptive name (e.g., "hackathon-starter-github-actions")
3. Copy the generated token
4. Go to your GitHub repository Settings → Secrets and variables → Actions
5. Click "New repository secret"
6. Name: `SONAR_TOKEN`
7. Value: Paste the token from SonarCloud
8. Click "Add secret"

### 2. Update package.json Test Script (if needed)

Ensure your `package.json` test script generates coverage reports:

```json
"scripts": {
  "test": "c8 --reporter=lcov --reporter=text mocha test --exit"
}
```

### 3. Verify Coverage Output

After running tests, verify that `coverage/lcov.info` is generated:

```bash
npm test
ls -la coverage/
```

### 4. Trigger First Analysis

Commit and push the workflow file:

```bash
git add .github/workflows/sonarcloud.yml sonar-project.properties
git commit -m "Add SonarCloud integration"
git push origin main
```

### 5. Configure SonarCloud Project

1. Go to [SonarCloud](https://sonarcloud.io)
2. Navigate to your organization: `sonar-brettmiller`
3. Find project: `hackathon-starter`
4. Go to Administration → General Settings
5. Enable "Automatic Analysis" if desired
6. Configure Quality Gate settings as needed

### 6. Enable Pull Request Decoration

1. In SonarCloud project settings
2. Go to Administration → General Settings → Pull Requests
3. Ensure GitHub integration is configured
4. Pull request comments will automatically appear on PRs

### 7. Optional: Branch Protection Rules

1. Go to GitHub repository Settings → Branches
2. Add branch protection rule for `main`
3. Enable "Require status checks to pass before merging"
4. Select "SonarCloud Code Analysis" check

## Workflow Details

- **Trigger**: Runs on push to `main`/`develop` branches and all pull requests
- **Runner**: ubuntu-latest
- **Node Version**: 22.16.0
- **Coverage Tool**: c8 with LCOV format
- **Scanner**: SonarSource/sonarqube-scan-action@v6
- **Quality Gate**: Enforced with 5-minute timeout

## Troubleshooting

### Coverage Not Showing

- Verify `coverage/lcov.info` exists after test run
- Check `sonar-project.properties` has correct path: `sonar.javascript.lcov.reportPaths=coverage/lcov.info`
- Ensure test script uses c8 with lcov reporter

### Analysis Failing

- Check SONAR_TOKEN secret is configured correctly
- Verify project key and organization match SonarCloud
- Review GitHub Actions logs for specific errors

### Quality Gate Failing

- Review SonarCloud dashboard for specific issues
- Check code coverage thresholds
- Review code smells, bugs, and vulnerabilities
- Adjust Quality Gate settings in SonarCloud if needed

## Resources

- [SonarCloud Documentation](https://docs.sonarcloud.io)
- [JavaScript Analysis](https://docs.sonarcloud.io/enriching/languages/javascript/)
- [GitHub Actions Integration](https://docs.sonarcloud.io/getting-started/github/)
