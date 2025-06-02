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

Rest Booking API Testing with Postman Newman
This project demonstrates API testing using Postman, providing a collection of tests to validate various endpoints of the API.

Features
Tests for GET, POST, PUT, DELETE requests
Collection of tests covering different API endpoints
Environment setup for easy switching between environments
Pre-request scripts for data setup
Test scripts for assertions and validations
API Documentation:
https://documenter.getpostman.com/view/13082503/2sA2xmUAJ1
Technology used:
Postman
Newman
Prerequisite:
Node Js
Newman
Newman Html Report Library
Installation
Postman: If you haven't already, download and install Postman.
Clone the repository:
git clone  git@github.com:Rupa-Dey/API_Testing_Project01.git
Import the Postman collection:
Open Postman.
Click on the Import button.
Select the file from the repository.
Import the Postman environment:
In Postman, click on the gear icon in the top right corner.
Select Import and choose the file.
Newman and Report Installation Process:
Newman Install Command:
 npm install -g newman
Newman Html Report Install Command:
 npm install -g newman-reporter-htmlextra
Usage
Select Environment:
In Postman, select the appropriate environment (e.g., Development, Production) from the top-right dropdown.
Run Collection:
Select the imported collection from the Collections sidebar.
Click on the Runner button to open the collection runner.
Select the desired environment.
Click Start Test to run the collection.
View Results:
Once the tests are complete, view the results in the Runner tab.
Detailed test results can be viewed for each request.
Testing
Test Case Scenarios:
1. Create New Booking
Request URL: https://restful-booker.herokuapp.com/booking/
Request Method: POST
Pre-request Script:
var firstName = pm.variables.replaceIn("{{$randomFirstName}}")

var lastName = pm.variables.replaceIn("{{$randomLastName}}")

var totalPrice = pm.variables.replaceIn("{{$randomInt}}")
// console.log(totalPrice)

var depo = pm.variables.replaceIn("{{$randomBoolean}}")
console.log(depo)
// console.log(firstName)

//DATE
const mnt = require('moment')
const today = mnt()
// console.log(today.add(1,'d').format('YYYY-MM-DD'))
var checkIn =  today.add(1,'d').format('YYYY-MM-DD')
var checkOut =  today.add(10,'d').add(1,'M').format('YYYY-MM-DD')

//additional needs
var need = ["Breakfast", "Lunch", "Snacks", "Dinner"]

//Math.random gives the float value betwwen 0 and 1
var needVal = Math.floor(Math.random()* need.length)
var addNeed = need[ needVal]
// console.log(needVal)
// console.log(addNeed)


pm.environment.set("first_name",firstName)
pm.environment.set("last_name",lastName)
pm.environment.set("totalPrice",totalPrice)
pm.environment.set("deposit_Paid",depo)
pm.environment.set("checkIn",checkIn)
pm.environment.set("checkOut",checkOut)
pm.environment.set("additionalNeed",addNeed)

Request Body:

{
   "firstname" : "{{first_name}}",
   "lastname" : "{{last_name}}",
   "totalprice" : {{totalPrice}},
   "depositpaid" : {{deposit_Paid}},
   "bookingdates" : {
   	"checkin" : "{{checkIn}}",
   	"checkout" : "{{checkOut}}"
   },
   "additionalneeds" : "{{additionalNeed}}"
}
Response Body:

{
   "bookingid": 2944,
   "booking": {
       "firstname": "Marjory",
       "lastname": "Ritchie",
       "totalprice": 833,
       "depositpaid": false,
       "bookingdates": {
           "checkin": "2025-02-19",
           "checkout": "2025-04-01"
       },
       "additionalneeds": "Lunch"
   }
}
2. Get Booking Details By ID
Request URL: https://restful-booker.herokuapp.com/booking/bookingid
Request Method: GET
Response Body:
{
   "bookingid": 2944,
   "booking": {
       "firstname": "Marjory",
       "lastname": "Ritchie",
       "totalprice": 833,
       "depositpaid": false,
       "bookingdates": {
           "checkin": "2025-02-19",
           "checkout": "2025-04-01"
       },
       "additionalneeds": "Lunch"
   }
}
3. Create A Token For Authentication.
Request URL: https://restful-booker.herokuapp.com/auth
Request Method: POST
Pre-request Script: None
Request Body:
{
   "username": "admin",
   "password": "password123"
}
Response Body:

{
   "token": "0ee30d009a885d0"
}
4. Update the Booking Details
Request URL: https://restful-booker.herokuapp.com/booking/bookingid
Request Method: PUT
Pre-request Script:
var updated_firstname = pm.variables.replaceIn("{{$randomFirstName}}")
var updated_lastname = pm.variables.replaceIn("{{$randomLastName}}")
var updated_price = pm.variables.replaceIn("{{$randomInt}}")
var updated_deposit = pm.variables.replaceIn("{{$randomBoolean}}")

//updated_DATE
const update_moment = require('moment')
const updated_today = update_moment()
// console.log(updated_today)

var updated_checkin = updated_today.add(2,'M').format("YYYY-MM-DD")
var updated_checkout = updated_today.add(5,'d').add(1,'Y').format("YYYY-MM-DD")

//additional need
var updated_need = ["Breakfast","Lunch","Snacks","Dinner"]
var updated_needval = Math.floor(Math.random()*updated_need.length)

var updated_addNeed = updated_need[updated_needval]

//environment_set
pm.environment.set("updated_firstname",updated_firstname)
pm.environment.set("updated_lastname",updated_lastname)
pm.environment.set("updated_price",updated_price)
pm.environment.set("updated_deposit",updated_deposit)
pm.environment.set("updated_checkin",updated_checkin)
pm.environment.set("updated_checkout",updated_checkout)
pm.environment.set("updated_aditionalneed",updated_addNeed)
Request Body:

{
   "firstname": "Jeanne",
   "lastname": "Waters",
   "totalprice": 754,
   "depositpaid": false,
   "bookingdates": {
       "checkin": "2025-04-18",
       "checkout": "2026-04-23"
   },
   "additionalneeds": "Snacks"
}
5. Delete Booking Record
Request URL: https://restful-booker.herokuapp.com/booking/bookingid
Request Method: DELETE
Response Body: None
Run Command:
Run Command for Console:
newman run API_CRUD_Testing.postman_collection.json -e API_CRUD_Testing.postman_environment.json
Run Command for Report:
newman run API_CRUD_Testing.postman_collection.json -e API_CRUD_Testing.postman_environment.json -r cli,htmlextra
Newman Report Summary:
Image


Author

MD. Abdul AlimAPI Test Automation | Postman | Newman | Software Quality Assurance
