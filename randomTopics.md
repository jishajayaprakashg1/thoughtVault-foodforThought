# Database : Replication v/s Sharding
- To scale Reads go for Replication: here one DB will be primary and rest will be a replica of this primary and all will have the same data.
Easier to implement and revert.
- To scale Writes do sharding: DB is split into multiple small DBs to distribute the load, storage, requests.
Usually sharding is combined with replaction.

# Docker v/s Kubernetes
- Earlier (before docker) : Developer writes the code, installs the dependecnies, tests it,
  prepares deployment artifacts, install all dependencies and requirements with same versions on another server where you want to deploy your application.
- Now (after docker) : dev writes the code, builds a docker image and deploys it as a container.

The application developed in your system will work fine, when you try to run on a different system errors might occur as the env of both systems are different,
you can put your application, configs and all related dependencies in a container,
and run that container in different systems. This is called containerisation.
Docker is used for it.

Docker image is created in docker, it contains the application along with it's, libraries, configs etc.
when the image is run, container starts in which the application runs.

To handle multiple requests, multiple containers will be required which have to be managed, scaled and recover, which is done by kubernetes.
Kubernetes is a container orchestrator.

# CI-CD
Continuous Integration :
- developer pushes the code, pipeline starts to execute, code is build ( is the process of converting human-readable source code (written in languages like 
TypeScript, Java, or C++) into an executable, optimized, or machine-readable format that a computer or runtime environment can actually run.)
- Then the unit/integrations tests are run, broken code must not be promoted, hence, if the tests fail, pipeline fails.
- If tests pass then application is packaged and docker image is created which is stored in the container resgistry.

Continuous Delivery: Sanity is done on staging env(prod like env) and code is deployed into production

The flow: 
- code push
- build
- test
- package
- registry
- staging
- production

# GIT : Global Information Tracker: 
- GIT : is a version control system that tracks your file.
- Online platform like GITHUB/GITLAB is used for collaboration and storing code on cloud.

* Commands to push changes to empty repo in GITHUB, First log in to the GITHUB repo and create an empty repository.

Go to VS code:
git init
git config --global user.name ""
git config --global user.email  ""
git add .
git commit -m "initial commit"
git remote add origin <GitHub project url>
git push -u origin master

git show (show all the history)

git branch
git branch -d branchName (deletes from the local)
git push --delete origin branchName (deletes from the remote)


Older multi purpose command : checkout
git checkout main (switch to main branch)
git checkout -b feature (create and switch to new branch called feature)
git checkout -- file.txt  (restore file)

Newer commands focussing on branch : switch
git switch main
git switch -c feature

git restore file.txt  (to discard changes made to file or maintain the old version of the file)

gitignore.io (to get templates)
.gitignore (will keep the project clean)

reset moves my branch to previous commit
git reset --soft HEAD~1   (move the branch and stage the changes)
git reset --mixed HEAD~1  (move the branch and unstage the changes)
git reset --hard HEAD~1   (move the branch and discard the changes)


SSH: Secure Shell Key :  are two files one has private key and other has public key residing in the local system.
private key : authorises you to push and pull code
public key : authenticates with GITHUB

PAT: Personal Access Token : create for tools that need authentication

Merge : combine changes of your branch with another, basically combines histories
Rebase : add your branch commits on top of another branch commits

Before:
       D ── E   feature
      /
A ── B ── C     main


git switch main
git merge feature
       D ── E
      /       \
A ── B ── C ── M


git switch feature
git rebase main
A ── B ── C ── D' ── E'

# ## Three types of automation
- WEB-UI
- API
- MOBILE

## What is API
*API (Application Programming Interface) : a way of communication between two applications which may differ in tech stack, platforms, etc. where the applciations can be termed as Frontend Backend or Client Server.*

Client (request) --> API (request) --> Server

Client (response) <--- API (response) <--- Server

Search for flights from India to Canada in MakeMyTrip.com (client) 
Get information from various APIs exposed by Servers like British Airways API, Canada Airlines API, etc.
Send the response back to MakeMyTrip.com (client) 

*If you inspect MakeMyTrip.com you can see the API calls in the Network tab.*

## What is API testing
Assessing:
- requests sent by API is producing the desired response
- performance, security and usability/functional tests

Why do we need API testing?
- API ensures that fronend and backend is working fine
- Validation of functionlity
- Integration testing (cart, payment integrationcheck for example)
- Security testing (auth, bank details, etc must not be exposed)
- Performance testing ( on normal days and on big billion sale day the numbe rof requests coming to the app varies)

