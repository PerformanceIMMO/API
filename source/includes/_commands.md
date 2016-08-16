# Commands

## CreateCompany

Il existe plusieurs types de `Company` et donc plusieurs commandes différentes pour créer une `Company`. 

cf. le détails sur la [ressource](#company) `Company`. 

### CreateClientAccount
 
```json
{
    "processUid":"6ed010a1-7481-4b38-87da-c219fc31ba64",
    "aggregateUid":"8c12f096-20e6-11ab-8ff7-2c39b4397040",
    "holdingReference":"9fe2e437-b237-8c9d-8b36-440d37fc8959",
    "callCenterUid":"f13ede3b-12d9-70ab-4874-e25ab23e33c0",
    "createdDate":"2016-06-27",
    "name":"My Client Account",
    "commandType":"CreateClientAccount"
} 
``` 

Name               | Type                                          | Description
-------------------| ----------------------------------------------| --------------------------------------------------
processUid         | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid       | [Option](#option)[[SafeUUID](#safeuuid)]      | the uid of the resource. Allow you to decide which uid is set to resource you create. If not setted, PerfImmo generate this uid
holdingReference   | [Option](#option)[[SafeUUID](#safeuuid)]      | the uid of the `ClientAccount`'s holding if exist 
callCenterReference| [SafeUUID](#safeuuid)                         | the uid of the `CallCenter` which send this Command  
createdDate        | [LocalDate](#localdate)                       | the creation's date of this `ClientAccount`  
name               | String                                        | the name of this `ClientAccount`.  
commandType        | Constant                                      | `"CreateClientAccount"`  

### CreateClientAccountHolding 

```json
{
    "processUid":"6ed010a1-7481-4b38-87da-c219fc31ba64",
    "aggregateUid":"8c12f096-20e6-11ab-8ff7-2c39b4397040",
    "callCenterUid":"f13ede3b-12d9-70ab-4874-e25ab23e33c0",
    "createdDate":"2016-06-27",
    "name":"My Holding",
    "commandType":"CreateClientAccountHolding"
} 
``` 

Name               | Type                                          | Description
-------------------| ----------------------------------------------| --------------------------------------------------
processUid         | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid       | [Option](#option)[[SafeUUID](#safeuuid)]      | the uid of the resource. Allow you to decide which uid is set to resource you create. If not setted, PerfImmo generate this uid
callCenterReference| [SafeUUID](#safeuuid)                         | the uid of the `CallCenter` which send this Command
createdDate        | [LocalDate](#localdate)                       | the creation's date of this `ClientAccountHolding`  
name               | String                                        | the name of this `ClientAccountHolding`.  
commandType        | Constant                                      | `"CreateClientAccountHolding"`

### CreateCallCenter

<aside class="notice">
	You need specifics rights to create CallCenter.
</aside>

```json
{
    "processUid":"6ed010a1-7481-4b38-87da-c219fc31ba64",
    "aggregateUid":"8c12f096-20e6-11ab-8ff7-2c39b4397040",
    "createdDate":"2016-06-27",
    "name":"My CallCenter",
    "commandType":"CreateCallCenter"
} 
``` 

Name               | Type                                          | Description
-------------------| ----------------------------------------------| --------------------------------------------------
processUid         | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid       | [Option](#option)[[SafeUUID](#safeuuid)]      | the uid of the resource. Allow you to decide which uid is set to resource you create. If not setted, PerfImmo generate this uid
createdDate        | [LocalDate](#localdate)                       | the creation's date of this `CallCenter`  
name               | String                                        | the name of this `CallCenter`.  
commandType        | Constant                                      | `"CreateCallCenter"`

## IncrementCompany

### CancelCompany

```json
{
    "processUid":"6ed010a1-7481-4b38-87da-c219fc31ba64",
    "canceledDate":"2016-06-27",
    "commandType":"CancelCompany"
} 
``` 

Name               | Type                                          | Description
-------------------| ----------------------------------------------| --------------------------------------------------
processUid         | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
canceledDate       | [LocalDate](#localdate)                       | the cancelation's date of this `Company`  
commandType        | Constant                                      | `"CancelCompany"`

### ReactiveCompany

```json
{
    "processUid":"6ed010a1-7481-4b38-87da-c219fc31ba64",
    "reactivatedDate":"2016-06-27",
    "commandType":"ReactiveCompany"
} 
``` 

Name               | Type                                          | Description
-------------------| ----------------------------------------------| --------------------------------------------------
processUid         | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
reactivatedDate    | [LocalDate](#localdate)                       | the reactivated's date of this `Company`  
commandType        | Constant                                      | `"ReactiveCompany"`

### UpdateClientAccount

```json
{
    "processUid":"6ed010a1-7481-4b38-87da-c219fc31ba64",
    "holdingReference":"8c12f096-20e6-11ab-8ff7-2c39b4397040",
    "updatedDate":"2016-06-28",
    "name":"new name",
    "commandType":"UpdateClientAccount"
} 
``` 

Name               | Type                                          | Description
-------------------| ----------------------------------------------| --------------------------------------------------
processUid         | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
holdingReference   | [Option](#option)[[SafeUUID](#safeuuid)]      | the updated holding reference of this `Company`  
updatedDate        | [LocalDate](#localdate)                       | the updated's date of this `Company`  
name               | String                                        | the updated name of this `Company`  
commandType        | Constant                                      | `"UpdateClientAccount"`

### UpdateClientAccountHolding

```json
{
    "processUid":"6ed010a1-7481-4b38-87da-c219fc31ba64",
    "updatedDate":"2016-06-28",
    "name":"new name",
    "commandType":"UpdateClientAccountHolding"
} 
``` 

Name               | Type                                          | Description
-------------------| ----------------------------------------------| --------------------------------------------------
processUid         | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
updatedDate        | [LocalDate](#localdate)                       | the updated's date of this `Company`  
name               | String                                        | the updated name of this `Company`  
commandType        | Constant                                      | `"UpdateClientAccountHolding"`

### UpdateCallCenter

```json
{
    "processUid":"6ed010a1-7481-4b38-87da-c219fc31ba64",
    "updatedDate":"2016-06-28",
    "name":"new name",
    "commandType":"UpdateCallCenter"
} 
``` 

Name               | Type                                          | Description
-------------------| ----------------------------------------------| --------------------------------------------------
processUid         | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
updatedDate        | [LocalDate](#localdate)                       | the updated's date of this `Company`  
name               | String                                        | the updated name of this `Company`  
commandType        | Constant                                      | `"UpdateCallCenter"`

## CreateAgency

```json
{
    "processUid":"6ed010a1-7481-4b38-87da-c219fc31ba64",
    "createdDate":"2016-06-28",
    "agency":{
        "agencyUid":"2e761b3c-404e-710b-f3ea-317942ab3fb9",
        "name":"My Agency name",
        "extName":"a public name",
        "address":{
            "number":"12",
            "street":"Rue de la performance",
            "zipCode":"75001",
            "city":"Paris"
        },
        "phones": ["0603245678"],
        "fax": "0123784590",
        "emails": ["myagency@performance-immo.com"]
    },
    "commandType":"CreateAgency"
} 
``` 

Name               | Type                                          | Description
-------------------| ----------------------------------------------| --------------------------------------------------
processUid         | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
createdDate        | [LocalDate](#localdate)                       | the created's date of this `Agency`  
agency             | [RawAgency](#rawagency)                       |   
commandType        | Constant                                      | `"CreateAgency"`

## IncrementAgency

### DeleteAgency
 
```json
{
    "processUid":"6ed010a1-7481-4b38-87da-c219fc31ba64",
    "deletedDate":"2016-06-28",
    "agencyUid":"7634c414-8822-e29d-fe2b-0a18b3174369",
    "commandType":"DeleteAgency"
} 
``` 

Name               | Type                                          | Description
-------------------| ----------------------------------------------| --------------------------------------------------
processUid         | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
deletedDate        | [LocalDate](#localdate)                       |   
agencyUid          | [SafeUUID](#safeuuid)                         |   
commandType        | Constant                                      | `"DeleteAgency"` 
 
### UpdateAgency

```json
{
    "processUid":"6ed010a1-7481-4b38-87da-c219fc31ba64",
    "createdDate":"2016-06-28",
    "agency":{
        "agencyUid":"2e761b3c-404e-710b-f3ea-317942ab3fb9",
        "name":"My Agency name",
        "extName":"a public name",
        "address":{
            "number":"12",
            "street":"Rue de la performance",
            "zipCode":"75001",
            "city":"Paris"
        },
        "phones": ["0603245678"],
        "fax": "0123784590",
        "emails": ["myagency@performance-immo.com"]
    },
    "commandType":"CreateAgency"
} 
``` 

Name               | Type                                          | Description
-------------------| ----------------------------------------------| --------------------------------------------------
processUid         | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
updatedDate        | [LocalDate](#localdate)                       | the updated's date of this `Agency`  
agency             | [RawAgency](#rawagency)                       | the agency updated  
commandType        | Constant                                      | `"UpdateAgency"`

## IncrementPatrimony

### ReferenceBuilding

> json body example :

```json
{
    "processUid":"6ed010a1-7481-4b38-87da-c219fc31ba64",
    "label":"Batiment A",
    "commandType":"ReferenceBuilding"
} 
``` 

Name               | Type                                          | Description
-------------------| ----------------------------------------------| --------------------------------------------------
processUid         | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
label              | String                                        | the label of this `Building`  
commandType        | Constant                                      | `"ReferenceBuilding"`

### AddComplementaryAddressToPatrimony

> json body example :

```json
{
    "processUid":"6ed010a1-7481-4b38-87da-c219fc31ba64",
    "complementaryAddress":{
        "quality":"Entreprise Houdon père & fils",
        "number":"12",
        "street":"rue de la performance",
        "complement":"impasse de l'immobilier",
        "city":"Paris",
        "zipCode":"75001",
        "country":"France",
        "state":"Ile de France",
        "geoLocation":{
            "lat":12.34,
            "lng":15.12
        },
        "checker":{
            "googlePlaceId":"12345"
        }
    },
    "commandType":"AddComplementaryAddressToPatrimony"
} 
``` 

Name                | Type                                                    | Description
------------------- | --------------------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                                   | the uid of this command. Allow PerfImmo to know if this Command is duplicated
complementaryAddress| [PatrimonyAddressReference](#patrimonyaddressreference) | a complementary address is an `Address` that is not referenced by a `Lot` but can be use for this `Patrimony`  
commandType         | Constant                                                | `"AddComplementaryAddressToPatrimony"`

### RemoveComplementaryAddressFromPatrimony

> json body example :

```json
{
    "processUid":"6ed010a1-7481-4b38-87da-c219fc31ba64",
    "addressUid":"2e761b3c-404e-710b-f3ea-317942ab3fb9",
    "commandType":"RemoveComplementaryAddressFromPatrimony"
} 
``` 

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
addressUid          | [SafeUUID](#safeuuid)                         | the uid of the `Address` will be removed  
commandType         | Constant                                      | `"RemoveComplementaryAddressFromPatrimony"`

### UpdatePatrimony

> json body example :

```json
{
    "processUid":"6ed010a1-7481-4b38-87da-c219fc31ba64",
    "ref":"#Patrimony_2",
    "label":"Immeuble des rousses",
    "comment":"un commentaire",
    "commandType":"UpdatePatrimony"
} 
``` 

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
ref                 | String                                        |   
label               | [Option](#option)[String]                     |   
comment             | String                                        |   
commandType         | Constant                                      | `"UpdatePatrimony"`

### AssociatePatrimonyInAgency

> json body example :

```json
{
    "processUid":"6ed010a1-7481-4b38-87da-c219fc31ba64",
    "agencyUid":"2e761b3c-404e-710b-f3ea-317942ab3fb9",
    "commandType":"AssociatePatrimonyInAgency"
} 
``` 

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
agencyUid           | [SafeUUID](#safeuuid)                         | the uid of the agency associated   
commandType         | Constant                                      | `"AssociatePatrimonyInAgency"`

### DissociatePatrimonyFromAgency

> json body example :

```json
{
    "processUid":"6ed010a1-7481-4b38-87da-c219fc31ba64",
    "agencyUid":"2e761b3c-404e-710b-f3ea-317942ab3fb9",
    "commandType":"DissociatePatrimonyFromAgency"
} 
``` 

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
agencyUid           | [SafeUUID](#safeuuid)                         | the uid of the agency dissociated
commandType         | Constant                                      | `"DissociatePatrimonyFromAgency"`

## IncrementProviderContact

### AssociateProviderContactToAgency

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
agencyUid           | [SafeUUID](#safeuuid)                         | the uid of the agency associated
date                | [LocalDate](#localdate)                       | 
commandType         | Constant                                      | `"AssociateProviderContactToAgency"`

### DissociateProviderContactFromAgency

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
agencyUid           | [SafeUUID](#safeuuid)                         | the uid of the agency associated
date                | [LocalDate](#localdate)                       | 
commandType         | Constant                                      | `"DissociateProviderContactFromAgency"`

### UpdateProviderContact

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
name                | [Name](#name)                                 | 
phones              | Array[String]                                 | 
fax                 | Array[String]                                 | 
emails              | Array[String]                                 | 
date                | [DateTime](#datetime)                         | 
commandType         | Constant                                      | `"UpdateProviderContact"`
            
### DisableProviderContact

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
date                | [DateTime](#datetime)                         | 
commandType         | Constant                                      | `"DisableProviderContact"`
            
### EnableProviderContact

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
date                | [DateTime](#datetime)                         | 
commandType         | Constant                                      | `"EnableProviderContact"`            