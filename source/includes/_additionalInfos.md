# AdditionalInfos

<aside class="warning">
	You must be authenticated to use these API.
</aside>

Vous pouvez avoir besoin d'afficher des informations propres sur chacune des entitées 
chargées sur la plateforme Performance Immo.

Pour ce faire nous mettons à disposition une API unique, permettant de lier un ensemble de clé-valeur
à une entité donnée.

## Ajouter une info aditionnelle à une entité

Pour mettre à jour la donnée il suffit de rejouer la requête d'ajout d'infos qui mettra à jour l'ancienne.

### HTTP Request

> HTTP query example :

```shell
curl -XPOST \                                                                                                        
-H "Cookie: PI_SESSION=..." \
-H "Content-Type: application/json" \
-d {
 "infos": {
   "key_1":"value_1",
   "key_2":"value_2"
 },
 "linkToEntity": {
   "uid":"6e71965c-e1ea-37e9-fa45-770753dc5147",
   "type":"ProviderContactContract"
 }
} \
https://base_url/api/v1/additionalinfos
```

> HTTP response example :

```http
HTTP/1.1 201 Created
Content-Type: application/json
```
```json
{
	"uid": "6e71965c-e1ea-37e9-fa45-770753dc5147"	
}	
```

**`POST`** `/api/v1/additionalinfos`

### Parameters

Name            | In    | Type                                         | Default   | Description
--------------- | ------| ---------------------------------------------| ----------| -------------
infos           | body  | Map[String,String]                           |           | the collection of key-value to link with an entity
linkToEntity    | body  | [AdditionInfosEntityLink](#additioninfosentitylink) |           | with which entity to link this infos


### Responses

Http code | Type                                        | Description
----------| --------------------------------------------| ----------------------------
201       | [CompanyEventResultView](#companyeventresultview) | The `Company` is created. Return the `Event`s resulting of this successful `Command`.
400       | [CompanyEventError](#companyeventerror)     | Bad request, occurs most often when parameters passed are invalid, or if data in command is not coherent.
