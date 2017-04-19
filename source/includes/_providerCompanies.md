# ProviderCompanies

<aside class="warning">
	You must be authenticated to use these API.
</aside>

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