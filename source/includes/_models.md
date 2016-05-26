# Models

## Option

Means that field is optional. If parameter has no value, it is not present in the json payload.

<aside class="warning">
	<code> { "field1":"toto", field2:"" } is not equivalent to { "field1":"toto" } </code>
</aside>

## NonEmptyList

An json `array`that can't be empty.

## SafeUUID

Identifiant garanti unique en utilisant la norme [GUUID](https://fr.wikipedia.org/wiki/Globally_Unique_Identifier)    

S'exprime sous forme de chaîne de caractères avec une contrainte sur le format.

ex: `8074964f-c633-3c2a-055f-bbaf8ca8181b`

## LocalDate

[ISO-8601 calendar system](https://fr.wikipedia.org/wiki/ISO_8601)  
`YYYY-MM-DD` ex: `2016-02-29`

## DateTime

[ISO-8601 calendar system](https://fr.wikipedia.org/wiki/ISO_8601)  
`YYYY-MM-DDTHH:mm:ss+02:00` ex: `2016-02-29T12:03:32+02:00`

## ItemAbstract

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
uid         | [SafeUUID](#safeuuid)                             | the uid of the item
label       | String                                            | the label of the item

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
userType    | String                                            | "superUser"

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
userType    | String                                            | "callCenterUser"

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
userType    | String                                            | "clientAccountManager"

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
userType        | String                                            | "executive"

## TicketResultView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
result      | Array[[TicketQueryView](#ticketqueryview)]        | Array of selected `Ticket`s
aggergations| [Aggregations](#aggregations)                     | Aggregations of several params.

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
agency      | [AgencyAbstract](#agencyabstract)                 | the `Agency` linked to this `Ticket`.
status      | ENUM                                              | `OPENED` or `CLOSED`.
state       | [Option](#option)[[TicketStateView](#ticketstateview)] | the actual `state` of this `Ticket`.<br/> ex: `MissionAccepted`
created     | [DateTime](#datetime)                             | the date when this `Ticket` was opened.
updated     | [DateTime](#datetime)                             | the date when last update of this `Ticket` occured.
closed      | [DateTime](#datetime)                             | the date when this `Ticket` was closed.
callPurpose | String                                            | the `callPurpose` of this `Ticket`.
caller      | [CallerQueryView](#callerqueryview)               | informations on person who ask for open this `Ticket`.
provider    | [Option](#option)[[ProviderQueryView](#providerqueryview)] | informations on the possible last `Provider` acting on this `Ticket`.
address     | [BasicAddress](#basicaddress)                     | the `Address` where the incident occurs.

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

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
quality     | [Option](#option)[String]                         | 
street      | String                                            | 
complement  | [Option](#option)[String]                         | 
zipCode     | String                                            |
city        | String                                            |
state       | String                                            |
country     | [Option](#option)[String]                         |

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
agency      | [AgencyAbstract](#agencyabstract)                 | the `Agency` linked to this `Ticket`.
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
callCenterReactionTime  | Option[Number]                        | duration in milliseconds.
transmissionTime        | Option[Number]                        | duration in milliseconds.
interventionResponseTime| Option[Number]                        | duration in milliseconds.
interventionDuration    | Option[Number]                        | duration in milliseconds.
repairTime              | Option[Number]                        | duration in milliseconds.

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

