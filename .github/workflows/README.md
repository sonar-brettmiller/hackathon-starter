# GitHub Actions Workflows

## SonarCloud Analysis

This workflow performs automated code quality and security analysis using SonarCloud.

### Setup Instructions

1. **Create SonarCloud Token**
   - Go to https://sonarcloud.io/account/security/
   - Generate a new token
   - Copy the token value

2. **Configure GitHub Secret**
   - Go to your repository Settings → Secrets and variables → Actions
   - Click "New repository secret"
   - Name: `SONAR_TOKEN`
   - Value: Paste your SonarCloud token
   - Click "Add secret"

3. **Import Project to SonarCloud**
   - Go to https://sonarcloud.io/projects/create
   - Select your organization: `sonar-brettmiller`
   - Import this repository: `hackathon-starter`
   - Follow the setup wizard

4. **Update Test Coverage Configuration**
   - Ensure your `package.json` test script includes coverage generation
   - Recommended configuration:
   ```json
   "scripts": {
     "test": "c8 --reporter=lcov --reporter=text mocha test/**/*.test.js"
   }
   ```

5. **Trigger First Analysis**
   - Push a commit to `main` or `develop` branch
   - Or create a pull request
   - The workflow will run automatically

### Workflow Features

- **Automatic Triggers**: Runs on push to main/develop and on pull requests
- **Node.js Setup**: Uses Node.js 22.16.0 with npm caching
- **Test Execution**: Runs tests with coverage collection
- **Code Analysis**: Analyzes JavaScript and CSS code
- **Quality Gate**: Validates code meets quality standards
- **PR Decoration**: Adds analysis results as PR comments

### Troubleshooting

- **Coverage not detected**: Verify `coverage/lcov.info` file is generated after tests
- **Quality Gate fails**: Check SonarCloud dashboard for specific issues
- **Token issues**: Ensure `SONAR_TOKEN` secret is correctly configured
- **Node version mismatch**: Workflow uses Node.js 22.16.0 as specified in repository context

### Additional Resources

- [SonarCloud Documentation](https://docs.sonarcloud.io/)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Project Dashboard](https://sonarcloud.io/project/overview?id=hackathon-starter)