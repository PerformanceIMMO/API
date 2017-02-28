# Tickets

<aside class="warning">
	You must be authenticated to use these API.
</aside>

## Get tickets and filter it

### HTTP Request

```shell
curl -XGET \
-H "Cookie: PI_SESSION=..." \
https://base_url/api/v1/tickets?range=0-0
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
            "uid": "17ab7b5b-b7ca-18f6-d5f3-3dfbcbaee1a2",
            "ref": "REF20160526",
            "agencies": [
                {
                    "uid": "17d706c1-7844-00f5-a4a4-f1afa1975184",
                    "name": "My Agency"
                }
            ],    
            "patrimony": {
                "uid": "17ab7b5b-b7ca-18f6-d5f3-3dfbcbaee1a2", 
                "name": "My patrimony"
            },
            "status": "CLOSED",
            "state": {
                "value": "TicketClosed",
                "date": "2016-05-26T08:18:52.000Z"
            },
            "created": "2016-05-26T08:14:44.000Z",
            "updated": "2016-05-26T08:18:52.000Z",
            "closed": "2016-05-26T08:18:52.000Z",
            "callPurpose": "Chauffage  / Chauffage HS",
            "provider": {
                "name": "Mr Provider",
                "phones": ["0146304312"],
                "fax": [],
                "emails": []
            },
            "caller": {
                "name": "John Doe",
                "medium": {
                    "mediumType": "PHONE",
                    "identifier": "0601020304"
                }
            },
            "address": {
                "street": "8 rue des batignolles",
                "complement": "Batiment C",
                "zipCode": "75001",
                "city": "PARIS"
            }
        }
	]	
}	
```

**`GET`** `/api/v1/tickets`

### Parameters

