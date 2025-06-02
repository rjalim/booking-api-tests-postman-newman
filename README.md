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
- https://documenter.getpostman.com/view/45376092/2sB2qgfeQo
  
### **Technology used:**
- Postman
- Newman

### **Prerequisite:**
- Node Js
- Newman
- Newman Html Report Library

### **Installation**

1. Postman: If you haven't already, [download and install Postman.](https://www.postman.com/downloads/)
2. Clone the repository:
```console
https://github.com/rjalim/booking-api-tests-postman-newman.git
```
3. Import the Postman collection:
    - Open Postman.
    - Click on the Import button.
    - Select the file from the repository.
4. Import the Postman environment:
    - In Postman, click on the gear icon in the top right corner.
    - Select **Import** and choose the file.
5. Newman and Report Installation Process:
    - Newman Install Command:
     ```console 
      npm install -g newman
    ```
    - Newman Html Report Install Command:
     ```console 
      npm install -g newman-reporter-htmlextra
    ```
