# Models

## Option

Means that field is optional. If parameter has no value, it is not present in the json payload.

<aside class="warning">
	<code> { "field1":"toto", field2:"" } is not equivalent to { "field1":"toto" } </code>
</aside>

## NonEmptyList

A json `array`that can't be empty.

## Map

a json object with "free" field

> Map[String, String] example :

```json
{
    "field1":"value1",
    "field2":"value2"
}
```

## SafeUUID

Identifiant garanti unique en utilisant la norme [GUUID](https://fr.wikipedia.org/wiki/Globally_Unique_Identifier)    

S'exprime sous forme de chaîne de caractères avec une contrainte sur le format.

ex: `8074964f-c633-3c2a-055f-bbaf8ca8181b`

## LocalDate

[ISO-8601 calendar system](https://fr.wikipedia.org/wiki/ISO_8601)  
`YYYY-MM-DD` ex: `"2016-02-29"`

## DateTime

[ISO-8601 calendar system](https://fr.wikipedia.org/wiki/ISO_8601)  
`YYYY-MM-DDTHH:mm:ss+02:00` ex: `"2016-02-29T12:03:32+02:00"`

## Duration

a duration represented in milliseconds. ex: `"300000"`

## SIRET

a [SIRET](https://fr.wikipedia.org/wiki/Syst%C3%A8me_d'identification_du_r%C3%A9pertoire_des_%C3%A9tablissements) 
is an unique identifier for `Company`. ex: `"80242504100018"`

## RestNavigationLink

> RestNavigationLink example : 

```json
{
    "rel": "self",
    "href": "https://base_url/api/v1/providercompanies/7634c414-8822-e29d-fe2b-0a18b3174369",
    "method": "GET"
}
```

Rest Navivation Links represent what it is possible to do with this resource.

These different links below (except `self` that is mandatory) are optional in  
the response because of the specific state of the request done to retrieve this response.

ex: state of the resource, rights of the user performing the request, etc...

### Fields

Name        | Type           | Description
------------| ---------------| --------------------------------------------------
rel         | String         | a label to identifiy what this navigation link is supposed to do.
href        | String         | the complete URL to perform request.
method      | String         | the http method to use to perform request (GET, POST, PATCH, ...)

## ItemAbstract

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
uid         | [SafeUUID](#safeuuid)                             | the uid of the item
label       | String                                            | the label of the item

## Name

`Name` is an Enum, i.e type can take different values : 

```haskell
data Name = PoorName | CivilName
```

### PoorName

> PoorName example :

```json
{
	"value":"John Doe",
    "nameType":"PoorName"
}
```

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
value       | String                                            | 
nameType    | Constant                                          | `"PoorName"`

### CivilName

> CivilName example :

```json
{
	"gender":"female",
	"firstName":"John",
	"lastName":"Doe",
    "nameType":"CivilName"
}
```

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
gender      | [Option](#option)[String]                         | only value accepted are `"Male"` or `"Female"`
firstName   | String                                            | 
lastName    | String                                            | 
nameType    | Constant                                          | `"CivilName"`

## CompanyQueryView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------
uid         | [SafeUUID](#safeuuid)                             | id of the `Company`
label       | String                                            | the `Company`'s label
isActive    | Boolean                                           | `true` if the `Company` is active
holding     | [Option](#option)[[HoldingQueryView](#holdingqueryview)] | a reference to `Company`'s holding if has it
companyType | Enum                                              | enum : `"CallCenter"` or `"ClientAccountHolding"` or `"ClientAccount"`

## AgencyQueryView

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------
uid         | [SafeUUID](#safeuuid)                             | id of the `Agency`
sda         | [Option](#option)[String]                         |
label       | String                                            | the `Agency`'s label
group       | [Option](#option)[String]                         | 
ref         | String                                            | a client reference for the `Agency`
address     | [Option](#option)[RationalAddress]                | 
phones      | Array[String]                                     |
fax         | [Option](#option)[String]                         |
emails      | Array[String]                                     |

## UserQueryView

`UserQueryView` is an Enum, i.e type can take different values : 

```haskell
data UserQueryView = SuperUser | CallCenterUser | ClientAccountManager | Executive
```

### SuperUser 

> SuperUser example :

```json
{
	"uid":"d5c48f2f-2bcc-40ff-9a5c-4ba5d33419df",       
    "login":"john.doe@performance-immo.com",       
    "firstName":"John",   
    "lastName":"Doe",    
    "job": "master of the world", 
    "phone":"0605040302",
    "userType":"superUser"
}
```

Super Admin of the plateform. A priori, you should not deal with this kind of `User`.

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------
uid         | [SafeUUID](#safeuuid)                             | `User`'s uid
login       | String                                            | `User`'s login
firstName   | String                                            | `User`'s first name
lastName    | String                                            | `User`'s last name
job         | [Option](#option)[String]                         | `User`'s job (optional)
phone       | [Option](#option)[String]                         | `User`'s phone number (optional)
userType    | Constant                                          | `"superUser"

### CallCenterUser 

> CallCenterUser example :

```json
{
	"uid":"d5c48f2f-2bcc-40ff-9a5c-4ba5d33419df",       
    "login":"john.doe@performance-immo.com",       
    "company": {
        "uid": "1471965c-e1ea-37e9-fa45-770753dc5154",
        "label": "My Call Center"
    },
    "firstName":"John",   
    "lastName":"Doe",    
    "job": "manager of a Call Center", 
    "phone":"0605040302",
    "userType":"callCenterUser"
}
```

`User` who have right on all entities linked with his `CallCenter` (ex: `Company`, `Ticket`, `User` etc...).

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------
uid         | [SafeUUID](#safeuuid)                             | `User`'s uid
login       | String                                            | `User`'s login
company     | [CompanyUserQueryView](#companyuserqueryview)     | `User`'s `Company`
firstName   | String                                            | `User`'s first name
lastName    | String                                            | `User`'s last name
job         | [Option](#option)[String]                         | `User`'s job (optional)
phone       | [Option](#option)[String]                         | `User`'s phone number (optional)
userType    | Constant                                          | `"callCenterUser"`

### ClientAccountManager 

> ClientAccountManager example :

```json
{
	"uid":"d5c48f2f-2bcc-40ff-9a5c-4ba5d33419df",       
    "login":"john.doe@performance-immo.com",       
    "company": {
        "uid": "1471965c-e1ea-37e9-fa45-770753dc5154",
        "label": "My Company"
    },
    "firstName":"John",   
    "lastName":"Doe",    
    "job": "manager of a ClientAccount", 
    "phone":"0605040302",
    "userType":"clientAccountManager"
}
```

`User` who have right on all entities linked with his `Company` (ex: `Ticket`, `Agencies`, `User` etc...).

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------
uid         | [SafeUUID](#safeuuid)                             | `User`'s uid
login       | String                                            | `User`'s login
company     | [CompanyUserQueryView](#companyuserqueryview)     | `User`'s `Company`
firstName   | String                                            | `User`'s first name
lastName    | String                                            | `User`'s last name
job         | [Option](#option)[String]                         | `User`'s job (optional)
phone       | [Option](#option)[String]                         | `User`'s phone number (optional)
userType    | Constant                                          | `"clientAccountManager"

### Executive

> ClientAccountManager example :

```json
{
	"uid":"d5c48f2f-2bcc-40ff-9a5c-4ba5d33419df",       
    "login":"john.doe@performance-immo.com",       
    "company": {
        "uid": "1471965c-e1ea-37e9-fa45-770753dc5154",
        "label": "My Company"
    },
    "managedAgencies": [
        {"uid":"5671965c-e1ea-37e9-fa45-770753dc5e34", "label":"my agency"}
    ],
    "firstName":"John",   
    "lastName":"Doe",    
    "job": "manager of a ClientAccount", 
    "phone":"0605040302",
    "userType":"executive"
}
```

`User` who have right on all entities linked with his `Agencies` (ex: `Ticket`, `Agencies`, `User` etc...).

Name            | Type                                              | Description
----------------| --------------------------------------------------| --------------------------
uid             | [SafeUUID](#safeuuid)                             | `User`'s uid
login           | String                                            | `User`'s login
company         | [CompanyUserQueryView](#companyuserqueryview)     | `User`'s `Company`
managedAgencies | [NonEmptyList](#nonemptylist)[[AgencyUserQueryView](#agencyuserqueryview)] | A non empty list of `Agencies`managed by the executive
firstName       | String                                            | `User`'s first name
lastName        | String                                            | `User`'s last name
job             | [Option](#option)[String]                         | `User`'s job (optional)
phone           | [Option](#option)[String]                         | `User`'s phone number (optional)
userType        | Constant                                          | `"executive"

## TicketResultView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
result      | Array[[TicketQueryView](#ticketqueryview)]        | Array of selected `Ticket`s
aggergations| [Aggregations](#aggregations)                     | Aggregations of several params.

## TicketExportView

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
result      | Array[[ExportedTicket](#exportedticket)]          | Array of exported `Ticket`s

## HoldingQueryView 

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
uid         | [SafeUUID](#safeuuid)                             | the holding's uid
label       | String                                            | the holding's label

## CompanyUserQueryView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
uid         | [SafeUUID](#safeuuid)                             | the `Company`'s uid
label       | String                                            | the `Company`'s label

## AgencyUserQueryView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
uid         | [SafeUUID](#safeuuid)                             | the `Agency`'s uid
label       | String                                            | the `Agency`'s label

## TicketQueryView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
uid         | [SafeUUID](#safeuuid)                             | the `Ticket`'s uid
ref         | String                                            | the `Ticket`'s client reference.<br/> Could be `clientClaimNumber`or `callCenterClaimNumber` or `ticket_uid`.
agencies    | Array[[AgencyAbstract](#agencyabstract)]          | the `Agency` linked to this `Ticket`.
patrimony   | [Option](#option)[[PatrimonyAbstract](#patrimonyabstract)] | the `Patrimony` linked to this `Ticket`. optional.
status      | ENUM                                              | `OPENED` or `CLOSED`.
state       | [Option](#option)[[TicketStateView](#ticketstateview)] | the actual `state` of this `Ticket`.<br/> ex: `MissionAccepted`
created     | [DateTime](#datetime)                             | the date when this `Ticket` was opened.
updated     | [DateTime](#datetime)                             | the date when last update of this `Ticket` occured.
closed      | [DateTime](#datetime)                             | the date when this `Ticket` was closed.
callPurpose | String                                            | the `callPurpose` of this `Ticket`.
caller      | [CallerQueryView](#callerqueryview)               | informations on person who ask for open this `Ticket`.
provider    | [Option](#option)[[ProviderQueryView](#providerqueryview)] | informations on the possible last `Provider` acting on this `Ticket`.
address     | [BasicAddress](#basicaddress)                     | the `Address` where the incident occurs.

## ExportedTicket

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
uid         | [SafeUUID](#safeuuid)                             | the `Ticket`'s uid
ref         | String                                            | the `Ticket`'s client reference.<br/> Could be `clientClaimNumber`or `callCenterClaimNumber` or `ticket_uid`.
agencies    | Array[[AgencyAbstract](#agencyabstract)]          | the `Agency` linked to this `Ticket`.
patrimony   | [Option](#option)[[PatrimonyAbstract](#patrimonyabstract)] | the `Patrimony` linked to this `Ticket`. optional.
status      | ENUM                                              | `OPENED` or `CLOSED`.
state       | [Option](#option)[[TicketStateView](#ticketstateview)] | the actual `state` of this `Ticket`.<br/> ex: `MissionAccepted`
created     | [DateTime](#datetime)                             | the date when this `Ticket` was opened.
updated     | [DateTime](#datetime)                             | the date when last update of this `Ticket` occured.
closed      | [DateTime](#datetime)                             | the date when this `Ticket` was closed.
callPurpose | String                                            | the `callPurpose` of this `Ticket`.
request     | String                                            | the details of the demand.
caller      | [CallerQueryView](#callerqueryview)               | informations on person who ask for open this `Ticket`.
provider    | [Option](#option)[[ProviderQueryView](#providerqueryview)] | informations on the possible last `Provider` acting on this `Ticket`.
address     | [BasicAddress](#basicaddress)                     | the `Address` where the incident occurs.
journalAdditionalInfos | [JournalExportAdditionalInfos](#journalexportadditionalinfos) | a set of several infos extract from the `Ticket`'s journal.
freeCommentaries    | Array[[FreeCommentary](#freecommentary)]  | the list of free commentaries added in this ticket
stats        | [DetailedTicketStats](#detailedticketstats)      | a set of several stats on this `Ticket`.
additionalDataz     | Map[String, String]                       |


## JournalExportAdditionalInfos

### Fields

Name                    | Type                                              | Description
------------------------| --------------------------------------------------| -----------------
interventionStarted     | [Option](#option)[[DateTime](#datetime)]          | date when possible intervention started.
interventionScheduled   | [Option](#option)[[InterventionScheduled](#interventionscheduled)] | period of the last scheduled intervention for this `Ticket`.
interventionDeadline    | [Option](#option)[[DateTime](#datetime)]          | last intervention deadline for this `Ticket`. 
formalNotice            | [Option](#option)[[FormalNotice](#formalnotice)]  | last formalNotice for this `Ticket`.

## FreeCommentary

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
date        | [DateTime](#datetime)                             | the date when the free commentary was written
message     | String                                            | 

## InterventionScheduled

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
startDate   | [DateTime](#datetime)                             | startDate of the scheduled period
endDate     | [DateTime](#datetime)                             | endDate of the scheduled period

## FormalNotice

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
date        | [DateTime](#datetime)                             | date when this formal notice was sent
deadline    | [DateTime](#datetime)                             | deadline of this formal notice


## Aggregations

### Fields

Name            | Type                                              | Description
----------------| --------------------------------------------------| -----------------
status          | Array[[Aggregation](#aggregation)]                | the list of status collected in all Tickets requested. 
agencies        | Array[[Aggregation](#aggregation)]                | the list of agencies collected in all Tickets requested.
callPurposes    | Array[[Aggregation](#aggregation)]                | the list of callPurposes collected in all Tickets requested.
locations       | Array[[Aggregation](#aggregation)]                | the list of locations collected in all Tickets requested.
interventions   | Array[[Aggregation](#aggregation)]                | the list of interventions collected in all Tickets requested.
providers       | Array[[Aggregation](#aggregation)]                | the list of providers collected in all Tickets requested.

## Aggregation                        

`Aggregation` is an Enum, i.e type can take different values : 

```haskell
data Aggregation = TermAggregation | NestedTermAggregation
```

### TermAggregation 

> TermAggregation example :

```json
{
	"value":"d5c48f2f-2bcc-40ff-9a5c-4ba5d33419df",       
    "count":123
}
```

`TermAggregation` count the occurence number of a term.

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------
value       | String                                            | the term counted.
count       | Long                                              | the count.
                        
### NestedTermAggregation                        
   
> NestedTermAggregation example :

```json
{
	"value":"d5c48f2f-2bcc-40ff-9a5c-4ba5d33419df",       
    "label":"the label",
    "count":123
}
```                        
                        
`NestedTermAggregation` count the occurence number of a term. This term is associated with a label.

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------
value       | String                                            | the term counted.
count       | Number                                            | the count.
label       | String                                            | the label associated with this term.

## AgencyAbstract

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
uid         | [SafeUUID](#safeuuid)                             | the `Agency`'s uid
name        | String                                            | the `Agency`'s name

## PatrimonyAbstract

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
uid         | [SafeUUID](#safeuuid)                             | the `Patrimony`'s uid
name        | String                                            | the `Patrimony`'s name

## TicketStateView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
value       | String                                            | the `state` label
date        | [DateTime](#datetime)                             | the date when the state was setted

## CallerQueryView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
name        | String                                            | the name of the caller
medium      | [Option](#option)[[ContactMediumView](#contactmediumview)] | the medium use by the caller to open `Ticket`. 

## ContactMediumView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
mediumType  | String                                            | the type of the medium.<br/> ex: `PHONE | FAX | MAIL | SMS`
identifier  | String                                            | the identifier for this medium. <br/> ex: `0604030201`

## ProviderQueryView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
uid         | [Option](#option)[[SafeUUID](#safeuuid)]          | the uid of the `Provider`. (optional)
name        | [Option](#option)[String]                         | the name of the `Provider`. (optional)
phones      | Array[String]                                     | the phones's list of the `Provider`.
fax         | Array[String]                                     | the fax's list of the `Provider`.
emails      | Array[String]                                     | the emails's list of the `Provider`.

## BasicAddress

<aside class="warning">
	This kind of address will be deprecated soon.
</aside>

cf. [Recommendation format d'adresse par La Poste](https://www.amabis.com/rediger-saisir-adresse-postale/)

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
quality     | [Option](#option)[String]                         | 
street      | String                                            | 
complement  | [Option](#option)[String]                         | 
recipientSupplement    | [Option](#option)[[RecipientIdentificationSupplement](#recipientidentificationsupplement)]    |
geographicalSupplement | [Option](#option)[[GeographicalIdentificationSupplement](#geographicalidentificationsupplement)] |
zipCode     | String                                            |
city        | String                                            |
state       | String                                            |
country     | [Option](#option)[String]                         |

## RecipientIdentificationSupplement

Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
floor       | Option[String]                                    | Etage
unit        | Option[String]                                    | numéro d'appartement
entrance    | Option[String]                                    | Entrée
elevator    | Option[String]                                    | ascensceur
staircase   | Option[String]                                    | escalier
   
## GeographicalIdentificationSupplement

Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
building    | Option[String]                                    | batiment

## AbstractProviderView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
uid         | [SafeUUID](#safeuuid)                             | the `Provider`'s uid.
name        | String                                            | the `Provider`'s name.

## TicketStats

### Fields

Name                    | Type                                              | Description
------------------------| --------------------------------------------------| --------------------------------
newTickets              | [NewTicketsStats](#newticketsstats)               | some statistics on the `Tickets`. 
ticketCreationFrequency | [TicketCreationFrequencyStats](#ticketcreationfrequencystats) | 

## NewTicketsStats 

### Fields

Name            | Type    | Description
----------------| --------| -----------------
lastSevenDays   | Number  | The number of `Ticket`created the last seven days. 
lastMonth       | Number  | The number of `Ticket`created the last month.
currentMonth    | Number  | The number of `Ticket`created this current month.

## TicketCreationFrequencyStats

### Fields

Name            | Type    | Description
----------------| --------| -----------------
byDay           | Number  | the `Ticket`'s creation frequency by day.

## DetailedTicketView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
uid         | [SafeUUID](#safeuuid)                             | the `Ticket`'s uid
ref         | String                                            | the `Ticket`'s client reference.<br/> Could be `clientClaimNumber`or `callCenterClaimNumber` or `ticket_uid`.
agencies    | Array[[AgencyAbstract](#agencyabstract)]          | the `Agency` linked to this `Ticket`.
patrimony   | [Option](#option)[[PatrimonyAbstract](#patrimonyabstract)] | the `Patrimony` linked to this `Ticket`. optional.
status      | ENUM                                              | `OPENED` or `CLOSED`.
state       | [Option](#option)[[TicketStateView](#ticketstateview)] | the actual `state` of this `Ticket`.<br/> ex: `MissionAccepted`
request     | String                                            | description of the issue.
instructions| String                                            | insctructions about the intervention.
created     | [DateTime](#datetime)                             | the date when this `Ticket` was opened.
updated     | [DateTime](#datetime)                             | the date when last update of this `Ticket` occured.
closed      | [DateTime](#datetime)                             | the date when this `Ticket` was closed.
callPurpose | String                                            | the `callPurpose` of this `Ticket`.
caller      | [CallerTicketDetailedQueryView](#callerticketdetailedqueryview) | informations on person who ask for open this `Ticket`.
report      | [Option](#option)[String]                         | intervention report, when intervention took place. 
provider    | [Option](#option)[[ProviderQueryView](#providerqueryview)] | informations on the possible last `Provider` acting on this `Ticket`.
address     | [BasicAddress](#basicaddress)                     | the `Address` where the incident occurs.
journal     | Array[[DayEvent](#dayevent)]                      | the `Ticket`'s event log.
additionalDataz | Map[String,String]                            | a map of client's additional fields.<br/> ex: `{field1: value_1}`
stats       | DetailedTicketStats                               | a set of several stats on this `Ticket`.


## DetailedTicketStats

> DetailedTicketStats example :

```json
{
	"callCenterReactionTime":"300000",       
    "transmissionTime":"3600000",
    "interventionResponseTime":"4560000",
    "interventionDuration":"360000",
    "repairTime":"54000"
}
``` 

### Fields

Name                    | Type                                     | Description
------------------------| -----------------------------------------| -----------------
callCenterReactionTime  | [Option[[Duration](#duration)]](#option) | Calcul du temps de réaction du centre d'appel. <br/> Cette valeur est obtenue en calculant le temps entre la date de création du `Ticket` et la première action signficative du centre d'appel
transmissionTime        | [Option[[Duration](#duration)]](#option) | Calcul du temps de transmission vers un intervenant. <br/> Cette valeur est obtenue en calculant le temps entre la date de création du `Ticket` et l'acceptation d'une mission par un intervenant. <br/> i.e l'évènement `MissionAccepted` 
interventionResponseTime| [Option[[Duration](#duration)]](#option) | Calcul du temps de réponse pour intervenir sur un problème. <br/> Cette valeur est obtenue en calculant le temps entre la date de création du `Ticket` et une action significative de l'intervenant. <br/> i.e `InterventionStarted`, `InterventionFinished`, `ArrivedOnSite`, `GoneFromSite` 
interventionDuration    | [Option[[Duration](#duration)]](#option) | Calcul de la durée d'intervention. <br/> i.e le temps entre `InterventionStarted` et `InterventionFinished`
repairTime              | [Option[[Duration](#duration)]](#option) | Calcul le délai de réparation. <br/> Cette valeur est obtenue en calculant le temps entre la date de création du ticket et la date de fin d'intervention


## DayEvent

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
day         | [LocalDate](#localdate)                           | the day when the events took place.
events      | Array[[JournalEvent](#journalevent)]              | the list of `JournalEvent` for this day.

## JournalEvent

### Fields

Name        | Type                                  | Description
------------| --------------------------------------| -------------------------------------
eventName   | String                                | the event's name.
date        | [DateTime](#datetime)                 | the date when event took place.
data        | [JournalEventData](#journaleventdata) | some data associated with this event.

## CallerTicketDetailedQueryView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
name        | String                                            | the name of the caller
medium      | [Option](#option)[[ContactMediumView](#contactmediumview)] | the medium use by the caller to open `Ticket`.
comment     | [Option](#option)[String]                         | set to enter the place of intervention 

## JournalEventData

Each Journal Event has its own data format. 

If you don't see an Event you use, it means this Event doesn't have additional data. `data: {}`

### CallEmittedTo

Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
called      | String                                            | the name of the person called.
medium      | Enum                                              | the medium use to emit call.<br/> `PHONE | FAX | MAIL | SMS`
identifier  | String                                            | set to enter the place of intervention

### CallReceived

Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
caller      | String                                            | the name of the person called.
medium      | Enum                                              | the medium use to emit call.<br/> `PHONE | FAX | MAIL | SMS`
identifier  | String                                            | set to enter the place of intervention

### ProviderAssigned
	
Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
type        | Enum                                              | the type of the assignation.<br/> `RecourseChanged | ProviderAssigned`
provider    | [Option](#option)[String]                                    | the `Provider`s name assigned. 

### CallAnsweredByProvider		

Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
provider    | [Option](#option)[String]                                    | the `Provider`s name who answered.

### CallNotAnsweredByProvider 		

Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
provider    | [Option](#option)[String]                                    | the `Provider`s name who did not answer.

### MissionAccepted		

Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
provider    | [Option](#option)[String]                                    | the `Provider`s name who accepted the mission.

### MissionRefused		

Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
provider    | [Option](#option)[String]                                    | the `Provider`s name who dit not accept the mission.
		
### LogTrialAdded

Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
trialLabel  | String                                            | the label of the trial log.

### MessageAdded		

Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
message     | String                                            | 

### ArrivedOnSite		

Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
provider    | [Option](#option)[String]                                    | the `Provider`s name arrived on site.

### GoneFromSite		

Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
provider    | [Option](#option)[String]                                    | the `Provider`s name gone from site.

### TicketClosed

Name            | Type                                              | Description
----------------| --------------------------------------------------| -----------------
brakeDownNature | [Option](#option)[String]                                    | description of the breakdown

### PermanentlyFixed

Name            | Type                                              | Description
----------------| --------------------------------------------------| -----------------
brakeDownNature | [Option](#option)[String]                                    | description of the breakdown

### PartiallyFixed

Name            | Type                                              | Description
----------------| --------------------------------------------------| -----------------
brakeDownNature | [Option](#option)[String]                                    | description of the breakdown

### TicketClosedImpossibleRepair

Name            | Type                                              | Description
----------------| --------------------------------------------------| -----------------
brakeDownNature | [Option](#option)[String]                                    | description of the breakdown

### PostponedFix

Name            | Type                                              | Description
----------------| --------------------------------------------------| -----------------
brakeDownNature | [Option](#option)[String]                                    | description of the breakdown
		
## PatrimonyResultView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
result      | Array[[PatrimonyQueryView](#patrimonyqueryview)]  | Array of selected `PatrimonyQueryView`s

## PatrimonyQueryView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
uid         | [SafeUUID](#safeuuid)                             | the uid of the `Patrimony`
ref         | String                                            | a client reference to `Patrimony`
label       | [Option](#option)[String]                         | an optional label of the `Patrimony`
agencies    | [NonEmptyList](#nonemptylist)[[SafeUUID](#safeuuid)] | a non empty array of agency uid linked to the `Patrimony`
complementaryAddresses | Array[[PatrimonyQueryAddressReference](#patrimonyqueryaddressreference)]  |
addresses   | Array[[PatrimonyQueryAddressReferenceWithBuildingInfo](#patrimonyqueryaddressreferencewithbuildinginfo)] |

## PatrimonyDetailQueryView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
uid         | [SafeUUID](#safeuuid)                             | the uid of the `Patrimony`
ref         | String                                            | a client reference to `Patrimony`
label       | [Option](#option)[String]                         | an optional label of the `Patrimony`
agencies    | [NonEmptyList](#nonemptylist)[[PatrimonyAgencyQueryView](#patrimonyagencyqueryview)] | a non empty array of agency infos linked to the `Patrimony`
complementaryAddresses | Array[[PatrimonyQueryAddressReference](#patrimonyqueryaddressreference)] |
addresses   | Array[[PatrimonyQueryAddressReferenceWithBuildingInfo](#patrimonyqueryaddressreferencewithbuildinginfo)] |

## PatrimonyAgencyQueryView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
uid         | [SafeUUID](#safeuuid)                             | the uid of the `Agency`
label       | String                                            | the name of the `Agency`

## PatrimonyBuildingResultView

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
result      | Array[[BuildingQueryView](#buildingqueryview)]    | Array of selected `Building`s

## PatrimonyDetailedBuildingQueryView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
uid         | [SafeUUID](#safeuuid)                             | the uid of the `Building`
label       | String                                            | the name of the `Building`
patrimony   | PatrimonyBuildingView                             | reference to the `Patrimony` of this `Building`
addresses   | Array[[PatrimonyQueryAddressReference](#patrimonyqueryaddressreference)] | the `Addresses` of the requested `Building`

## PatrimonyQueryAddressReference

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
uid         | [SafeUUID](#safeuuid)                             | 
number      | String                                            | 
street      | String                                            | 
city        | String                                            | 
zipCode     | String                                            | 
country     | [Option](#option)[String]                         | 
quality     | [Option](#option)[String]                         | 
complement  | [Option](#option)[String]                         | 
state       | [Option](#option)[String]                         | 
geoLocation | [GeoLocation](#geolocation)                       | geolocation of the `Address`. 
checker     | [AddressChecker](#addresschecker)                 | a variable to allow to verify `Address`. 

## PatrimonyQueryAddressReferenceWithBuildingInfo

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
uid         | [SafeUUID](#safeuuid)                             | 
number      | String                                            | 
street      | String                                            | 
city        | String                                            | 
zipCode     | String                                            | 
country     | [Option](#option)[String]                         | 
quality     | [Option](#option)[String]                         | 
complement  | [Option](#option)[String]                         | 
state       | [Option](#option)[String]                         | 
geoLocation | [GeoLocation](#geolocation)                       | geolocation of the `Address`. 
checker     | [AddressChecker](#addresschecker)                 | a variable to allow to verify `Address`.
building    | [ItemAbstract](#itemabstract)                     | a `Building` reference for this `Address`.

## BuildingQueryView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
uid         | [SafeUUID](#safeuuid)                             | the uid of the `Building`
label       | String                                            | the name of the `Building`
patrimony   | PatrimonyBuildingView                             | reference to the `Patrimony` of this `Building`

## PatrimonyBuildingView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
uid         | [SafeUUID](#safeuuid)                             | the uid of the `Patrimony`

## GeoLocation

Geolocation of the `Address`.

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
lat         | Float                                             | latitude
lng         | Float                                             | longitude 

## AddressChecker

`AddressChecker` is an Enum, i.e type can take different values : 

```haskell
data AddressChecker = GooglePlaceIdChecker
```

### GooglePlaceIdChecker 

> GooglePlaceIdChecker example :

```json
{
	"googlePlaceId":"123456hg"
}
```

`GooglePlaceIdChecker` allow to check `Address`via Google Maps API.

Name          | Type   | Description
--------------| -------| --------------------------------------------------------
googlePlaceId | String | identifier to check the `Address` with Google Maps API. 

## RawAgency

> RawAgency example :

```json
{
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
}
```

`RawAgency` describe an `Agency` for create it.

Name          | Type                                                       | Description
--------------| -----------------------------------------------------------| --------------------------------------------------------
agencyUid     | [Option](#option)[[SafeUUID](#safeuuid)]                   | The UID of the `Agency`. If you don't set this param. PerfImmo generate it for you. 
name          | String                                                     | The name of the `Agency` 
extName       | [Option](#option)[String]                                  |  
address       | [Option](#option)[[AddressForCommand](#addressforcommand)] | The address of the `Agency`
phones        | Array[String]                                              | a list of phone number to contact the `Agency`
fax           | [Option](#option)[String]                                  |  
emails        | Array[String]                                              | a list of emails to contact the `Agency`

## AddressForCommand

`AddressForCommand` is an Enum, i.e type can take different values : 

```haskell
data AddressForCommand = RationalAddress | AddressReference
```

### RationalAddress
 
Name          | Type                        | Description
--------------| ----------------------------| --------------------------------------------------------
quality       | [Option](#option)[String]   |   
number        | String                      |  
street        | String                      |  
complement    | [Option](#option)[String]   | 
zipCode       | String                      | 
city          | String                      |  
state         | [Option](#option)[String]   | 
country       | [Option](#option)[String]   | 
 
 
### AddressReference  
  
Name          | Type                                | Description
--------------| ------------------------------------| --------------------------------------------------------
quality       | [Option](#option)[String]           |  
number        | String                              |  
street        | String                              |  
complement    | [Option](#option)[String]           | 
zipCode       | String                              | 
city          | String                              |  
state         | [Option](#option)[String]           | 
country       | [Option](#option)[String]           |  
geoLocation   | [GeoLocation](#geolocation)         |  
checker       | [AddressChecker](#addresschecker)   |  

## PatrimonyAddressReference

> json body example : 

```json
{
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
	},
	"floor":"3",
	"unit":"1C",
	"digicode":"1435",
	"entrance":"B",
	"elevator":"C",
	"staircase":"2E"
}
```

Name          | Type                                | Description
--------------| ------------------------------------| --------------------------------------------------------
quality       | [Option](#option)[String]           |  
number        | String                              | the number of the street. ex: 12 
street        | String                              | ex: avenue de Paris 
complement    | [Option](#option)[String]           | 
zipCode       | String                              | zipCode of this `Address` 
city          | String                              | ex: Paris 
state         | [Option](#option)[String]           | 
country       | [Option](#option)[String]           | ex: France 
geoLocation   | [GeoLocation](#geolocation)         | geolocation of the `Address` (with latitude & longitude value) 
checker       | [AddressChecker](#addresschecker)   | used to identify `Address` across external tools (ex: google place ID)
floor         | [Option](#option)[String]           | 
unit          | [Option](#option)[String]           |
digicode      | [Option](#option)[String]           |
entrance      | [Option](#option)[String]           |
elevator      | [Option](#option)[String]           |
staircase     | [Option](#option)[String]           |

## ProviderContactResultView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
result      | Array[[ProviderContactQueryView](#providercontactqueryview)]  | Array of selected `ProviderContactQueryView`s
_links      | Array[[RestNavigationLink](#restnavigationlink)]  | Array of `RestNavigationLink`. Allow building decoupled navigation workflow.

## ProviderContactQueryView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
uid         | [SafeUUID](#safeuuid)                             | the uid of the `ProviderContact`
label       | String                                            | label of the `ProviderContact`
phones      | Array[String]                                     | 
fax         | Array[String]                                     | 
emails      | Array[String]                                     | 
active      | Boolean                                           | 
_links      | Array[[RestNavigationLink](#restnavigationlink)]  | Array of `RestNavigationLink`. Allow building decoupled navigation workflow.

## ProviderCompanyResultView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
result      | Array[[ProviderCompanyQueryView](#providercompanyqueryview)]  | Array of selected `ProviderCompanyQueryView`s
_links      | Array[[RestNavigationLink](#restnavigationlink)]  | Array of `RestNavigationLink`. Allow building decoupled navigation workflow.

## ProviderCompanyQueryView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
uid         | [SafeUUID](#safeuuid)                             | the uid of the `ProviderCompany`
name        | String                                            | the name of the `ProviderCompany` 
siretNumber | [SIRET](#siret)                                   | the siret number of the `ProviderCompany`  
_links      | Array[[RestNavigationLink](#restnavigationlink)]  | Array of `RestNavigationLink`. Allow building decoupled navigation workflow.

## ProviderContactStats

### Fields

Name                        | Type                                              | Description
----------------------------| --------------------------------| --------------------------------------------------
interventionDelay           | Array[[DelayStat](#delaystat)]  | Time between [`MissionAccepted`](#missionaccepted) & [`InterventionStarted`](#interventionstarted) 
missionAcceptedDelay        | Array[[DelayStat](#delaystat)]  | Time between [`CallEmittedTo`](#callemittedto) & [`MissionAccepted`](#missionaccepted)
repairDelay                 | Array[[DelayStat](#delaystat)]  | Time between [`MissionAccepted`](#missionaccepted) & [`InterventionFinished`](#interventionfinished) or `ClosingTicketEvent` 
callBeforeMissionAccepted   | Array[[CountStat](#countstat)]  | Count the number of [`CallEmittedTo`](#callemittedto) before [`MissionAccepted`](#missionaccepted) 
interventionNumber          | Array[[CountStat](#countstat)]  | Count the number of intervention of this `ProviderContact`

## DelayStat

### Fields

This statistic measure a time average in milliseconds grouped by day of ticket creation.

Name                        | Type                            | Description
----------------------------| --------------------------------| --------------------------------------------------
day                         | [LocalDate](#localdate)         | a day when tickets are created
value                       | Long                            | a time average in milliseconds

## CountStat

### Fields

Name                        | Type                            | Description
----------------------------| --------------------------------| --------------------------------------------------
day                         | [LocalDate](#localdate)         | a day when tickets are created
value                       | Float                           | a count with 2 significant figures

## CompanyEventResultView

### Fields

Name                        | Type                            | Description
----------------------------| --------------------------------| --------------------------------------------------
events                      | Array[[CompanyEvent](#companyevent)] | The `Event`s resulting of this `Command`

## ProviderContactEventResultView

### Fields

Name                        | Type                            | Description
----------------------------| --------------------------------| --------------------------------------------------
events                      | Array[[ProviderContactEvent](#providercontactevent)] | The `Event`s resulting of this `Command`

## ProviderCompanyEventResultView

### Fields

Name                        | Type                            | Description
----------------------------| --------------------------------| --------------------------------------------------
events                      | Array[[ProviderCompanyEvent](#providercompanyevent)] | The `Event`s resulting of this `Command`

## TicketEventResultView

> example :

```json
{
    "events": [
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
    ]
}        
```


### Fields

Name                        | Type                            | Description
----------------------------| --------------------------------| --------------------------------------------------
events                      | Array[[TicketEvent](#ticketevent)] | The `Event`s resulting of this `Command`

## LocationReference

`LocationReference` is an Enum, i.e type can take different values : 

```haskell
data LocationReference = AgencyLocation | PatrimonyLocation
```

### AgencyLocation 

> AgencyLocation example :

```json
{
	"agencyUid":"d5c48f2f-2bcc-40ff-9a5c-4ba5d33419df",
    "locationReferenceType":"AgencyLocation"
}
```

A `AgencyLocation` bind a `Ticket` with an `Agency`.

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------
agencyUid   | [SafeUUID](#safeuuid)                             | uid of the `Agency`.
locationReferenceType | Constant                                | `"AgencyLocation"`
                        
### PatrimonyLocation                        
   
> PatrimonyLocation example :

```json
{
	"patrimonyUid":"d5c48f2f-2bcc-40ff-9a5c-4ba5d33419df",
    "locationReferenceType":"PatrimonyLocation"
}
```                        
                        
A `PatrimonyLocation` bind a `Ticket` with an `Patrimony`.

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------
patrimonyUid| [SafeUUID](#safeuuid)                             | uid of the `Patrimony`.
locationReferenceType | Constant                                | `"PatrimonyLocation"`

## Operator

`Operator` is an Enum, i.e type can take different values : 

```haskell
data Operator = ReferencedOperator | AnonymousOperator | ReferencedUser
```

An `Operator` is a person who perform the `Command` on a `Ticket`.

### ReferencedOperator 

`ReferencedOperator` is a known `Operator` on Perfimmo and we can retrieve him with his uid.

> ReferencedOperator example :

```json
{
	"operatorUid":"d5c48f2f-2bcc-40ff-9a5c-4ba5d33419df",
    "operatorType":"ReferencedOperator"
}
```

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------
operatorUid | [SafeUUID](#safeuuid)                             | uid of the `Operator`.
operatorType| Constant                                          | `"ReferencedOperator"`
                        
### AnonymousOperator                        
   
> AnonymousOperator example :

```json
{
	"name":"John Doe",
    "operatorType":"AnonymousOperator"
}
```                        

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------
name        | String                                            | the name of the `Operator`. 
operatorType| Constant                                          | `"AnonymousOperator"`

### ReferencedUser                        
   
> ReferencedUser example :

```json
{
	"userUid":"d5c48f2f-2bcc-40ff-9a5c-4ba5d33419df",
    "operatorType":"ReferencedUser"
}
```                        

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------
userUid     | [SafeUUID](#safeuuid)                             | the uid of the `ReferencedUser` who perform this `Command`. 
operatorType| Constant                                          | `"ReferencedUser"`

## TicketInfos

> TicketInfos example :

```json
{
	"ticket": {
         "caller": {
           "name": {
             "value": "Mr John Doe",
             "nameType": "PoorName"
           },
           "medium": {
             "phone": "0320015450",
             "contactMediumType": "Phone"
           },
           "callerType": "HumanCaller"
         },
         "claimNumber": {
           "clientClaimNumber": "2016256649"
         },
         "address": {
           "quality": "quality",
           "street":"street",
           "complement": "complement",
           "zipCode": "zipCode",
           "city": "city",
           "state": "state",
           "country":"country"
         },
         "request": "FRIGOS EN PANNE",
         "callPurposeLabel": "frigoriste",
         "altCallPurpose":{},
         "additionalData":{
           "Code magasin": "FRPK98",
           "Corps de métier": "FRIGORISTE",
           "Libellé Code panne": "FRIGORISTE",
           "Nom magasin": "TOURCOING",
           "Heure réception OT": "16:51:02",
           "OS urgent": "NON"
         }
    }
}
```

### Fields

Name              | Type                                              | Description
------------------| --------------------------------------------------| --------------------------
caller            | [CallerType](#callertype)                         | the origin of the creation of the `Ticket`.
contactToCallback | [Option](#option)[[ContactToCallback](#contacttocallback)] | a person to callback.
claimNumber       | [ClaimNumber](#claimnumber)                       | an external `Ticket id to display on Perfimmo web app.
address           | [BasicAddress](#basicaddress)                               | the `Address` where the incident took place.
request           | String                                            | a description of the problem that is causing the opening of the ticket. 
instructions      | [Option](#option)[String]                         | optional instructions about this incident.
callPurposeLabel  | String                                            | the purpose of the incident. This field will be display on the Perfimmo web app. 
altCallPurpose    | [Map](#map)[String, Array[String]],               |  
additionalData    | [Map](#map)[String, [Option](#option)[String]]    | some addional data you want to display on the detailed `Ticket` page.

## CallerType

`CallerType` is an Enum, i.e type can take different values : 

```haskell
data CallerType = HumanCaller | AutomatonCaller
```

### HumanCaller 

> HumanCaller example :

```json
{
    "name":{
        "name":"John Doe",
        "nameType":"PoorName"
    },
    "medium":{
        "phone":"0146305645",
        "contactMediumType":"Phone"
    },
    "comment":"Some comments.",
    "callerType":"HumanCaller"
}
```

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------
name        | [Name](#name)                                     | the name of the caller.
medium      | [Option](#option)[[ContactMedium](#contactmedium)]| the medium used to contact.
comment     | [Option](#option)[String]                         | 
callerType  | Constant                                          | `"HumanCaller"`
                        
### AutomatonCaller                        
   
> AutomatonCaller example :

```json
"AutomatonCaller"
```                        

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------
            | Constant                                          | `"AutomatonCaller"`

## ContactToCallback

> ContactToCallback example :

```json
{
    "name":"John Doe",
    "medium":{
        "phone":"0146305645",
        "contactMediumType":"Phone"
    },
    "availability":"2016-02-29T12:03:32+02:00",
    "comment":"this person is the real owner of the apartment"
}
```

### Fields
 
Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------
name        | String                                            | the name of the person to call back.
medium      | [ContactMedium](#contactmedium)                   | the medium to use to call back.
availability| [Option](#option)[[DateTime](#datetime)]          | the moment when the person must be call back. 
comment     | [Option](#option)[String]                         | 

## ClaimNumber

`ClaimNumber` is an `Ticket` identifier you can use to display for your clients and for research `Ticket`.
This allows to use identifier that have more sense than Perfimmo one for users.

The rules is :
  
  - display `clientClaimNumber` first if exist
  
  - then display `callCenterClaimNumber` if exist
  
  - then display the internal Perfimmo uid (i.e aggregateUid)

> ClaimNumber example :

```json
{
    "callCenterClaimNumber":"CC_234",
    "clientClaimNumber":"CLIENT_1234"
} 
```

### Fields
 
Name                  | Type                                              | Description
----------------------| --------------------------------------------------| --------------------------
callCenterClaimNumber | [Option](#option)[String]                         | an id specific to the `CallCenter`.
clientClaimNumber     | [Option](#option)[String]                         | an id specific to the client of the `CallCenter`.

## ContactMedium

`ContactMedium` is an Enum, i.e type can take different values : 

```haskell
data ContactMedium = Phone | Fax | Mail | SMS
```

### Phone 

> Phone example :

```json
{
    "phone":"0146305674",
    "contactMediumType":"Phone"
}
```

Name              | Type                                              | Description
------------------| --------------------------------------------------| --------------------------
phone             | String                                            | 
contactMediumType | Constant                                          | `"Phone"`
                        
### Fax 

> Fax example :

```json
{
    "fax":"0146305674",
    "contactMediumType":"Fax"
}
```

Name              | Type                                              | Description
------------------| --------------------------------------------------| --------------------------
fax               | String                                            | 
contactMediumType | Constant                                          | `"Fax"`

### Mail 

> Mail example :

```json
{
    "fax":"0146305674",
    "contactMediumType":"Mail"
}
```

Name              | Type                                              | Description
------------------| --------------------------------------------------| --------------------------
mail              | String                                            | 
contactMediumType | Constant                                          | `"Mail"`

### SMS 

> SMS example :

```json
{
    "phone":"0146305674",
    "contactMediumType":"SMS"
}
```

Name              | Type                                              | Description
------------------| --------------------------------------------------| --------------------------
phone             | String                                            | 
contactMediumType | Constant                                          | `"SMS"`

## Persona

`Persona` is an Enum, i.e type can take different values : 

```haskell
data Persona = UnClassifiedPersona | ProviderPersona
```

### UnClassifiedPersona 

> UnClassifiedPersona example :

```json
{
    "name":{
        "name":"John Doe",
        "nameType":"PoorName"
    },
    "status":"guardian",
    "callPurpose":"ask for open doors",
    "personaType":"UnClassifiedPersona"
}
```

Name              | Type                                              | Description
------------------| --------------------------------------------------| --------------------------
name              | [Name](#name)                                     | the name of the person called.
status            | [Option](#option)[String]                         | the status of this person. 
callPurpose       | [Option](#option)[String]                         | the purpose of the call. 
personaType       | Constant                                          | `"UnClassifiedPersona"`    
    
### ProviderPersona 

> ProviderPersona example :

```json
{
    "provider":{
        "providerUid":"d5c48f2f-2bcc-40ff-9a5c-4ba5d33419df",
        "providerType":"ReferencedProvider"
    },
    "personaType":"ProviderPersona"
}
```

Name              | Type                                              | Description
------------------| --------------------------------------------------| --------------------------
provider          | [Provider](#provider)                             | the provider called.
personaType       | Constant                                          | `"ProviderPersona"`    

## Provider

`Provider` is an Enum, i.e type can take different values : 

```haskell
data Provider = ReferencedProvider | AnonymousProvider
```

### ReferencedProvider 

A `ReferencedProvider` is a `Provider` that can be identified by its uid on Performance-immo app. 

> ReferencedProvider example :

```json
{
    "providerUid":"d5c48f2f-2bcc-40ff-9a5c-4ba5d33419df",
    "providerType":"ReferencedProvider"
}
```

Name              | Type                                              | Description
------------------| --------------------------------------------------| --------------------------
providerUid       | [SafeUUID](#safeuuid)                             | 
providerType      | Constant                                          | `"ReferencedProvider"`

### AnonymousProvider 

An `AnonymousProvider` is a `Provider` that is not referenced on Performance-immo app.

> AnonymousProvider example :

```json
{
    "name":{
        "firstName":"John",
        "lastName":"Doe",
        "gender":"Male",
        "nameType":"CivilName"
    },
    "phones":["0146374567", "0645342378"],
    "fax":[],
    "emails":["john.doe@performance-immo.com"],
    "providerType":"AnonymousProvider"
}
```

Name              | Type                                              | Description
------------------| --------------------------------------------------| --------------------------
name              | [Name](#name)                                     |  
phones            | Array[String]                                     |  
fax               | Array[String]                                     |  
emails            | Array[String]                                     |  
providerType      | Constant                                          | `"AnonymousProvider"`

## ProviderAssignationPurpose

`ProviderAssignationPurpose` is an Enum, i.e type can take different values : 

```haskell
data ProviderAssignationPurpose = RecourseChanged | Purpose
```

### Purpose 

> Purpose example :

```json
{
    "purpose":"pre assignation",
    "providerAssignationPurposeType":"Purpose"
}
```

Name              | Type                                              | Description
------------------| --------------------------------------------------| --------------------------
purpose           | String                                            | 
providerAssignationPurposeType | Constant                             | `"Purpose"`


### RecourseChanged 

> RecourseChanged example :

```json
{
    "comment":"not for plumbing",
    "providerAssignationPurposeType":"RecourseChanged"
}
```

Name              | Type                                              | Description
------------------| --------------------------------------------------| --------------------------
comment           | [Option](#option)[String]                                            | 
providerAssignationPurposeType | Constant                             | `"RecourseChanged"`

## LogTrial

> LogTrial example :

```json
{
    "trialCode":"123",
    "trialLabel":"a log append to the journal of the Ticket"
}
```

Name              | Type                                              | Description
------------------| --------------------------------------------------| --------------------------
trialCode         | [Option](#option)[String]                         | 
trialLabel        | String                                            | 

## StillOnSite

`StillOnSite` is an Enum, i.e type can take different values. 

```haskell
data StillOnSite = Yes | No | NotAsked | ProviderRefuseToReply | NA
```

A simple String value that only can be :

- Yes 

- No 

- NotAsked

- ProviderRefuseToReply

- NA

## ServiceOrderKind

Allow to know who sent the service order (Perfimmo or the client for example)

`ServiceOrderKind` is an Enum, i.e type can take different values. 

```haskell
data ServiceOrderKind = NotSentByPerfimmo | SentByPerfimmo
```

A simple String value that only can be :

- NotSentByPerfimmo
 
- SentByPerfimmo 

## ServiceOrder

> ServiceOrder example :

```json
{
	"ref":"123DRX34",
	"sendingDate":"2016-02-29T12:03:32+02:00"
}
```

Name              | Type                                              | Description
------------------| --------------------------------------------------| --------------------------
ref               | String                                            | the reference of the service order.
sendingDate       | [DateTime](#datetime)                             | the sending date of the service order.

## FieldsToCorrect

<aside class="warning">
	It is possible to set <b>closingReport</b> field only if the <b>Ticket</b> is already closed.
</aside>

Name              | Type                                              | Description
------------------| --------------------------------------------------| --------------------------
request           | [Option](#option)[String]                         | field `request` in [TicketInfos](#ticketinfos). If setted with non blank value, will be overwritten the old value.
instructions      | [Option](#option)[String]                         | field `instructions` in [TicketInfos](#ticketinfos). If setted with non blank value, will be overwritten the old value.
closingReport     | [Option](#option)[String]                         | `closingReport` when `Ticket` is closed. If setted with non blank value, will be overwritten the old value.
