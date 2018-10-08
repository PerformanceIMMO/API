# ProviderContacts

<aside class="warning">
	You must be authenticated to use these API.
</aside>

## Get Provider Contacts

### HTTP Request

> HTTP query example :

```shell
curl -XGET \
-H "Cookie: PI_SESSION=..." \
https://base_url/api/v1/providercontacts?range=0-0
```

> HTTP response example :

```http
HTTP/1.1 206 Partial Content
Content-Type: application/json
Content-Range: 0-0/19234
```
```json
{
    "result": [
        {
            "uid": "16fc6e5e-163d-799c-89ef-a764f2090d74",
            "label": "atti nord",
            "phones": [
                "06.71.01.83.65"
            ],
            "fax": [ ],
            "emails": [
                "relation.client@itac-itservices.eu"
            ],
            "active": false,
            "_links": [
                {
                    "rel": "self",
                    "href": "https://base_url/api/v1/providercontacts/16fc6e5e-163d-799c-89ef-a764f2090d74",
                    "method": "GET"
                }
            ]
        
        },    
    ],
    "_links": [
        {
            "rel": "self",
            "href": "https://base_url/api/v1/providercontacts",
            "method": "GET"
        }
    ]
}	
```

**`GET`** `/api/v1/providercontacts`

### Parameters

