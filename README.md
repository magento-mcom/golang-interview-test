# Adobe GoLang Exercise - API Gateway

## Objectives

We would like you to build an API Gateway that would receive POST request with any JSON payload, and it would redirect 
it to a specific Subscriber. For the Subscriber to be able to receive requests it has to be registered into the API Gateway 
beforehand.

_Example_: One Subscriber has been registered into the API Gateway with URL `http://subscriber.dev` and name `sub1`. 
Any POST request made to API Gateway as `http://gateway.dev/sub1` (with body `{"any": "field"}`) should be redirected 
as a new POST to `http://subscriber.dev` with same body.

![api-gateway](https://user-images.githubusercontent.com/1073799/122784380-b81f4200-d2b2-11eb-9701-10205fa91643.png)

### 1. Registering a new subscriber into API Gateway
On each call to this endpoint, API Gateway must:
 * store data about a new subscriber;
 * reply to the caller with the result of the operation.

We have provided to you a ready to use Subscriber that can be spin up with Docker: `docker-compose up -d api`. The URL
of the Subscriber is `http://localhost:8083`. 

⚠️ **IMPORTANT:** This Subscriber is intentionally unstable. Sometimes returns 202 (ACCEPTED) responses and sometimes 5xx errors. 
Try to call several times to `curl -v http://localhost:8083 -d` and you'll see the different responses. We would expect 
from you to implement some kind of retry mechanism inside API Gateway.

**Requirements**:
  * accepts 2 mandatory fields: 
      * a `name` of the subscriber
      * http `url` of the subscriber;
  * the name must be validated and can only contain letters and numbers [a-z0-9];
  * the url must be validated to make sure it's a valid url;

### 2. Sending a request to a subscriber through API Gateway
On each POST call to this endpoint, API Gateway must:
  * forward the request to the provided subscriber;
  * retry the request if the response to the subscriber failed with HTTP 5xx; 
  * reply to the caller with the last response code from the subscriber.

**Requirements**:
 * accepts 2 mandatory fields:
    * a `subscriber` name (_e.g_ `sub1`, remember the Subscriber has to be previously registered in API Gateway);
    * a `body` (json payload, _e.g_ `{"any": "field"}`) that needs to be sent to the subscriber;

## Submission Guidelines
### Should
  * be written in Go;
  * use in-memory storage for the implementation. No need to use persistent storage _e.g_ mysql;
  * be well tested to the level you would expect in a production environment;
  * should contain tests that run with `make test` - our reviewers will run `make test` to assess if your tests pass;
  * should contain `make start` command to run the API Gateway locally;
  * contain documentation that explains your technical decisions, for example, why you chose a particular retry mechanism. The better the documentation, the easier it will be for reviewers to understand and evaluate your project;
  * in the documentation, include curl examples to call endpoints of the application;  

### Should not
  * use a code generator to write the client library;
  * use (copy or otherwise) code from any third party without attribution to complete the exercise, as this will result in the test being rejected;

### How to submit your solution
  * use the original repository as a [template](https://docs.github.com/es/github/creating-cloning-and-archiving-repositories/creating-a-repository-on-github/creating-a-repository-from-a-template) 
    to create your own repository and make it private. **Do not fork the repository;**
  * implement your solution;
  * create documentation for the solution; 
  * invite reviewers to your private repo: rubencougil, AVoskoboinikov, pablomoreno61 (these are github users)
  * send the link to your repository back to the Adobe person of contact;
