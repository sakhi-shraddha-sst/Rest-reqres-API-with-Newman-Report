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
├── Postman Collections/         # Postman collection files
│   └── Reqres_API_Collections.json
├── README.md                    # Project documentation
└── .git/                        # Git repository
```

## Collection Structure

The Postman collection `Reqres_API_Collections.json` contains the following organized test suites:

### Page_1 & Page_2 Folders
Both folders contain identical test requests for comprehensive validation:

#### User Management Tests
1. **Fetch a list of users with pagination**
   - **Method**: GET
   - **Endpoint**: `{{BaseURL}}/api/users?page=1`
   - **Tests**:
     - Status code validation (200)
     - Response time < 1000ms
     - Email schema validation (eve.holt@reqres.in)

2. **Fetch a single user by ID**
   - **Method**: GET
   - **Endpoint**: `{{BaseURL}}/api/users/{id}`
   - **Tests**:
     - Status code validation (200)
     - Response time < 1000ms
     - Content-Type header presence
     - Etag header presence
     - Response body validation

3. **Single User Not Found**
   - **Method**: GET
   - **Endpoint**: `{{BaseURL}}/api/users/23` (non-existent user)
   - **Tests**:
     - Status code validation (404)
     - Response time validation
     - Error response handling

4. **Create a new user**
   - **Method**: POST
   - **Endpoint**: `{{BaseURL}}/api/users`
   - **Body**: `{"name": "{{$randomFirstName}}", "job": "{{$randomJobTitle}}"}`
   - **Tests**:
     - Status code validation (201)
     - Collection variable setting for created user ID

5. **Update an existing user**
   - **Method**: PUT
   - **Endpoint**: `{{BaseURL}}/api/users/{id}`
   - **Body**: `{"name": "{{$randomFirstName}}", "job": "{{$randomJobTitle}}"}`
   - **Tests**:
     - Status code validation (200)

6. **Delete a user**
   - **Method**: DELETE
   - **Endpoint**: `{{BaseURL}}/api/users/{id}`
   - **Tests**:
     - Status code validation (204)

## API Endpoints Tested

The collection covers testing of the following ReqRes API endpoints:

### Users Endpoints
- `GET /api/users?page={page}` - List users with pagination
- `GET /api/users/{id}` - Get single user by ID
- `GET /api/users/23` - Single user not found (404 error case)
- `POST /api/users` - Create new user
- `PUT /api/users/{id}` - Update existing user
- `DELETE /api/users/{id}` - Delete a user

## Test Scenarios

### Functional Testing
- **CRUD Operations**: Complete Create, Read, Update, Delete cycles for users
- **Pagination**: Testing list endpoints with page parameters
- **Error Handling**: Testing 404 responses for non-existent users
- **Data Validation**: Schema validation for user data (email verification)

### Performance Testing
- **Response Time Validation**: All requests tested for < 1000ms response time
- **Concurrent Testing**: Duplicate test suites in Page_1 and Page_2 folders

### Validation Testing
- **Status Code Verification**: 
  - 200 for successful GET/PUT operations
  - 201 for successful POST creation
  - 204 for successful DELETE operations
  - 404 for user not found scenarios
- **Header Validation**: Content-Type and Etag headers presence verification
- **Response Body Validation**: JSON structure and data integrity checks

### Data-Driven Testing
- **Dynamic Data**: Uses Postman dynamic variables (`{{$randomFirstName}}`, `{{$randomJobTitle}}`)
- **Variable Management**: Collection variables for storing and reusing created user IDs

## Test Validations & Assertions

### Status Code Assertions
- **GET /api/users**: Expects 200 OK
- **GET /api/users/{id}**: Expects 200 OK for valid users, 404 for non-existent users
- **POST /api/users**: Expects 201 Created
- **PUT /api/users/{id}**: Expects 200 OK
- **DELETE /api/users/{id}**: Expects 204 No Content

### Response Time Assertions
- All requests validate response time < 1000ms
- Ensures API performance meets requirements

### Header Validations
- **Content-Type**: Presence verification for API responses
- **Etag**: Header presence validation for caching support

### Data Schema Validations
- **Email Validation**: Specific email format checking (eve.holt@reqres.in)
- **JSON Structure**: Response body structure validation
- **Data Integrity**: Ensuring required fields are present

### Variable Management
- **ID Storage**: Automatically stores created user ID for subsequent operations
- **Dynamic Content**: Random data generation for test variety

## Running Tests

### Basic Test Execution
```bash
# Run all tests with default settings
newman run "Postman Collections/Reqres_API_Collections.json"

# Run specific folder
newman run "Postman Collections/Reqres_API_Collections.json" --folder "Page_1"

# Run with custom timeout
newman run "Postman Collections/Reqres_API_Collections.json" --timeout 5000
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
newman run "Postman Collections/Reqres_API_Collections.json" \
  -r html --reporter-html-export reports/html/report.html
```

### JSON Reports
```bash
newman run "Postman Collections/Reqres_API_Collections.json" \
  -r json --reporter-json-export reports/json/report.json
```

### JUnit Reports
```bash
newman run "Postman Collections/Reqres_API_Collections.json" \
  -r junit --reporter-junit-export reports/junit/report.xml
```

### Multiple Reports
```bash
newman run "Postman Collections/Reqres_API_Collections.json" \
  -r html,json,junit \
  --reporter-html-export reports/html/report.html \
  --reporter-json-export reports/json/report.json \
  --reporter-junit-export reports/junit/report.xml
```

## Environment Configuration

### Collection Variables Used
- **BaseURL**: `https://reqres.in` - The ReqRes API base URL
- **token**: Authentication token (currently set but not actively used in tests)
- **id**: User ID stored after creating a new user for subsequent operations
- **num**: Static user ID for delete operations

### Dynamic Variables
The collection utilizes Postman's built-in dynamic variables:
- **{{$randomFirstName}}**: Generates random first names for user creation/update
- **{{$randomJobTitle}}**: Generates random job titles for user creation/update

### Environment File (Future Enhancement)
While not currently implemented, you can create a Postman environment file:
```json
{
  "id": "reqres-env",
  "name": "ReqRes Environment",
  "values": [
    {
      "key": "BaseURL",
      "value": "https://reqres.in",
      "type": "default",
      "enabled": true
    }
  ]
}
```

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
                sh 'newman run "Postman Collections/Reqres_API_Collections.json" -r html,junit'
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