# GitHub Actions Workflows

## SonarCloud Analysis

This workflow performs automated code quality and security analysis using SonarCloud.

### Prerequisites

1. **SonarCloud Token**: Add `SONAR_TOKEN` to your repository secrets
   - Go to: Settings → Secrets and variables → Actions → New repository secret
   - Name: `SONAR_TOKEN`
   - Value: Your SonarCloud token from https://sonarcloud.io/account/security

2. **SonarCloud Project**: Ensure your project is set up on SonarCloud
   - Organization: `sonar-brettmiller`
   - Project Key: `hackathon-starter`

### Workflow Triggers

- **Push**: Runs on push to `master` branch
- **Pull Request**: Runs on PR open, synchronize, or reopen events

### Features

- ✅ Code quality analysis
- ✅ Security vulnerability detection
- ✅ Test coverage reporting (using c8)
- ✅ Quality gate enforcement
- ✅ Dependency caching for faster builds
- ✅ Pull request decoration

### Test Coverage

The workflow runs tests with coverage using c8. Ensure your tests are properly configured in package.json:

```json
{
  "scripts": {
    "test": "mocha test/**/*.test.js",
    "test:coverage": "c8 --reporter=lcov --reporter=text npm test"
  }
}
```

### Quality Gate

The workflow includes a quality gate check that will fail if:
- Code coverage drops below threshold
- New bugs or vulnerabilities are introduced
- Code smells exceed acceptable levels
- Security hotspots are detected

The quality gate is set to `continue-on-error: true` to avoid blocking PRs, but results will be visible in the SonarCloud dashboard.

### Troubleshooting

- **Missing SONAR_TOKEN**: Add the token to repository secrets
- **Coverage not appearing**: Ensure tests run successfully and generate lcov.info
- **Quality gate timeout**: Increase `timeout-minutes` in the workflow
- **Node version issues**: Update node-version in workflow to match your requirements