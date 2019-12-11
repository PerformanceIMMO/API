# SimplifiedRequests

<aside class="warning">
	You must be authenticated to use these API.
</aside>

Les demandes simplifiées (a.k.a `SimplifiedRequest`) sont à l'usage d'utilisateurs non professionnels (par exmeple les co-propriétaires)
 pour leur permettre d'effectuer une demande.
 
Une demande simplifiée a pour objet la création d'un `Ticket`. Ce qui équivaut à la qualification de cette demande simplifiée. 

Cette demande est qualifé de simplifiée, car elle ne considère que le patrimoine impacté et la catégorie de raison d'ouverture de ticket.

## Get simplified requests and filter it

### HTTP Request

```shell
curl -XGET \
-H "Cookie: PI_SESSION=..." \
https://base_url/api/v1/simplifiedrequests?range=0-0
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
            "uid": "5f86dd27-ef9e-4659-8d61-c3e7cf5baae7",
            "state": "Declared",
            "category": {
                "uid": "c5d1462f-a3c8-4c87-a529-47ae53a45fa7",
                "label": "Fuite d'eau",
                "iconId": "waterdrop"
            },
            "patrimony": {
                "uid": "b5be2f60-11a6-4769-96ec-76bc6cb367fc",
                "name": "67 route de la Reine",
                "ref": "P-001"
            },
            "requestDate": "2019-11-21T11:00:37.564Z",
            "_links": [
                
            ]
        }
	]	
}	
```

**`GET`** `/api/v1/simplifiedrequests`

### Parameters

Name            | In    | Type                                      | Default   | Description
--------------- | ------| ------------------------------------------| ----------| -----------------------------------------------------------------------------------------
range           | query | [Option](#option)[String]                 | 0-99      | range selector for result pagination.<br/> ex: `range=0-19` <br/> startRange should be <= endRange
ticketuid       | query | [Option](#option)[[SafeUUID](#safeuuid)]  | None      | query matching with `Ticket` uid.<br/> ex: `ticketuid=5f86dd27-ef9e-4659-8d61-c3e7cf5baae7`
patrimony       | query | Array[[SafeUUID](#safeuuid)]              | None      | query matching with `Patrimony` uid.<br/> ex: `patrimony=5f86dd27-ef9e-4659-8d61-c3e7cf5baae7&patrimony=5f86dd27-ef9e-4659-8d61-c3e7cf5baae6`
state           | query | Array[ENUM]                               | None      | query matching with `state` { Declared or Seen or Qualified }.<br/> ex: `state=Declared&state=Seen`

### Responses

Http code | Type                                          | Description
----------| ----------------------------------------------| ----------------------------
200       | [SimplifiedRequestResultView](#simplifiedrequestresultview) | All resources's elements are returned.
206       | [SimplifiedRequestResultView](#simplifiedrequestresultview) | Partial Content. See `Content-Range` header for use pagination.
400       | Error                                                       | Bad request, occurs most often when parameters passed are invalid.

## Get a simplified request

### HTTP Request

```shell
curl -XGET \
-H "Cookie: PI_SESSION=..." \
https://base_url/api/v1/simplifiedrequests/17ab7b5b-b7ca-18f6-d5f3-3dfbcbaee1a2
```

> HTTP response example :

```http
HTTP/1.1 200 OK
Content-Type: application/json
```
```json
{

    "uid": "5f86dd27-ef9e-4659-8d61-c3e7cf5baae7",
    "state": "Qualified",
    "category": {
        "uid": "c5d1462f-a3c8-4c87-a529-47ae53a45fa7",
        "label": "Fuite d'eau",
        "iconId": "waterdrop"
    },
    "linkedEntities": {
        "patrimony": {
            "uid": "b5be2f60-11a6-4769-96ec-76bc6cb367fc",
            "name": "67 route de la Reine",
            "ref": "P-001"
        },
        "company": {
            "uid": "3500cb21-ba56-4d3b-b8cd-88c01d949e42",
            "name": "Loiselet & Daigremont"
        },
        "agencies": [
            {
                "uid": "27caacc6-b98f-4860-b912-a6660ffd07f0",
                "name": "Loiselet & Daigremont Boulogne"
            }
        ],
        "callCenters": [
            "8a8a2283-0ef1-4755-b398-8ae7880766e5"
        ]
    },
    "requestDate": "2019-11-21T11:00:37.564Z",
    "description": "Thjvvhjjbgjkggjiiuuyh",
    "requester": {
        "uid": "9e96638e-be9f-4252-a87a-d1a0a2bf6644",
        "name": "Thierry  Godo Gestionnaire",
        "medium": [
            {
                "mediumType": "PHONE",
                "identifier": "+33141225538"
            },
            {
                "mediumType": "MAIL",
                "identifier": "thierry.godo+gestionnaire@gmail.com"
            }
        ],
        "callerInfos": {
            "companyUid": "3500cb21-ba56-4d3b-b8cd-88c01d949e42",
            "userType": "PatrimonyManager",
            "callerType": "ClientCompanyUserCaller"
        }
    },
    "qualified": {
        "ticketUid": "0a0c5ce7-3dcb-41f8-86e7-616f291b7c7f",
        "qualifier": {
            "uid": "6dbe20d1-bc57-4cff-8317-adeffd9bc4c2",
            "name": "Nicolas Marx",
            "userType": "ReferencedUser"
        },
        "date": "2019-12-11T15:51:15.716Z"
    },
    "_links": [ ]
}
```

**`GET`** `/api/v1/simplifiedrequests/:sr_uid`

### Parameters

Name            | In    | Type                                      | Default   | Description
--------------- | ------| ------------------------------------------| ----------| -------------
sr_uid          | path  | [SafeUUID](#safeuuid)                     | 0-99      | the uid of the selected `SimplifiedRequest`.

### Responses

Http code | Type                                        | Description
----------| --------------------------------------------| ----------------------------
200       | [SimplifiedRequestDetailedView](#simplifiedrequestdetailedview)   | The detailed `SimplifiedRequest`
400       | Error                                       | Bad request, occurs most often when parameters passed are invalid.
