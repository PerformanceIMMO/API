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

Name            | In    | Type                                      | Default   | Description
--------------- | ------| ------------------------------------------| ----------| -----------------------------------------------------------------------------------------
range           | query | [Option](#option)[String]                 | 0-100     | range selector for result pagination.<br/> ex: `range=0-19` <br/> startRange should be > endRange

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
200       | [ProviderContactQueryView](#providercontactqueryview)     | the requested `ProviderContact`
400       | Error                                                     | Bad request, occurs most often when parameters passed are invalid.

### NavigationLinks

Rest Navivation Links represent what it is possible to do with this resource.

These different links below (except `self` that are mandatory) are optional in  
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

## Create ProviderContact

POST         /api/vEvent/providerContacts                                   cqrs.commands.application.controllers.ProvidersContactCommandAPI.create

case class AddProviderContact(processUid: SafeUUID,
                              aggregateUid: SafeUUID,
                              date: DateTime,
                              name: Name,
                              phones: List[String],
                              fax: List[String],
                              emails: List[String],
                              sentDate: DateTime) extends ProviderContactCommand

## Increment ProviderContact State

PATCH        /api/vEvent/providerContacts/:aggregateUid                     cqrs.commands.application.controllers.ProvidersContactCommandAPI.increment(aggregateUid: String)

case class UpdateProviderContact(processUid: SafeUUID,
                                 aggregateUid: SafeUUID,
                                 name: Name,
                                 phones: List[String],
                                 fax: List[String],
                                 emails: List[String],
                                 date: DateTime,
                                 sentDate: DateTime) extends OtherProviderContactCommand

case class DisableProviderContact(processUid: SafeUUID,
                                  aggregateUid: SafeUUID,
                                  date: DateTime,
                                  sentDate: DateTime) extends OtherProviderContactCommand

case class EnableProviderContact(processUid: SafeUUID,
                                 aggregateUid: SafeUUID,
                                 date: DateTime,
                                 sentDate: DateTime) extends OtherProviderContactCommand