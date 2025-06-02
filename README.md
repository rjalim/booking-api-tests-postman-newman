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

## 📄 API Documentation

- 🔗 [View on Postman Documenter](https://documenter.getpostman.com/view/45376092/2sB2qgfeQo)

  
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
  ### **Usage**
1. Select Environment:
    -   In Postman, select the appropriate environment (e.g., Development, Production) from the top-right dropdown.
2. Run Collection:
    -   Select the imported collection from the Collections sidebar.
    -   Click on the Runner button to open the collection runner.
    -   Select the desired environment.
    -   Click Start Test to run the collection.
3. View Results:
    -   Once the tests are complete, view the results in the Runner tab.
    -   Detailed test results can be viewed for each request.

## **Testing**

## Test Case Scenarios:

## _**1. Create New Booking**_
### BaseUrl : https://restful-booker.herokuapp.com
### Request URL: {{BaseUrl}}/booking/
### Request Method: POST
### Pre-request Script:
```console 
var firstName = pm.variables.replaceIn("{{$randomFirstName}}")
console.log(firstName)
pm.environment.set("FirstName",firstName)

var lastname = pm.variables.replaceIn("{{$randomLastName}}")
console.log(lastname)
pm.environment.set("LastName",lastname)

var totalprice = pm.variables.replaceIn("{{$randomInt}}")
console.log(totalprice)
pm.environment.set("TotalPrice",totalprice)

var depositpaid = pm.variables.replaceIn("{{$randomBoolean}}")
console.log(depositpaid)
pm.environment.set("DepositPaid", depositpaid)

const moment = require('moment')
const today = moment()
var checkin = today.format("YYYY-MM-DD")
console.log(today.format("YYYY-MM-DD"))
pm.environment.set("CheckIn",checkin)

var checkout = today.add(10, 'd').format("YYYY-MM-DD")
console.log(today.add(10,'d').format("YYYY-MM-DD"))
pm.environment.set("CheckOut", checkout)

const needs = ["Breakfast", "Lunch", "Dinner"];
const randomNeed = needs[Math.floor(Math.random() * needs.length)];
console.log("Additional Needs:", randomNeed);
pm.environment.set("UAdditionalNeeds", randomNeed);  

```
### Post Response script
```console

var jsonData = pm.response.json()
pm.environment.set("ID",jsonData.bookingid)

```
 **Request Body:** 
 ```console 
{
    "firstname": "{{FirstName}}",
    "lastname": "{{LastName}}",
    "totalprice": {{TotalPrice}},
    "depositpaid": {{DepositPaid}},
    "bookingdates": {
        "checkin": "{{CheckIn}}",
        "checkout": "{{CheckOut}}"
    },
    "additionalneeds": "{{additionalneeds}}"
}
```
**Response Body:**
 ```console 
{
    "bookingid": 4878,
    "booking": {
        "firstname": "Emma",
        "lastname": "Corwin",
        "totalprice": 511,
        "depositpaid": true,
        "bookingdates": {
            "checkin": "2025-06-02",
            "checkout": "2025-06-12"
        },
        "additionalneeds": "Breakfast, Lunch, Dinner"
    }
}
```
 ## _**2. Get Booking Details By ID**_
### Request URL: {{BaseUrl}}/booking/{{ID}}
### Request Method: GET
### Response Body:
 ```console 
{
    "bookingid": 4878,
    "booking": {
        "firstname": "Emma",
        "lastname": "Corwin",
        "totalprice": 511,
        "depositpaid": false,
        "bookingdates": {
            "checkin": "2025-06-02",
            "checkout": "2025-06-12"
        },
        "additionalneeds": "Breakfast, Lunch, Dinner"
    }
}
```
## _**3. Create A Token For Authentication.**_
### Request URL: {{BaseUrl}}/auth
### Request Method: POST
### Pre-request Script: None
### Request Body:
 ```console 
{
	"username": "admin",
	"password": "password123"
}
```
  **Response Body:**
 ```console 
{
    "token": "975c06e393952db"
}
```

 ## _**4. Update the Booking Details**_
### Request URL: {{BaseUrl}}/booking/{{ID}}
### Request Method: PUT
### Pre-request Script:
```console 
var ufirstName = pm.variables.replaceIn("{{$randomFirstName}}");
console.log("First Name:", ufirstName);
pm.environment.set("UFirstName", ufirstName);

var ulastname = pm.variables.replaceIn("{{$randomLastName}}");
console.log("Last Name:", ulastname);
pm.environment.set("ULastName", ulastname);

var utotalprice = pm.variables.replaceIn("{{$randomInt}}");
console.log("Total Price:", utotalprice);
pm.environment.set("UTotalPrice", utotalprice);

var udepositpaid = pm.variables.replaceIn("{{$randomBoolean}}");
console.log("Deposit Paid:", udepositpaid);
pm.environment.set("UDepositPaid", udepositpaid);

const moment = require('moment');
const today = moment();

var ucheckin = today.format("YYYY-MM-DD");
console.log("Check-in:", ucheckin);
pm.environment.set("UCheckIn", ucheckin);

var ucheckout = moment(today).add(10, 'd').format("YYYY-MM-DD");
console.log("Check-out:", ucheckout);
pm.environment.set("UCheckOut", ucheckout);

const needs = ["Breakfast", "Lunch", "Dinner"];
const randomNeed = needs[Math.floor(Math.random() * needs.length)];
console.log("Additional Needs:", randomNeed);
pm.environment.set("UAdditionalNeeds", randomNeed); 
```
  **Request Body:** 
 ```console
{
	"firstname" : "{{UFirstName}}",
	"lastname" : "{{ULastName}}",
	"totalprice" : {{UTotalPrice}},
	"depositpaid" : {{UDepositPaid}},
	"bookingdates" : {
    	"checkin" : "{{UCheckIn}}",
    	"checkout" : "{{UCheckOut}}"
	},
	"additionalneeds" : "{{UAdditionalNeeds}}"
}
```

**Response Body:**

 ```console
{
    "firstname": "Sally",
    "lastname": "Beatty",
    "totalprice": 18,
    "depositpaid": false,
    "bookingdates": {
        "checkin": "2025-06-02",
        "checkout": "2025-06-12"
    },
    "additionalneeds": "Breakfast"
}
```

 ## _**5. Varify Update Booking**_
### Request URL: {{BaseUrl}}/booking/{{ID}}
### Request Method: GET
### Pre-request Script:

```console 
var statusCode =pm.response.code
console.log(statusCode)

if(statusCode==200){

pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

var jsonData = pm.response.json()

pm.test("First Name Validation", function(){
    pm.expect(jsonData.firstname).to.eql (pm.environment.get("UFirstName"))
})

pm.test("Last Name Validation", function(){
    pm.expect(jsonData.lastname).to.eql (pm.environment.get("ULastName"))
})
pm.test("Total Price Validation", function(){
    pm.expect(jsonData.totalprice.toString()).to.eql (pm.environment.get("UTotalPrice"))
})

pm.test("Deposit Paid Validation", function () {
    var expectedValue = pm.environment.get("UDepositPaid") === 'true'; // convert string to boolean
    pm.expect(jsonData.depositpaid).to.eql(expectedValue);
})

pm.test("Check In Validation", function(){
    pm.expect(jsonData.bookingdates.checkin).to.eql (pm.environment.get("UCheckIn"))
})

pm.test("Check Out Validation", function(){
    pm.expect(jsonData.bookingdates.checkout).to.eql (pm.environment.get("UCheckOut"))
})
pm.test("Additional Needs Validation", function(){
    pm.expect(jsonData.additionalneeds).to.eql(pm.environment.get("UAdditionalNeeds"))
})
} 
else if(statusCode==404){
    pm.test("Not Found")
}
else{
    pm.test("Something went wrong")
}

```

## _**6. Delete Booking**_
### Request URL:{{BaseUrl}}/booking/{{ID}}
### Request Method: DELETE
### Post Response Script


## _**7. Varify Delet**_
### Request URL:{{BaseUrl}}/booking/{{ID}}
### Request Method: DELETE
### Post Response Script

```console 
let statusCode = pm.response.code;
console.log("Status Code:", statusCode);

if (statusCode === 404) {
    pm.test("Booking has been successfully deleted", function () {
        pm.expect(statusCode).to.eql(404);
    });
} else {
    pm.test("Booking still exists or something went wrong", function () {
        pm.expect(statusCode).to.eql(404);  // force fail if not 404
    });

    console.log("Response Body:", pm.response.text());
}
```
### Response: 
Booking has been successfully deleted

## Run Command:  
- Run Command for Console: 
```console 
newman run API_CRUD_Testing.postman_collection.json -e API_CRUD_Testing.postman_environment.json
```
- Run Command for Report: 
```console 
newman run API_CRUD_Testing.postman_collection.json -e API_CRUD_Testing.postman_environment.json -r cli,htmlextra
```

## 📄 API Documentation



