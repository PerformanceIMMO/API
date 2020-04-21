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
    "billingType":"StandardAccount",
    "createdDate":"2016-06-27",
    "name":"My Client Account",
    "siretNumber":"80242504100018",
    "commandType":"CreateClientAccount"
} 
``` 

Name               | Type                                          | Description
-------------------| ----------------------------------------------| --------------------------------------------------
processUid         | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid       | [Option](#option)[[SafeUUID](#safeuuid)]      | the uid of the resource. Allow you to decide which uid is set to resource you create. If not setted, PerfImmo generate this uid
holdingReference   | [Option](#option)[[SafeUUID](#safeuuid)]      | the uid of the `ClientAccount`'s holding if exist 
callCenterReference| [SafeUUID](#safeuuid)                         | the uid of the `CallCenter` which send this Command  
billingType        | [Option](#option)[[CompanyBillingType](#companybillingtype)]     | the billing type of the company. Optional. Sponsored by default.
createdDate        | [LocalDate](#localdate)                       | the creation's date of this `ClientAccount`  
name               | String                                        | the name of this `ClientAccount`.
siretNumber        | [Option](#option)[[SIRET](#siret)]            | an optional siret number for this `ClientAccount`.
commandType        | Constant                                      | `"CreateClientAccount"`  

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
ClientAccountCreated                      | mandatory                         |
CompanyIdentified                         | optional                          | if `siretNumber` is set
CompanyUpgradedToPremiumAccount           | optional                          | if `billingType` is set with `PremiumAccount`
CompanyUpgradedToStandardAccount          | optional                          | if `billingType` is set with `StandardAccount`

### CreateClientAccountHolding 

```json
{
    "processUid":"6ed010a1-7481-4b38-87da-c219fc31ba64",
    "aggregateUid":"8c12f096-20e6-11ab-8ff7-2c39b4397040",
    "callCenterUid":"f13ede3b-12d9-70ab-4874-e25ab23e33c0",
    "billingType":"PremiumAccount",
    "createdDate":"2016-06-27",
    "name":"My Holding",
    "siretNumber":"80242504100018",
    "commandType":"CreateClientAccountHolding"
} 
``` 

Name               | Type                                          | Description
-------------------| ----------------------------------------------| --------------------------------------------------
processUid         | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid       | [Option](#option)[[SafeUUID](#safeuuid)]      | the uid of the resource. Allow you to decide which uid is set to resource you create. If not setted, PerfImmo generate this uid
callCenterReference| [SafeUUID](#safeuuid)                         | the uid of the `CallCenter` which send this Command
billingType        | [Option](#option)[[CompanyBillingType](#companybillingtype)]     | the billing type of the company. Optional. Sponsored by default.
createdDate        | [LocalDate](#localdate)                       | the creation's date of this `ClientAccountHolding`  
name               | String                                        | the name of this `ClientAccountHolding`.  
siretNumber        | [Option](#option)[[SIRET](#siret)]            | an optional siret number for this `ClientAccountHolding`.
commandType        | Constant                                      | `"CreateClientAccountHolding"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
ClientAccountHoldingCreated               | mandatory                         |
CompanyIdentified                         | optional                          | if `siretNumber` is set
CompanyUpgradedToPremiumAccount           | optional                          | if `billingType` is set with `PremiumAccount`
CompanyUpgradedToStandardAccount          | optional                          | if `billingType` is set with `StandardAccount`

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
    "siretNumber":"80242504100018",
    "commandType":"CreateCallCenter"
} 
``` 

Name               | Type                                          | Description
-------------------| ----------------------------------------------| --------------------------------------------------
processUid         | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid       | [Option](#option)[[SafeUUID](#safeuuid)]      | the uid of the resource. Allow you to decide which uid is set to resource you create. If not setted, PerfImmo generate this uid
createdDate        | [LocalDate](#localdate)                       | the creation's date of this `CallCenter`  
name               | String                                        | the name of this `CallCenter`.  
siretNumber        | [Option](#option)[[SIRET](#siret)]            | an optional siret number for this `CallCenter`.
commandType        | Constant                                      | `"CreateCallCenter"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
CallCenterCreated                         | mandatory                         |
CompanyIdentified                         | optional                          | if `siretNumber` is set
CompanyUpgradedToPremiumAccount           | optional                          | if `billingType` is set with `PremiumAccount`
CompanyUpgradedToStandardAccount          | optional                          | if `billingType` is set with `StandardAccount`

## IncrementCompany

### IdentifyCompany

<aside class="notice">
	You need specifics rights to identify a Company.
</aside>

> IdentifyCompany example : 

```json
{
    "processUid":"6ed010a1-7481-4b38-87da-c219fc31ba64",
    "siretNumber":"80242504100018",
    "commandType":"IdentifyCompany"
} 
```

