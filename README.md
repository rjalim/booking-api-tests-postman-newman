# booking-api-tests-postman-newman
End-to-end automated testing of a RESTful Booking API using Postman and Newman, including dynamic data, token-based auth, and HTML reports.

This project demonstrates automated API testing using Postman for a RESTful Booking API. It includes comprehensive test scenarios, dynamic data handling, and test reporting via Newman.

### **Features**

-Dynamic test data using pre-request scripts
-Automated tests for Create, Read, Update, and Delete (CRUD) operations
-Token-based authentication
-Environment support for flexible configurations
-Assertions and validation scripts in Postman
-HTML reports using Newman

## API Documentation:

Postman Public Documentation :

### **Technology used:**

-Postman
-Newman CLI
-Newman HTML Extra Reporter

### **Prerequisite:**

-Node.js
-Newman (npm install -g newman)
-Newman HTML Extra Reporter (npm install -g newman-reporter-htmlextra)
-Postman App (optional for local testing)

### **Installation**

Clone the Repository:

git clone https://github.com/rjalim/booking-api-tests-postman-newman.git

Import into Postman:

Collection: Go to Postman > Import > Choose the collection file

Environment: Go to Postman > Environments > Import environment file

Install Dependencies:

npm install -g newman newman-reporter-htmlextra

Usage

Run Tests in Console

newman run API_CRUD_Testing.postman_collection.json -e API_CRUD_Testing.postman_environment.json

Generate HTML Report

newman run API_CRUD_Testing.postman_collection.json -e API_CRUD_Testing.postman_environment.json -r cli,htmlextra

Test Scenarios

1. Create New Booking

Method: POSTEndpoint: /booking

Includes a pre-request script to dynamically generate:

First & last name

Random total price

Boolean for deposit

Dates using moment.js

Random "additional needs"

2. Get Booking by ID

Method: GETEndpoint: /booking/{{bookingid}}

Tests if the booking ID exists and validates the response structure.

3. Generate Auth Token

Method: POSTEndpoint: /auth

Sends credentials and stores the returned token in environment variables.

4. Update Booking

Method: PUTEndpoint: /booking/{{bookingid}}

Uses dynamically generated data to update an existing booking with token authentication.

5. Delete Booking

Method: DELETEEndpoint: /booking/{{bookingid}}

Deletes a booking using an admin token.

Sample Report Screenshots



Project Status

Fully functional and tested end-to-end REST API automation framework. Future improvements may include CI/CD integration and test coverage metrics.

Contributions

Feel free to fork and open pull requests if you'd like to extend the collection or improve the report structure.

Author

MD. Abdul AlimAPI Test Automation | Postman | Newman | Software Quality Assurance
