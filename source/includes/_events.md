# Events

## CompanyEvent

### ClientAccountCreated

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
createdDate         | [LocalDate](#localdate)                       |
holdingReference    | [Option](#option)[SafeUUID]                   |
callCenterReference | [SafeUUID](#safeuuid)                         |
name                | String                                        |
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
eventType           | Constant                                      | `"ClientAccountCreated"`

### CallCenterCreated

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
createdDate         | [LocalDate](#localdate)                       |
name                | String                                        |
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
eventType           | Constant                                      | `"CallCenterCreated"`

### ClientAccountHoldingCreated

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
createdDate         | [LocalDate](#localdate)                       |
callCenterReference | [SafeUUID](#safeuuid)                         |
name                | String                                        |
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
eventType           | Constant                                      | `"ClientAccountHoldingCreated"`

### CompanyIdentified

> CompanyIdentified example :

```json
{
	"processUid":"8c12f096-20e6-11ab-8ff7-2c39b4397040",
    "aggregateUid":"7634c414-8822-e29d-fe2b-0a18b3174369",
    "siretNumber":"80242504100018",
    "sentDate":"2016-02-29T12:03:32+02:00",
	"eventType":"CompanyIdentified"
}
```

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
siretNumber         | [SIRET](#siret)                               | the siret number of the `Company`.
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
eventType           | Constant                                      | `"CallReceived"`

### CompanyCanceled

Name               | Type                                          | Description
-------------------| ----------------------------------------------| --------------------------------------------------
processUid         | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid       | [SafeUUID](#safeuuid)                         | the uid of the resource.
canceledDate       | [LocalDate](#localdate)                       |
sentDate           | [DateTime](#datetime)                         | the received date of this `Event`.
eventType          | Constant                                      | `"CompanyCanceled"`

### CompanyReactivated

Name               | Type                                          | Description
-------------------| ----------------------------------------------| --------------------------------------------------
processUid         | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid       | [SafeUUID](#safeuuid)                         | the uid of the resource.
reactivatedDate    | [LocalDate](#localdate)                       |
sentDate           | [DateTime](#datetime)                         | the received date of this `Event`.
eventType          | Constant                                      | `"CompanyReactivated"`

### ClientAccountUpdated

Name               | Type                                          | Description
-------------------| ----------------------------------------------| --------------------------------------------------
processUid         | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid       | [SafeUUID](#safeuuid)                         | the uid of the resource.
updatedDate        | [LocalDate](#localdate)                       |
name               | String
sentDate           | [DateTime](#datetime)                         | the received date of this `Event`.
eventType          | Constant                                      | `"ClientAccountUpdated"`

### ClientAccountHoldingUpdated

Name               | Type                                          | Description
-------------------| ----------------------------------------------| --------------------------------------------------
processUid         | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid       | [SafeUUID](#safeuuid)                         | the uid of the resource.
updatedDate        | [LocalDate](#localdate)                       |
name               | String
sentDate           | [DateTime](#datetime)                         | the received date of this `Event`.
eventType          | Constant                                      | `"ClientAccountHoldingUpdated"`

### CallCenterUpdated

Name               | Type                                          | Description
-------------------| ----------------------------------------------| --------------------------------------------------
processUid         | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid       | [SafeUUID](#safeuuid)                         | the uid of the resource.
updatedDate        | [LocalDate](#localdate)                       |
name               | String
sentDate           | [DateTime](#datetime)                         | the received date of this `Event`.
eventType          | Constant                                      | `"CallCenterUpdated"`

### CompanyUpgradedToPremiumAccount

Name               | Type                                          | Description
-------------------| ----------------------------------------------| --------------------------------------------------
processUid         | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid       | [SafeUUID](#safeuuid)                         | the uid of the resource.
upgradedDate       | [LocalDate](#localdate)                       |
sentDate           | [DateTime](#datetime)                         | the received date of this `Event`.
eventType          | Constant                                      | `"CompanyUpgradedToPremiumAccount"`

### PremiumAccountDowngraded

Name               | Type                                          | Description
-------------------| ----------------------------------------------| --------------------------------------------------
processUid         | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid       | [SafeUUID](#safeuuid)                         | the uid of the resource.
downgradedDate     | [LocalDate](#localdate)                       |
sentDate           | [DateTime](#datetime)                         | the received date of this `Event`.
eventType          | Constant                                      | `"PremiumAccountDowngraded"`

### CompanyUpgradedToStandardAccount

> CompanyUpgradedToStandardAccount example :

```json
{
    "processUid":"6ed010a1-7481-4b38-87da-c219fc31ba64",
    "aggregateUid":"7634c414-8822-e29d-fe2b-0a18b3174369",
    "upgradedDate":"2016-06-28",
    "sentDate":"2016-06-28T12:03:32+02:00",
    "eventType":"CompanyUpgradedToStandardAccount"
}
```

Name               | Type                                          | Description
-------------------| ----------------------------------------------| --------------------------------------------------
processUid         | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid       | [SafeUUID](#safeuuid)                         | the uid of the resource.
upgradedDate       | [LocalDate](#localdate)                       | the upgraded's date of this `Company`
sentDate           | [DateTime](#datetime)                         | the received date of this `Event`.
eventType          | Constant                                      | `"CompanyUpgradedToStandardAccount"`

### CompanySubscribedToAnotherCallCenter

Name               | Type                                          | Description
-------------------| ----------------------------------------------| --------------------------------------------------
processUid         | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid       | [SafeUUID](#safeuuid)                         | the uid of the resource.
newCallCenter      | [SafeUUID](#safeuuid)                         |
sentDate           | [DateTime](#datetime)                         | the received date of this `Event`.
eventType          | Constant                                      | `"CompanySubscribedToAnotherCallCenter"`

### CompanyDowngradedToPremiumAccount

Name               | Type                                          | Description
-------------------| ----------------------------------------------| --------------------------------------------------
processUid         | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid       | [SafeUUID](#safeuuid)                         | the uid of the resource.
downgradedDate     | [LocalDate](#localdate)                       |
sentDate           | [DateTime](#datetime)                         | the received date of this `Event`.
eventType          | Constant                                      | `"CompanyDowngradedToPremiumAccount"`

### AgencyCreated

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the Company.
createdDate         | [LocalDate](#localdate)                       |
agency              | [Agency](#rawagency)                             |
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
eventType           | Constant                                      | `"AgencyCreated"`

### AgencyDeleted

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the Company.
deletedDate         | [LocalDate](#localdate)                       |
agencyUid           | [SafeUUID](#safeuuid)                         |
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
eventType           | Constant                                      | `"AgencyDeleted"`

### AgencyUpdated

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the Company.
updatedDate         | [LocalDate](#localdate)                       |
agency              | [Agency](#rawagency)                             |
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
eventType           | Constant                                      | `"AgencyUpdated"`


## ProviderContactEvent

### ProviderContactAdded

> ProviderContactAdded example :

```json
{
    "processUid":"8c12f096-20e6-11ab-8ff7-2c39b4397040",
    "aggregateUid":"7634c414-8822-e29d-fe2b-0a18b3174369",
    "date":"2016-02-29T12:03:32+02:00",
    "name":{
        "gender":"Male",
        "firstName":"John",
        "lastName":"Doe",
        "nameType":"CivilName"
     },
     "phones":[ "0145123456" ],
     "fax":[],
     "emails":[],
     "sentDate":"2016-02-29T12:05:32+02:00",
     "eventType":"ProviderContactAdded"
}
```

### ProviderContactAssociatedToCallCenter

> ProviderContactAssociatedToCallCenter example :

```json
{
    "processUid":"8c12f096-20e6-11ab-8ff7-2c39b4397040",
    "aggregateUid":"7634c414-8822-e29d-fe2b-0a18b3174369",
    "date":"2016-02-29",
    "callCenterUid":"16fc6e5e-163d-799c-89ef-a764f2090d74",
    "sentDate":"2016-02-29T12:05:32+02:00",
    "eventType":"ProviderContactAssociatedToCallCenter"
}
```

### ProviderContactAssociatedToAgency

> ProviderContactAssociatedToAgency example :

```json
{
    "processUid":"8c12f096-20e6-11ab-8ff7-2c39b4397040",
    "aggregateUid":"7634c414-8822-e29d-fe2b-0a18b3174369",
    "date":"2016-02-29",
    "agencyUid":"16fc6e5e-163d-799c-89ef-a764f2090d74",
    "sentDate":"2016-02-29T12:05:32+02:00",
    "eventType":"ProviderContactAssociatedToAgency"
}
```

### ProviderContactAssociatedToCompany

> ProviderContactAssociatedToCompany example :

```json
{
    "processUid":"8c12f096-20e6-11ab-8ff7-2c39b4397040",
    "aggregateUid":"7634c414-8822-e29d-fe2b-0a18b3174369",
    "date":"2016-02-29",
    "companyUid":"16fc6e5e-163d-799c-89ef-a764f2090d74",
    "sentDate":"2016-02-29T12:05:32+02:00",
    "eventType":"ProviderContactAssociatedToCompany"
}
```

### ProviderContactDissociatedFromAgency

> ProviderContactDissociatedFromAgency example :

```json
{
    "processUid":"8c12f096-20e6-11ab-8ff7-2c39b4397040",
    "aggregateUid":"7634c414-8822-e29d-fe2b-0a18b3174369",
    "date":"2016-02-29",
    "agencyUid":"16fc6e5e-163d-799c-89ef-a764f2090d74",
    "sentDate":"2016-02-29T12:05:32+02:00",
    "eventType":"ProviderContactDissociatedFromAgency"
}
```

### ProviderContactUpdated

> ProviderContactUpdated example :

```json
{
    "processUid":"8c12f096-20e6-11ab-8ff7-2c39b4397040",
    "aggregateUid":"7634c414-8822-e29d-fe2b-0a18b3174369",
    "date":"2016-02-29T12:05:32+02:00",
    "name":{
            "gender":"Male",
            "firstName":"John",
            "lastName":"Doe",
            "nameType":"CivilName"
         },
    "phones":[ "0145123456" ],
    "fax":[],
    "emails":[],
    "sentDate":"2016-02-29T12:05:32+02:00",
    "eventType":"ProviderContactUpdated"
}
```

### ProviderContactDisabled

> ProviderContactDisabled example :

```json
{
    "processUid":"8c12f096-20e6-11ab-8ff7-2c39b4397040",
    "aggregateUid":"7634c414-8822-e29d-fe2b-0a18b3174369",
    "date":"2016-02-29T12:05:32+02:00",
    "sentDate":"2016-02-29T12:05:32+02:00",
    "eventType":"ProviderContactDisabled"
}
```

### ProviderContactEnabled

> ProviderContactEnabled example :

```json
{
    "processUid":"8c12f096-20e6-11ab-8ff7-2c39b4397040",
    "aggregateUid":"7634c414-8822-e29d-fe2b-0a18b3174369",
    "date":"2016-02-29T12:05:32+02:00",
    "sentDate":"2016-02-29T12:05:32+02:00",
    "eventType":"ProviderContactEnabled"
}
```

### ProviderContactAssociatedWithProviderCompany

> ProviderContactAssociatedWithProviderCompany example :

```json
{
    "processUid":"8c12f096-20e6-11ab-8ff7-2c39b4397040",
    "aggregateUid":"7634c414-8822-e29d-fe2b-0a18b3174369",
    "providerCompanyUid":"c9c5c9d2-ab38-a010-46cd-97013fbfbeb2",
    "sentDate":"2016-02-29T12:05:32+02:00",
    "eventType":"ProviderContactAssociatedWithProviderCompany"
}
```
### ProviderContactAssociatedWithPatrimony

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the `ProviderContact` referenced.
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
patrimonyUid        | [SafeUUID](#safeuuid)                         | the uid of the `Patrimony` resource associated with the `ProviderContact`
eventType           | Constant                                      | `"ProviderContactAssociatedWithPatrimony"`

(processUid: ProcessUid,
                                                  aggregateUid: AggregateUid,
                                                  sentDate: DateTime,
                                                  patrimonyUid: SafeUUID) extends OtherProviderContactEvent

### ProviderContactDissociatedFromPatrimony

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the `ProviderContact` referenced.
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
patrimonyUid        | [SafeUUID](#safeuuid)                         | the uid of the `Patrimony` resource dissociated with the `ProviderContact`
eventType           | Constant                                      | `"ProviderContactDissociatedFromPatrimony"`

### ActivityAssignedToProviderContact

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the `ProviderContact` referenced.
activityUid         | [SafeUUID](#safeuuid)                         | the uid of the `Activity` assigned to this `ProviderContact` 
includedIncidentTypes | Array[[SafeUUID](#safeuuid)]                | the list of incident type that is managed for this Activity by this `ProviderContact` 
eventType           | Constant                                      | `"ActivityAssignedToProviderContact"`

### ActivityRemovedFromProviderContact

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the `ProviderContact` referenced.
activityUid         | [SafeUUID](#safeuuid)                         | the uid of the `Activity` removed from this `ProviderContact` 
eventType           | Constant                                      | `"ActivityRemovedFromProviderContact"`


## ProviderCompanyEvent

### ProviderCompanyReferenced 

> ProviderCompanyEvent example :

```json
{
    "processUid":"8c12f096-20e6-11ab-8ff7-2c39b4397040",
    "aggregateUid":"7634c414-8822-e29d-fe2b-0a18b3174369",
    "name":"Performance Immo",
    "siretNumber":"80242504100018",
    "sentDate":"2017-04-19T15:11:32+01:00",
    "eventType":"ProviderCompanyReferenced"
}
```

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the `ProviderCompany` referenced.
name                | String                                        | the name of the `ProviderCompany`
siretNumber         | [SIRET](#siret)                               | the siret number of this `ProviderCompany`
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
eventType           | Constant                                      | `"ProviderCompanyReferenced"`

## LotEvent

### LotReferenced

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the `Lot` referenced.
patrimonyUid        | [SafeUUID](#safeuuid)                         | the uid of the `Patrimony` of the `Lot`.
ref                 | String                                        | a public reference to distinguish the `Lot` in a `Agency` context 
lotNumber           | String                                        | a public number to distinguish the `Lot` in its `Patrimony`   
usage               | [LotUsage](#lotusage)                         | what kind of `Lot` it is. 
addresses           | [NonEmptyList](#nonemptylist)[[LotAddressReference](#lotaddressreference)]  |
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
eventType           | Constant                                      | `"LotReferenced"`

### AddressAddedToLot

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the `Lot` incremented.
lotAddress          | [LotAddressReference](#lotaddressreference)   |
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
eventType           | Constant                                      | `"AddressAddedToLot"`

### AddressRemovedFromLot

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the `Lot` incremented.
addressUid          | [SafeUUID](#safeuuid)                         |
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
eventType           | Constant                                      | `"AddressRemovedFromLot"`

### LotReferenceUpdated

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the `Lot` incremented.
ref                 | String                                        |
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
eventType           | Constant                                      | `"LotReferenceUpdated"`

### LotNumberUpdated

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the `Lot` incremented.
lotNumber           | [SafeUUID](#safeuuid)                         |
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
eventType           | Constant                                      | `"LotNumberUpdated"`

### LotUsageUpdated

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the `Lot` incremented.
usage               | [LotUsage](#lotusage)                         |
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
eventType           | Constant                                      | `"LotUsageUpdated"`

### LotDeleted

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the `Lot` incremented.
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
eventType           | Constant                                      | `"LotDeleted"`

## TicketEvent

### TicketOpened

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the `Ticket` opened.
locationRef         | [LocationReference](#locationreference)       | a reference to another resource (`Agency`, `Patrimony`, etc...)
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. We can say who open this `Ticket`. 
ticket              | [TicketInfos](#ticketinfos)                   | infos specific to the `Ticket` opened. 
openedDate          | [DateTime](#datetime)                         | the opened date of this `Ticket`.
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
eventType           | Constant                                      | `"TicketOpened"`

### CallEmittedTo 

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. 
recipient           | [Persona](#persona)                           | the recipient of this call.
comment             | [Option](#option)[String]                     |  
medium              | [ContactMedium](#contactmedium)               | the medium used to perform this call.
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
date                | [DateTime](#datetime)                         | 
eventType           | Constant                                      | `"CallEmittedTo"`

### CallReceived

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. 
callPurpose         | String                                        | purpose of the call.
caller              | String                                        | 
comment             | [Option](#option)[String]                     |  
medium              | [ContactMedium](#contactmedium)               | the medium used to perform this call.
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
eventType           | Constant                                      | `"CallReceived"`

### AssigneeIdentified

> AssigneeIdentified example :

```json
{
  "processUid": "f5391199-e544-60f3-037c-16f3229fd59d",
  "aggregateUid": "c9c5c9d2-ab38-a010-46cd-97013fbfbeb2",
  "operator": {
    "operatorUid": "98bfb3a8-ae4a-7486-1ee3-96131d994801",
    "operatorType": "ReferencedOperator"
  },
  "assignee": {
    "providerUid": "7943797a-93c4-73f9-48f8-6baea5e94d13",
    "assigneeType": "ReferencedProviderContact"
  },
  "comment":"a commentary",
  "date": "2016-08-25T15:31:53.000+02:00",
  "sentDate": "2016-08-25T15:31:50.000+02:00",
  "eventType": "AssigneeIdentified"
}
```


Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. 
assignee            | [TicketAssignee](#ticketassignee)             | a reference to the `TicketAssignee` identified on this `Ticket`.
comment             | [Option](#option)[String]                     |
sentDate            | [DateTime](#datetime)                         | when `Event` was sending to Perfimmo.
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
eventType           | Constant                                      | `"AssigneeIdentified"`

### InterventionRequested

> InterventionRequested example :

```json
{
  "processUid": "f5391199-e544-60f3-037c-16f3229fd59d",
  "aggregateUid": "c9c5c9d2-ab38-a010-46cd-97013fbfbeb2",
  "operator": {
    "operatorUid": "98bfb3a8-ae4a-7486-1ee3-96131d994801",
    "operatorType": "ReferencedOperator"
  },
  "assignee": {
    "providerUid": "7943797a-93c4-73f9-48f8-6baea5e94d13",
    "assigneeType": "ReferencedProviderContact"
  },
  "comment":"a commentary",
  "date": "2016-08-25T15:31:53.000+02:00",
  "sentDate": "2016-08-25T15:31:50.000+02:00",
  "eventType": "InterventionRequested"
}
```


Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`.
assignee            | [TicketAssignee](#ticketassignee)             | a reference to the `TicketAssignee` requested (Must be the same as identified one)
medium              | [ContactMedium](#contactmedium)               | the medium used to perform this request.
comment             | [Option](#option)[String]                     |
sentDate            | [DateTime](#datetime)                         | when `Event` was sending to Perfimmo.
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
eventType           | Constant                                      | `"InterventionRequested"`

### SendingServiceOrderReported

> SendingServiceOrderReported example : 

```json
{
  "processUid": "f5391199-e544-60f3-037c-16f3229fd59d",
  "aggregateUid": "c9c5c9d2-ab38-a010-46cd-97013fbfbeb2",
  "operator": {
    "operatorUid": "98bfb3a8-ae4a-7486-1ee3-96131d994801",
    "operatorType": "ReferencedOperator"
  },
  "assignee": {
      "providerUid":"f5391199-e544-60f3-037c-16f3229fd59d",
      "assigneeType":"ReferencedProviderCompany"
  },
  "ref": "1234FRX",
  "reportDate": "2016-08-25T15:31:53.000+02:00",
  "sendingDate": "2016-08-25T15:31:53.000+02:00",
  "sentDate": "2016-08-25T15:31:50.000+02:00",
  "eventType": "SendingServiceOrderReported"
}
```

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. 
assignee            | [TicketAssignee](#ticketassignee)             | a reference to the `TicketAssignee` for who sending service order is reported.
ref                 | String                                        | the reference of the service order sent.
reportDate          | [DateTime](#datetime)                         | date on which the `Event` took place.
sendingDate         | [DateTime](#datetime)                         | date when the service order was sending.
sentDate            | [DateTime](#datetime)                         | when `Event` was sending to Perfimmo.
eventType           | Constant                                      | `"SendingServiceOrderReported"`

### CallAnsweredByProvider

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. 
provider            | [Provider](#provider)                         | a reference to the `Provider` who answer.
comment             | String                                        | 
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
eventType           | Constant                                      | `"CallAnsweredByProvider"`

### CallNotAnsweredByProvider

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. 
provider            | [Provider](#provider)                         | a reference to the `Provider` who not answer.
comment             | String                                        | 
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
eventType           | Constant                                      | `"CallNotAnsweredByProvider"`

### InterventionScheduled

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. 
assignee            | [TicketAssignee](#ticketassignee)             | a reference to the `TicketAssignee` for who intervention is scheduled.
comment             | [Option](#option)[String]                     |
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
startDate           | [DateTime](#datetime)                         | the start date of this scheduled intervention.
endDate             | [DateTime](#datetime)                         | the end date of this scheduled intervention.
eventType           | Constant                                      | `"InterventionScheduled"`

### InterventionDeadlineDefined

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. 
assignee            | [TicketAssignee](#ticketassignee)             | a reference to the `TicketAssignee` for who intervention deadline is defined.
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
deadline            | [DateTime](#datetime)                         | the deadline defined.
eventType           | Constant                                      | `"InterventionDeadlineDefined"`

### FormalNoticeForProviderReported

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
ref                 | [Option](#option)[String]                     | an optional reference to this formal notice.
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. 
assignee            | [TicketAssignee](#ticketassignee)             | a reference to the `TicketAssignee` for who formal notice is reported (Must be the same as identified one).
reportDate          | [DateTime](#datetime)                         | date on which the `Event` took place.
deadline            | [DateTime](#datetime)                         | a new deadline defined.
eventType           | Constant                                      | `"FormalNoticeForProviderReported"`

### InterventionAccepted

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. 
assignee            | [TicketAssignee](#ticketassignee)             | a reference to the `TicketAssignee` who accept the intervention.
comment             | [Option](#option)[String]                     |
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
eventType           | Constant                                      | `"InterventionAccepted"`

### InterventionRefused

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. 
assignee            | [TicketAssignee](#ticketassignee)             | a reference to the `TicketAssignee` who accept the intervention.
comment             | [Option](#option)[String]                     |
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
eventType           | Constant                                      | `"InterventionRefused"`

### TicketReopened

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. 
purpose             | Option[String]                                | the reason why the `Ticket` was reopened. 
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
eventType           | Constant                                      | `"TicketReopened"`

### LogTrialAdded

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. 
provider            | [Option](#option)[[Provider](#provider)]      | 
logTrial            | [LogTrial](#logtrial)                         | 
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
logTrialAddedDate   | [DateTime](#datetime)                         | date on which the `Event` took place.
eventType           | Constant                                      | `"LogTrialAdded"`

### MessageAdded

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. 
message             | String                                        | 
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
messageAddedDate    | [DateTime](#datetime)                         | date on which the `Event` took place.
eventType           | Constant                                      | `"MessageAdded"`

### TicketCancelled

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. 
comment             | [Option](#option)[String]                     | Explain why this `Event` happened.
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
eventType           | Constant                                      | `"TicketCancelled"`

### ArrivedOnSite

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. 
assignee            | [TicketAssignee](#ticketassignee)             | a reference to the `TicketAssignee` for who arrive on site.
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
eventType           | Constant                                      | `"ArrivedOnSite"`

### GoneFromSite

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. 
assignee            | [TicketAssignee](#ticketassignee)             | a reference to the `TicketAssignee` who gone from site.
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
eventType           | Constant                                      | `"GoneFromSite"`

### InterventionStarted

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. 
assignee            | [TicketAssignee](#ticketassignee)             | a reference to the `TicketAssignee` who start the intervention.
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
startedDate         | [DateTime](#datetime)                         | date on which the `Event` took place.
eventType           | Constant                                      | `"InterventionStarted"`

### InterventionFinished

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. 
assignee            | [TicketAssignee](#ticketassignee)             | a reference to the `TicketAssignee` who finish the intervention.
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
finishedDate        | [DateTime](#datetime)                         | date on which the `Event` took place.
eventType           | Constant                                      | `"InterventionFinished"`

### TicketUpdated

A compensation 'Event' to correct issue in the original `TicketOpened`. 
Don't use it for increment the `Ticket` state. Use other `Command` for that.

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the `Ticket` opened.
locationRef         | [LocationReference](#locationreference)       | a reference to another resource (`Agency`, `Patrimony`, etc...)
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. We can say who update this `Ticket`. 
ticket              | [TicketInfos](#ticketinfos)                   | infos specific to the `Ticket` opened. 
openedDate          | [DateTime](#datetime)                         | the opened date of this `Ticket`.
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
eventType           | Constant                                      | `"TicketUpdated"`

### TicketInformationsCorrected

Some text in the `Ticket` were updated.

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
fieldsCorrected     | [FieldsToCorrect](#fieldstocorrect)           | a 'list' of optional field corrected 
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. We can say who update this `Ticket`. 
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
eventType           | Constant                                      | `"TicketInformationsCorrected"`

### TicketEventInformationsCorrected

The text of a previous `Event` was updated.
                                            
Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated.
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
targetedEvent       | [SafeUUID](#safeuuid)                         | the uid of the `Event` whose text has been updated.
text                | String                                        | the new text of the targeted `Event`.
operator            | [Operator](#operator)                         | a reference to who perform for this `Command`. We can say who update this `Ticket`. 
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
commandType         | Constant                                      | `"CorrectTicketEventInformations"`
                                            

<br/>
<br/>

<aside class="notice">
Received the following events means the Ticket was closed.
</aside>

### TicketClosed

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. 
provider            | [Option](#option)[[Provider](#provider)]      | a reference to the `Provider` who close the `Ticket`.
brakedownNature     | [Option](#option)[String]                     | an optional explanation of the reason of the breakedown.
stillOnSite         | [StillOnSite](#stillonsite)                   | 
report              | [Option](#option)[String]                     | an optional explanation of the intervention.
result              | [Option](#option)[String]                     |
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
closingDate         | [DateTime](#datetime)                         | date on which the `Event` took place.
eventType           | Constant                                      | `"TicketClosed"`

### TicketCancelled

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
operator            | [Operator](#operator)                         | a reference to who perform for this `Command`. 
comment             | [Option](#option)[String]                     |
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
commandType         | Constant                                      | `"TicketCancelled"`

### TicketArchived

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. 
comment             | [Option](#option)[String]                     | 
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
closingDate         | [DateTime](#datetime)                         | date on which the `Event` took place.
eventType           | Constant                                      | `"TicketArchived"`

### PermanentlyFixed

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. 
provider            | [Option](#option)[[Provider](#provider)]      | a reference to the `Provider` who close the `Ticket`.
brakedownNature     | [Option](#option)[String]                     | an optional explanation of the reason of the breakedown.
stillOnSite         | [StillOnSite](#stillonsite)                   | 
report              | [Option](#option)[String]                     | an optional explanation of the intervention.
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
closingDate         | [DateTime](#datetime)                         | date on which the `Event` took place.
eventType           | Constant                                      | `"PermanentlyFixed"`

### PartiallyFixed

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. 
provider            | [Option](#option)[[Provider](#provider)]      | a reference to the `Provider` who close the `Ticket`.
brakedownNature     | [Option](#option)[String]                     | an optional explanation of the reason of the breakedown.
stillOnSite         | [StillOnSite](#stillonsite)                   | 
report              | [Option](#option)[String]                     | an optional explanation of the intervention.
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
closingDate         | [DateTime](#datetime)                         | date on which the `Event` took place.
eventType           | Constant                                      | `"PartiallyFixed"`

### TicketClosedImpossibleRepair

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. 
provider            | [Option](#option)[[Provider](#provider)]      | a reference to the `Provider` who close the `Ticket`.
brakedownNature     | [Option](#option)[String]                     | an optional explanation of the reason of the breakedown.
stillOnSite         | [StillOnSite](#stillonsite)                   | 
report              | [Option](#option)[String]                     | an optional explanation of the intervention.
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
closingDate         | [DateTime](#datetime)                         | date on which the `Event` took place.
eventType           | Constant                                      | `"TicketClosedImpossibleRepair"`

### PostponedFix

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. 
provider            | [Option](#option)[[Provider](#provider)]      | a reference to the `Provider` who close the `Ticket`.
brakedownNature     | [Option](#option)[String]                     | an optional explanation of the reason of the breakedown.
stillOnSite         | [StillOnSite](#stillonsite)                   | 
report              | [Option](#option)[String]                     | an optional explanation of the intervention.
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
closingDate         | [DateTime](#datetime)                         | date on which the `Event` took place.
eventType           | Constant                                      | `"PostponedFix"`

### ClosedBeyondCallCenterScope

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. 
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
closingDate         | [DateTime](#datetime)                         | date on which the `Event` took place.
comment             | [Option](#option)[String]                     | Explain why this `Event` happened.
eventType           | Constant                                      | `"ClosedBeyondCallCenterScope"`

### ClosedAfterSeveralUnsuccessfulRecalls

After several attempt, it seems it is impossible to contact a `Provider` to resolve this `Ticket`. 

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. 
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
closingDate         | [DateTime](#datetime)                         | date on which the `Event` took place.
comment             | [Option](#option)[String]                     | Explain why this `Event` happened.
eventType           | Constant                                      | `"ClosedAfterSeveralUnsuccessfulRecalls"`

## PatrimonyContactEvent

### PatrimonyContactReferenced

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
name                | [Name](#name)                                 |
address             | [Option](#option)[[PatrimonyContactAddressReference](#patrimonyaddressreference)] | an optional address for this `PatrimonyContact`
contacts            | [NonEmptyList](#nonemptylist)[[ContactInfo](#contactinfo)] | a non empty list of contact like phone number or email 
eventType           | Constant                                      | `"PatrimonyContactReferenced"`

### PatrimonyContactLinkedWith

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
linkedWith          | [NonEmptyList](#nonemptylist)[[PatrimonyContactEntityLink](#patrimonycontactentitylink)] | a non empty list of link to several `Patrimony` or `Lot`entity. 
eventType           | Constant                                      | `"PatrimonyContactLinkedWith"`


### LinkRemovedFromPatrimonyContact

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
linkedWith          | [NonEmptyList](#nonemptylist)[[PatrimonyContactEntityLink](#patrimonycontactentitylink)] | a non empty list of link to several `Patrimony` or `Lot`entity. 
eventType           | Constant                                      | `"LinkRemovedFromPatrimonyContact"`

### ContactAdded

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
contact             | [ContactInfo](#contactinfo)                 | a contact like phone number or email 
eventType           | Constant                                      | `"ContactAdded"`

### ContactRemoved

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
contact             | [ContactInfo](#contactinfo)                   | a contact like phone number or email 
eventType           | Constant                                      | `"ContactRemoved"`


### PatrimonyContactIdentityUpdated

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
name                | [Option](#option)[[Name](#name)]              | if None, field not updated
address             | [Option](#option)[[PatrimonyContactAddressReference](#patrimonyaddressreference)] | if None, field not updated 
eventType           | Constant                                      | `"PatrimonyContactIdentityUpdated"`
