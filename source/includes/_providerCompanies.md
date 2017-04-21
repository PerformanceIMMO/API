# ProviderCompanies

<aside class="warning">
	You must be authenticated to use these API.
</aside>

## Get Provider Companies & filter it

### HTTP Request

```shell
curl -XGET \
-H "Cookie: PI_SESSION=..." \
https://base_url/api/v1/providercompanies?range=0-0
```

> HTTP response example :

```http
HTTP/1.1 206 Partial Content
Content-Type: application/json
Content-Range: 0-0/256
```
```json
{
	"result": [
		{
			"uid":"7634c414-8822-e29d-fe2b-0a18b3174369",
			"name":"Performance Immo",
			"siretNumber":"80242504100018"	
		}
	],
	"_links": [
        {
            "rel": "self",
            "href": "https://base_url/api/v1/providercompanies",
            "method": "GET"
        },
        {
            "rel": "ReferenceProviderCompany",
            "href": "https://base_url/api/vEvent/providercompanies",
            "method": "POST"
        }
    ]
}	
```

**`GET`** `/api/v1/providercompanies`

### Parameters

Name            | In    | Type                                      | Default   | Description
--------------- | ------| ------------------------------------------| ----------| -----------------------------------------------------------------------------------------
range           | query | [Option](#option)[String]                 | 0-99      | range selector for result pagination.<br/> ex: `range=0-19` <br/> startRange should be <= endRange
fulltext        | query | [Option](#option)[[String](#localdate)]   | None      | `fulltext` query matching with several terms.<br/> ex: `fulltext=word,other+word`.<br/> This param is incompatible with the others (except for range). <br/> You can filter by name or by siretNumber for example.


### Responses

Http code | Type                                                             | Description
----------| -----------------------------------------------------------------| ----------------------------
200       | [ProviderCompanyResultView](#providercompanyresultview)          | All resources's elements are returned.
206       | [ProviderCompanyResultView](#providercompanyresultview)          | Partial Content. See `Content-Range` header for use pagination.
400       | Error                                                            | Bad request, occurs most often when parameters passed are invalid.

### NavigationLinks

Rest Navivation Links represent what it is possible to do with this resource.

These different links below (except `self` that is mandatory) are optional in  
the response because of the specific state of the request done to retrieve this response.

ex: state of the resource, rights of the user performing the request, etc... 

rel                                     | Description                  |
----------------------------------------|------------------------------|
`self`                                  | the resource itself
`ReferenceProviderCompnay`              | cf. [Reference a Provider Company](#reference-a-provider-company)

## Get a Provider Company

### HTTP Request

> HTTP query example :

```shell
curl -XGET \
-H "Cookie: PI_SESSION=..." \
https://base_url/api/v1/providercompanies/7634c414-8822-e29d-fe2b-0a18b3174369
```

> HTTP response example :

```http
HTTP/1.1 200 OK
Content-Type: application/json
```
```json
{
    "uid": "7634c414-8822-e29d-fe2b-0a18b3174369",
    "name":"Performance Immo",
    "siretNumber":"80242504100018",
    "_links": [
            {
                "rel": "self",
                "href": "https://base_url/api/v1/providercompanies/7634c414-8822-e29d-fe2b-0a18b3174369",
                "method": "GET"
            }
        ]
}    
```

**`GET`** `/api/v1/providercompanies/:providercompany_uid`

### Parameters

Name                | In    | Type                                      | Default   | Description
------------------- | ------| ------------------------------------------| ----------| -----------------------------------------------------------------------------------------
providercompany_uid | path  | [SafeUUID](#safeuuid)             |           | uid of the requested `ProviderCompany`

### Responses

Http code | Type                                                      | Description
----------| ----------------------------------------------------------| ----------------------------
200       | [ProviderCompanyQueryView](#providercompanyqueryview)     | the requested `ProviderCompany`
400       | Error                                                     | Bad request, occurs most often when parameters passed are invalid.

### NavigationLinks

Rest Navivation Links represent what it is possible to do with this resource.

These different links below (except `self` that is mandatory) are optional in  
the response because of the specific state of the request done to retrieve this response.

ex: state of the resource, rights of the user performing the request, etc... 

rel                                     | Description                  |
----------------------------------------|------------------------------|
`self`                                  | the resource itself


## Reference a Provider Company
 
> HTTP command example :
 
```shell
curl -XPOST \                                                                                                        
-H "Cookie: PI_SESSION=..." \
-H "Content-Type: application/json" \
-d '{
"processUid":"8c12f096-20e6-11ab-8ff7-2c39b4397040",
"aggregateUid":"7634c414-8822-e29d-fe2b-0a18b3174369",
"name":"Performance Immo",
"siretNumber":"80242504100018",
"commandType":"ReferenceProviderCompany"
}' \
https://base_url/api/vEvent/providercompanies
```
 
> HTTP response example :
 
```http
HTTP/1.1 201 Created
```
```json
{
	"events":[
    	{
        	"processUid":"8c12f096-20e6-11ab-8ff7-2c39b4397040",
         	"aggregateUid":"7634c414-8822-e29d-fe2b-0a18b3174369",
         	"name":"Performance Immo",
         	"siretNumber":"80242504100018",
         	"sentDate":"2017-04-19T15:11:32+01:00",
         	"eventType":"ProviderCompanyReferenced"
     	}
 	]
}
```
 
**`POST`** `/api/vEvent/providercompanies`

### Parameters

Name            | In    | Type                                             | Default   | Description
--------------- | ------| -------------------------------------------------| ----------| -------------
processUid      | body  | [SafeUUID](#safeuuid)                            |           | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid    | body  | [Option](#option)[[SafeUUID](#safeuuid)]         |           | the optional uid of the resource created. You can set yourself this uid or let Perfimmo do it for you.
name            | body  | String                                           |           | the name of the `ProviderCompany`
siretNumber     | body  | [SIRET](#siret)                                  |           | the siret number of this `ProviderCompany`
commandType     | body  | Constant                                         |           | `"ReferenceProviderCompany"`

### Responses

Http code | Type                                                              | Description
----------| ------------------------------------------------------------------| ----------------------------
201       | [ProviderCompanyEventResultView](#providercompanyeventresultview) | The `Event`s resulting of this `Command`
400       | [ProviderCompanyEventError](#providercompanyeventerror)           | Bad request, occurs most often when parameters passed are invalid, or if data in command is not coherent.