# Lots

<aside class="warning">
	You must be authenticated to use these API.
</aside>

## Get all lots of a Patrimony

### HTTP Request

> HTTP query example :

```shell
curl -XGET \
-H "Cookie: PI_SESSION=..." \
https://base_url/api/v1/lots?patrimonyuid=89532be8-543c-4d45-a0fc-4762b774eee5
```

> HTTP response example :

```http
HTTP/1.1 200 OK
Content-Type: application/json
Content-Range: 0-0/1
```
```json
{
	"result":[
		{
			"uid":"814443ab-b495-487b-bf17-b786880de384",
			"addresses":[
				{
					"uid":"01761fce-aafa-4d01-adbf-12021f0d72b4",
					"number":"21",
					"street":"Rue de Paris",
					"city":"Montpellier",
					"zipCode":"34000",
					"country":"France",
					"geoLocation":{"lat":43.6037654,"lng":3.8730828},
					"checker":{"googlePlaceId":"ChIJ72W3Da-vthIRPu9q87gz_D8"}
				}
			],
			"patrimony":{
				"uid":"dcac705e-175e-6a23-c314-ebb77242ff87",
				"label":"My Patrimony",
				"ref":"00101"
			},
			"ref":"97079",
			"usage":"Apartment",
			"owners":[],
			"occupants":[],
			"_links":[
				{"rel":"self", "href":"https://preprod.performance-immo.com/api/v1/lots/814443ab-b495-487b-bf17-b786880de384","method":"GET"},
				{"rel":"AddAddressToLot","href":"https://preprod.performance-immo.com/api/vEvent/lots/814443ab-b495-487b-bf17-b786880de384","method":"PATCH"},
				{"rel":"RemoveAddressFromLot","href":"https://preprod.performance-immo.com/api/vEvent/lots/814443ab-b495-487b-bf17-b786880de384","method":"PATCH"},
				{"rel":"UpdateLotReference","href":"https://preprod.performance-immo.com/api/vEvent/lots/814443ab-b495-487b-bf17-b786880de384","method":"PATCH"},
				{"rel":"UpdateLotNumber","href":"https://preprod.performance-immo.com/api/vEvent/lots/814443ab-b495-487b-bf17-b786880de384","method":"PATCH"},
				{"rel":"UpdateLotUsage","href":"https://preprod.performance-immo.com/api/vEvent/lots/814443ab-b495-487b-bf17-b786880de384","method":"PATCH"},
				{"rel":"DeleteLot","href":"https://preprod.performance-immo.com/api/vEvent/lots/814443ab-b495-487b-bf17-b786880de384","method":"PATCH"}
			]
		}
	]
	,"_links":[
		{"rel":"self","href":"https://preprod.performance-immo.com/api/v1/lots","method":"GET"},
		{"rel":"ReferenceLot","href":"https://preprod.performance-immo.com/api/vEvent/lots","method":"POST"}
	]
} 
```

**`GET`** `/api/v1/patrimonies`

### Parameters

