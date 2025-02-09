### **Rest API Testing with Postman Newman**
This project demonstrates API testing using Postman, providing a collection of tests to validate various endpoints of the API. 

### **Features**

- Tests for GET, POST, PUT, DELETE requests
- Collection of tests for different API endpoints
- Easy environment switching setup
- Pre-request scripts for setting up data
- Test scripts for checking results and validations

## API Documentation:
- https://documenter.getpostman.com/view/19885870/2sAYX5M3Gi
  
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
  git clone https://github.com/AdritaAlam/API_Testing_with_Postman_Newman_Report.git
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
//first name
var firstName = pm.variables.replaceIn("{{$randomFirstName}}")
console.log(firstName)    
pm.environment.set("firstName",firstName)

//last name
var lastName = pm.variables.replaceIn("{{$randomLastName}}")
pm.environment.set("lastName",lastName)

//total price
var totalPrice = pm.variables.replaceIn("{{$randomInt}}")
pm.environment.set("totalPrice",totalPrice)

//depositpaid
var depositPaid = pm.variables.replaceIn("{{$randomBoolean}}")
pm.environment.set("depositPaid",depositPaid)

//Date
const moment = require('moment')
const today = moment()
//checkin
var checkin = today.add(1,'d').format("YYYY-MM-DD")
// console.log(checkin)
pm.environment.set("checkin",checkin)

// checkout
var checkout = today.add(1,'d').format("YYYY-MM-DD")
// console.log(checkout)
pm.environment.set("checkout",checkout)

//additional need
const additionalNeed = ["Breakfast","Lunch","Dinner","Wifi"]
pm.variables.set("additionalNeed",additionalNeed[Math.floor(Math.random()*additionalNeed.length)])




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
	"additionalneeds" : "{{additionalNeed}}"
}

```
  **Response Body:**
 ```console 
  {
    "bookingid": 1471,
    "booking": {
        "firstname": "Dora",
        "lastname": "Quigley",
        "totalprice": 238,
        "depositpaid": false,
        "bookingdates": {
            "checkin": "2025-02-05",
            "checkout": "2025-02-06"
        },
        "additionalneeds": "Dinner"
    }
}
```
 ## _**2. Get Booking Details By ID**_
### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: GET
### Response Body:
 ```console 
{
    "firstname": "Dora",
    "lastname": "Quigley",
    "totalprice": 238,
    "depositpaid": false,
    "bookingdates": {
        "checkin": "2025-02-05",
        "checkout": "2025-02-06"
    },
    "additionalneeds": "Dinner"
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
    "token": "85cdeb8e0b275b1"
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
var updated_checkin = today.add(1,'d').format("YYYY-MM-DD")
// console.log(checkin)
pm.environment.set("updated_checkin",updated_checkin)

// checkout
var updated_checkout = today.add(1,'d').format("YYYY-MM-DD")
// console.log(checkout)
pm.environment.set("updated_checkout",updated_checkout)

//additional need
const updated_additionalNeed = ["Breakfast","Lunch","Dinner","Wifi"]
pm.variables.set("updated_additionalNeed",updated_additionalNeed[Math.floor(Math.random()*updated_additionalNeed.length)])

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
	"additionalneeds" : "{{updated_additionalNeed}}"
}

```
  **Response Body:**
 ```console 
  {
    "firstname": "Raquel",
    "lastname": "Muller",
    "totalprice": 933,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2025-02-05",
        "checkout": "2025-02-06"
    },
    "additionalneeds": "Dinner"
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
![image](https://github.com/user-attachments/assets/937fdc55-5cd2-4a79-8a0b-3c9a79fd950e)
![image](https://github.com/user-attachments/assets/1a3f5e2f-5ce8-458d-a056-eb40ede03b0e)
![image](https://github.com/user-attachments/assets/b41f21ed-2cf8-4b0b-93aa-d8f706a46e70)
![image](https://github.com/user-attachments/assets/40d392b9-258c-4b0c-b298-79716fa2b1ca)
