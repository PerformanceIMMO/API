# Patrimonies

<aside class="warning">
	You must be authenticated to use these API.
</aside>

## Get all patrimonies

### HTTP Request

```shell
curl -XGET \
-H "Cookie: PI_SESSION=..." \
https://base_url/api/v1/patrimonies
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
            "uid": "6ed010a1-7481-4b38-87da-c219fc31ba64",
            "ref": "PATRIMONY_42",
            "label": "Résidence des Lillas",
            "agencies": [
                "17d706c1-7844-00f5-a4a4-f1afa1975184"
            ],
            "complementaryAddresses": [
                {
                    "uid": "8fb38a44-7a31-4f6f-9948-2ff3515bdafa",
                    "number": "17",
                    "street": "Rue de Solférino",
                    "city": "Boulogne-Billancourt",
                    "zipCode": "92100",
                    "country": "France",
                    "geoLocation": {
                        "lat": 48.8287815,
                        "lng": 2.243447699999999
                    },
                    "checker": {
                        "googlePlaceId": "ChIJh7Ckz-965kcROIvFZzyeeok"
                    }
                }
            ],
            "addresses": [
                {
                    "uid": "89532be8-543c-4d45-a0fc-4762b774eee5",
                    "number": "17",
                    "street": "Rue de Solférino",
                    "city": "Boulogne-Billancourt",
                    "zipCode": "92100",
                    "country": "France",
                    "geoLocation": {
                        "lat": 48.8287815,
                        "lng": 2.243447699999999
                    },
                    "checker": {
                        "googlePlaceId": "ChIJh7Ckz-965kcROIvFZzyeeok"
                    }
                }
            ]
        }
    ]
}	
```

**`GET`** `/api/v1/patrimonies`

### Parameters

Name            | In    | Type                                      | Default   | Description
--------------- | ------| ------------------------------------------| ----------| -----------------------------------------------------------------------------------------
range           | query | [Option](#option)[String]                 | 0-100     | range selector for result pagination.<br/> ex: `range=0-19` <br/> startRange should be > endRange


### Responses

Http code | Type                                          | Description
----------| ----------------------------------------------| ----------------------------
200       | [PatrimonyResultView](#ticketresultview)      | All resources's elements are returned.
206       | [PatrimonyResultView](#ticketresultview)      | Partial Content. See `Content-Range` header for use pagination.
400       | Error                                         | Bad request, occurs most often when parameters passed are invalid.





GET         /api/v1/patrimonies/:uid                                        cqrs.queries.application.controllers.PatrimoniesQueryAPI.patrimony(uid: SafeUUID)
GET         /api/v1/patrimonies/:patrimonyUid/buildings                     cqrs.queries.application.controllers.PatrimoniesQueryAPI.buildings(range: Option[String], patrimonyUid: SafeUUID)
GET         /api/v1/patrimonies/:patrimonyUid/buildings/:buildingUid        cqrs.queries.application.controllers.PatrimoniesQueryAPI.building(patrimonyUid: SafeUUID, buildingUid: SafeUUID)