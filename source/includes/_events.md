# Events

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

### ProviderAssigned

> ProviderAssigned example : 

```json
{
  "processUid": "f5391199-e544-60f3-037c-16f3229fd59d",
  "aggregateUid": "c9c5c9d2-ab38-a010-46cd-97013fbfbeb2",
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
  "sentDate": "2016-08-25T15:31:50.000+02:00",
  "eventType": "ProviderAssigned"
}
```


Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. 
provider            | [Provider](#provider)                         | a reference to the `Provider` assigned to this `Ticket`.
purpose             | [ProviderAssignationPurpose](#providerassignationpurpose) | the purpose of this assignation. (can be RecourseChanged)
sentDate            | [DateTime](#datetime)                         | when `Event` was sending to Perfimmo.
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
eventType           | Constant                                      | `"ProviderAssigned"`

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
  "provider": {
    "providerUid": "7943797a-93c4-73f9-48f8-6baea5e94d13",
    "providerType": "ReferencedProvider"
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
provider            | [Provider](#provider)                         | a reference to the `Provider` assigned to this `Ticket`.
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

### MissionScheduled

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. 
provider            | [Provider](#provider)                         | a reference to the `Provider` who will perform the mission.
comment             | [Option](#option)[[String]]                   | 
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
startDate           | [DateTime](#datetime)                         | the start date of this scheduled mission.
endDate             | [DateTime](#datetime)                         | the end date of this scheduled mission.
eventType           | Constant                                      | `"MissionScheduled"`

### MissionAccepted

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. 
provider            | [Provider](#provider)                         | a reference to the `Provider` who accept the mission.
comment             | String                                        | 
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
eventType           | Constant                                      | `"MissionAccepted"`

### MissionRefused

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. 
provider            | [Provider](#provider)                         | a reference to the `Provider` who refuse the mission.
comment             | String                                        | 
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
eventType           | Constant                                      | `"MissionRefused"`

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
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
eventType           | Constant                                      | `"TicketCancelled"`

### ArrivedOnSite

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. 
provider            | [Provider](#provider)                         | a reference to the `Provider` who arrive on site.
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
eventType           | Constant                                      | `"ArrivedOnSite"`

### GoneFromSite

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. 
provider            | [Provider](#provider)                         | a reference to the `Provider` who gone from site.
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
date                | [DateTime](#datetime)                         | date on which the `Event` took place.
eventType           | Constant                                      | `"GoneFromSite"`

### InterventionStarted

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. 
provider            | [Provider](#provider)                         | a reference to the `Provider` who start the intervention.
sentDate            | [DateTime](#datetime)                         | the received date of this `Event`.
startedDate         | [DateTime](#datetime)                         | date on which the `Event` took place.
eventType           | Constant                                      | `"InterventionStarted"`

### InterventionFinished

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
processUid          | [SafeUUID](#safeuuid)                         | the uid of this command. Allow PerfImmo to know if this Command is duplicated
aggregateUid        | [SafeUUID](#safeuuid)                         | the uid of the resource.
operator            | [Operator](#operator)                         | a reference to who ask for this `Command`. 
provider            | [Provider](#provider)                         | a reference to the `Provider` who finish the intervention.
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
eventType           | Constant                                      | `"ClosedAfterSeveralUnsuccessfulRecalls"`
