# CI/CD Pipeline Documentation

This document explains the Continuous Integration and Continuous Deployment (CI/CD) setup for the StructuredPy project.

## Workflows

### Main Workflow (`main.yml`)

This workflow runs on every push and pull request to the main branch and includes:

1. **Testing**:
   - Runs Python tests using pytest
   - Generates coverage reports
   - Uploads coverage to Codecov

2. **Code Quality**:
   - Lints code using ruff
   - Checks formatting with black

3. **Documentation**:
   - Builds Quarto documentation
   - Deploys to GitHub Pages

### Example Tests (`test.yml`)

This workflow runs when code in the `code/` directory changes:

1. **Time Series Examples**:
   - Tests time series analysis code
   - Verifies both functional and OOP approaches

2. **Device Communication**:
   - Tests mock device communication
   - Verifies serial protocol implementation

3. **API Examples**:
   - Tests FastAPI server implementation
   - Verifies endpoints and WebSocket functionality

## Setting Up Required Secrets

1. Add these secrets to your GitHub repository:

   ```text
   CODECOV_TOKEN     # For coverage reports
   ```

2. Enable GitHub Pages:
   - Go to repository Settings
   - Navigate to Pages
   - Select gh-pages branch as source

## Local Development

To run CI checks locally:

1. **Install Dependencies**:
   ```bash
   uv venv
   source .venv/bin/activate
   uv pip install -r requirements.txt
   ```

2. **Run Tests**:
   ```bash
   pytest --cov=.
   ```

3. **Check Code Quality**:
   ```bash
   ruff check .
   black --check .
   ```

4. **Build Documentation**:
   ```bash
   quarto render
   ```

## Deployment

The documentation is automatically deployed when:
1. All tests pass
2. Code quality checks pass
3. Changes are pushed to main branch

The deployed site will be available at:
`https://[username].github.io/StructuredPy/`

## Troubleshooting

1. **Failed Tests**:
   - Check the test output in Actions tab
   - Run tests locally for more details

2. **Failed Deployment**:
   - Verify GitHub Pages is enabled
   - Check if gh-pages branch exists
   - Review deployment logs in Actions tab

3. **Coverage Issues**:
   - Verify CODECOV_TOKEN is set
   - Check Codecov website for detailed reports

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Ensure all tests pass locally
5. Create a pull request

The CI pipeline will automatically run on your pull request.