Name            | In    | Type                                      | Default   | Description
--------------- | ------| ------------------------------------------| ----------| -----------------------------------------------------------------------------------------
range           | query | [Option](#option)[String]                 | 0-99      | range selector for result pagination.<br/> ex: `range=0-19` <br/> startRange should be <= endRange
agency          | query | [Option](#option)[[SafeUUID](#safeuuid)]  | None      | query matching with several `agencies` uid.<br/> ex: `agency=agency_uid1,agency_uid2`
status          | query | [Option](#option)[ENUM]                   | None      | query matching with `status` { OPENED or CLOSED }.<br/> ex: `status=OPENED`
location        | query | [Option](#option)[String]                 | None      | query matching with several `locations`.<br/> ex: `location=paris,marseille,toulouse`
from            | query | [Option](#option)[[LocalDate](#localdate)]| None      | query matching with `from` local date.<br/> ex: `from=2015-07-02`.<br/> if **`from`** but not **`to`** => from **`from`** to **now**
to              | query | [Option](#option)[[LocalDate](#localdate)]| None      | query matching with `to` local date.<br/> ex: `to=2015-07-03`.<br/> if **`to`** but not **`from`** => until **`to`**. **`to`** must be >= **`from`**
callpurpose     | query | [Option](#option)[String]                 | None      | query matching with several `callpurpose`.<br/> ex: `callpurpose=one,two,three`
activeproviders | query | [Option](#option)[String]                 | None      | query matching with several active provider contacts uid.<br/> ex: `activeproviders=provider_uid1,provider_uid2`
fulltext        | query | [Option](#option)[[String](#localdate)]   | None      | `fulltext` query matching with several terms.<br/> ex: `fulltext=word,other+word`.<br/> This param is incompatible with the others (except for range).


### Responses

Http code | Type                                          | Description
----------| ----------------------------------------------| ----------------------------
200       | [TicketResultView](#ticketresultview)          | All resources's elements are returned.
206       | [TicketResultView](#ticketresultview)          | Partial Content. See `Content-Range` header for use pagination.
400       | Error                                         | Bad request, occurs most often when parameters passed are invalid.


## Export bulk tickets

### HTTP Request

```shell
curl -XGET \
-H "Cookie: PI_SESSION=..." \
https://base_url/api/v1/tickets/export
```

> HTTP response example :

```http
HTTP/1.1 206 Partial Content
Content-Type: application/json
Content-Range: 0-19999/80000
```
```json
{
	"result": [
        {
            "uid": "ebf5b908-dc8d-cd22-02f8-8dc9bfc8c345",
            "ref": "20163000er4",
            "agencies": [
                {
                    "uid": "7yccba5b-25c6-153f-2feb-7aef9e509123",
                    "name": "Agence du Nord"
                }
            ],
            "patrimony": {
                "uid": "f178e729-3286-74d1-ab19-c8539d1dc741",
                "name": "ZER319"
            },
            "status": "OPENED",
            "state": {
                "value": "MissionAccepted",
                "date": "2016-11-09T11:44:48.000Z"
            },
            "created": "2016-11-09T11:42:30.000Z",
            "updated": "2016-11-09T11:45:00.000Z",
            "callPurpose": "froid alimentaire",
            "request": "MEUBLE CHARCUTERIE TRAD.",
            "provider": {
                "uid": "b1dbc546-48bd-f49c-b76f-5028426d5321",
                "name": "chauffagiste Raymond & Fils",
                "phones": [
                    "0146306552",
                    "0345632753"
                ],
                "fax": [ ],
                "emails": [
                    "john.doe@unknown.com"
                ]
            },
            "caller": {
                "name": "email DI",
                "medium": {
                    "mediumType": "PHONE",
                    "identifier": "0654675432"
                }
            },
            "address": {
                "street": "zi saint hermentaire",
                "zipCode": "83300",
                "city": "DRAGUIGNAN"
            },
            "freeCommentaries": [
                {
                   "date":"2017-02-28T15:35:00+01:00", 
                   "message":"le message"
                }
            ],
            "additionalDataz": {
                "Code magasin": "OT456",
                "Heure réception OT": "12:41:07",
                "OT urgente": "NON"
            }
        }
    ]	
}	
```

**`GET`** `/api/v1/tickets/export`

### Parameters

Name            | In    | Type                                      | Default   | Description
--------------- | ------| ------------------------------------------| ----------| -----------------------------------------------------------------------------------------
range           | query | [Option](#option)[String]                 | 0-19999   | range selector for result pagination.<br/> ex: `range=0-10000` <br/> startRange should be <= endRange
agency          | query | [Option](#option)[[SafeUUID](#safeuuid)]  | None      | query matching with several `agencies` uid.<br/> ex: `agency=agency_uid1,agency_uid2`
status          | query | [Option](#option)[ENUM]                   | None      | query matching with `status` { OPENED or CLOSED }.<br/> ex: `status=OPENED`
location        | query | [Option](#option)[String]                 | None      | query matching with several `locations`.<br/> ex: `location=paris,marseille,toulouse`
from            | query | [Option](#option)[[LocalDate](#localdate)]| None      | query matching with `from` local date.<br/> ex: `from=2015-07-02`.<br/> if **`from`** but not **`to`** => from **`from`** to **now**
to              | query | [Option](#option)[[LocalDate](#localdate)]| None      | query matching with `to` local date.<br/> ex: `to=2015-07-03`.<br/> if **`to`** but not **`from`** => until **`to`**. **`to`** must be >= **`from`**
callpurpose     | query | [Option](#option)[String]                 | None      | query matching with several `callpurpose`.<br/> ex: `callpurpose=one,two,three`
activeproviders | query | [Option](#option)[String]                 | None      | query matching with several active provider contacts uid.<br/> ex: `activeproviders=provider_uid1,provider_uid2`
fulltext        | query | [Option](#option)[[String](#localdate)]   | None      | `fulltext` query matching with several terms.<br/> ex: `fulltext=word,other+word`.

### Responses

Http code | Type                                          | Description
----------| ----------------------------------------------| ----------------------------
200       | [TicketExportView](#ticketexportview)         | All resources's elements are returned.
206       | [TicketExportView](#ticketexportview)         | Partial Content. See `Content-Range` header for use pagination.
400       | Error                                         | Bad request, occurs most often when parameters passed are invalid.


## Get stats on tickets

### HTTP Request

```shell
curl -XGET \
-H "Cookie: PI_SESSION=..." \
https://base_url/api/v1/tickets
```

> HTTP response example :

```http
HTTP/1.1 200 OK
Content-Type: application/json
```
```json
{
    "newTickets": {
        "lastSevenDays": 67,
        "lastMonth": 12,
        "currentMonth": 138
    },
    "ticketCreationFrequency": {
        "byDay": 1
    }
}	
```

**`GET`** `/api/v1/tickets/stats`

### Parameters

Name            | In    | Type                                      | Default   | Description
--------------- | ------| ------------------------------------------| ----------| -----------------------------------------------------------------------------------------
range           | query | [Option](#option)[String]                 | 0-99      | range selector for result pagination.<br/> ex: `range=0-19` <br/> startRange should be > endRange
agency          | query | [Option](#option)[[SafeUUID](#safeuuid)]  | None      | query matching with several `agencies` uid.<br/> ex: `agency=agency_uid1,agency_uid2`
status          | query | [Option](#option)[ENUM]                   | None      | query matching with `status` { OPENED or CLOSED }.<br/> ex: `status=OPENED`
location        | query | [Option](#option)[String]                 | None      | query matching with several `locations`.<br/> ex: `location=paris,marseille,toulouse`
from            | query | [Option](#option)[[LocalDate](#localdate)]| None      | query matching with `from` local date.<br/> ex: `from=2015-07-02`.<br/> if **`from`** but not **`to`** => from **`from`** to **now**
to              | query | [Option](#option)[[LocalDate](#localdate)]| None      | query matching with `to` local date.<br/> ex: `to=2015-07-03`.<br/> if **`to`** but not **`from`** => until **`to`**. **`to`** must be >= **`from`**
callpurpose     | query | [Option](#option)[String]                 | None      | query matching with several `callpurpose`.<br/> ex: `callpurpose=one,two,three`
fulltext        | query | [Option](#option)[[String](#localdate)]   | None      | `fulltext` query matching with several terms.<br/> ex: `fulltext=word,other+word`.<br/> This param is incompatible with the others (except for range).

### Responses

Http code | Type                        | Description
----------| ----------------------------| ----------------------------
200       | [TicketStats](#ticketstats) | All resources's elements are returned.
400       | Error                       | Bad request, occurs most often when parameters passed are invalid.

## Get a ticket

### HTTP Request

```shell
curl -XGET \
-H "Cookie: PI_SESSION=..." \
https://base_url/api/v1/tickets/17ab7b5b-b7ca-18f6-d5f3-3dfbcbaee1a2
```

> HTTP response example :

```http
HTTP/1.1 200 OK
Content-Type: application/json
```
```json
{
    "uid": "17ab7b5b-b7ca-18f6-d5f3-3dfbcbaee1a2",
    "ref": "REF20160526",
    "agencies": [
        {
            "uid": "17d706c1-7844-00f5-a4a4-f1afa1975184",
            "name": "My Agency"
        }
    ],    
    "patrimony": {
        "uid": "17ab7b5b-b7ca-18f6-d5f3-3dfbcbaee1a2", 
        "name": "My patrimony"
    },
    "status": "CLOSED",
    "state": {
        "value": "TicketClosed",
        "date": "2016-05-26T08:18:52.000Z"
    },
    "request": "water leak in my apartment",
    "created": "2016-05-26T08:14:44.000Z",
    "updated": "2016-05-26T08:18:52.000Z",
    "closed": "2016-05-26T08:18:52.000Z",
    "callPurpose": "Chauffage  / Chauffage HS",
    "caller": {
        "name": "john Doe",
        "medium": {
            "mediumType": "PHONE",
            "identifier": "0601020304"
        }
    },
    "provider": {
        "name": "Mr Provider",
        "phones": ["0146304312"],
        "fax": [],
        "emails": []
    },
    "address": {
        "street": "8 rue des batignolles",
        "complement": "Batiment C",
        "zipCode": "75001",
        "city": "PARIS"
    },
    "journal": [
        {
            "day": "2016-05-26",
            "events": [
                {
                    "eventName": "TicketUpdated",
                    "date": "2016-05-26T08:16:06.000Z",
                    "data": { }
                },
                {
                    "eventName": "InterventionFinished",
                    "date": "2016-05-26T08:18:00.000Z",
                    "data": { }
                },
                {
                    "eventName": "CallEmittedTo",
                    "date": "2016-05-26T08:18:30.000Z",
                    "data": {
                        "called": "Mr Provider",
                        "medium": "PHONE",
                        "identifier": "0146304312"
                    }
                },
                {
                    "eventName": "TicketClosed",
                    "date": "2016-05-26T08:18:52.000Z",
                    "data": { }
                }
            ]
        }
    ],
    "additionalDataz": {
        "localisation_urgence": "Cet incident a été détecté comme urgent",
        "tel_contact": "0141221835",
        "degres_urgence": "Cet incident a été détecté comme étant situé dans les parties communes",
        "nom_contact": "Godo",
        "reponse_urgence": "Nous déclenchons une intervention auprès d'un prestataire spécialisé. Nous vous recontactons rapidement afin de vous préciser le nom du prestataire et l'heure d'intervention prévisionnelle"
    },
    "callCenterReactionTime": 82000,
    "interventionResponseTime": 196000
}
```

**`GET`** `/api/v1/tickets/:ticket_uid`

### Parameters

Name            | In    | Type                                      | Default   | Description
--------------- | ------| ------------------------------------------| ----------| -------------
ticket_uid      | path  | [SafeUUID](#safeuuid)                     | 0-99      | the uid of the selected `Ticket`.

### Responses

Http code | Type                                        | Description
----------| --------------------------------------------| ----------------------------
200       | [DetailedTicketView](#detailedticketview)   | The detailed `Ticket`
400       | Error                                       | Bad request, occurs most often when parameters passed are invalid.

## Open a Ticket

> HTTP query example :

```shell
curl -XPOST \                                                                                                        
-H "Cookie: PI_SESSION=..." \
-H "Content-Type: application/json" \
-d {
   "processUid": "5a7bd760-9487-cd87-860a-e043d0b3e99d",
   "aggregateUid": "eb0ea007-67af-4bf5-a34a-43dfca55717c",
   "locationRef": {
     "patrimonyUid": "74aa4bf3-8fde-4985-b16e-e3ba2788868f",
     "locationReferenceType": "PatrimonyLocation"
   },
   "operator": {
     "operatorUid": "f281d579-084e-95a1-8abb-582f2dcc2ed5",
     "operatorType": "ReferencedOperator"
   },
   "ticket": {
     "caller": {
       "name": {
         "value": "Mr John Doe",
         "nameType": "PoorName"
       },
       "medium": {
         "phone": "0320015450",
         "contactMediumType": "Phone"
       },
       "callerType": "HumanCaller"
     },
     "claimNumber": {
       "clientClaimNumber": "2016256649"
     },
     "address": {
       "quality": "quality",
       "street":"street",
       "complement": "complement",
       "zipCode": "zipCode",
       "city": "city",
       "state": "state",
       "country":"country"
     },
     "request": "FRIGOS EN PANNE",
     "callPurposeLabel": "frigoriste",
     "altCallPurpose": {},
     "additionalData": {
       "Code magasin": "FRPK98",
       "Corps de métier": "FRIGORISTE",
       "Libellé Code panne": "FRIGORISTE",
       "Nom magasin": "TOURCOING",
       "Heure réception OT": "16:51:02",
       "OS urgent": "NON",
     }
   },
   "openedDate": "2016-08-25T16:51:23.000+02:00",
   "commandType": "OpenTicket"
} \
https://base_url/api/vEvent/tickets
```

> HTTP response example :

```http
HTTP/1.1 201 Created
```

**`POST`** `/api/vEvent/tickets`

### Parameters

Name            | In    | Type                                         | Description
--------------- | ------| ---------------------------------------------| -------------
processUid      | body  | [SafeUUID](#safeuuid)                        | the uid of this `Command`. Allow PerfImmo to know if this Command is duplicated 
aggregateUid    | body  | [Option](#option)[[SafeUUID](#safeuuid)]     | the optional uid of the resource created. You can set yourself this uid or let Perfimmo do it for you.
locationRef     | body  | [LocationReference](#locationreference)      | a reference to another resource (`Agency`, `Patrimony`, etc...)
operator        | body  | [Option](#option)[[Operator](#operator)]     | an optional reference to who perform this `Command`. We can say who open this `Ticket`. 
ticket          | body  | [TicketInfos](#ticketinfos)                  | infos specific to the `Ticket` opened. 
openedDate      | body  | [DateTime](#datetime)                        | the opened date of this `Ticket`.
commandType     | body  | Constant                                     | `"OpenTicket"` 

### Responses

Http code | Type                                        | Description
----------| --------------------------------------------| ----------------------------
201       | [TicketEventResultView](#ticketeventresultview) | The `Event`s resulting of this successful `Command`.
400       | [TicketEventError](#ticketeventerror)       | Bad request, occurs most often when parameters passed are invalid, or if data in command is not coherent.
401       |                                             | Not authenticated user
403       |                                             | `User` doesn't have right to perform this `Command`

## Increment Ticket State

> HTTP query example :

```shell
curl -XPATCH \                                                                                                        
-H "Cookie: PI_SESSION=..." \
-H "Content-Type: application/json" \
-d {
   "processUid": "f5391199-e544-60f3-037c-16f3229fd59d",
   "operator": {
     "operatorUid": "98bfb3a8-ae4a-7486-1ee3-96131d994801",
     "operatorType": "ReferencedOperator"
   },
   "provider": {
     "providerUid": "7943797a-93c4-73f9-48f8-6baea5e94d13",
     "providerType": "ReferencedProvider"
   },
   "purpose": {
     "comment": "Choix du contact par l'opérateur",
     "providerAssignationPurposeType": "RecourseChanged"
   },
   "date": "2016-08-25T15:31:53.000+02:00",
   "commandType": "AssignProvider"
} \
https://base_url/api/vEvent/tickets/1d178826-76dc-cd04-e174-346ba60eedad
```

> HTTP response example :

```http
HTTP/1.1 200 OK
```

```json
{
    "events": [
        {
          "processUid": "f5391199-e544-60f3-037c-16f3229fd59d",
          "aggregateUid": "c9c5c9d2-ab38-a010-46cd-97013fbfbeb2",
          "operator": {
            "operatorUid": "98bfb3a8-ae4a-7486-1ee3-96131d994801",
            "operatorType": "ReferencedOperator"
          },
          "provider": {
            "providerUid": "7943797a-93c4-73f9-48f8-6baea5e94d13",
            "providerType": "ReferencedProvider"
          },
          "purpose": {
            "comment": "Choix du contact par l'opérateur",
            "providerAssignationPurposeType": "RecourseChanged"
          },
          "date": "2016-08-25T15:31:53.000+02:00",
          "sentDate": "2016-08-25T15:31:50.000+02:00",
          "eventType": "ProviderAssigned"
        }
    ]
}        
```

**`PATCH`** `/api/vEvent/tickets/:ticket_uid`

### Parameters

Name            | In    | Type                                             | Description
--------------- | ------| -------------------------------------------------| -------------
ticket_uid      | query | [SafeUUID](#safeuuid)                            | the uid of the `Ticket`
                | body  | [IncrementTicket](#incrementticket)              | the `Command` for increment a `Ticket` state

### Responses

Http code | Type                                        | Description
----------| --------------------------------------------| ----------------------------
200       | [TicketEventResultView](#ticketeventresultview) | The `Event`s resulting of this successful `Command`.
400       | [TicketEventError](#ticketeventerror)       | Bad request, occurs most often when parameters passed are invalid, or if data in command is not coherent.
401       |                                             | Not authenticated user
403       |                                             | `User` doesn't have right to perform this `Command`

## Listen Ticket Event

### HTTP Request

```shell
curl -XGET \
-H "Cookie: PI_SESSION=..." \
https://base_url/api/vEvent/tickets?range=0-0&from=2015-10-01T05:30:59.000Z&to=2016-10-02T05:30:59.000Z
```

> HTTP response example :

```http
HTTP/1.1 206 Partial Content
Content-Type: application/json
Content-Range: 0-0/256
```
```json
{
	"events": [
		{
            "processUid": "b000454f-6561-179a-35e5-254d09934d43",
            "aggregateUid": "b20efb62-a12a-cc8f-e1b7-edcf5c869e57",
            "locationRef": {
                "agencyUid": "5ced7e8e-3baa-1cb1-575d-b0e98cf21d5c",
                "locationReferenceType": "AgencyLocation"
            },
            "operator": {
                "operatorUid": "d7b82473-8fcc-739c-4e2e-7665d942f387",
                "operatorType": "ReferencedOperator"
            },
            "sentDate": "2015-10-01T05:34:59.000Z",
            "ticket": {
                "caller": {
                    "name": {
                        "value": "John Doe",
                        "nameType": "PoorName"
                    },
                    "medium": {
                        "phone": "0146304563",
                        "contactMediumType": "Phone"
                    },
                    "callerType": "HumanCaller"
                },
                "claimNumber": { },
                "address": {
                    "street": "3 rue de Paris",
                    "zipCode": "75001",
                    "city": "Paris"
                },
                "request": "Fuite au niveau du plafond de la cuisine.",
                "callPurposeLabel": "Fuite d'eau",
                "altCallPurpose": { },
                "additionalData": { }
            },
            "openedDate": "2015-10-01T05:34:59.000Z",
            "eventType": "TicketOpened"
        }
	]	
}	
```

**`GET`** `/api/vEvent/tickets`

### Parameters

Name            | In    | Type                                      | Default   | Description
--------------- | ------| ------------------------------------------| ----------| -----------------------------------------------------------------------------------------
range           | query | [Option](#option)[String]                 | 0-99      | range selector for result pagination.<br/> ex: `range=0-19` <br/> startRange should be <= endRange
from            | query | [DateTime](#datetime)                     |           | select all the events since that date (included).<br/> ex: `from=2015-10-01T05:30:59.000Z`.<br/>
to              | query | [DateTime](#datetime)                     |           | select all the events until this date (included).<br/> ex: `to=2015-10-01T05:30:59.000Z`.<br/> **`to`** must be >= **`from`**


### Responses

Http code | Type                                          | Description
----------| ----------------------------------------------| ----------------------------
200       | [TicketEventResultView](#ticketeventresultview) | All resources's elements are returned.
206       | [TicketEventResultView](#ticketeventresultview) | Partial Content. See `Content-Range` header for use pagination.
400       | Error                                           | Bad request, occurs most often when parameters passed are invalid.