Name               | Type                                          | Description
-------------------| ----------------------------------------------| --------------------------------------------------
processUid         | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
siretNumber        | [SIRET](#siret)                               | the siret number of the `Company`.  
commandType        | Constant                                      | `"IdentifyCompany"`

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

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
CompanyCanceled                           | mandatory                         |

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

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
CompanyReactived                          | mandatory                         |

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

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
ClientAccountUpdated                      | mandatory                         |

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

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
ClientAccountHoldingUpdated               | mandatory                         |

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

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
CallCenterUpdated                         | mandatory                         |

### UpgradeCompanyToPremiumAccount

```json
{
    "processUid":"6ed010a1-7481-4b38-87da-c219fc31ba64",
    "upgradedDate":"2016-06-28",
    "commandType":"UpgradeCompanyToPremiumAccount"
} 
``` 

Name               | Type                                          | Description
-------------------| ----------------------------------------------| --------------------------------------------------
processUid         | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
upgradedDate       | [LocalDate](#localdate)                       | the updated's date of this `Company`  
commandType        | Constant                                      | `"UpgradeCompanyToPremiumAccount"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
CompanyUpgradedToPremiumAccount           | mandatory                         |

### DowngradePremiumAccount

```json
{
    "processUid":"6ed010a1-7481-4b38-87da-c219fc31ba64",
    "upgradedDate":"2016-06-28",
    "commandType":"DowngradePremiumAccount"
} 
``` 

Name               | Type                                          | Description
-------------------| ----------------------------------------------| --------------------------------------------------
processUid         | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
downgradedDate     | [LocalDate](#localdate)                       | the updated's date of this `Company`  
commandType        | Constant                                      | `"DowngradePremiumAccount"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
PremiumAccountDowngraded                  | mandatory                         |

### UpgradeCompanyToStandardAccount

```json
{
    "processUid":"6ed010a1-7481-4b38-87da-c219fc31ba64",
    "upgradedDate":"2016-06-28",
    "commandType":"UpgradeCompanyToStandardAccount"
} 
``` 

Name               | Type                                          | Description
-------------------| ----------------------------------------------| --------------------------------------------------
processUid         | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
downgradedDate     | [LocalDate](#localdate)                       | the upgraded's date of this `Company`  
commandType        | Constant                                      | `"UpgradeCompanyToStandardAccount"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
CompanyUpgradedToStandardAccount          | mandatory                         |

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

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
AgencyCreated                             | mandatory                         |

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

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
AgencyDeleted                             | mandatory                         |

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

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
AgencyUpdated                             | mandatory                         |

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

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
BuildingReferenced                        | mandatory                         |

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

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
ComplementaryAddressAddedToPatrimony      | mandatory                         |

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

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
ComplementaryAddressRemovedFromPatrimony  | mandatory                         |

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

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
PatrimonyUpdated                          | mandatory                         |

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

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
PatrimonyAssociatedInAgency               | mandatory                         |

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

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
PatrimonyDissociatedFromAgency            | mandatory                         |

## IncrementProviderContact

### AssociateProviderContactToAgency

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
agencyUid           | [SafeUUID](#safeuuid)                         | the uid of the agency associated
date                | [LocalDate](#localdate)                       | 
commandType         | Constant                                      | `"AssociateProviderContactToAgency"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
ProviderContactAssociatedToAgency         | mandatory                         |

### AssociateProviderContactToCompany

Associate this `ProviderContact` to a specific `Company`. 
Works only if the `Company` is a `ClientAccount`

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
companyUid          | [SafeUUID](#safeuuid)                         | the uid of the agency associated
date                | [LocalDate](#localdate)                       | 
commandType         | Constant                                      | `"AssociateProviderContactToCompany"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
ProviderContactAssociatedToCompany        | mandatory                         |

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

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
ProviderContactUpdated                    | mandatory                         |

### DisableProviderContact

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
date                | [DateTime](#datetime)                         | 
commandType         | Constant                                      | `"DisableProviderContact"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
ProviderContactDisabled                   | mandatory                         |

### EnableProviderContact

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
date                | [DateTime](#datetime)                         | 
commandType         | Constant                                      | `"EnableProviderContact"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
ProviderContactEnabled                    | mandatory                         |

### AssociateProviderContactWithProviderCompany

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
providerCompanyUid  | [SafeUUID](#safeuuid)                         | the uid of the `ProviderCompany` with which this `ProviderContact` should be associated. 
commandType         | Constant                                      | `"AssociateProviderContactWithProviderCompany"`            

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
ProviderContactAssociatedWithProviderCompany | mandatory                         |

### AssociateProviderContactWithPatrimony

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
patrimonyUid        | [SafeUUID](#safeuuid)                         | the uid of the `Patrimony` with which this `ProviderContact` should be associated. 
commandType         | Constant                                      | `"AssociateProviderContactWithPatrimony"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
ProviderContactAssociatedWithPatrimony    | mandatory                         |

### DissociateProviderContactFromPatrimony

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
patrimonyUid        | [SafeUUID](#safeuuid)                         | the uid of the `Patrimony` with which this `ProviderContact` should be associated. 
commandType         | Constant                                      | `"DissociateProviderContactFromPatrimony"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
ProviderContactDissociatedFromPatrimony   | mandatory                         |

### AssignActivityToProviderContact

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
activityUidUid      | [SafeUUID](#safeuuid)                         | the uid of the `Activity` assigned to this `ProviderContact` 
includedIncidentTypes | Array[[SafeUUID](#safeuuid)]                | the list of incident type that is managed for this Activity by this `ProviderContact` 
commandType         | Constant                                      | `"AssignActivityToProviderContact"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
ActivityAssignedToProviderContact         | mandatory                         |

### RemoveActivityFromProviderContact

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
activityUidUid      | [SafeUUID](#safeuuid)                         | the uid of the `Activity` should be removed from this `ProviderContact` 
commandType         | Constant                                      | `"RemoveActivityFromProviderContact"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
ActivityRemovedFromProviderContact        | mandatory                         |


### DefineInterventionPeriod

> Example :

```json
{
    "processUid":"17ab7b5b-b7ca-18f6-d5f3-3dfbcbaee1a2",
    "activityUid":"17d706c1-7844-00f5-a4a4-f1afa1975184",
    "period": {
        "label":"ma période",
        "startDate": "2018-02-01T08:00:00.000+01:00",
        "endDate": "2018-11-30T18:00:00.000+02:00",
        "periodType": "DateTimePeriod"
    },
    "commandType":"DefineInterventionPeriod"
}
```

Une période d'intervention est associée à une activité d'un `ProviderContact`.<br/>
Elle définit des plages de dates (sous plusieurs format utiles) où le `ProviderContact` est disponible pour intervention (cf. [InterventionPeriod](#interventionperiod)).

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
activityUid         | [SafeUUID](#safeuuid)                         |
period              | [InterventionPeriodForCommand](#interventionperiodforcommand)     |
commandType         | Constant                                      | `"DefineInterventionPeriod"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
[InterventionPeriodDefined](#interventionperioddefined) | mandatory           |
[InterventionPeriodDefinedAsReferencePeriod](#interventionperioddefinedasreferenceperiod) | Optional | sent if it is the first period created for the activity

### UpdateInterventionPeriod

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
interventionPeriodUid | [SafeUUID](#safeuuid)                         |
period              | [InterventionPeriodForCommand](#interventionperiodforcommand)     |
commandType         | Constant                                      | `"UpdateInterventionPeriod"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
[InterventionPeriodUpdated](#interventionperiodupdated)                 | mandatory                         |

### RemoveInterventionPeriod

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
interventionPeriodUid | [SafeUUID](#safeuuid)                         |
commandType         | Constant                                      | `"RemoveInterventionPeriod"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
[InterventionPeriodRemoved](#interventionperiodremoved)                 | mandatory                         |

### DefineRepairTimelimitForInterventionPeriod

### DefineInterventionTimelimitForInterventionPeriod

### DefineInterventionZoneForInterventionPeriod

### RemoveRepairTimelimitFromInterventionPeriod

### RemoveInterventionTimelimitFromInterventionPeriod

### RemoveInterventionZoneFromInterventionPeriod

### ExcludeOpeningTicketPurposesFromInterventionPeriod

### DefineContract

Name                | Type                                                 | Description
------------------- | -----------------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                                | the uid of this command. Allow PerfImmo to know if this Command is duplicated
label               | [NonEmptyString](#nonemptystring)                    |
contractNumber      | [Option](#option)[[NonEmptyString](#nonemptystring)] |
validityPeriod      | [Option](#option)[[NonEmptyString](#nonemptystring)] |
phoneNumbers        | Array[[PhoneNumber](#phonenumber)]                   |
instructions        | [Option](#option)[[NonEmptyString](#nonemptystring)] |
commentaries        | [Option](#option)[[NonEmptyString](#nonemptystring)] |
activities          | [NonEmptyList](#nonemptylist)[[SafeUUID](#safeuuid)] |
contractor          | [ProviderContractContractor](#providercontractcontractor) | with which entity the `ProviderContact` sign a Contract (ex: with a `Patrimony`)
commandType         | Constant                                             | `"DefineContract"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
[ContractDefined](#contractdefined)       | mandatory                         |


### CancelContract

Name                | Type                                                 | Description
------------------- | -----------------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                                | the uid of this command. Allow PerfImmo to know if this Command is duplicated
contractUid         | [SafeUUID](#safeuuid)                    |
commandType         | Constant                                             | `"CancelContract"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
[ContractCanceled](#contractcanceled)     | mandatory                         |

### FixContract

Name                | Type                                                 | Description
------------------- | -----------------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                                | the uid of this command. Allow PerfImmo to know if this Command is duplicated
contractUid         | [SafeUUID](#safeuuid)                                |
label               | [NonEmptyString](#nonemptystring)                    |
contractNumber      | [Option](#option)[[NonEmptyString](#nonemptystring)] |
validityPeriod      | [Option](#option)[[NonEmptyString](#nonemptystring)] |
phoneNumbers        | Array[[PhoneNumber](#phonenumber)]                   |
instructions        | [Option](#option)[[NonEmptyString](#nonemptystring)] |
commentaries        | [Option](#option)[[NonEmptyString](#nonemptystring)] |
activities          | [NonEmptyList](#nonemptylist)[[SafeUUID](#safeuuid)] |
contractor          | [ProviderContractContractor](#providercontractcontractor) | with which entity the `ProviderContact` sign a Contract (ex: with a `Patrimony`)
commandType         | Constant                                             | `"FixContract"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
[ContractFixed](#contractfixed)           | mandatory                         |

### DefineInterventionPeriodForContract

Name                | Type                                                 | Description
------------------- | -----------------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                                | the uid of this command. Allow PerfImmo to know if this Command is duplicated
contractUid         | [SafeUUID](#safeuuid)                                |
activityUid         | [SafeUUID](#safeuuid)                                |
period              | [InterventionPeriodForCommand](#interventionperiodforcommand)     |
commandType         | Constant                                             | `"DefineInterventionPeriodForContract"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
[InterventionPeriodForContractDefined](#interventionperiodforcontractdefined) | mandatory                         |

### CrushUpdateProviderContact

<aside class="warning">
	Mise à jour non différentielle du `ProviderContact`. Préférez utilisez les commandes d'incrémentation.
</aside>

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
name                | [Name](#name)                                 |
phones              | Array[[PhoneNumber](#phonenumber)]            |
fax                 | Array[[PhoneNumber](#phonenumber)]            |
emails              | Array[String]                                 |
patrimonies         | Array[[SafeUUID](#safeuuid)]                  | list of the patrimonies with which `ProviderContact` is associated
activities          | Array[[ProviderContactActivity](#providercontactactivitycmd)] | list of the activities with which `ProviderContact` is associated
commandType         | Constant                                      | `"CrushUpdateProviderContact"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
ProviderContactUpdated                    | optionnal                         |
ActivityAssignedToProviderContact         | optionnal                         |
ActivityRemovedFromProviderContact        | optionnal                         |
ProviderContactAssociatedWithPatrimony    | optionnal                         |
ProviderContactDissociatedFromPatrimony   | optionnal                         |


### CrushUpdateContracts

<aside class="warning">
	Mise à jour non différentielle des Contrats du `ProviderContact`. Préférez utilisez les commandes d'incrémentation.
</aside>

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
contracts           | Array[[ContractForProviderContact](#contractforprovidercontact)] | list of all contracts of a `ProviderContract`.
commandType         | Constant                                      | `"CrushUpdateContracts"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
[ContractDefined](#contractdefined)       | optionnal                         |
[ContractCanceled](#contractcanceled)     | optionnal                         |
[ContractFixed](#contractfixed)           | optionnal                         |


## OpenTicket

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
locationRef         | [LocationReference](#locationreference)       | a reference to another resource (`Agency`, `Patrimony`, etc...)
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. We can say who open this `Ticket`. 
ticket              | [TicketInfos](#ticketinfos)                   | infos specific to the `Ticket` opened. 
openedDate          | [DateTime](#datetime)                         | the opened date of this `Ticket`.
commandType         | Constant                                      | `"OpenTicket"`

## IncrementTicket

### EmitCallTo 

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
recipient           | [Persona](#persona)                           | the recipient of this call.
comment             | [Option](#option)[String]                     |
medium              | [ContactMedium](#contactmedium)               | the medium used to perform this call.
date                | [DateTime](#datetime)                         | 
commandType         | Constant                                      | `"EmitCallTo"`

### ReceiveCall

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
callPurpose         | String                                        | purpose of the call.
caller              | String                                        | 
comment             | [Option](#option)[String]                     |
medium              | [ContactMedium](#contactmedium)               | the medium used to perform this call.
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
commandType         | Constant                                      | `"ReceiveCall"`

### IdentifyAssignee

> IdentifyAssignee example : 

```json
{
  "processUid": "f5391199-e544-60f3-037c-16f3229fd59d",
  "operator": {
    "operatorUid": "98bfb3a8-ae4a-7486-1ee3-96131d994801",
    "operatorType": "ReferencedOperator"
  },
  "assignee": {
    "providerUid": "7943797a-93c4-73f9-48f8-6baea5e94d13",
    "assigneeType": "ReferencedProviderContact"
  },
  "comment":"an optionnal commentary",
  "date": "2018-08-28T16:33:00:000+02:00",
  "commandType": "IdentifyAssignee"
}
```

Report this `TicketAssignee` is identified to resolve the issue brought by the `Ticket`.

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. (if doesn't set, setted by the server)
assignee            | [TicketAssignee](#ticketassignee)             | a reference to the `TicketAssignee` identified on this `Ticket`.
comment             | [Option](#option)[String]                     |
instructions        | [Option](#option)[String]                     | some instructions for the assignee to perform his mission. If valued, produce `InstructionsForAssigneeDefined` event.
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
commandType         | Constant                                      | `"IdentifyAssignee"`

### RequestIntervention

> RequestIntervention example :

```json
{
    "processUid":"127621-1298217-1298721",
    "operator": {
        "operatorUid":"127621-1298217-1298721",
        "operatorType":"ReferencedOperator"
    },
    "assignee": {
        "providerUid":"1234-987798_865765",
        "assigneeType":"ReferencedProviderCompany"
    },
    "medium": {
        "phone":"0123456783",
        "contactMediumType":"Phone"
    },
    "comment": "an optionnal commentary",
    "date":"2018-08-28T16:33:00:000+02:00",
    "commandType":"RequestIntervention"
}
```

Report the identified `TicketAssignee` was contacted to request intervention to resolve `Ticket` issue.

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. (if doesn't set, setted by the server)
assignee            | [TicketAssignee](#ticketassignee)             | a reference to the `TicketAssignee` requested (Must be the same as identified one).
medium              | [ContactMedium](#contactmedium)               | the medium used to perform this request.
comment             | [Option](#option)[String]                     |
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
commandType         | Constant                                      | `"RequestIntervention"`

### ReportSendingServiceOrder

> ReportSendingServiceOrder example : 

```json
{
    "processUid":"5deed63d-a7f4-254e-9127-7c177d7fd5a8",
    "operator": {
         "operatorUid": "98bfb3a8-ae4a-7486-1ee3-96131d994801",
         "operatorType": "ReferencedOperator"
    },
    "provider": {
         "providerUid": "7943797a-93c4-73f9-48f8-6baea5e94d13",
         "providerType": "ReferencedProvider"
    },
    "ref":"AEX34J",
    "reportDate":"2016-08-18T16:40:51.000+02:00",
    "sendingDate":"2016-08-18T16:40:51.000+02:00",
    "commandType":"ReportSendingServiceOrder"
}
```

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. 
assignee            | [TicketAssignee](#ticketassignee)             | a reference to the `TicketAssignee` for who sending service order is reported (Must be the same as identified one).
ref                 | String                                        | the reference of the service order sent.
reportDate          | [DateTime](#datetime)                         | date on which the `Event` took place.
sendingDate         | [DateTime](#datetime)                         | date when the service order was sent.
commandType         | Constant                                      | `"ReportSendingServiceOrder"`

### ProviderAnswerCall

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
provider            | [Provider](#provider)                         | a reference to the `Provider` who answer.
comment             | String                                        | 
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
commandType         | Constant                                      | `"ProviderAnswerCall"`

### ProviderNotAnswerCall

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
provider            | [Provider](#provider)                         | a reference to the `Provider` who not answer.
comment             | String                                        | 
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
commandType         | Constant                                      | `"ProviderNotAnswerCall"`

### ScheduleIntervention

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
assignee            | [TicketAssignee](#ticketassignee)             | a reference to the `TicketAssignee` for who intervention is scheduled (Must be the same as identified one).
comment             | [Option](#option)[String]                     | 
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
startDate           | [DateTime](#datetime)                         | the start date of this scheduled intervention.
endDate             | [DateTime](#datetime)                         | the end date of this scheduled intervention.
commandType         | Constant                                      | `"ScheduleIntervention"`

### DefineInterventionDeadline

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
assignee            | [TicketAssignee](#ticketassignee)             | a reference to the `TicketAssignee` for who intervention deadline is defined (Must be the same as identified one).
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
deadline            | [DateTime](#datetime)                         | the deadline defined.
commandType         | Constant                                      | `"DefineInterventionDeadline"`

### ReportFormalNoticeForProvider

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
ref                 | [Option](#option)[String]                     | an optional reference to this formal notice.
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
assignee            | [TicketAssignee](#ticketassignee)             | a reference to the `TicketAssignee` for who formal notice is reported (Must be the same as identified one).
reportDate          | [DateTime](#datetime)                         | date on which the `Event` took place.
deadline            | [DateTime](#datetime)                         | a new deadline defined.
commandType         | Constant                                      | `"ReportFormalNoticeForProvider"`

### AcceptIntervention

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
assignee            | [TicketAssignee](#ticketassignee)             | a reference to the `TicketAssignee` who accept the intervention (Must be the same as identified one).
comment             | [Option](#option)[String]                     |
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
requestNotificationTo | [Option](#option)[[EmailsForNotificationFor](#emailsfornotificationfor)] | set it if you want sent a notification to some actors. (produce [NotificationForInterventionAcceptedRequested](#notificationforinterventionacceptedrequested) event)
commandType         | Constant                                      | `"AcceptIntervention"`

### RefuseIntervention

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
assignee            | [TicketAssignee](#ticketassignee)             | a reference to the `TicketAssignee` who refuse the intervention (Must be the same as identified one).
comment             | [Option](#option)[String]                     |
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
commandType         | Constant                                      | `"RefuseIntervention"`

### ReopenTicket

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
purpose             | Option[String]                                | the reason why the `Ticket` was reopened. 
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
commandType         | Constant                                      | `"ReopenTicket"`

### AddLogTrial

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
provider            | [Option](#option)[[Provider](#provider)]      | 
logTrial            | [LogTrial](#logtrial)                         | 
logTrialAddedDate   | [DateTime](#datetime)                         | date on which the `Event` took place.
commandType         | Constant                                      | `"AddLogTrial"`

### AddMessage

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
message             | String                                        | 
messageAddedDate    | [DateTime](#datetime)                         | date on which the `Event` took place.
commandType         | Constant                                      | `"AddMessage"`

### CancelTicket

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
comment             | [Option](#option)[String]                     | Explain what happened.
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
commandType         | Constant                                      | `"CancelTicket"`

### ArriveOnSite

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
assignee            | [TicketAssignee](#ticketassignee)             | a reference to the `TicketAssignee` for who arrive on site (Must be the same as identified one).
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
commandType         | Constant                                      | `"ArriveOnSite"`

### GoFromSite

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
assignee            | [TicketAssignee](#ticketassignee)             | a reference to the `TicketAssignee` who gone from site (Must be the same as identified one).
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
commandType         | Constant                                      | `"GoFromSite"`

### StartIntervention

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
assignee            | [TicketAssignee](#ticketassignee)             | a reference to the `TicketAssignee` who start the intervention (Must be the same as identified one).
startedDate         | [DateTime](#datetime)                         | date on which the `Event` took place.
commandType         | Constant                                      | `"StartIntervention"`

### FinishIntervention

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
assignee            | [TicketAssignee](#ticketassignee)             | a reference to the `TicketAssignee` who finish the intervention (Must be the same as identified one).
finishedDate        | [DateTime](#datetime)                         | date on which the `Event` took place.
commandType         | Constant                                      | `"FinishIntervention"`

### UpdateTicket

A compensation 'Command' to correct issue in the original `OpenTicket`. 
Don't use it for increment the `Ticket` state. Use the others `Command` for that.

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
locationRef         | [LocationReference](#locationreference)       | a reference to another resource (`Agency`, `Patrimony`, etc...)
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. We can say who update this `Ticket`. 
ticket              | [TicketInfos](#ticketinfos)                   | infos specific to the `Ticket` opened. 
openedDate          | [DateTime](#datetime)                         | the opened date of this `Ticket`.
commandType         | Constant                                      | `"UpdateTicket"`

### CorrectTicketInformations
 

> CorrectTicketInformations example : 

```json
{
    "processUid":"5deed63d-a7f4-254e-9127-7c177d7fd5a8",
    "operator": {
         "operatorUid": "98bfb3a8-ae4a-7486-1ee3-96131d994801",
         "operatorType": "ReferencedOperator"
    },
 	"fieldsToCorrect": {
 		"request": "TicketInfos.request field updated"
 	},   
    "date":"2016-08-18T16:40:51.000+02:00",
    "commandType":"CorrectTicketInformations"
}
``` 
 
A compensation 'Command' to correct some text informations in `Ticket`. <br/>
If you set a field with value, this field will be overwritten by this new value. <br/>
It is forbidden to set a field with blank value.

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
fieldsToCorrect     | [FieldsToCorrect](#fieldstocorrect)           | a 'list' of optional field to correct
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. We can say who update this `Ticket`. 
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
commandType         | Constant                                      | `"CorrectTicketInformations"`

### CorrectTicketEventInformations
 

> CorrectTicketEventInformations example : 

```json
{
    "processUid":"5deed63d-a7f4-254e-9127-7c177d7fd5a8",
    "targetedEvent":"5deed63d-a7f4-254e-9127-7c177d7fd5a7",
    "operator": {
         "operatorUid": "98bfb3a8-ae4a-7486-1ee3-96131d994801",
         "operatorType": "ReferencedOperator"
    },
 	"text":"text updated",   
    "date":"2016-08-18T16:40:51.000+02:00",
    "commandType":"CorrectTicketEventInformations"
}
``` 
 
A compensation 'Command' to correct some text informations in the `Ticket` journal `Event`. <br/>
Only few `Event` can see their text updated :<br/>
- MessageAdded.message <br/>
- CallReceived.comment <br/>
- CallEmittedTo.comment

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated.
targetedEvent       | [SafeUUID](#safeuuid)                         | the uid of the `Event` whose text has been updated.
text                | String                                        | the new text of the targeted `Event`.
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. We can say who update this `Ticket`. 
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
commandType         | Constant                                      | `"CorrectTicketEventInformations"`

### CorrectOpeningTicketPurpose

<aside class="notice">
The following commands are only available if Ticket is not already linked with an assignee.
</aside>

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
otpLabel            | String                                        | the new opening ticket purpose label to correct.
otpUid              | [Option](#option)[[SafeUUID](#safeuuid)]      | the new opening ticket purpose uid to correct.
commandType         | Constant                                      | `"CorrectOpeningTicketPurpose"`

### CorrectLocationReference

<aside class="notice">
The following command are only available if Ticket is not already linked with an assignee.
</aside>

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
address             | [BasicAddress](#basicaddress)                 | the new address to correct.
locationReference   | [LocationReference](#locationreference)       | the new locationReference to correct.
commandType         | Constant                                      | `"CorrectLocationReference"`

### CorrectCaller

<aside class="notice">
The following command are only available if Ticket is not already linked with an assignee.
</aside>

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
caller              | [CallerType](#callertype)                     |
commandType         | Constant                                      | `"CorrectCaller"`

<br/>
<br/>

<aside class="notice">
The following command are made to close the Ticket.
</aside>

### CloseTicket

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
provider            | [Option](#option)[[Provider](#provider)]      | a reference to the `Provider` who close the `Ticket`.
brakedownNature     | [Option](#option)[String]                     | an optional explanation of the reason of the breakedown.
stillOnSite         | [StillOnSite](#stillonsite)                   | 
report              | [Option](#option)[String]                     | an optional explanation of the intervention.
result              | [Option](#option)[String]                     |
closingDate         | [DateTime](#datetime)                         | date on which the `Event` took place.
commandType         | Constant                                      | `"CloseTicket"`

### CancelTicket

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
comment             | [Option](#option)[String]                     |
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
commandType         | Constant                                      | `"CancelTicket"`

### ArchiveTicket

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
comment             | [Option](#option)[String]                     | 
closingDate         | [DateTime](#datetime)                         | date on which the `Event` took place.
commandType         | Constant                                      | `"ArchiveTicket"`

### FixPermanently

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
provider            | [Option](#option)[[Provider](#provider)]      | a reference to the `Provider` who close the `Ticket`.
brakedownNature     | [Option](#option)[String]                     | an optional explanation of the reason of the breakedown.
stillOnSite         | [StillOnSite](#stillonsite)                   | 
report              | [Option](#option)[String]                     | an optional explanation of the intervention.
closingDate         | [DateTime](#datetime)                         | date on which the `Event` took place.
commandType         | Constant                                      | `"FixPermanently"`

### FixPartially

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
provider            | [Option](#option)[[Provider](#provider)]      | a reference to the `Provider` who close the `Ticket`.
brakedownNature     | [Option](#option)[String]                     | an optional explanation of the reason of the breakedown.
stillOnSite         | [StillOnSite](#stillonsite)                   | 
report              | [Option](#option)[String]                     | an optional explanation of the intervention.
closingDate         | [DateTime](#datetime)                         | date on which the `Event` took place.
commandType         | Constant                                      | `"FixPartially"`

### CloseTicketImpossibleRepair

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
provider            | [Option](#option)[[Provider](#provider)]      | a reference to the `Provider` who close the `Ticket`.
brakedownNature     | [Option](#option)[String]                     | an optional explanation of the reason of the breakedown.
stillOnSite         | [StillOnSite](#stillonsite)                   | 
report              | [Option](#option)[String]                     | an optional explanation of the intervention.
closingDate         | [DateTime](#datetime)                         | date on which the `Event` took place.
commandType         | Constant                                      | `"CloseTicketImpossibleRepair"`

### PostponeFix

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
provider            | [Option](#option)[[Provider](#provider)]      | a reference to the `Provider` who close the `Ticket`.
brakedownNature     | [Option](#option)[String]                     | an optional explanation of the reason of the breakedown.
stillOnSite         | [StillOnSite](#stillonsite)                   | 
report              | [Option](#option)[String]                     | an optional explanation of the intervention.
closingDate         | [DateTime](#datetime)                         | date on which the `Event` took place.
commandType         | Constant                                      | `"PostponeFix"`

### CloseBeyondCallCenterScope

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
closingDate         | [DateTime](#datetime)                         | date on which the `Event` took place.
comment             | [Option](#option)[String]                     | Explain what happened.
commandType         | Constant                                      | `"CloseBeyondCallCenterScope"`

### CloseAfterSeveralUnsuccessfulRecalls

After several attempt, it seems it is impossible to contact a `Provider` to resolve this `Ticket`. 

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`.
closingDate         | [DateTime](#datetime)                         | date on which the `Event` took place.
comment             | [Option](#option)[String]                     | Explain what happened.
commandType         | Constant                                      | `"CloseAfterSeveralUnsuccessfulRecalls"`

## IncrementLot

### AddAddressToLot

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
address             | [LotAddressReference](#lotaddressreference)   |
commandType         | Constant                                      | `"AddAddressToLot"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
AddressAddedToLot                         | mandatory                         |

### RemoveAddressFromLot

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
addressUid          | [SafeUUID](#safeuuid)                         |
commandType         | Constant                                      | `"RemoveAddressFromLot"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
AddressRemovedFromLot                         | mandatory                         |

### UpdateLotReference

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
ref                 | [NonEmptyString](#nonemptystring)             |
commandType         | Constant                                      | `"UpdateLotReference"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
LotReferenceUpdated                       | mandatory                         |

### UpdateLotNumber

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
lotNumber           | [NonEmptyString](#nonemptystring)             |
commandType         | Constant                                      | `"UpdateLotNumber"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
LotNumberUpdated                          | mandatory                         |

### UpdateLotUsage(processUid: SafeUUID, usage: LotUsage) extends IncrementLotJsonCommand

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
usage               | [LotUsage](#lotusage)                         |
commandType         | Constant                                      | `"UpdateLotUsage"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
LotUsageUpdated                           | mandatory                         |

### DeleteLot

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
commandType         | Constant                                      | `"DeleteLot"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
LotDeleted                                | mandatory                         |

## IncrementPatrimonyContact

### ReferencePatrimonyContact

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [Option](#option)[[SafeUUID](#safeuuid)]      | the uid of the resource. Allow you to decide which uid is set to resource you create. If not setted, PerfImmo generate this uid
name                | [Name](#name)                                 |
address             | [Option](#option)[[PatrimonyContactAddressReference](#patrimonyaddressreference)] | an optional address for this `PatrimonyContact`
contacts            | [NonEmptyList](#nonemptylist)[[ContactMedium](#contactmedium)] | a non empty list of contact like phone number or email 
commandType         | Constant                                      | `"ReferencePatrimonyContact"`

### LinkPatrimonyContactWith

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
linkedWith          | [NonEmptyList](#nonemptylist)[[PatrimonyContactEntityLink](#patrimonycontactentitylink)] | a non empty list of link to several `Patrimony` or `Lot`entity. 
commandType         | Constant                                      | `"LinkPatrimonyContactWith"`


### RemoveLinkFromPatrimonyContact

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
linkedWith          | [NonEmptyList](#nonemptylist)[[PatrimonyContactEntityLink](#patrimonycontactentitylink)] | a non empty list of link to several `Patrimony` or `Lot`entity. 
commandType         | Constant                                      | `"RemoveLinkFromPatrimonyContact"`

### AddContact

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
contact             | [ContactMedium](#contactmedium)               | a contact like phone number or email 
commandType         | Constant                                    | `"AddContact"`

### RemoveContact

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
contact             | [ContactMedium](#contactmedium)               | a contact like phone number or email 
commandType         | Constant                                      | `"RemoveContact"`


### UpdatePatrimonyContactIdentity

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
name                | [Option](#option)[[Name](#name)]              | if None, field not updated
address             | [Option](#option)[[PatrimonyContactAddressReference](#patrimonyaddressreference)] | if None, field not updated 
commandType         | Constant                                      | `"UpdatePatrimonyContactIdentity"`

### LinkPatrimonyContactWithUser

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
userUid             | [SafeUUID](#safeuuid)                         | 
commandType         | Constant                                      | `"LinkPatrimonyContactWithUser"`

## ReferenceUserCommand

### ReferenceClientAccountManager

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [Option](#option)[[SafeUUID](#safeuuid)]      | the uid of the resource. Allow you to decide which uid is set to resource you create. If not setted, PerfImmo generate this uid
login               | String                                        | the login of the user (must be a valid email).
companyUid          | [SafeUUID](#safeuuid)                         | the uid of the user's `ClientCompany`
firstName           | String                                        |
lastName            | String                                        |
job                 | [Option](#option)[String]                     | just a label to explain the role of the user.
phone               | [Option](#option)[String]                     |
commandType         | Constant                                      | `"ReferenceClientAccountManager"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
ClientAccountManagerReferenced            | mandatory                         |

### ReferenceExecutive

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [Option](#option)[[SafeUUID](#safeuuid)]      | the uid of the resource. Allow you to decide which uid is set to resource you create. If not setted, PerfImmo generate this uid
login               | String                                        | the login of the user (must be a valid email).
companyUid          | [SafeUUID](#safeuuid)                         | the uid of the user's `ClientCompany`
managedAgencies     | [NonEmptyList](#nonemptylist)[[SafeUUID](#safeuuid)] | the non empty list of the executive's agencies.
firstName           | String                                        |
lastName            | String                                        |
job                 | [Option](#option)[String]                     | just a label to explain the role of the user. Useful to calcul the user's rights on the data.
phone               | [Option](#option)[String]                     |
commandType         | Constant                                      | `"ReferenceExecutive"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
ExecutiveReferenced                       | mandatory                         |

### ReferencePatrimonyManager

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [Option](#option)[[SafeUUID](#safeuuid)]      | the uid of the resource. Allow you to decide which uid is set to resource you create. If not setted, PerfImmo generate this uid
login               | String                                        | the login of the user (must be a valid email).
companyUid          | [SafeUUID](#safeuuid)                         | the uid of the user's `ClientCompany`
managedPatrimonies  | [NonEmptyList](#nonemptylist)[[SafeUUID](#safeuuid)] | the non empty list of the patrimonyManager's patrimonies.
firstName           | String                                        |
lastName            | String                                        |
job                 | [Option](#option)[String]                     | just a label to explain the role of the user. Useful to calcul the user's rights on the data.
phone               | [Option](#option)[String]                     |
commandType         | Constant                                      | `"ReferencePatrimonyManager"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
PatrimonyManagerReferenced                | mandatory                         |

### ReferencePatrimonyUser

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [Option](#option)[[SafeUUID](#safeuuid)]      | the uid of the resource. Allow you to decide which uid is set to resource you create. If not setted, PerfImmo generate this uid
login               | [NonEmptyString](#nonemptystring)             | the login of the user (must be a valid email).
patrimonies         | [NonEmptyList](#nonemptylist)[[SafeUUID](#safeuuid)] | the non empty list of the user's patrimonies.
firstName           | [Option](#option)[[NonEmptyString](#nonemptystring)] |
lastName            | [NonEmptyString](#nonemptystring)             |
phone               | [Option](#option)[[PhoneNumber](#phonenumber)]|
externalLoginService | [Option](#option)[String]                    | Name of the service sso. ex: `"Lodaweb"`
commandType         | Constant                                      | `"ReferencePatrimonyUser"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
PatrimonyUserReferenced                   | mandatory                         |

## IncrementUserCommand

### AssociateUserWithAgency

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [Option](#option)[[SafeUUID](#safeuuid)]      | the uid of the resource. Allow you to decide which uid is set to resource you create. If not setted, PerfImmo generate this uid
agencyUid           | [SafeUUID](#safeuuid)                         |
commandType         | Constant                                      | `"AssociateUserWithAgency"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
UserAssociatedWithAgency                  | mandatory                         |

### DissociateUserFromAgency

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [Option](#option)[[SafeUUID](#safeuuid)]      | the uid of the resource. Allow you to decide which uid is set to resource you create. If not setted, PerfImmo generate this uid
agencyUid           | [SafeUUID](#safeuuid)                         |
commandType         | Constant                                      | `"DissociateUserFromAgency"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
UserDissociatedFromAgency                 | mandatory                         |

### AssociateUserWithPatrimony

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [Option](#option)[[SafeUUID](#safeuuid)]      | the uid of the resource. Allow you to decide which uid is set to resource you create. If not setted, PerfImmo generate this uid
patrimonyUid        | [SafeUUID](#safeuuid)                         |
commandType         | Constant                                      | `"AssociateUserWithPatrimony"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
UserAssociatedWithPatrimony               | mandatory                         |

### DissociateUserFromPatrimony

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [Option](#option)[[SafeUUID](#safeuuid)]      | the uid of the resource. Allow you to decide which uid is set to resource you create. If not setted, PerfImmo generate this uid
patrimonyUid        | [SafeUUID](#safeuuid)                         |
commandType         | Constant                                      | `"DissociateUserFromPatrimony"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
UserDissociatedFromPatrimony              | mandatory                         |

### DisableUser

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [Option](#option)[[SafeUUID](#safeuuid)]      | the uid of the resource. Allow you to decide which uid is set to resource you create. If not setted, PerfImmo generate this uid
commandType         | Constant                                      | `"DisableUser"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
UserDisabled                              | mandatory                         |

### DowngradeExecutiveToPatrimonyManager

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [Option](#option)[[SafeUUID](#safeuuid)]      | the uid of the resource. Allow you to decide which uid is set to resource you create. If not setted, PerfImmo generate this uid
managedPatrimonies  | [NonEmptyList](#nonemptylist)[[SafeUUID](#safeuuid)] |
commandType         | Constant                                      | `"DowngradeExecutiveToPatrimonyManager"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
ExecutiveDowngradedToPatrimonyManager     | mandatory                         |

### UpdateUser

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
firstName           | String                                        |
lastName            | String                                        |
job                 | [Option](#option)[String]                     |
phone               | [Option](#option)[[PhoneNumber](#phonenumber)]|
commandType         | Constant                                      | `"UpdateUser"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
UserUpdated                               | mandatory                         |

### UpdateLogin

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
login               | [NonEmptyString](#nonemptystring)             |
commandType         | Constant                                      | `"UpdateLogin"`

Events answered                           | Optional or Mandatory in answer   | Rule / Comment
------------------------------------------| ----------------------------------| -------------
LoginUpdated                              | mandatory                         |


## QualifySimplifiedRequest

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
ticketUid           | [SafeUUID](#safeuuid)                         | 
commandType         | Constant                                      | `"QualifySimplifiedRequest"`
