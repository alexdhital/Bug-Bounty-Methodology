# Web Application pentest method

## Basic Enumeration
* Identify Stack/ Language Used
* Identify Server running the application
![](https://i.ibb.co/Q9z0Hww/hehe.png)

* JS Libraries used? Are any of them vulnerable?
* is the application using any kind of WAF? 0xInfection Awesome WAF => https://github.com/0xInfection/Awesome-WAF

## Authentication?
What is authentication done via?
![](https://i.ibb.co/s10kYCS/hehe1.png)

## Objects? (Real World Entities)
Since every application is solving real world problems, ask What are real world entities referred in the application and what are their data type?
For example an application like facebook, whatsapp might have,
***Messaging functionality*** 
* `conversationId`: `Number/String (ID)`
* `participants`: `Array of user objects`
* `messages`: `Array of message objects`
* `lastReadTimestamp`: `Date` 
![](https://i.ibb.co/sRrByBL/hehe2.png)

## Session Establishment
How does the application identify me? How does it identify i am alex and another user is Hari or Administrator?
* Using Cookies?
* JWT?
* Bearer Token?
* Searilized sessions? (java?, php?, .net?, python?)

## Handling Special Characters
How does the application handle special characters in input fields?
![](https://i.ibb.co/28KdjLw/hehe4.png)

* Ask why is it breaking the application? which certain character is breaking the application? why? think in code level
* Able to trigger error messages after fuzzing with special characters?

## CSRF validation
Is csrf token used on crutial functionalities? is it validated or not? Try same csrf token before and after logging out of the application. How does the application reacts?

## CRUD
What CRUD operation is each request doing? GET(READ), POST(CREATE), PATCH(UPDATE), etc. Am i able to manipulate GET to POST, PATCH to DELETE?

## Functionalities Identification
Identify what functionality is the application providing
* Inviting external users?
* Email / Messaging?
* Files Upload?
* Reservation/BOoking?
* Checkout?
* send money?
* sell something?
* Add, delete tasks? schedule tasks? update other member's tasks?
* Edit profile?, edit settings?
* Check, generate report?
* Approve, decline something?

## Multiple User Roles?
Privilege Escalation or functionality use of higher roles possible?
* Admin?
* Normal User?
* Manager?
* Supplier?

## Is API Used?
![](https://i.ibb.co/qxLVH3x/hehe5.png)

## Is CORS implemented?
For this we can utilized burp's search functionality Go to Burp => Search => Access-Control

## Is Websocket used?
Try owasp top 10 bugs on websocket requests as well

## IS captcha used?
Try various ways of bypassing captcha

## What other headers is the application acepting?
Use param miner for this

