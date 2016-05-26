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
            "agency": {
                "uid": "17d706c1-7844-00f5-a4a4-f1afa1975184",
                "name": "My Agency"
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
range           | query | [Option](#option)[String]                 | 0-100     | range selector for result pagination.<br/> ex: `range=0-19` <br/> startRange should be > endRange
agency          | query | [Option](#option)[[SafeUUID](#safeuuid)]  | None      | query matching with several `agencies` uid.<br/> ex: `agency=agency_uid1,agency_uid2`
status          | query | [Option](#option)[ENUM]                   | None      | query matching with `status` { OPENED or CLOSED }.<br/> ex: `status=OPENED`
location        | query | [Option](#option)[String]                 | None      | query matching with several `locations`.<br/> ex: `location=paris,marseille,toulouse`
from            | query | [Option](#option)[[LocalDate](#localdate)]| None      | query matching with `from` local date.<br/> ex: `from=2015-07-02`.<br/> if **`from`** but not **`to`** => from **`from`** to **now**
to              | query | [Option](#option)[[LocalDate](#localdate)]| None      | query matching with `to` local date.<br/> ex: `to=2015-07-03`.<br/> if **`to`** but not **`from`** => until **`to`**. **`to`** must be >= **`from`**
callpurpose     | query | [Option](#option)[String]                 | None      | query matching with several `callpurpose`.<br/> ex: `callpurpose=one,two,three`
fulltext        | query | [Option](#option)[[String](#localdate)]   | None      | `fulltext` query matching with several terms.<br/> ex: `fulltext=word,other+word`.<br/> This param is incompatible with the others (except for range).


### Responses

Http code | Type                                          | Description
----------| ----------------------------------------------| ----------------------------
200       | [TicketResultView](#ticketresultview)          | All resources's elements are returned.
206       | [TicketResultView](#ticketresultview)          | Partial Content. See `Content-Range` header for use pagination.
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
range           | query | [Option](#option)[String]                 | 0-100     | range selector for result pagination.<br/> ex: `range=0-19` <br/> startRange should be > endRange
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
    "agency": {
        "uid": "17d706c1-7844-00f5-a4a4-f1afa1975184",
        "name": "My Agency"
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
ticket_uid      | path  | [SafeUUID](#safeuuid)                     | 0-100     | the uid of the selected `Ticket`.

### Responses

Http code | Type                        | Description
----------| ----------------------------| ----------------------------
200       | Array[[DetailedTicketView](#detailedticketview)]    | All resources's elements are returned.
400       | Error                                               | Bad request, occurs most often when parameters passed are invalid.
