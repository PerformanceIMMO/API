# Companies

<aside class="warning">
	You must be authenticated to use these API.
</aside>

## Get all Companies

### HTTP Request

```shell
curl -XGET \
-H "Cookie: PI_SESSION=..." \
https://base_url/api/v1/companies
```

> HTTP response example :

```http
HTTP/1.1 200 OK
Content-Type: application/json
Content-Range: 0-0/1
```
```json
{
	"result": [
		{
			"uid":"6e71965c-e1ea-37e9-fa45-770753dc5147",
			"label":"My Company",
			"isActive":true,
			"holding": {
		        "uid":"1471965c-e1ea-37e9-fa45-770753dc5112",
		        "label":"The holding of this Company"
		    },
		    "companyType":"ClientAccount"
		}
	]	
}	
```

**`GET`** `/api/v1/companies`

### Parameters

Name            | In    | Type                                      | Default   | Description
--------------- | ------| ------------------------------------------| ----------| -------------
range           | query | [Option](#option)[String]                 | 0-100     | range selector for result pagination ex: `range=0-19` (startRange should be > endRange)
holdinguid      | query | [Option](#option)[[SafeUUID](#safeuuid)]  | None      | uid of ClientAccountHolding. If this param is setted, return ClientAccountHolding's subsidiairies list. **This param is incompatible with `companytype`.**
companytype     | query | [Option](#option)[String]                 | None      | If this param is setted to `CallCenter, return CallCenter's list. **This param is incompatible with `holdinguid`.**

### Responses

Http code | Type                        | Description
----------| ----------------------------| ----------------------------
200       | Array[[CompanyQueryView](#companyqueryview)]    | All resources's elements are returned.
206       | Array[[CompanyQueryView](#companyqueryview)]    | Partial Content. See `Content-Range` header for use pagination.
400       | Error                                           | Bad request, occurs most often when parameters passed are invalid.

## Get a specific Company

### HTTP Request

```shell
curl -XGET \
-H "Cookie: PI_SESSION=..." \
https://base_url/api/v1/companies/1471965c-e1ea-37e9-fa45-770753dc5154
```

> HTTP response example :

```http
HTTP/1.1 200 OK
Content-Type: application/json
```
```json
{
	"uid":"1471965c-e1ea-37e9-fa45-770753dc5154",
	"label":"My Holding Company",
	"isActive":true,
    "companyType":"ClientAccountHolding"
}
```

**`GET`** `/api/v1/companies/:company_uid`

### Parameters

Name            | In    | Type                          | Default   | Description
--------------- | ------| ------------------------------| ----------| -------------
company_uid     | path  | [SafeUUID](#safeuuid)         |           | uid of the requested `Company`

### Responses

Http code | Type                | Description
----------| --------------------| ----------------------------
200       | [CompanyQueryView](#companyqueryview)   | The `Company` requested 
400       | Error                                   | Bad request, occurs most often when parameters passed are invalid.

## Get Agencies of a Company

```shell
curl -XGET \
-H "Cookie: PI_SESSION=..." \
https://base_url/api/v1/companies/1471965c-e1ea-37e9-fa45-770753dc5154/agencies?range=0-0
```

> HTTP response example :

```http
HTTP/1.1 206 Partial Content
Content-Type: application/json
Content-Range: 0-0/2
```
```json
{
	"result": [
		{
			"uid":"6e71965c-e1ea-37e9-fa45-770753dc5147",
			"label":"My Company",
			"isActive":true,
			"holding": {
		        "uid":"1471965c-e1ea-37e9-fa45-770753dc5112",
		        "label":"The holding of this Company"
		    },
		    "companyType":"ClientAccount"
		}
	]	
}	
```

**`GET`** `/api/v1/companies/:company_uid/agencies`

### Parameters

Name            | In    | Type                          | Default   | Description
--------------- | ------| ------------------------------| ----------| -------------
company_uid     | path  | [SafeUUID](#safeuuid)         |           | uid of the requested `Company`
range           | query | [Option](#option)[String]     | 0-100     | range selector for result pagination ex: `range=0-19` (startRange should be > endRange)
active          | query | [Option](#option)[Boolean]    | None      | parameter to select **all**, only **active** or only **inactive** agencies

### Responses

Http code | Type                                        | Description
----------| --------------------------------------------| ----------------------------
200       | Array[[AgencyQueryView](#agencyqueryview)]  | All resources's elements are returned.
206       | Array[[AgencyQueryView](#agencyqueryview)]  | Partial Content. See `Content-Range` header for use pagination.
400       | Error                                       | Bad request, occurs most often when parameters passed are invalid.

## Get Users of a Company

```shell
curl -XGET \
-H "Cookie: PI_SESSION=..." \
https://base_url/api/v1/companies/1471965c-e1ea-37e9-fa45-770753dc5154/users
```

> HTTP response example :

```http
HTTP/1.1 200 OK
Content-Type: application/json
Content-Range: 0-0/1
```

```json
{
    "result": [
		{
			"uid": "d5c48f2f-2bcc-40ff-9a5c-4ba5d33419df",
			"login": "john.doe@performance-immo.com",
			"company": {
			    "uid": "1471965c-e1ea-37e9-fa45-770753dc5154",
			    "label": "My Company"
			},
			"managedAgencies": [
		        {
		            "uid": "17d706c1-7844-00f5-a4a4-f1afa1975184",
		            "label": "My Agency"
		        }
			],
		    "firstName": "John",
		    "lastName": "Doe",
		    "userType": "executive"
		}    
    ]
}	
```

**`GET`** `/api/v1/companies/:company_uid/users`

### Parameters

Name            | In    | Type                          | Default   | Description
--------------- | ------| ------------------------------| ----------| -------------
company_uid     | path  | [SafeUUID](#safeuuid)         |           | uid of the requested `Company`
range           | query | [Option](#option)[String]     | 0-100     | range selector for result pagination ex: `range=0-19` (startRange should be > endRange)

### Responses

Http code | Type                                        | Description
----------| --------------------------------------------| ----------------------------
200       | Array[[UserQueryView](#userqueryview)]      | All resources's elements are returned.
206       | Array[[UserQueryView](#userqueryview)]      | Partial Content. See `Content-Range` header for use pagination.
400       | Error                                       | Bad request, occurs most often when parameters passed are invalid.

## Get subsidiaries of a Company

> HTTP query example :

```shell
curl -XGET \
-H "Cookie: PI_SESSION=..." \
https://base_url/api/v1/companies/1471965c-e1ea-37e9-fa45-770753dc5154/subsidiaries
```

> HTTP response example :

```http
HTTP/1.1 200 OK
Content-Type: application/json
Content-Range: 0-0/1
```
```json
{
	"result": [
		{
			"uid":"6e71965c-e1ea-37e9-fa45-770753dc5147",
			"label":"My Company",
			"isActive":true,
			"holding": {
		        "uid":"1471965c-e1ea-37e9-fa45-770753dc5112",
		        "label":"The holding of this Company"
		    },
		    "companyType":"ClientAccount"
		}
	]	
}	
```

<aside class="notice">
	If the company requested is not a ClientAccountHolding, the API will return empty result [].
</aside>

**`GET`** `/api/v1/companies/:company_uid/subsidiaries`

### Parameters

Name            | In    | Type                          | Default   | Description
--------------- | ------| ------------------------------| ----------| -------------
company_uid     | path  | [SafeUUID](#safeuuid)         |           | uid of the requested `Company`
range           | query | [Option](#option)[String]     | 0-100     | range selector for result pagination ex: `range=0-19` (startRange should be > endRange)

### Responses

Http code | Type                                        | Description
----------| --------------------------------------------| ----------------------------
200       | Array[[CompanyQueryView](#companyqueryview)]| All resources's elements are returned.
206       | Array[[CompanyQueryView](#companyqueryview)]| Partial Content. See `Content-Range` header for use pagination.
400       | Error                                       | Bad request, occurs most often when parameters passed are invalid.

## Create Company

> HTTP query example :

```shell
curl -XPOST \                                                                                                        
-H "Cookie: PI_SESSION=..." \
-H "Content-Type: application/json" \
-d {
 "processUid":"8c12f096-20e6-11ab-8ff7-2c39b4397040",
 "callCenterReference":"b60521f2-cc1a-a4cf-5ba8-9510eeaf2d32",
 "name":"MyClientAccount",
 "createdDate":"2016-06-27",
 "commandType":"CreateClientAccount"
} \
https://base_url/api/vEvent/companies
```

> HTTP response example :

```http
HTTP/1.1 201 Created
```

**`POST`** `/api/vEvent/companies`

### Parameters

Name            | In    | Type                                         | Default   | Description
--------------- | ------| ---------------------------------------------| ----------| -------------
companyCommand  | body  | [CreateCompany](#createcompany)              |           | the event for create a Company


### Responses

Http code | Type                                        | Description
----------| --------------------------------------------| ----------------------------
201       | [CompanyEventResultView](#companyeventresultview) | The `Company` is created. Return the `Event`s resulting of this successful `Command`.
400       | [CompanyEventError](#companyeventerror)     | Bad request, occurs most often when parameters passed are invalid, or if data in command is not coherent.


## Increment Company State

> HTTP query example :

```shell
curl -XPATCH \                                                                                                        
-H "Cookie: PI_SESSION=..." \
-H "Content-Type: application/json" \
-d {
 "processUid":"8c12f096-20e6-11ab-8ff7-2c39b4397040",
 "createdDate":"2016-06-27",
 "commandType":"CancelCompany"
} \
https://base_url/api/vEvent/companies/1d178826-76dc-cd04-e174-346ba60eedad
```

> HTTP response example :

```http
HTTP/1.1 200 OK
```

**`PATCH`** `/api/vEvent/companies/company_uid`

### Parameters

Name            | In    | Type                                             | Default   | Description
--------------- | ------| -------------------------------------------------| ----------| -------------
company_uid     | query | [SafeUUID](#safeuuid)                            |           | the uid of the `Company`
companyCommand  | body  | [IncrementCompany](#incrementcompany)            |           | the `Command` for increment a `Company` state


### Responses

Http code | Type                                        | Description
----------| --------------------------------------------| ----------------------------
200       | String                                      | The `Command` is a success
400       | [CompanyEventError](#companyeventerror)     | Bad request, occurs most often when parameters passed are invalid, or if data in command is not coherent.

## Create Agency in Company

> HTTP command example :

```shell
curl -XPOST \                                                                                                        
-H "Cookie: PI_SESSION=..." \
-H "Content-Type: application/json" \
-d {
 "processUid":"8c12f096-20e6-11ab-8ff7-2c39b4397040",
 "createdDate":"2016-06-27",
 "agency":{
	"agencyUid":"4b4c3d2c-a828-ee38-de31-61ce0cd589e1",
	"name":"My Agency Name",
	"extName":"Name to display to client",
	"address":{
		"number":"12",
        "street":"Rue de la performance",
        "zipCode":"75001",
        "city":"Paris"
	},
	"phones": ["0603245678"],
	"fax": "0123784590",
	"emails": ["myagency@performance-immo.com"]
 },
 "commandType":"CreateAgency"
} \
https://base_url/api/vEvent/companies/1d178826-76dc-cd04-e174-346ba60eedad
```

> HTTP response example :

```http
HTTP/1.1 201 Created
```

**`POST`** `/api/vEvent/companies/company_uid/agencies`

### Parameters

Name            | In    | Type                                             | Default   | Description
--------------- | ------| -------------------------------------------------| ----------| -------------
company_uid     | query | [SafeUUID](#safeuuid)                            |           | the uid of the `Company` for which you want to create this `Agency`
agencyCommand   | body  | [CreateAgency](#createagency)                    |           | the `Command` for create an `Agency`


### Responses

Http code | Type                                        | Description
----------| --------------------------------------------| ----------------------------
200       | String                                      | The `Command` is a success
400       | [CompanyEventError](#companyeventerror)     | Bad request, occurs most often when parameters passed are invalid, or if data in command is not coherent.

## Increment Agency

> HTTP command example :

```shell
curl -XPATCH \                                                                                                        
-H "Cookie: PI_SESSION=..." \
-H "Content-Type: application/json" \
-d {
	"processUid":"6ed010a1-7481-4b38-87da-c219fc31ba64",
	"deletedDate":"2016-06-28",
	"agencyUid":"7634c414-8822-e29d-fe2b-0a18b3174369",
	"commandType":"DeleteAgency"
} \
https://base_url/api/vEvent/companies/1d178826-76dc-cd04-e174-346ba60eedad/agencies/de4ef45f-26ed-562c-801d-896ef0e19311
```

> HTTP response example :

```http
HTTP/1.1 200 Ok
```

**`PATCH`** `/api/vEvent/companies/company_uid/agencies/agency_uid`

### Parameters

Name            | In    | Type                                             | Default   | Description
--------------- | ------| -------------------------------------------------| ----------| -------------
company_uid     | query | [SafeUUID](#safeuuid)                            |           | the uid of the `Company` wherein the `Agency` is
agency_uid      | query | [SafeUUID](#safeuuid)                            |           | the uid of the `Agency` incremented
agencyCommand   | body  | [IncrementAgency](#incrementagency)              |           | the event for create a Company


### Responses

Http code | Type                                        | Description
----------| --------------------------------------------| ----------------------------
200       | String                                      | The `Command` is a success
400       | [CompanyEventError](#companyeventerror)     | Bad request, occurs most often when parameters passed are invalid, or if data in command is not coherent.