Advantages of API testing:
- APIs will be ready before UI, so we can test and detect bugs at an earlier stage.
- Also UI is constantly changing so for automation APIs are more stable than UI.
- Analogy: 7 days of putting a feature to prod on clicking an exisitng button on UI:  
5 days for dev and 2 days for testing, you have analysed and found that 3 days is not enough for testing as now th ebutton is not clickable. You can test the API to check that after button click everythng is workign fine or even catch bugs if something has gone wrong.
You will not be blocked as button is disabled also there is faster time to resolution.

### What is HTTP
- Hyper Text Transfer Protocol: communication protocol, works as the request-response protocol between the client and server.
- API uses HTTP for client server communication.
- Two types: HTTP and HTTPS (Hyper Text Transfer Protocol Secure)
- HTTPS: is more secure as the data sent between client and server is encrypted using SSL(Secure Sockets Layer) or TLS(Transport Layer Security), it makes it difficult for unauthorised parties to intercept/read data.

### Microservices
A monolithic architecture builds an application as a single, unified unit with one shared codebase, while a microservices architecture splits the application into small, independent services that communicate via 
APIs, gRPC, websockets, pub/sub, shared DB

Microservcies testing: each microservcie has to be tested for it's functionality and also integration testing between microservcoes is required for E2E functionality validation.

Components are separately developed and deployed.

API testing is very important in microservices:
perf test: performance issue in one service can impact other services
security test: microservices must communicate with each other without exposing sensitive data

### Webservices
are a way for different services / computer systems to communicate and exchange information over the internet.
Standard protocols used : HTTP and SOAP
REST: (Representational State Transfer) : architecture or a type of webservice that uses HTTP to exchange data
RESTFul webservice is a websevrice that has used and implemented REST: Example Twitter API, Facebook API
all webservices are APIs. Response is in xml or json format, hence it is light weight.
It is stateless as it does not store any information.
Endpoint is provided to test
In REST data is directly sent to server

SOAP: Simple Object access Protocol uses XML to exchange structured data.
Example : used in banking applications, stock quoute service offered by financial services
WSDL file is provided to test.
Supports only XML format
It has built in surity features : encryption and digital signatures
In SOAP the data is merged with SOAP standards and then sent to server

XML-RPC: Remote Procedure Call: Example WordPress blog : uses XML to encode it's calls and HTTP as transport mechanism. Example: WordPress blog is used by users to post their blogs from remote clients.

JSON-RPC

### Types of APIs : How the APIs are used
1. open: directly accessed by users: Example: weather API, facebook API, twitter API 
2. internal: secured APIs used internally by an organisation
3. partner: similar to internal but used by partner: example:  pizza APP using Paymnet API as they are partners
4. composite: combination of multiple endpoints in a single API: example: example on paymnt successful, we get notification via whatapp, gmail, text message

### Synchronous vs Asynchronous API
Synchronous: Unless the server responsds the program execution will not continue. for example : unless the payment is successful, order will not be placed.
Asynchronous: call does not block the execution, when the call returns from the server a callback function is executed.

### HTTP methods
Actions perfomed by API:
GET, POST, PUT, PATCH, DELETE
HEAD (similar to GET but only response headers is fetched, no response body), OPTION (what are the methods supported by a URL)
Latest HTTP method standardised in June 2026 : QUERY ( combo of GET and POST)

- Idempotency:  You make a single response again and again and response remains same.
POST is not idempotent: example creation of a user account if you hit 10 times , 10 different data is created.

### HTTP status codes/ response codes
- 1XX : Informational interim responses. They tell the client that the server received the initial part of the request and that the client should wait or continue sending the rest of the data
- 2XX : Success
- 3XX : Redirection, while making payment redirects to bank server
- 4XX : Client side error
- 5XX : Server side error

*Most used status codes*
- 200 OK : PUT, PATCH, GET
- 201 Created : POST
- 204 : DELETE
- 307 : temporary redirect
- 400 bad request : invalid syntax or request, explain with PUT request with missing attributes, or extra attributes not mentioned in contract
- 401 Unauthorized : wrong credentials
- 403 Forbidden : credentials might be correct but you don't have app level permissions
- 404 Not found
- 405 Method not allowed
- 422 unprocessable entity
- 415 unsupported media type indicated in Content-Type
- 500 internal server error

### GRAPHQL
is an open source query language for APIs developed by Facebook to solve over-fetching and under-fetch issues in API.
it is used to get specific information instead of all information.
Analogy : REST API is a buffet while GRAPHQL is A la Carte

Example, if you want to fetch orderNumber: GET returns complete response instead of only orderNumber in response, this is called over fetching of data
if you want user info along with returns info then you have to make two different API calls, this is called under fetching of data.

this results is performance issues. Hence, GRAPHQL was introduced





