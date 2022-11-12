# Content for Project 1
- [Introduction](https://github.com/Shahriar-1810/API-Testing-Projects#introduction)    
- [Summary](https://github.com/Shahriar-1810/API-Testing-Projects#summary)      
- [Requirements](https://github.com/Shahriar-1810/API-Testing-Projects#requirements)    
- [Pre-request Script Details](https://github.com/Shahriar-1810/API-Testing-Projects#Pre-request-Script-Details)
  - [Create Booking](https://github.com/Shahriar-1810/API-Testing-Projects#Create-booking)   
  - [Update Booking](https://github.com/Shahriar-1810/API-Testing-Projects#Update-booking)  
- [Request Body](https://github.com/Shahriar-1810/API-Testing-Projects#Request-body)
- [Assertions Details](https://github.com/musthafiz/API-Testing#assertions-details)   
  - [Create Booking](https://github.com/Shahriar-1810/API-Testing-Projects#create-booking)   
  - [Access Token Generate](https://github.com/musthafiz/API-Testing#Access-token-generate)   
  - [Update Booking](https://github.com/musthafiz/API-Testing#update-booking)   
  - [Delete Booking](https://github.com/musthafiz/API-Testing#delete-booking)  
- [Create Test Suites](https://github.com/musthafiz/API-Testing#create-test-suites)      
      

# Introduction
This document explains how to run an API test with Postman on a Book booking website.    

# Summary    
Completed an API test on Book booking site and the link is below.   
https://restful-booker.herokuapp.com/

**Tasks Done**
- CRUD Operation such as Create, Get, Put, Delete.
- Writing Pre-request Scripts using Dynamic Parameter.
- API Request & Response Chaining.
- Writing Test Scripts (For Data Validation).
- Newman HTML & HTML Extra Report.
  
**Summary:** Total **6 API requests**, **4 Pre-request scripts**, and **36 Assertions** were done, with **4 failed tests** and **0 skipped tests**.
Here in this API books can be booked with a centain check in and check out. Bookings can be viewed, updated, and deleted as well.

  
<p align="center">
  <img src="https://github.com/Shahriar-1810/API-Testing-Projects/blob/main/Project%201/Newman%20HTML%20Report/NewmanExtraa.png" />
</p>


# Requirements  
**Postman**   
https://www.postman.com/   
**Node JS**   
https://nodejs.org/en/    



# Pre-request Script Details   
#### Create Booking
```bash
//set random FirstName variable
pm.environment.set("FirstName", pm.variables.replaceIn('{{$randomFirstName}}'))

//set random LastName variable
pm.environment.set("LastName", pm.variables.replaceIn('{{$randomLastName}}'))

//set random integer as price variable
pm.environment.set("TotalPrice", parseInt(pm.variables.replaceIn('{{$randomInt}}')))

//set random boolean as payment variable
pm.environment.set("Payment", pm.variables.replaceIn('{{$randomBoolean}}'))

//set the time
const date = require('moment')

//set check in date
pm.environment.set("CheckIn", date().add(1,'day').format("YYYY-MM-DD"))

//set check out date
pm.environment.set("CheckOut", date().add(4,'day').format("YYYY-MM-DD"))
```



#### Updating Booking
```bash
//set random FirstName variable
pm.environment.set("FirstName", pm.variables.replaceIn('{{$randomFirstName}}'))

//set random LastName variable
pm.environment.set("LastName", pm.variables.replaceIn('{{$randomLastName}}'))

//set random integer as price variable
pm.environment.set("TotalPrice", parseInt(pm.variables.replaceIn('{{$randomInt}}')))

//set random boolean as payment variable
pm.environment.set("Payment", pm.variables.replaceIn('{{$randomBoolean}}'))

//set the time
const date = require('moment')

//set check in date
pm.environment.set("CheckIn", date().add(4,'day').format("YYYY-MM-DD"))

//set check out date
pm.environment.set("CheckOut", date().add(8,'day').format("YYYY-MM-DD"))
```

# Request Body
#### Create, Update
```bash
{
	"firstname" : "{{FirstName}}",
	"lastname" : "{{LastName}}",
	"totalprice" : "{{TotalPrice}}",
	"depositpaid" : "{{Payment}}",
	"bookingdates" : {
    	"checkin" : "{{CheckIn}}",
    	"checkout" : "{{CheckOut}}"
	},
	"additionalneeds" : "Breakfast"
}
```


# Assertions Details    
#### Create Booking        
```bash
 var jsonData = pm.response.json()

pm.environment.set("BookingID", jsonData.bookingid)

var StateCode = responseCode.code

//status code matched or not
switch(StateCode){
    case 200:
       pm.test("Verify status code 200", function () {
       console.log('StateCode')
       });
       break;
    case 201:
      pm.test("Verify status code 201", function () {
      console.log('StateCode')
      });
      break;
}

//booking ID matched or not
pm.test("Verify BookingID", function () {
    pm.expect(jsonData.bookingid).to.eql(pm.environment.get("BookingID"));
});

//firstname matched or not
pm.test("Verify First name", function () {
    pm.expect(jsonData.booking.firstname).to.eql(pm.environment.get("FirstName"));
});

//lastname matched or not
pm.test("Verify Last name", function () {
    pm.expect(jsonData.booking.lastname).to.eql(pm.environment.get("LastName"));
});

//price matched or not
pm.test("Verify Total price", function () {
    pm.expect(jsonData.booking.totalprice).to.eql(pm.environment.get("TotalPrice"));
});

//boolean value matched or not
pm.test("Verify Depositpaid", function () {
    pm.expect(jsonData.booking.depositpaid.toString()).to.eql(pm.environment.get("Payment"));
});

//check in date matched or not
pm.test("Verify Check in date", function () {
    pm.expect(jsonData.booking.bookingdates.checkin).to.eql(pm.environment.get("CheckIn"));
});

//check out date matched or not
pm.test("Verify Check out date", function () {
    pm.expect(jsonData.booking.bookingdates.checkout).to.eql(pm.environment.get("CheckOut"));
});

//additional needs matched or not
pm.test("Verify additionalneeds", function () {
    pm.expect(jsonData.booking.additionalneeds).to.eql("Breakfast");
});
```



#### Access Token Generate    
```bash   
var tokenData = pm.response.json()

//set token to environment
pm.environment.set("AccessToken", tokenData.token)

//token matched or not
pm.test("Verify TokenID", function () { 
    pm.expect(tokenData.token).to.eql(pm.environment.get('AccessToken'));
});

var StateCode = responseCode.code
//status code matched or not
switch(StateCode){
    case 200:
       pm.test("Verify status code 200", function () {
       console.log('StateCode')
       });
       break;
    case 201:
      pm.test("Verify status code 201", function () {
      console.log('StateCode')
      });
      break;
}
```   



#### Update Booking   
```bash
var jsonData = pm.response.json()
var StateCode = responseCode.code

//status code matched or not
switch(StateCode){
    case 200:
       pm.test("Verify status code 200", function () {
       console.log('StateCode')
       });
       break;
    case 201:
      pm.test("Verify status code 201", function () {
      console.log('StateCode')
      });
      break;
}

//firstname matched or not
pm.test("Verify First name", function () {
    pm.expect(jsonData.firstname).to.eql(pm.environment.get("FirstName"));
});

//lastname matched or not
pm.test("Verify Last name", function () {
    pm.expect(jsonData.lastname).to.eql(pm.environment.get("LastName"));
});

//total price matched or not
pm.test("Verify Total price", function () {
    pm.expect(jsonData.totalprice).to.eql(pm.environment.get("TotalPrice"));
});

//payment matched or not
pm.test("Verify Depositpaid", function () {
    pm.expect(jsonData.depositpaid.toString()).to.eql(pm.environment.get("Payment"));
});

//check in mtached or not
pm.test("Verify Check in date", function () {
    pm.expect(jsonData.bookingdates.checkin).to.eql(pm.environment.get("CheckIn"));
});

//check out matched or not
pm.test("Verify Check out date", function () {
    pm.expect(jsonData.bookingdates.checkout).to.eql(pm.environment.get("CheckOut"));
});

//additional needs matched or not
pm.test("Verify additionalneeds", function () {    
    pm.expect(jsonData.additionalneeds).to.eql("Lunch");
});
```   




#### Delete Booking 
```bash

var StateCode = responseCode.code

//status code matched or not
switch(StateCode){
    case 200:
       pm.test("Verify status code 200", function () {
       console.log('StateCode')
       });
       break;
    case 201:
      pm.test("Verify status code 201", function () {
      console.log('StateCode')
      });
      break;
}
```   

# Create Test Suites   

### Using Newman   


  Newman is a command-line Collection Runner for Postman. It enables you to run and test a Postman Collection directly from the command line.
#### Install Command    
```bash
npm install -g newman    
```
#### Run Command    
- newman run “Path/CollectionName.json” -e Path/EnvironmentName.json
- newman run “Collection Link” -e “Path”/EnvironmentName.json    

#### Create HTML Report  
 
#### Install Command      
```bash
npm install -g newman-reporter-html
```
**or**   
```bash
npm install -g newman-reporter-htmlextra    
```
#### Run Command      
- newman run “Collection Link” -e “Path”/EnvironmentName.json -r cli,html    
**or**    
- newman run “Collection Link” -e “Path”/EnvironmentName.json -r cli,htmlextra    
