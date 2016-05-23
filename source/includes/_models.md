# Models

## SafeUUID

Identifiant garanti unique en utilisant la norme [GUUID](https://fr.wikipedia.org/wiki/Globally_Unique_Identifier)    

ex: `8074964f-c633-3c2a-055f-bbaf8ca8181b`

## CompanyQueryView

### Fields

Name        | Type                                              | Mandatory | Description
------------| --------------------------------------------------| ----------| ----------------
uid         | [SafeUUID](#safeuuid)                             | true      | id of the `Company`
label       | String                                            | true      | the `Company`'s label
isActive    | Boolean                                           | true      | `true` if the `Company` is active
holding     | [HoldingQueryView](#holdingqueryview)             | false     | a reference to `Company`'s holding if has it
companyType | String                                            | true      | enum : `"CallCenter"` or `"ClientAccountHolding"` or `"ClientAccount"`

## HoldingQueryView 

Name        | Type                                              | Mandatory | Description
------------| --------------------------------------------------| ----------| -----------------
uid         | [SafeUUID](#safeuuid)                             | true      | the holding's uid
label       | String                                            | true      | the holding's label

