# REST API Design

## Contents

1) [API Basics](#id-1)
2) [REST Basics](#id-2)
3) [HTTP Verbs](#id-3)
4) [URL Structure](#id-4)
5) [](#id-5)

<div id="id-1"></div>

### 1) API Basics


### API Types

- OS api —> os exposes apis, used by apps (Ex win32 api)


- Library Api -> libraries in same app talks to each other   using same process not over network


- Remote api -> two remote components talk each other over network using proxy. This proxy contains all data like network protocol, nw address, methods, signatures, authorisation to access the target component.  This proxy can access data from target component using proprietary protocol. This only works if both are of same platform ( both in python) wont work if one in. Net and one in python.  Ex Java RMI, . Net remoting


- Web Api ->  Standard protocol, two apps or components can be any platform or os. Communicate over internet

***

#### Importance of API

- For UI  — for apps meant for both web and mobile .  For web clients built using SPA single page application. (React or angular which are independent from server)
- For Reach — other apps can use your api
- Monetize — charge to access api

***

#### Web API Types

ApI should be easy to understand and Consistent

Web Api types differentiated by 

- Request format — json or xml
- Request Content — content in request
- Response format
- Response content

Types

- **SOAP**

    ( simple object access protocol )

    1998 for microsoft, xml based. RPC style remote procedure call.  Outdated tech


- **REST**

    Representational state transfer
    
    2000 by Roy fielding
    
    Url + json based
    
    Message style not calling specific method like soap
    
    De facto standard api today


- **GraphQL**

    2012 by facebook
    
    Flexible querying like specific field
    
    Json in and out  request and response is json
    
    Tough to develop, 


- **gRPC**

    By google in 2015
    
    Using HTTP/2 allows 2 way streaming duplex server too can send to client
    
    Uses protobuf instead of jaon or xml. 
    
    Bi directional. High performance. Not widely used yet. Need special libraries at both ends.


- **R**


***
***

<div id="id-2"></div>

### 2) REST Basics


Rest api enables transfer of representation of a resource’s state

Client, request for resource’s state to server

State means current resource properties or result of some action on resource



**Structure of API**

    Url -> location of resource + parameter
    
    Header -> metadata like user agent, authorisation
    
    Body -> content of request (optional)


![API Structure](/Images/Backend_Design_Notes/REST_API_Design/api_structure.png)


**Structure of API Response**

    Status code
    
    Header - metadata
    
    Body

Response can be json. It can also be xml or html (rare)

![Response structure](/Images/Backend_Design_Notes/REST_API_Design/response_structure.png)


***
***


<div id="id-3"></div>

### 3) HTTP Verbs

Action to be performed - CRUD (Create read update delete) a resource

Rest uses already existing http standard

***

**GET** 

Default verb of browsers address bar

Get request Don't need body

Go to browser. Press f15 or inspect and select network. Now go to google site. Click on `http://google.com` in inspect and see api details like method, status, header

If api request url is too long more than 1000 like  then get 414 request uri too large status error

Too many parameters also fails get like 200 parameters. Such case use post. 

***

#### Post

To add resource

Should need body

No query parameters (POST /api/entity?company=6) 

Same url can be used for get and post and put and they will be different actually

You can type json body in body raw text also

***

#### PUT

Update 

No query params

Need body

Similar like post

Returns response json

Put is idempotent. Means no matter how many times we execute same result

Post is not idempotent because no of entities is identical to no of post request i send

Multiple put request doest create redundant data

***

#### Delete verb

No body    only method, url, header

Returns a response json mesage

***

#### Rarely used verbs

#### PATCH

Similar to put, but with partial updates

No need to send full entity

***

#### HEAD

Same as get, but without body in response

Used to precheck if an entity exists. Returns only status code

***

#### OPTIONS

describes the available verbs for the url

```
curl -X OPTIONS http://example.org -i

HTTP/1.1 204 No Content
Allow: OPTIONS, GET, HEAD, POST
```

| Verb   | Body | Params in… |
|--------|------|------------|
| GET    | no   | Url        |
| POST   | Yes  | Body       |
| PUT    | Yes  | Body       |
| DELETE | No   | Url        |


***
***

<div id="id-4"></div>

### 4) URL Structure

Url should be self-explanatory, consistent across the api, predictable(other apis guessable) 

#### Domain name

First part of url

Contains FQDN fully qualified domain name 
 or server name. Better to have api word in fqdn

`https://api.myapp.com`

***

#### The API word

If domain has no api, include after that

`https://www.myapp.com/api`

Shows this is for api not website

Or include instead in domain name like google `https://language.googleapis.com/v1/documents:analyzeEntities`

***

#### Version

Natural number

No decimal

Could be prefixed with v

`Domain/api/v1`

*** 

#### Entity

Rest deals with resources or entity. Not method or action

Should be one word

Never a verb (do that, save,). Use only nouns

`/api/v1/order`

`/api/v1/travel`

`/api/v1/order`

***

#### ID parameter

When dealing with specific entity

Relavant for get, put, delete

Not for post —  no id for new post

`/api/v1/order/17`

***

#### Sub Entity

Used for accessing entities that are dependent on other entities

Ex get all items of order id 17

Mistake  `/api/v1/ItemsInOrder/17`  Dont do this

Correct  `api/v1/order/17/items`

Url is hierarchical and easy to understand

Same goes for sub-sub-entity

***

#### Query Parameters

Used to query the entities in GET method

Come at end of url after? 

Concatenated with &

`/api/v1/orders?fromDate=12/12/2018&toDate=2/2/2019`

![Query vs Id parameter](/Images/Backend_Design_Notes/REST_API_Design/queryVsId.png)


Singular or plural entities in api

Best practice  - Use singular for api returning single entity `/api/v1/order/17`

Use plural for api returning multiple entities `/api/v1/orders?user=john`

```
Question

which url to use for adding grades to student no 15? 

Correct → POST api/v1/student/15/grades

Wrong → POST api/v1/grades?student=15
```

![API Example](/Images/Backend_Design_Notes/REST_API_Design/api_example.png)

***
***

<div id="id-5"></div>

5) 