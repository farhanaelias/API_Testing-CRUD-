### **Rest API Testing with Postman Newman**
This project demonstrates API testing using Postman, providing a collection of tests to validate various endpoints of the API. 

### **Features**

- Tests for GET, POST, PUT, DELETE requests
- Collection of tests for different API endpoints
- Easy environment switching setup
- Pre-request scripts for setting up data
- Test scripts for checking results and validations

## API Documentation:
- https://documenter.getpostman.com/view/40139252/2sAYX9kzE3
  
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
  git clone 
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
3. Run Collection:
    -   Select the imported collection from the Collections sidebar.
    -   Click on the Runner button to open the collection runner.
    -   Select the desired environment.
    -   Click Start Test to run the collection.
8. View Results:
    -   Once the tests are complete, view the results in the Runner tab.
    -   Detailed test results can be viewed for each request.

## **Testing**

## Test Case Scenarios:

## _**1. Create New Booking**_

### Request URL: https://restful-booker.herokuapp.com/booking/
### Request Method: POST
### Pre-request Script:
```console 
var firstName = pm.variables.replaceIn("{{$randomFirstName}}")
console.log(firstName)
pm.environment.set("firstName", firstName)

var lastName = pm.variables.replaceIn("{{$randomLastName}}")
console.log(lastName)
pm.environment.set("lastName", lastName)

var totalPrice = pm.variables.replaceIn("{{$randomInt}}")
console.log(totalPrice)
pm.environment.set("totalPrice", totalPrice)

var depositPaid = pm.variables.replaceIn("{{$randomBoolean}}")
pm.environment.set("depositPaid",depositPaid)


//Date

const moment = require('moment')
const today = moment()
var checkin = today.add(5, 'd').format("YYYY-MM-DD")
pm.environment.set("checkin", checkin)

var checkout = today.add(5, 'd').format("YYYY-MM-DD")
pm.environment.set("checkout", checkout)









```
  **Request Body:** 
 ```console 
  {
	"firstname" : "{{firstName}}",
	"lastname" : "{{lastName}}",
	"totalprice" : {{totalPrice}},
	"depositpaid" : {{depositPaid}},
	"bookingdates" : {
    	"checkin" : "{{checkin}}",
    	"checkout" : "{{checkout}}"
	},
	"additionalneeds" : "lunch"
}

```
  **Response Body:**
 ```console 
 {
    "bookingid": 826,
    "booking": {
        "firstname": "Watson",
        "lastname": "Feil",
        "totalprice": 541,
        "depositpaid": false,
        "bookingdates": {
            "checkin": "2025-02-14",
            "checkout": "2025-02-19"
        },
        "additionalneeds": "lunch"
    }
}
```
 ## _**2. Get Booking Details By ID**_
### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: GET
### Response Body:
 ```console 
{
    "firstname": "Watson",
    "lastname": "Feil",
    "totalprice": 541,
    "depositpaid": false,
    "bookingdates": {
        "checkin": "2025-02-14",
        "checkout": "2025-02-19"
    },
    "additionalneeds": "lunch"
}
```
## _**3. Create A Token For Authentication.**_
### Request URL: https://restful-booker.herokuapp.com/auth
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
    "token": "599aed80e466f8e"
}
```

 ## _**4. Update the Booking Details**_
### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: PUT
### Pre-request Script:
```console 
//first name
var updated_firstName = pm.variables.replaceIn("{{$randomFirstName}}")
// console.log(firstName)    
pm.environment.set("updated_firstName",updated_firstName)

//last name
var updated_lastName = pm.variables.replaceIn("{{$randomLastName}}")
pm.environment.set("updated_lastName",updated_lastName)

//total price
var updated_totalPrice = pm.variables.replaceIn("{{$randomInt}}")
pm.environment.set("updated_totalPrice",updated_totalPrice)

//depositpaid
var updated_depositPaid = pm.variables.replaceIn("{{$randomBoolean}}")
pm.environment.set("updated_depositPaid",updated_depositPaid)


//Date
const moment = require('moment')
const today = moment()

//checkin
var updated_checkin = today.add(5,'d').format("YYYY-MM-DD")
pm.environment.set("updated_checkin",updated_checkin)

// checkout
var updated_checkout = today.add(5,'d').format("YYYY-MM-DD")
pm.environment.set("updated_checkout",updated_checkout)


```
  **Request Body:** 
 ```console 
 {
	"firstname" : "{{updated_firstName}}",
	"lastname" : "{{updated_lastName}}",
	"totalprice" : {{updated_totalPrice}},
	"depositpaid" : {{updated_depositPaid}},
	"bookingdates" : {
    	"checkin" : "{{updated_checkin}}",
    	"checkout" : "{{updated_checkout}}"
	},
	"additionalneeds" : "lunch"
}

```
  **Response Body:**
 ```console 
  {
    "firstname": "Gustave",
    "lastname": "Hansen",
    "totalprice": 471,
    "depositpaid": false,
    "bookingdates": {
        "checkin": "2025-02-14",
        "checkout": "2025-02-19"
    },
    "additionalneeds": "lunch"
}
```

 ## _**5. Delete Booking Record**_

#### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
#### Request Method: DELETE
#### Response Body: None 

## Run Command:  
- Run Command for Console: 
```console 
newman run API_Testing_CRUD.postman_collection.json -e API_Testing_CRUD.postman_environment.json
```
- Run Command for Report: 
```console 
newman run API_Testing_CRUD.postman_collection.json -e API_Testing_CRUD.postman_environment.json -r cli,htmlextra
```

## Newman Report Summary:
![image](https://github.com/user-attachments/assets/baae0ab2-2bb0-4a51-8427-6670ee6204ad)

