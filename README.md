# Rest-reqres-API-with-Newman-Report

This project demonstrates comprehensive API testing using Postman collections and Newman for automated test execution and report generation. It focuses on testing the ReqRes API, a popular REST API service designed for testing and prototyping.

## Table of Contents

- [Features](#features)
- [Project Overview](#project-overview)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Project Structure](#project-structure)
- [API Endpoints Tested](#api-endpoints-tested)
- [Test Scenarios](#test-scenarios)
- [Running Tests](#running-tests)
- [Report Generation](#report-generation)
- [Environment Configuration](#environment-configuration)
- [CI/CD Integration](#cicd-integration)
- [Contributing](#contributing)
- [License](#license)

## Features

### 🧪 Comprehensive Test Coverage
- **HTTP Methods**: Tests for GET, POST, PUT, PATCH, DELETE operations
- **Status Code Validation**: Ensures correct HTTP status codes for all responses
- **Response Time Monitoring**: Validates API performance with response time assertions
- **Data Validation**: Comprehensive checks on response body structure and content
- **Header Validation**: Verifies required headers and their values

### 📊 Automated Reporting
- **HTML Reports**: Interactive, visually appealing test reports
- **JSON Reports**: Machine-readable format for further processing
- **JUnit/XML Reports**: Compatible with CI/CD pipelines and test management tools
- **CLI Output**: Real-time test execution feedback

### 🔧 Advanced Testing Features
- **Environment Variables**: Dynamic configuration for different test environments
- **Data-Driven Testing**: CSV/JSON data files for parameterized tests
- **Pre-request Scripts**: Setup and authentication logic
- **Test Scripts**: Custom JavaScript assertions and validations
- **Global Variables**: Shared data across test requests

### 🚀 Automation & Integration
- **Command Line Execution**: Run tests via Newman CLI
- **CI/CD Pipeline Ready**: Integrates with GitHub Actions, Jenkins, etc.
- **Parallel Execution**: Run multiple collections simultaneously
- **Scheduled Runs**: Automate periodic test execution

### 📈 Monitoring & Analytics
- **Test Metrics**: Pass/fail rates, response times, error tracking
- **Trend Analysis**: Historical test performance data
- **Failure Analysis**: Detailed error reporting and debugging information

## Project Overview

This project serves as a complete example of API testing best practices using:

- **ReqRes API**: A hosted REST API for testing (https://reqres.in/)
- **Postman Collections**: Organized test suites with requests and assertions
- **Newman**: Postman collection runner for automated execution
- **Multiple Report Formats**: Various output formats for different stakeholders

The ReqRes API provides endpoints for user management, resource handling, and authentication simulation, making it ideal for demonstrating various testing scenarios.

## Prerequisites

Before running this project, ensure you have the following installed:

- **Node.js** (v14 or higher) - Required for Newman
- **npm** or **yarn** - Package manager
- **Git** - Version control
- **Postman** (optional) - For manual testing and collection editing

### System Requirements
- Operating System: Windows, macOS, or Linux
- RAM: Minimum 2GB
- Disk Space: 100MB free space

## Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/sakhi-shraddha-sst/Rest-reqres-API-with-Newman-Report.git
   cd Rest-reqres-API-with-Newman-Report
   ```

2. **Install Newman globally**:
   ```bash
   npm install -g newman
   ```

3. **Install project dependencies** (if any):
   ```bash
   npm install
   ```

4. **Verify installation**:
   ```bash
   newman --version
   ```

## Project Structure

```
Rest-reqres-API-with-Newman-Report/
├── collections/                 # Postman collection files
│   ├── reqres-api-tests.postman_collection.json
│   └── environment.postman_environment.json
├── data/                        # Test data files
│   ├── users.csv
│   └── test-data.json
├── reports/                     # Generated test reports
│   ├── html/
│   ├── json/
│   └── junit/
├── scripts/                     # Automation scripts
│   ├── run-tests.sh
│   └── generate-report.js
├── .github/workflows/           # CI/CD pipelines
│   └── api-tests.yml
├── README.md                    # Project documentation
├── package.json                 # Node.js dependencies
└── newman-config.json          # Newman configuration
```

## API Endpoints Tested

The project covers testing of the following ReqRes API endpoints:

### Users Endpoints
- `GET /api/users` - List users with pagination
- `GET /api/users/{id}` - Get single user
- `POST /api/users` - Create new user
- `PUT /api/users/{id}` - Update user
- `PATCH /api/users/{id}` - Partially update user
- `DELETE /api/users/{id}` - Delete user

### Resources Endpoints
- `GET /api/unknown` - List resources
- `GET /api/unknown/{id}` - Get single resource

### Authentication Endpoints
- `POST /api/login` - User login
- `POST /api/register` - User registration

## Test Scenarios

### Functional Testing
- **CRUD Operations**: Complete Create, Read, Update, Delete cycles
- **Pagination**: Testing list endpoints with different page parameters
- **Data Validation**: Ensuring response data matches expected schemas
- **Error Handling**: Testing invalid requests and error responses

### Performance Testing
- **Response Time**: Asserting maximum response times
- **Concurrent Requests**: Testing API behavior under load
- **Rate Limiting**: Verifying API rate limit handling

### Security Testing
- **Input Validation**: Testing with malicious or invalid input
- **Authentication**: Verifying secure endpoints
- **Data Exposure**: Checking for sensitive data leakage

### Integration Testing
- **End-to-End Flows**: Complete user journeys
- **Data Consistency**: Ensuring data integrity across operations
- **API Dependencies**: Testing interdependent endpoints

## Running Tests

### Basic Test Execution
```bash
# Run all tests with default settings
newman run collections/reqres-api-tests.postman_collection.json

# Run with environment file
newman run collections/reqres-api-tests.postman_collection.json \
  -e collections/environment.postman_environment.json
```

### Advanced Execution Options
```bash
# Run with custom data file
newman run collections/reqres-api-tests.postman_collection.json \
  -d data/users.csv

# Run specific folder/requests
newman run collections/reqres-api-tests.postman_collection.json \
  --folder "User Management"

# Run with custom timeout
newman run collections/reqres-api-tests.postman_collection.json \
  --timeout 5000
```

### Using Automation Scripts
```bash
# Run tests with custom script
./scripts/run-tests.sh

# Generate comprehensive reports
node scripts/generate-report.js
```

## Report Generation

### HTML Reports
```bash
newman run collections/reqres-api-tests.postman_collection.json \
  -r html --reporter-html-export reports/html/report.html
```

### JSON Reports
```bash
newman run collections/reqres-api-tests.postman_collection.json \
  -r json --reporter-json-export reports/json/report.json
```

### JUnit Reports
```bash
newman run collections/reqres-api-tests.postman_collection.json \
  -r junit --reporter-junit-export reports/junit/report.xml
```

### Multiple Reports
```bash
newman run collections/reqres-api-tests.postman_collection.json \
  -r html,json,junit \
  --reporter-html-export reports/html/report.html \
  --reporter-json-export reports/json/report.json \
  --reporter-junit-export reports/junit/report.xml
```

## Environment Configuration

### Environment Variables
- `baseUrl`: API base URL (https://reqres.in)
- `apiVersion`: API version (v1)
- `timeout`: Request timeout in milliseconds
- `retries`: Number of retry attempts

### Data Files
- **users.csv**: Test data for user creation/update operations
- **test-data.json**: Complex test scenarios and edge cases

### Newman Configuration
Custom configuration file (`newman-config.json`) for:
- Default reporters
- Global timeouts
- SSL settings
- Proxy configuration

## CI/CD Integration

### GitHub Actions
Automated testing pipeline that runs on:
- Push to main branch
- Pull request creation
- Scheduled runs (daily/weekly)

### Jenkins Pipeline
```groovy
pipeline {
    agent any
    stages {
        stage('API Tests') {
            steps {
                sh 'npm install -g newman'
                sh 'newman run collections/reqres-api-tests.postman_collection.json -r html,junit'
            }
        }
    }
    post {
        always {
            publishHTML(target: [reportDir: 'reports/html', reportFiles: 'report.html'])
            junit 'reports/junit/*.xml'
        }
    }
}
```

### Other CI/CD Tools
- **Azure DevOps**: Pipeline templates for API testing
- **GitLab CI**: Automated testing with merge request integration
- **CircleCI**: Docker-based test execution

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/new-test-scenario`)
3. Add your test cases or improvements
4. Run tests to ensure everything works
5. Commit your changes (`git commit -am 'Add new test scenario'`)
6. Push to the branch (`git push origin feature/new-test-scenario`)
7. Create a Pull Request

### Guidelines
- Follow Postman collection best practices
- Include comprehensive test assertions
- Add documentation for new features
- Ensure tests pass in CI/CD pipeline

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Support

For questions or issues:
- Create an issue in this repository
- Check the [ReqRes API documentation](https://reqres.in/)
- Review [Newman documentation](https://learning.postman.com/docs/running-collections/using-newman-cli/command-line-integration-with-newman/)

## Future Enhancements

- [ ] Add GraphQL API testing
- [ ] Implement load testing with Artillery
- [ ] Add API contract testing
- [ ] Integrate with API management tools
- [ ] Add performance benchmarking
- [ ] Implement chaos engineering tests