Name               | In    | Type                                      | Default   | Description
------------------ | ------| ------------------------------------------| ----------| -----------------------------------------------------------------------------------------
range              | query | [Option](#option)[String]                 | 0-100     | range selector for result pagination.<br/> ex: `range=0-19` <br/> startRange should be > endRange
companyuid         | query | [Option](#option)[[SafeUUID](#safeuuid)]  | None      | query matching with one `Company` uid.<br/> ex: `companyuid=company_uid`
agencyuids         | query | Array[[SafeUUID](#safeuuid)]              | [ ]       | query matching with several `agencies` uid.<br/> ex: `agencyuids=agency_uid1,agency_uid2`
providercompanyuid | query | [Option](#option)[[SafeUUID](#safeuuid)]  | None      | query matching with one `ProviderCompany` uid. <br/> `providercompanyuid=company_uid`
patrimonyuids      | query | Array[[SafeUUID](#safeuuid)]              | [ ]       | query matching with several `Patrimony` uid.<br/> ex: `patrimonyuids=patrimony_uid1,patrimony_uid2`
fulltext           | query | [Option](#option)[String]                 | None      | `fulltext` query matching with several terms.<br/> ex: `fulltext=word,other+word`.

### Responses

Http code | Type                                                      | Description
----------| ----------------------------------------------------------| ----------------------------
200       | [ProviderContactResultView](#providercontactresultview)   | All resources's elements are returned.
206       | [ProviderContactResultView](#providercontactresultview)   | Partial Content. See `Content-Range` header for use pagination.
400       | Error                                                     | Bad request, occurs most often when parameters passed are invalid.

## Get a Provider Contact

### HTTP Request

> HTTP query example :

```shell
curl -XGET \
-H "Cookie: PI_SESSION=..." \
https://base_url/api/v1/providercontacts/16fc6e5e-163d-799c-89ef-a764f2090d74
```

> HTTP response example :

```http
HTTP/1.1 200 OK
Content-Type: application/json
```
```json
{
    "uid": "16fc6e5e-163d-799c-89ef-a764f2090d74",
    "label": "atti nord",
    "phones": [
        "0671018362"
    ],
    "fax": [ ],
    "emails": [
        "relation.client@perfimmo.com"
    ],
    "active": false,
    "_links": [
        {
            "rel": "self",
            "href": "https://base_url/api/v1/providercontacts/16fc6e5e-163d-799c-89ef-a764f2090d74",
            "method": "GET"
        }
    ]

}    
```

**`GET`** `/api/v1/providercontacts/:contact_uid`

### Parameters

Name            | In    | Type                                      | Default   | Description
--------------- | ------| ------------------------------------------| ----------| -----------------------------------------------------------------------------------------
contact_uid     | path  | [SafeUUID](#safeuuid)                     |           | uid of the requested `ProviderContact`

### Responses

Http code | Type                                                      | Description
----------| ----------------------------------------------------------| ----------------------------
200       | [ProviderContactDetailedQueryView](#providercontactdetailedqueryview)     | the requested `ProviderContact`
400       | Error                                                     | Bad request, occurs most often when parameters passed are invalid.

### NavigationLinks

Rest Navivation Links represent what it is possible to do with this resource.

These different links below (except `self` that is mandatory) are optional in  
the response because of the specific state of the request done to retrieve this response.

ex: state of the resource, rights of the user performing the request, etc... 

rel                                     | Description                  |
----------------------------------------|------------------------------|
`self`                                  | the resource itself
`stats`                                 | statistics associate with this `ProviderContact`. cf. [Get stats on a Provider Contact](#get-stats-on-a-provider-contact) 
`AssociateProviderContactToAgency`      | cf. [Increment ProviderContact](#increment-providercontact-state)
`DissociateProviderContactToAgency`     | cf. [Increment ProviderContact](#increment-providercontact-state)
`UpdateProviderContact`                 | cf. [Increment ProviderContact](#increment-providercontact-state)
`DisableProviderContact`                | cf. [Increment ProviderContact](#increment-providercontact-state)
`EnableProviderContact`                 | cf. [Increment ProviderContact](#increment-providercontact-state)
       
## Get stats on a Provider Contact

### HTTP Request

> HTTP query example :

```shell
curl -XGET \
-H "Cookie: PI_SESSION=..." \
https://base_url/api/v1/providercontacts/16fc6e5e-163d-799c-89ef-a764f2090d74/stats
```

> HTTP response example :

```http
HTTP/1.1 200 OK
Content-Type: application/json
```
```json
{
    "interventionDelay": [
        {
            "day": "2016-04-29",
            "value": 5090000
        }
    ],
    "missionAcceptedDelay": [
        {
            "day": "2016-04-29",
            "value": 133000
        }
    ],
    "repairDelay": [
        {
        
            "day": "2016-04-29",
            "value": 6590000
        
        }
    ],
    "callBeforeMissionAccepted": [
        {
            "day": "2016-04-29",
            "value": 2
        }
    ],
    "interventionNumber": [
        {
            "day": "2016-04-29",
            "value": 2
        }
    ]
}	
```

**`GET`** `/api/v1/providercontacts/:contact_uid/stats`

### Parameters

Name            | In    | Type                                      | Default   | Description
--------------- | ------| ------------------------------------------| ----------| -----------------------------------------------------------------------------------------
contact_uid     | path  | [SafeUUID](#safeuuid)                     |           | uid of the requested `ProviderContact`
from            | query | [Option](#option)[[LocalDate](#localdate)]| None      | query matching with `from` local date.<br/> ex: `from=2015-07-02`.<br/> if **`from`** but not **`to`** => from **`from`** to **now**
to              | query | [Option](#option)[[LocalDate](#localdate)]| None      | query matching with `to` local date.<br/> ex: `to=2015-07-03`.<br/> if **`to`** but not **`from`** => until **`to`**. **`to`** must be >= **`from`**

### Responses

Http code | Type                                                      | Description
----------| ----------------------------------------------------------| ----------------------------
200       | [ProviderContactStats](#providercontactstats)             | All resources's elements are returned.
400       | Error                                                     | Bad request, occurs most often when parameters passed are invalid.

## Get suggestions for assign ProviderContact

Given a `Patrimony` & referenced incident type, this API provide a restricted list of `ProviderContact` 
able to intervene on this incident for this `Patrimony`.
This list will be sorted like that : <br/>
- first the `ProviderContact`s directly linked with the selected `Patrimony` <br/> 
- after the `ProviderContact`s linked with `Patrimony` by means of its direct link with `Agency` itself linked with this `Patrimony`.                                             

### HTTP Request

> HTTP query example :

```shell
curl -XGET \
-H "Cookie: PI_SESSION=..." \
https://base_url/api/v1/providercontacts/suggest?patrimonyuid=8c12f096-20e6-11ab-8ff7-2c39b4397040&incidenttypeuid=7634c414-8822-e29d-fe2b-0a18b3174369&responsesize=1
```

> HTTP response example :

```http
HTTP/1.1 200 OK
Content-Type: application/json
```
```json
{
    "result": [
        {
            "uid": "16fc6e5e-163d-799c-89ef-a764f2090d74",
            "label": "atti nord",
            "activities": [
            	{
            		"activityUid": "16fc6e5e-163d-799c-89ef-a764f2090d74", 
            		"includedIncidentTypes": ["7634c414-8822-e29d-fe2b-0a18b3174369"]
            	}
            ],
            "isDirectlyLinkedWithPatrimony": true,
            "phones": [
                "06.71.01.83.65"
            ],
            "fax": [ ],
            "emails": [
                "relation.client@perfimmo.com"
            ],
            "active": false
        }    
    ]
}	
```

**`GET`** `/api/v1/providercontacts/suggest`

### Parameters

Name            | In    | Type                                      | Default   | Description
--------------- | ------| ------------------------------------------| ----------| -----------------------------------------------------------------------------------------
patrimonyuid    | query | [SafeUUID](#safeuuid)                     | mandatory | uid of a `Patrimony` 
incidenttypeuid | query | [SafeUUID](#safeuuid)                     | mandatory | uid of an incident type
responsesize    | query | [Option](#option)[Int]                    | 5         | an optional parameter to precise response size (max 100)

### Responses

Http code | Type                                                      | Description
----------| ----------------------------------------------------------| ----------------------------
200       | [ProviderContactSuggestResultView](#providercontactsuggestresultview) | All resources's elements are returned.
400       | Error                                                     | Bad request, occurs most often when parameters passed are invalid.

## Create ProviderContact

> HTTP command example :

```shell
curl -XPOST \                                                                                                        
-H "Cookie: PI_SESSION=..." \
-H "Content-Type: application/json" \
-d {
 "processUid":"8c12f096-20e6-11ab-8ff7-2c39b4397040",
 "aggregateUid":"7634c414-8822-e29d-fe2b-0a18b3174369",
 "date":"2016-02-29T12:03:32+02:00",
 "name":{
    "gender":"Male",
    "firstName":"John",
    "lastName":"Doe",
    "nameType":"CivilName"
 },
 "companyUid":"6ed010a1-7481-4b38-87da-c219fc31ba64",
 "phones":[ "0145123456" ],
 "fax":[],
 "emails":[],
 "commandType":"AddProviderContact"
} \
https://base_url/api/vEvent/providercontacts
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
            "date":"2016-02-29T12:03:32+02:00",
            "name":{
                "gender":"Male",
                "firstName":"John",
                "lastName":"Doe",
                "nameType":"CivilName"
             },
             "phones":[ "0145123456" ],
             "fax":[],
             "emails":[],
             "sentDate":"2016-02-29T12:05:32+02:00",
             "eventType":"ProviderContactAdded"
        },
        {
            "processUid":"8c12f096-20e6-11ab-8ff7-2c39b4397040",
            "aggregateUid":"7634c414-8822-e29d-fe2b-0a18b3174369",
            "date":"2016-02-29",
            "callCenterUid":"16fc6e5e-163d-799c-89ef-a764f2090d74",
            "sentDate":"2016-02-29T12:05:32+02:00",
            "eventType":"ProviderContactAssociatedToCallCenter"
        },
        {
            "processUid": "8c12f096-20e6-11ab-8ff7-2c39b4397040",
            "aggregateUid": "7634c414-8822-e29d-fe2b-0a18b3174369",
            "date": "2016-02-29",
            "companyUid": "6ed010a1-7481-4b38-87da-c219fc31ba64",
            "sentDate": "2016-02-29T12:05:32+02:00",
            "eventType": "ProviderContactAssociatedToCompany"
        }
    ]
}
```

**`POST`** `/api/vEvent/providercontacts`

### Parameters

Name               | In    | Type                                             | Description
------------------ | ------| -------------------------------------------------| -------------
processUid         | body  | [SafeUUID](#safeuuid)                            | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid       | body  | [Option](#option)[[SafeUUID](#safeuuid)]         | the optional uid of the resource created. You can set yourself this uid or let Perfimmo do it for you.
providerCompanyUid | body  | [Option](#option)[[SafeUUID](#safeuuid)]         | if this field is set, this produce an association between `ProviderContact` created & that `ProviderCompany`. 
companyUid         | body  | [SafeUUID](#safeuuid)                            | a `ProviderContact` is a private entity for a given `Company`. 
date               | body  | [DateTime](#datetime)                            | the creation date of this resource
name               | body  | [Name](#name)                                    | the name of the `ProviderContact`
phones             | body  | Array[String]                                    | 
fax                | body  | Array[String]                                    | 
emails             | body  | Array[String]                                    | 
commandType        | body  | Constant                                         | `"AddProviderContact"`

### Responses

Http code | Type                                                              | Description
----------| ------------------------------------------------------------------| ----------------------------
201       | [ProviderContactEventResultView](#providercontacteventresultview) | The `Event`s resulting of this `Command`
400       | [ProviderContactEventError](#providercontacteventerror)           | Bad request, occurs most often when parameters passed are invalid, or if data in command is not coherent.

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
ProviderContactAdded                      | mandatory                         |
ProviderContactAssociatedToCompany        | mandatory                         |
ProviderContactAssociatedWithProviderCompany | optional                       | if field `providerCompanyUid` is setted


## Increment ProviderContact State

> HTTP command example :

```shell
curl -XPATCH \                                                                                                        
-H "Cookie: PI_SESSION=..." \
-H "Content-Type: application/json" \
-d {
    "processUid":"6ed010a1-7481-4b38-87da-c219fc31ba64",
    "agencyUid":"16fc6e5e-163d-799c-89ef-a764f2090d74",
    "date":"2016-02-29",
    "commandType":"AssociateProviderContactToAgency"
 } \
https://base_url/api/vEvent/providercontacts/7634c414-8822-e29d-fe2b-0a18b3174369
```

> HTTP response example :

```http
HTTP/1.1 200 Ok
```
```json
{
    "events":[
        {
            "processUid":"6ed010a1-7481-4b38-87da-c219fc31ba64",
            "aggregateUid":"7634c414-8822-e29d-fe2b-0a18b3174369",
            "date":"2016-02-29",
            "agencyUid":"16fc6e5e-163d-799c-89ef-a764f2090d74",
            "sentDate":"2016-02-29T12:05:32+02:00",
            "eventType":"ProviderContactAssociatedToAgency"
        }    
    ]
}    
```

**`PATCH`** `/api/vEvent/providercontacts/aggregate_uid`

### Parameters

Name            | In    | Type                                                  | Default   | Description
--------------- | ------| ------------------------------------------------------| ----------| -------------
                | body  | [IncrementProviderContact](#incrementprovidercontact) |           | 


### Responses

Http code | Type                                                              | Description
----------| ------------------------------------------------------------------| ----------------------------
200       | [ProviderContactEventResultView](#providercontacteventresultview) | The `Event`s resulting of this `Command`
400       | [ProviderContactEventError](#providercontacteventerror)           | Bad request, occurs most often when parameters passed are invalid, or if data in command is not coherent.