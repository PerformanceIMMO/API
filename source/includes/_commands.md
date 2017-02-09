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

### AssociateProviderContactToCompany

Associate this `ProviderContact` to a specific `Company` and by inheritance to all of its `Agencies`. 
Works only if the `Company` is a `ClientAccount`(i.e have agencies itself)

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
companyUid          | [SafeUUID](#safeuuid)                         | the uid of the agency associated
date                | [LocalDate](#localdate)                       | 
commandType         | Constant                                      | `"AssociateProviderContactToCompany"`

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

### AssignProvider

> AssignProvider example : 

```json
{
  "processUid": "f5391199-e544-60f3-037c-16f3229fd59d",
  "operator": {
    "operatorUid": "98bfb3a8-ae4a-7486-1ee3-96131d994801",
    "operatorType": "ReferencedOperator"
  },
  "provider": {
    "providerUid": "7943797a-93c4-73f9-48f8-6baea5e94d13",
    "providerType": "ReferencedProvider"
  },
  "purpose": {
    "comment": "Choix du contact par l'opérateur",
    "providerAssignationPurposeType": "RecourseChanged"
  },
  "date": "2016-08-25T15:31:53.000+02:00",
  "commandType": "AssignProvider"
}
```

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
provider            | [Provider](#provider)                         | a reference to the `Provider` assigned to this `Ticket`.
purpose             | [ProviderAssignationPurpose](#providerassignationpurpose) | the purpose of this assignation. (can be RecourseChanged).
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
commandType         | Constant                                      | `"AssignProvider"`

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
provider            | [Provider](#provider)                         | a reference to the `Provider` assigned to this `Ticket`.
ref                 | String                                        | the reference of the service order sent.
reportDate          | [DateTime](#datetime)                         | date on which the `Event` took place.
sendingDate         | [DateTime](#datetime)                         | date when the service order was sending.
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

### ScheduleMission

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
provider            | [Provider](#provider)                         | a reference to the `Provider` who will perform the mission.
comment             | [Option](#option)[String]                     | 
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
startDate           | [DateTime](#datetime)                         | the start date of this scheduled mission.
endDate             | [DateTime](#datetime)                         | the end date of this scheduled mission.
commandType         | Constant                                      | `"ScheduleMission"`

### DefineInterventionDeadline

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
provider            | [Provider](#provider)                         | a reference to the `Provider` who will perform the mission.
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
deadline            | [DateTime](#datetime)                         | the deadline defined.
commandType         | Constant                                      | `"DefineInterventionDeadline"`

### ReportFormalNoticeForProvider

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
ref                 | [Option](#option)[String]                     | an optional reference to this formal notice.
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
provider            | [Provider](#provider)                         | a reference to the `Provider` who will perform the mission.
reportDate          | [DateTime](#datetime)                         | date on which the `Event` took place.
deadline            | [DateTime](#datetime)                         | a new deadline defined.
commandType         | Constant                                      | `"ReportFormalNoticeForProvider"`

### AcceptMission

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
provider            | [Provider](#provider)                         | a reference to the `Provider` who accept the mission.
comment             | String                                        | 
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
commandType         | Constant                                      | `"AcceptMission"`

### RefuseMission

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
provider            | [Provider](#provider)                         | a reference to the `Provider` who refuse the mission.
comment             | String                                        | 
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
commandType         | Constant                                      | `"RefuseMission"`

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
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
commandType         | Constant                                      | `"CancelTicket"`

### ArriveOnSite

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
provider            | [Provider](#provider)                         | a reference to the `Provider` who arrive on site.
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
commandType         | Constant                                      | `"ArriveOnSite"`

### GoFromSite

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
provider            | [Provider](#provider)                         | a reference to the `Provider` who gone from site.
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
commandType         | Constant                                      | `"GoFromSite"`

### StartIntervention

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
provider            | [Provider](#provider)                         | a reference to the `Provider` who start the intervention.
startedDate         | [DateTime](#datetime)                         | date on which the `Event` took place.
commandType         | Constant                                      | `"StartIntervention"`

### FinishIntervention

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`. 
provider            | [Provider](#provider)                         | a reference to the `Provider` who finish the intervention.
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
date                | [DateTime](#datetime)                         | the opened date of this `Ticket`.
commandType         | Constant                                      | `"CorrectTicketInformations"`

<aside class="notice">
The following commands are made to close the Ticket.
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
commandType         | Constant                                      | `"CloseBeyondCallCenterScope"`

### CloseAfterSeveralUnsuccessfulRecalls

After several attempt, it seems it is impossible to contact a `Provider` to resolve this `Ticket`. 

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
operator            | [Option](#option)[[Operator](#operator)]      | an optional reference to who perform for this `Command`.
closingDate         | [DateTime](#datetime)                         | date on which the `Event` took place.
commandType         | Constant                                      | `"CloseAfterSeveralUnsuccessfulRecalls"`
