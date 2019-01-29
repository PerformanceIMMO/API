# PatrimonyContacts

<aside class="warning">
	You must be authenticated to use these API.
</aside>

## search Patrimony Contacts

### HTTP Request

> HTTP query example :

```shell
curl -XGET \
-H "Cookie: PI_SESSION=..." \
https://base_url/api/v1/patrimonycontacts?range=0-0
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
            "name": {
            	"value":"John Doe",
            	"nameType":"PoorName"
            },
            "linkedWith": [
            	{
            		"patrimonyUid":"e453139a-8f78-4d41-9745-3e3ddfe8adb3",
            		"linkType":"LinkToPatrimonyAsCareTaker"
            	}
            ],
            "contacts": [
                {
                	"phone":"0781780746",
                	"contactInfoType":"Phone"
                }
            ],
            "_links": [
                {
                    "rel": "self",
                    "href": "https://base_url/api/v1/patrimonycontacts/16fc6e5e-163d-799c-89ef-a764f2090d74",
                    "method": "GET"
                }
            ]
        
        },    
    ],
    "_links": [
        {
            "rel": "self",
            "href": "https://base_url/api/v1/patrimonycontacts",
            "method": "GET"
        }
    ]
}	
```

**`GET`** `/api/v1/patrimonycontacts`

### Parameters

