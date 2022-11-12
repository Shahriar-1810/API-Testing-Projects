# Content    
- [Introduction](https://github.com/Shahriar-1810/API-Testing-Projects#introduction)    
- [Summary](https://github.com/Shahriar-1810/API-Testing-Projects#summary)      
- [Requirements](https://github.com/Shahriar-1810/API-Testing-Projects#requirements)      

# Introduction
This document explains how to run an API test with Postman on a Book booking website.    

# Summary    
Completed an API test on Book booking site and the link is below.   
https://restful-booker.herokuapp.com/

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