Name            | In    | Type                                      | Default   | Description
--------------- | ------| ------------------------------------------| ----------| -----------------------------------------------------------------------------------------
range           | query | [Option](#option)[String]                 | 0-100     | range selector for result pagination.<br/> ex: `range=0-19` <br/> startRange should be > endRange
patrimonyuid    | query | [SafeUUID](#safeuuid)                     |           | the patrimony linked to these lots
buildinguids    | query | Array[[SafeUUID](#safeuuid)]              | [ ]       | 

### Responses

Http code | Type                                          | Description
----------| ----------------------------------------------| ----------------------------
200       | [LotResultView](#lotresultview)               | All resources's elements are returned.
206       | [LotResultView](#lotresultview)               | Partial Content. See `Content-Range` header for use pagination.
400       | Error                                         | Bad request, occurs most often when parameters passed are invalid.

## Get a specific Lot

### HTTP Request

> HTTP query example :

```shell
curl -XGET \
-H "Cookie: PI_SESSION=..." \
https://base_url/api/v1/lots/6ed010a1-7481-4b38-87da-c219fc31ba64
```

> HTTP response example :

```http
HTTP/1.1 200 OK
Content-Type: application/json
```
```json
{
	"uid":"814443ab-b495-487b-bf17-b786880de384",
	"addresses":[
		{
			"uid":"01761fce-aafa-4d01-adbf-12021f0d72b4",
			"number":"21",
			"street":"Avenue de Paris",
			"city":"Montpellier",
			"zipCode":"34000",
			"country":"France",
			"geoLocation":{"lat":43.6037654,"lng":3.8730828},
			"checker":{"googlePlaceId":"ChIJ72W3Da-vthIRPu9q87gz_D8"}
		}
	],
	"patrimony": {
		"uid":"dcac705e-175e-6a23-c314-ebb77242ff87",
		"label":"My patrimony",
		"ref":"00101"
	},
	"ref":"97079",
	"usage":"Apartment",
	"owners":[],
	"occupants":[],
	"_links":[
		{"rel":"self","href":"https://preprod.performance-immo.com/api/v1/lots/814443ab-b495-487b-bf17-b786880de384","method":"GET"},
		{"rel":"AddAddressToLot","href":"https://preprod.performance-immo.com/api/vEvent/lots/814443ab-b495-487b-bf17-b786880de384","method":"PATCH"},
		{"rel":"RemoveAddressFromLot","href":"https://preprod.performance-immo.com/api/vEvent/lots/814443ab-b495-487b-bf17-b786880de384","method":"PATCH"},
		{"rel":"UpdateLotReference","href":"https://preprod.performance-immo.com/api/vEvent/lots/814443ab-b495-487b-bf17-b786880de384","method":"PATCH"},
		{"rel":"UpdateLotNumber","href":"https://preprod.performance-immo.com/api/vEvent/lots/814443ab-b495-487b-bf17-b786880de384","method":"PATCH"},
		{"rel":"UpdateLotUsage","href":"https://preprod.performance-immo.com/api/vEvent/lots/814443ab-b495-487b-bf17-b786880de384","method":"PATCH"},
		{"rel":"DeleteLot","href":"https://preprod.performance-immo.com/api/vEvent/lots/814443ab-b495-487b-bf17-b786880de384","method":"PATCH"}
	]
}	
```

**`GET`** `/api/v1/lots/:lot_uid`

### Parameters

Name            | In    | Type                                      | Default   | Description
--------------- | ------| ------------------------------------------| ----------| -----------------------------------------------------------------------------------------
lot_uid         | path  | [SafeUUID](#safeuuid)                     |           | the uid of the `Lot` requested


### Responses

Http code | Type                                          | Description
----------| ----------------------------------------------| ----------------------------
200       | [LotDetailQueryView](#lotdetailqueryview)     | the `Lot` requested.
400       | Error                                         | Bad request, occurs most often when parameters passed are invalid.

## Reference a Lot

> HTTP query example :

```shell
curl -XPOST \                                                                                                        
-H "Cookie: PI_SESSION=..." \
-H "Content-Type: application/json" \
-d {
 "processUid":"8c12f096-20e6-11ab-8ff7-2c39b4397040",
 "ref":"#Lot_1",
 "lotNumber":"34",
 "patrimonyUid":"b60521f2-cc1a-a4cf-5ba8-9510eeaf2d32",
 "addresses": [
    {
      ...
    }
 ],
 "usage":"Apartement",
 "commandType":"ReferencePatrimony"
} \
https://base_url/api/vEvent/patrimonies
```

> HTTP response example :

```http
HTTP/1.1 201 Created
```

**`POST`** `/api/vEvent/lots`

### Parameters

Name            | In    | Type                                         | Description
--------------- | ------| ---------------------------------------------| -------------
processUid      | body  | [SafeUUID](#safeuuid)                        | the uid of this `Command`. Allow PerfImmo to know if this Command is duplicated 
aggregateUid    | body  | [Option](#option)[[SafeUUID](#safeuuid)]     | the optional uid of the resource created. You can set yourself this uid or let Perfimmo do it for you.
ref             | body  | String                                       | a public reference to distinguish the `Lot` in a `Agency` context 
lotNumber       | body  | String                                       | a public number to distinguish the `Lot` in its `Patrimony`   
patrimonyUid    | body  | [SafeUUID](#safeuuid)                        |   
addresses       | body  | [NonEmptyList](#nonemptylist)[[LotAddressCommand](#lotaddresscommand)] |
usage           | body  | [LotUsage](#lotusage)                        | what kind of `Lot` it is. 
commandType     | body  | Constant                                     | `"ReferenceLot"` 

### Responses

Http code | Type                                        | Description
----------| --------------------------------------------| ----------------------------
201       | [LotEventResultView](#loteventresultview)   | The `Lot` is referenced.
400       | [LotEventError](#loteventerror)             | Bad request, occurs most often when parameters passed are invalid, or if data in command is not coherent.
401       |                                             | Not authenticated user .
403       |                                             | `User` doesn't have right to perform this `Command`.

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
LotReferenced                             | mandatory                         |
LotNumberUpdated                          | mandatory                         |

## Increment Lot State
                    
> HTTP query example :

```shell
curl -XPATCH \                                                                                                        
-H "Cookie: PI_SESSION=..." \
-H "Content-Type: application/json" \
-d {
 "processUid":"8c12f096-20e6-11ab-8ff7-2c39b4397040",
 "ref":"new_ref",
 "commandType":"UpdateLotReference"
} \
https://base_url/api/vEvent/lots/1d178826-76dc-cd04-e174-346ba60eedad
```

> HTTP response example :

```http
HTTP/1.1 200 OK
```

**`PATCH`** `/api/vEvent/lots/lot_uid`

### Parameters

Name            | In    | Type                                             | Description
--------------- | ------| -------------------------------------------------| -------------
lot_uid         | query | [SafeUUID](#safeuuid)                            | the uid of the `Lot`
lotCommand      | body  | [IncrementLot](#incrementlot)                    | the `Command` for increment a `Lot` state

### Responses

Http code | Type                                        | Description
----------| --------------------------------------------| ----------------------------
200       | [LotEventResultView](#loteventresultview)   | The `Command` is a success
400       | [LotEventError](#loteventerror)             | Bad request, occurs most often when parameters passed are invalid, or if data in command is not coherent.
401       |                                             | Not authenticated user
403       |                                             | `User` doesn't have right to perform this `Command`