Name               | In    | Type                                      | Default   | Description
------------------ | ------| ------------------------------------------| ----------| -----------------------------------------------------------------------------------------
range              | query | [Option](#option)[String]                 | 0-100     | range selector for result pagination.<br/> ex: `range=0-19` <br/> startRange should be > endRange
patrimonyuids      | query | [List](#list)[[SafeUUID](#safeuuid)]      | None      | query matching with several `Patrimony` uid.<br/> ex: `patrimonyuids=patrimony_uid&patrimonyuids=other_uid`
lotuid             | query | [Option](#option)[[SafeUUID](#safeuuid)]  | None      | query matching with one `Lot` uid. <br/> `lotuid=lot_uid`
fulltext           | query | [Option](#option)[String]                 | None      | `fulltext` query matching with several terms.<br/> ex: `fulltext=word,other+word`.

### Responses

Http code | Type                                                      | Description
----------| ----------------------------------------------------------| ----------------------------
200       | [PatrimonyContactResultView](#patrimonycontactresultview)   | All resources's elements are returned.
206       | [PatrimonyContactResultView](#patrimonycontactresultview)   | Partial Content. See `Content-Range` header for use pagination.
400       | Error                                                       | Bad request, occurs most often when parameters passed are invalid.

## Get a Patrimony Contact

### HTTP Request

> HTTP query example :

```shell
curl -XGET \
-H "Cookie: PI_SESSION=..." \
https://base_url/api/v1/patrimonycontacts/16fc6e5e-163d-799c-89ef-a764f2090d74
```

> HTTP response example :

```http
HTTP/1.1 200 OK
Content-Type: application/json
```
```json
{
	"uid":"16fc6e5e-163d-799c-89ef-a764f2090d74",
	"name":{
		"firstName":"Nicolas",
		"lastName":"MARX",
		"gender":"Male",
		"nameType":"CivilName"
	},
	"linkedWith":[
		{
			"lotUid":"e8433445-2921-455b-98dc-0f8a33966f96",
			"linkType":"LinkToLotAsTenant"
		}
	],
	"contacts":[
		{
			"phone":"0781780746",
			"contactInfoType":"Phone"
		},
		{
			"mail":"nicolas.marx@performance-immo.com",
			"contactInfoType":"Mail"
		}
	],
	"_links":[
		{"rel":"self", "href":"https://base_url/api/v1/patrimonycontacts/16fc6e5e-163d-799c-89ef-a764f2090d74","method":"GET"},
		{"rel":"LinkPatrimonyContactWith","href":"https://base_url/api/vEvent/patrimonycontacts/16fc6e5e-163d-799c-89ef-a764f2090d74","method":"PATCH"}
	]
}
   
```

**`GET`** `/api/v1/patrimonycontacts/:contact_uid`

### Parameters

Name            | In    | Type                                      | Default   | Description
--------------- | ------| ------------------------------------------| ----------| -----------------------------------------------------------------------------------------
contact_uid     | path  | [SafeUUID](#safeuuid)                     |           | uid of the requested `PatrimonyContact`

### Responses

Http code | Type                                                      | Description
----------| ----------------------------------------------------------| ----------------------------
200       | [PatrimonyContactQueryView](#patrimonycontactqueryview)   | the requested `PatrimonyContact`
400       | Error                                                     | Bad request, occurs most often when parameters passed are invalid.

### NavigationLinks

Rest Navivation Links represent what it is possible to do with this resource.

These different links below (except `self` that is mandatory) are optional in  
the response because of the specific state of the request done to retrieve this response.

ex: state of the resource, rights of the user performing the request, etc... 

rel                                     | Description                  |
----------------------------------------|------------------------------|
`self`                                  | the resource itself
`LinkPatrimonyContactWith`              | cf. [Increment PatrimonyContact](#increment-patrimonycontact-state)
`RemoveLinkFromPatrimonyContact`        | cf. [Increment PatrimonyContact](#increment-patrimonycontact-state)
`AddContact`                            | cf. [Increment PatrimonyContact](#increment-patrimonycontact-state)
`RemoveContact`                         | cf. [Increment PatrimonyContact](#increment-patrimonycontact-state)
`UpdatePatrimonyContactIdentity`        | cf. [Increment PatrimonyContact](#increment-patrimonycontact-state)

## Create PatrimonyContact

> HTTP command example :

```shell
curl -XPOST \                                                                                                        
-H "Cookie: PI_SESSION=..." \
-H "Content-Type: application/json" \
-d {
"processUid":"aaa029b6-5e56-9be7-2e05-fb6a95f9fa93",
"name": {
    "value":"toto lito",
    "nameType":"PoorName"
},
"contacts": [{
    "phone":"0345673546",
    "contactInfoType":"Phone"
}],
"linkedWithEntities": [{
    "patrimonyUid":"ea29ef55-df08-5a8a-f05a-1fe5e2b42dd4",
    "linkType":"LinkToPatrimonyAsCareTaker"
}],
"commandType":"ReferencePatrimonyContact"
} \
https://base_url/api/vEvent/patrimonycontacts
```

> HTTP response example :

```http
HTTP/1.1 201 Created
```
```json
{
    "events":[
    	{
          "processUid": "aaa029b6-5e56-9be7-2e05-fb6a95f9fa93",
          "aggregateUid": "ab09b38c-1b44-4b38-8eb1-cccc801eeed3",
          "sentDate": "2017-06-20T13:47:30.806Z",
          "name": {
            "value": "toto lito",
            "nameType": "PoorName"
          },
          "contacts": [
            {
              "phone": "0345673546",
              "contactInfoType": "Phone"
            }
          ],
          "eventType": "PatrimonyContactReferenced"
        },
        {
          "processUid": "aaa029b6-5e56-9be7-2e05-fb6a95f9fa93",
          "aggregateUid": "ab09b38c-1b44-4b38-8eb1-cccc801eeed3",
          "sentDate": "2017-06-20T13:47:30.806Z",
          "linkedWith": {
            "patrimonyUid": "ea29ef55-df08-5a8a-f05a-1fe5e2b42dd4",
            "linkAs": "CareTaker",
            "linkType": "LinkToPatrimony"
          },
          "eventType": "PatrimonyContactLinkedWith"
        }    
    ]
}
```

**`POST`** `/api/vEvent/patrimonycontacts`

### Parameters

Name               | In    | Type                                             | Description
------------------ | ------| -------------------------------------------------| -------------
processUid         | body  | [SafeUUID](#safeuuid)                            | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid       | body  | [Option](#option)[[SafeUUID](#safeuuid)]         | the optional uid of the resource created. You can set yourself this uid or let Perfimmo do it for you.
name               | body  | [Name](#name)                                    | the name of the `PatrimonyContact`
address            | body  | [Option](#option)[[PatrimonyContactAddressReference](#patrimonyaddressreference)] | an optional address for this `PatrimonyContact`  
contacts           | body  | [NonEmptyList](#nonemptylist)[[ContactInfo](#contactinfo)] | a non empty list of contact like phone number or email
linkedWithEntities | body  | [NonEmptyList](#nonemptylist)[[PatrimonyContactEntityLink](#patrimonycontactentitylink)] | a non empty list of link to several `Patrimony` or `Lot`entity. 
commandType        | body  | Constant                                         | `"ReferencePatrimonyContact"`

### Responses

Http code | Type                                                              | Description
----------| ------------------------------------------------------------------| ----------------------------
201       | [PatrimonyContactEventResultView](#patrimonycontacteventresultview) | The `Event`s resulting of this `Command`
400       | [PatrimonyContactEventError](#PatrimonyContacteventerror)           | Bad request, occurs most often when parameters passed are invalid, or if data in command is not coherent.


## Increment PatrimonyContact State

> HTTP command example :

```shell
curl -XPATCH \                                                                                                        
-H "Cookie: PI_SESSION=..." \
-H "Content-Type: application/json" \
-d {
    "processUid":"6ed010a1-7481-4b38-87da-c219fc31ba64",
    "contact": {
        "phone":"0456734563",
        "contactInfoType":"Phone"
    },
    "commandType":"AddContact"
 } \
https://base_url/api/vEvent/patrimonycontacts/7634c414-8822-e29d-fe2b-0a18b3174369
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
            "sentDate":"2016-02-29T12:05:32+02:00",
            "contact": {
                "phone":"0456734563",
                "contactInfoType":"Phone"
            },
            "eventType":"ContactAdded"
        }    
    ]
}    
```

**`PATCH`** `/api/vEvent/patrimonycontacts/aggregate_uid`

### Parameters

Name            | In    | Type                                                  | Default   | Description
--------------- | ------| ------------------------------------------------------| ----------| -------------
                | body  | [IncrementPatrimonyContact](#incrementpatrimonycontact) |           | 


### Responses

Http code | Type                                                              | Description
----------| ------------------------------------------------------------------| ----------------------------
200       | [PatrimonyContactEventResultView](#patrimonycontacteventresultview) | The `Event`s resulting of this `Command`
400       | [PatrimonyContactEventError](#patrimonycontacteventerror)           | Bad request, occurs most often when parameters passed are invalid, or if data in command is not coherent.

