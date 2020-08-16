![NodeJS RESTful API Microservice Logo](https://github.com/Abdizriel/nodejs-microservice-starter/blob/master/logo.jpg)

# NodeJS RESTful API Microservice Starter v1.2.0
This repository contains a full configuration that runs NodeJS RESTful API Microservice Starter.

[![Build Status](https://secure.travis-ci.org/Abdizriel/nodejs-microservice-starter.png?branch=master)](https://travis-ci.org/Abdizriel/nodejs-microservice-starter)
[![Coverage Status](https://coveralls.io/repos/github/Abdizriel/nodejs-microservice-starter/badge.svg?branch=master)](https://coveralls.io/github/Abdizriel/nodejs-microservice-starter?branch=master)
[![Dependency Status](https://img.shields.io/david/Abdizriel/nodejs-microservice-starter.svg)](https://david-dm.org/Abdizriel/nodejs-microservice-starter)
[![Dev-Dependency Status](https://img.shields.io/david/dev/Abdizriel/nodejs-microservice-starter.svg)](https://david-dm.org/Abdizriel/nodejs-microservice-starter#info=devDependencies)

## Requirements

* [MongoDB](https://www.mongodb.com/download-center "MongoDB")
* [NodeJS](https://nodejs.org/en/download "NodeJS")

## Build for local development

You have to use the following command to start a development server:

```sh
npm run dev
```

See `package.json` for more details.

## Build for staging and production environments

Use following command to build project:

```sh
npm run build
```

Use following command to start project on staging and production environments:

```sh
npm start
```

See `package.json` for more details.

## Tests

Following tests libraries are used for unit/integration tests:
* [MochaJS](https://mochajs.org "MochaJS")
* [SinonJS](http://sinonjs.org "SinonJS")
* [ChaiJS](http://chaijs.com/ "ChaiJS")

Tests are kept next to source with following pattern *.spec.js

Use following command to run tests:

```sh
npm test
```

Use following command to run tests coverage:

```sh
npm run coverage
```

## Docker container

There is available Docker container and Docker Composer if you would like to run many NodeJS Microservices.

Build API Microservice by using following command:

```sh
npm run build
```

Then use following command to build Docker containers:

```sh
docker-compose up -d --build
```

See `Dockerfile` and `docker-compose.yml` for more details.


## Service Formulations Overview
- Vantage view of Service from Database query service point of View (What is a DB Query Service/ Query Service REST API endpoints)

***
Query Service REST API endpoints

The Query Service is a RESTful web service for databases that allows web pages, mobile devices, and scripting languages to query a database using HTTP as the wire protocol and JSON as the data interchange format. Since support for HTTP and JSON is available in most programming languages, applications can use  this service to access a database without requiring a **driver**.
The DB service offers a large number of API's, but most applications will only need to use the  `POST /system/[systemName]/queries` API. This API enables you to submit a query and get back the response in a   single API call.

****

 #### HTTP Headers

    There are several HTTP headers that must be submitted along with each request and some that are optional.

    | Header | Value | Description | Required |
    | ------- | ----- | ----------- | -------- |
    | Authorization | Bearer TOKEN | Contains an access token issued by the Query Service | One of these two is required
    | Authorization | Basic _\[Base64 encoded "username:password"\]_ | Contains the credentials used to access the Teradata Database. The Authorization header is constructed as follows: 1. Username and password are combined into a string "username:password" 2. The resulting string is then encoded using the RFC2045-MIME variant of Base64, except not limited to 76 char/line 3. The authorization method and a space i.e. "Basic " is then put before the encoded string. | One of these two is required
    | Accept | application/[vnd.com](http://vnd.com).teradata.rest-v1.0+json | Instructs the web service that the client wants to use the 1.0 version of the REST API for Teradata Database. Ensures backwards compatibility if the REST API ever changes. | Yes |
    | Accept-Encoding | gzip | Instructs the web service to GZIP compress the response. If omitted, the response will be returned without compression. | No |
    | Content-Type | application/json | Instructs the web service that the request contains JSON data. | Yes |

```bash
    curl --insecure -X POST \
    "$HOST:1443/api/query/systems/prod/queries" \
    -H 'Accept: application/vnd.com.teradata.rest-v1.0+json, */*; q=0.01' \
    -H 'Content-Type: application/json' \
    -H "Authorization: Basic ZGJjOmRiYw==' \
    -d '{"query": "SELECT * FROM dbc.dbcinfo"}'
```

#### Service Response Code
100 Continue
101 Switching Protocols
103 Early Hints
200 OK
201 Created
202 Accepted
203 Non-Authoritative Information
204 No Content
205 Reset Content
206 Partial Content
300 Multiple Choices
301 Moved Permanently
302 Found
303 See Other
304 Not Modified
307 Temporary Redirect
308 Permanent Redirect
400 Bad Request
401 Unauthorized
402 Payment Required
403 Forbidden
404 Not Found
405 Method Not Allowed
406 Not Acceptable
407 Proxy Authentication Required
408 Request Timeout
409 Conflict
410 Gone
411 Length Required
412 Precondition Failed
413 Payload Too Large
414 URI Too Long
415 Unsupported Media Type
416 Range Not Satisfiable
417 Expectation Failed
418 I'm a teapot
422 Unprocessable Entity
425 Too Early
426 Upgrade Required
428 Precondition Required
429 Too Many Requests
431 Request Header Fields Too Large
451 Unavailable For Legal Reasons
500 Internal Server Error
501 Not Implemented
502 Bad Gateway
503 Service Unavailable
504 Gateway Timeout
505 HTTP Version Not Supported
506 Variant Also Negotiates
507 Insufficient Storage
508 Loop Detected
511 Network Authentication Required
