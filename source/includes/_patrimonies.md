# Patrimonies

<aside class="warning">
	You must be authenticated to use these API.
</aside>

## Get all patrimonies

### HTTP Request

> HTTP query example :

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
200       | [PatrimonyResultView](#patrimonyresultview)   | All resources's elements are returned.
206       | [PatrimonyResultView](#patrimonyresultview)   | Partial Content. See `Content-Range` header for use pagination.
400       | Error                                         | Bad request, occurs most often when parameters passed are invalid.

## Get a specific Patrimony

### HTTP Request

> HTTP query example :

```shell
curl -XGET \
-H "Cookie: PI_SESSION=..." \
https://base_url/api/v1/patrimonies/6ed010a1-7481-4b38-87da-c219fc31ba64
```

> HTTP response example :

```http
HTTP/1.1 200 OK
Content-Type: application/json
```
```json
{
    "uid": "6ed010a1-7481-4b38-87da-c219fc31ba64",
    "ref": "DEMO_SOLFERINO",
    "label": "17 RUE DE SOLFERINO II",
    "agencies": [
        {
            "uid": "17d706c1-7844-00f5-a4a4-f1afa1975184",
            "label": "Foncia Agence Centrale"
        }
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
```

**`GET`** `/api/v1/patrimonies/:patrimony_uid`

### Parameters

Name            | In    | Type                                      | Default   | Description
--------------- | ------| ------------------------------------------| ----------| -----------------------------------------------------------------------------------------
patrimony_uid   | path  | [SafeUUID](#safeuuid)                     |           | the uid of the `Patrimony` requested


### Responses

Http code | Type                                          | Description
----------| ----------------------------------------------| ----------------------------
200       | [PatrimonyDetailQueryView](#patrimonydetailqueryview) | the `Patrimony` requested.
400       | Error                                         | Bad request, occurs most often when parameters passed are invalid.

## Get all Buildings of a Patrimony

### HTTP Request

> HTTP query example :

```shell
curl -XGET \
-H "Cookie: PI_SESSION=..." \
https://base_url/api/v1/patrimonies/6ed010a1-.../building
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
            "uid": "456f4a1d-5287-494c-93d6-6535aaf1bc68",
            "label": "Archipel",
            "patrimony": {
                "uid": "1f745b09-2e15-4dd7-82de-99d4c3e0a764"
            }
        }
    ]
}	
```

**`GET`** `/api/v1/patrimonies/:patrimony_uid/buildings`

### Parameters

Name            | In    | Type                                      | Default   | Description
--------------- | ------| ------------------------------------------| ----------| -----------------------------------------------------------------------------------------
range           | query | [Option](#option)[String]                 | 0-100     | range selector for result pagination.<br/> ex: `range=0-19` <br/> startRange should be > endRange


### Responses

Http code | Type                                          | Description
----------| ----------------------------------------------| ----------------------------
200       | [PatrimonyBuildingResultView](#patrimonybuildingresultview) | All resources's elements are returned.
206       | [PatrimonyBuildingResultView](#patrimonybuildingresultview) | Partial Content. See `Content-Range` header for use pagination.
400       | Error                                         | Bad request, occurs most often when parameters passed are invalid.

## Get a specific Building

### HTTP Request

> HTTP query example :

```shell
curl -XGET \
-H "Cookie: PI_SESSION=..." \
https://base_url/api/v1/patrimonies/6ed010a1-.../buildings/456f4a1d-...
```

> HTTP response example :

```http
HTTP/1.1 200 OK
Content-Type: application/json
```
```json
{
    "uid": "456f4a1d-5287-494c-93d6-6535aaf1bc68",
    "label": "Archipel",
    "patrimony": {
        "uid": "1f745b09-2e15-4dd7-82de-99d4c3e0a764"
    },
    "addresses": [
        {
            "uid": "1c8ead50-45b8-4771-ae46-d795d6e0cc8d",
            "number": "45",
            "street": "Avenue des États Unis",
            "city": "Versailles",
            "zipCode": "78000",
            "country": "France",
            "geoLocation": {
                "lat": 48.8112548,
                "lng": 2.1479988
            },
            "checker": {
                "googlePlaceId": "ChIJcYTADlB85kcRvg9dbMxqljc"
            }
        }
    ]
}	
```

**`GET`** `/api/v1/patrimonies/:patrimony_uid/buildings/:building_uid`

### Parameters

Name            | In    | Type                                      | Default   | Description
--------------- | ------| ------------------------------------------| ----------| -----------------------------------------------------------------------------------------
patrimony_uid   | path  | [SafeUUID](#safeuuid)                     |           | the uid of the `Patrimony` requested
building_uid    | path  | [SafeUUID](#safeuuid)                     |           | the uid of the `Building` requested


### Responses

Http code | Type                                          | Description
----------| ----------------------------------------------| ----------------------------
200       | [PatrimonyDetailedBuildingQueryView](#patrimonydetailedbuildingqueryview) | the `Building` requested.
400       | Error                                         | Bad request, occurs most often when parameters passed are invalid.

## Reference a Patrimony

> HTTP query example :

```shell
curl -XPOST \                                                                                                        
-H "Cookie: PI_SESSION=..." \
-H "Content-Type: application/json" \
-d {
 "processUid":"8c12f096-20e6-11ab-8ff7-2c39b4397040",
 "ref":"#Patrimony_1",
 "agencyUids":["b60521f2-cc1a-a4cf-5ba8-9510eeaf2d32"],
 "label":"Résidence des flots bleu",
 "commandType":"ReferencePatrimony"
} \
https://base_url/api/vEvent/patrimonies
```

> HTTP response example :

```http
HTTP/1.1 201 Created
```

**`POST`** `/api/vEvent/patrimonies`

### Parameters

Name            | In    | Type                                         | Description
--------------- | ------| ---------------------------------------------| -------------
processUid      | body  | [SafeUUID](#safeuuid)                        | the uid of this `Command`. Allow PerfImmo to know if this Command is duplicated 
ref             | body  | String                                       | a public reference to distinguish the `Patrimony` 
agencyUids      | body  | [NonEmptyList](#nonemptylist)[[SafeUUID](#safeuuid)] | list of agency uids associated with this Patrimony. Allow Perfimmo to handle rights of read or update this Patrimony  
label           | body  | [Option](#option)[String]                    | label of the patrimony 
commandType     | body  | Constant                                     | `"ReferencePatrimony"` 

### Responses

Http code | Type                                        | Description
----------| --------------------------------------------| ----------------------------
201       | String                                      | The `Patrimony` is created
400       | [PatrimonyEventError](#patrimonyeventerror) | Bad request, occurs most often when parameters passed are invalid, or if data in command is not coherent.
401       |                                             | Not authenticated user
403       |                                             | `User` doesn't have right to perform this `Command`

## Increment Patrimony State

> HTTP query example :

```shell
curl -XPATCH \                                                                                                        
-H "Cookie: PI_SESSION=..." \
-H "Content-Type: application/json" \
-d {
 "processUid":"8c12f096-20e6-11ab-8ff7-2c39b4397040",
 "agencyUid":"b60521f2-cc1a-a4cf-5ba8-9510eeaf2d32",
 "commandType":"AssociatePatrimonyInAgency"
} \
https://base_url/api/vEvent/patrimonies/1d178826-76dc-cd04-e174-346ba60eedad
```

> HTTP response example :

```http
HTTP/1.1 200 OK
```

**`PATCH`** `/api/vEvent/patrimonies/patrimony_uid`

### Parameters

Name            | In    | Type                                             | Description
--------------- | ------| -------------------------------------------------| -------------
patrimony_uid   | query | [SafeUUID](#safeuuid)                            | the uid of the `Patrimony`
patrimonyCommand | body | [IncrementPatrimony](#incrementpatrimony)        | the `Command` for increment a `Patrimony` state

### Responses

Http code | Type                                        | Description
----------| --------------------------------------------| ----------------------------
200       | String                                      | The `Command` is a success
400       | [PatrimonyEventError](#patrimonyeventerror) | Bad request, occurs most often when parameters passed are invalid, or if data in command is not coherent.
401       |                                             | Not authenticated user
403       |                                             | `User` doesn't have right to perform this `Command`