# Models

## Option

Means that field is optional. If parameter has no value, it is not present in the json payload.

<aside class="warning">
	<code> { "field1":"toto", field2:"" } is not equivalent to { "field1":"toto" } </code>
</aside>

## NonEmptyList

A json `array`that can't be empty.

## NonEmptyString

A `String` that can't be empty.

## Map

a json object with "free" field

> Map[String, String] example :

```json
{
    "field1":"value1",
    "field2":"value2"
}
```

## FormattedText

Tag the field can be formatted in a certain way.

ex: FormattedText[String] you can display `\n` in your client. 

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

## PhoneNumber

a String formatted as a valid PhoneNumber

ex: "0123344556" or "+33123344556"

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

## ItemAbstractWithRef

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
uid         | [SafeUUID](#safeuuid)                             | the uid of the item
ref         | String                                            | the reference of the item
label       | [Option](#option)[String]                         | the label of the item

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
	"company":"My Compnay & sons",
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
company     | [Option](#option)[String]                         | an optional company's name
nameType    | Constant                                          | `"CivilName"`

## CompanyQueryView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------
uid         | [SafeUUID](#safeuuid)                             | id of the `Company`
label       | String                                            | the `Company`'s label
isActive    | Boolean                                           | `true` if the `Company` is active
holding     | [Option](#option)[[HoldingQueryView](#holdingqueryview)] | a reference to `Company`'s holding if has it
siretNumber | [Option](#option)[[SIRET](#siret)]                |
billingType | [Option](#option)[[CompanyBillingType](#companybillingtype)] |
companyType | Enum                                              | enum : `"CallCenter"` or `"ClientAccountHolding"` or `"ClientAccount"`

## CompanyBillingType

`CompanyBillingType` is an Enum, i.e type can take different values :
 
```haskell
data CompanyBillingType = SponsoredAccount | PremiumAccount | StandardAccount
```

A simple String value that only can be :

- SponsoredAccount (Account sponsored by a CallCenter) 

- PremiumAccount   (Account sponsored by a CallCenter but with more rights)

- StandardAccount  (Account that is directly billing with Perfimmo)


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
state       | [Option](#option)[[TicketStateView](#ticketstateview)] | the actual `state` of this `Ticket`.<br/> ex: `InterventionAccepted`
created     | [DateTime](#datetime)                             | the date when this `Ticket` was opened.
updated     | [DateTime](#datetime)                             | the date when last update of this `Ticket` occured.
closed      | [DateTime](#datetime)                             | the date when this `Ticket` was closed.
openingTicketPurpose | [OpeningTicketPurpose](#openingticketpurpose) | the `purpose` of this `Ticket`.
caller      | [CallerQueryView](#callerqueryview)               | informations on person who ask for open this `Ticket`.
assignee    | [Option](#option)[[TicketAssigneeQueryView](#ticketassigneequeryview)] | informations on the possible last `TicketAssignee` acting on this `Ticket`.
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
state       | [Option](#option)[[TicketStateView](#ticketstateview)] | the actual `state` of this `Ticket`.<br/> ex: `InterventionAccepted`
created     | [DateTime](#datetime)                             | the date when this `Ticket` was opened.
updated     | [DateTime](#datetime)                             | the date when last update of this `Ticket` occured.
closed      | [DateTime](#datetime)                             | the date when this `Ticket` was closed.
callPurpose | String                                            | the `callPurpose` of this `Ticket`.
request     | String                                            | the details of the demand.
caller      | [CallerQueryView](#callerqueryview)               | informations on person who ask for open this `Ticket`.
assignee    | [Option](#option)[[TicketAssigneeQueryView](#ticketassigneequeryview)] | informations on the possible last `TicketAssignee` acting on this `Ticket`.
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

## ClientCompanyAbstract

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
uid         | [SafeUUID](#safeuuid)                             | the `ClientCompany`'s uid
name        | String                                            | the `ClientCompany`'s name
holding     | [Option](#option)[[SafeUUID](#safeuuid)]          | the `ClientCompany`'s holding uid if exist

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
uid         | [SafeUUID](#safeuuid)                             | the `Patrimony`'s perfimmo uid
name        | String                                            | the `Patrimony`'s name
ref         | String                                            | the `Patrimony`'s reference

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
uid         | [Option](#option)[[SafeUUID](#safeuuid)]          | the uid of the caller if he is referenced by Perfimmo as `PatrimonyContact`
name        | String                                            | the name of the caller
medium      | Array[[ContactMediumView](#contactmediumview)]    | the mediums of the caller. 

## ContactMediumView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
mediumType  | String                                            | the type of the medium.<br/> ex: `PHONE | FAX | MAIL | SMS`
identifier  | String                                            | the identifier for this medium. <br/> ex: `0604030201`

## TicketAssigneeQueryView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
uid         | [Option](#option)[[SafeUUID](#safeuuid)]          | the uid of the `TicketAssignee`. (optional)
name        | String                                            | the name of the `TicketAssignee`.
phones      | Array[String]                                     | the phones's list of the `TicketAssignee`.
fax         | Array[String]                                     | the fax's list of the `TicketAssignee`.
emails      | Array[String]                                     | the emails's list of the `TicketAssignee`.
instructionsForAssignee | [Option](#option)[[FormattedText](#formattedtext)[String]] | some instructions for the assignee to perform his mission.
comment     | [Option](#option)[String]                         | some comments to report discussion with assignee.
assigneeType | [AssigneeType](#assigneetype)                    | the type of the assignee.

## AssigneeType

Simple enum value that can have these values : `ProviderContact | ProviderCompany | Anonymous`

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
clientCompany | [SafeUUID](#safeuuid)                           | the `ClientCompany` linked to this `Ticket`.
status      | ENUM                                              | `OPENED` or `CLOSED`.
state       | [Option](#option)[[TicketStateView](#ticketstateview)] | the actual `state` of this `Ticket`.<br/> ex: `InterventionAccepted`
request     | [FormattedText](#formattedtext)[String]           | description of the issue.
instructions| String                                            | insctructions about the intervention.
dates       | [TicketDates](#ticketdates)                       |
openingTicketPurpose | [OpeningTicketPurpose](#openingticketpurpose) | The reason the `Ticket` was opened.
caller      | [CallerTicketDetailedQueryView](#callerticketdetailedqueryview) | informations on person who ask for open this `Ticket`.
report      | [Option](#option)[String]                         | intervention report, when intervention took place. 
assignee    | [Option](#option)[[TicketAssigneeQueryView](#ticketassigneequeryview)] | informations on the possible last `TicketAssignee` acting on this `Ticket`.
address     | [BasicAddress](#basicaddress)                     | the `Address` where the incident occurs.
journal     | Array[[JournalEvent](#journalevent)]              | the `Ticket`'s event log.
additionalDataz | Map[String,String]                            | a map of client's additional fields.<br/> ex: `{field1: value_1}`
stats       | DetailedTicketStats                               | a set of several stats on this `Ticket`.

## TicketDates

Name        | Type                                              | Description
------------| --------------------------------------------------| -----------------
created     | [DateTime](#datetime)                             | the date when this `Ticket` was opened.
updated     | [DateTime](#datetime)                             | the date when last update of this `Ticket` occured.
closed      | [DateTime](#datetime)                             | the date when this `Ticket` was closed.

## OpeningTicketPurpose

### Fields

Name            | Type                                              | Description
----------------| --------------------------------------------------| -----------------
callPurpose     | String                                            | the label of the purpose
callPurposeUid: | [Option](#option)[[SafeUUID](#safeuuid)]          | if a referenced `CallPurpose` on Performance Immo was used. (recommended)

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
transmissionTime        | [Option[[Duration](#duration)]](#option) | Calcul du temps de transmission vers un intervenant. <br/> Cette valeur est obtenue en calculant le temps entre la date de création du `Ticket` et l'acceptation d'une mission par un intervenant. <br/> i.e l'évènement `InterventionAccepted`
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
medium      | Array[[ContactMediumView](#contactmediumview)]    | the medium use by the caller to open `Ticket`.
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

### InterventionAccepted

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

## PatrimonyManagersResultView

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
result      | Array[[PatrimonyManagerForPatrimony](#patrimonymanagerforpatrimony)]    | Array of selected `PatrimonyManager`s

## PatrimonyManagerForPatrimony

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
uid         | [SafeUUID](#safeuuid)                             | 
name        | String                                            | 
email       | String                                            | 
phoneNumber | [Option](#option)[String]                         | 
job         | [Option](#option)[String]                         | 

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

## LotUsage

`LotUsage` is an Enum, i.e type can take different values :

```haskell
data LotUsage = Apartment | IndividualHouse | ResidentialParking | ResidentialCellar | ResidentialAnnex |           -- ResidentialUsage
                   Restaurant | MeetingRoom | Fitness | SPA | SportFacility | Pool | PoolHouse | Playground | Laundry | OtherService |      -- ServiceUsage
                   TertiaryParking | Workspace | Workstation | Office | RetailShop | Warehouse | GasStation |                               -- TertiaryUsage
                   BoilerRoom | Elevator | VentilationSystem | Gate | Intercom | BinStorageArea | MachineRoom | GardeningShed | OtherTechnical  -- TechnicalUsage
```

## LotResultView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
result      | Array[[LotQueryView](#lotqueryview)]              | Array of selected `Lot`s

## LotQueryView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
uid         | [SafeUUID](#safeuuid)                             | the uid of the `Lot`
patrimony   | [PatrimonyInfoView](#patrimonyinfoview)           |
addresses   | Array[[LotQueryAddress](#lotqueryaddress)]        | 
ref         | String                                            | a client reference to `Lot`
lotNumber   | String                                            | describe a `Lot` inside a `Patrimony`
usage       | [LotUsage](#lotusage)                             | What kind of `Lot` it is.
_links      | Array[[RestNavigationLink](#restnavigationlink)]  | 

## LotQueryAddress

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
recipientSupplement    | [Option](#option)[[RecipientIdentificationSupplement](#recipientidentificationsupplement)] |
geographicalSupplement | [Option](#option)[[GeographicalIdentificationSupplement](#geographicalidentificationsupplement)] |
state       | [Option](#option)[String]                         |
geoLocation | [Option](#option)[[GeoLocation](#geolocation)]                       |
checker     | [Option](#option)[[AddressChecker](#addresschecker)]                 |
building    | [Option](#option)[[BuildingInfoView](#buildinginfoview)] |
status      | "AddressIsVerified" / "AddressIsNotVerified" / "AddressToCheck" | l'adresses est-elle vérifiée (les champs `geoLocation` et `checker` sont valué) ou non.

## PatrimonyInfoView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
uid         | [SafeUUID](#safeuuid)                             | 
label       | [Option](#option)[String]                         |
ref         | String                                            |

## BuildingInfoView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
uid         | [SafeUUID](#safeuuid)                             | 
label       | String                                            |

## LotDetailQueryView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
uid         | [SafeUUID](#safeuuid)                             | the uid of the `Lot`
patrimony   | [PatrimonyInfoView](#patrimonyinfoview)           |
addresses   | Array[[LotQueryAddress](#lotqueryaddress)]        | 
ref         | String                                            | a client reference to `Lot`
lotNumber   | String                                            | describe a `Lot` inside a `Patrimony`
usage       | [LotUsage](#lotusage)                             | What kind of `Lot` it is.
_links      | Array[[RestNavigationLink](#restnavigationlink)]  |


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
data AddressChecker = GooglePlaceIdChecker | DataGouvAPIIdChecker
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

### DataGouvAPIIdChecker

> DataGouvAPIIdChecker example :

```json
{
	"dataGouvAddressId":"123456hg"
}
```

`DataGouvAPIIdChecker` allow to check `Address`via data.gouv.fr API.

Name          | Type   | Description
--------------| -------| --------------------------------------------------------
dataGouvAddressId | String | identifier to check the `Address` with data.gouv.fr API.

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

## ValidAddress

`ValidAddress` is an Enum, i.e type can take different values :

```haskell
data ValidAddress = RationalAddress | AddressReference
```

### RationalAddress

Name          | Type                        | Description
--------------| ----------------------------| --------------------------------------------------------
uid           | [SafeUUID](#safeuuid)       |
quality       | [Option](#option)[String]   |
number        | [Option](#option)[String]   |
street        | String                      |
complement    | [Option](#option)[String]   |
recipientSupplement | [Option](#option)[[RecipientIdentificationSupplement](#recipientidentificationsupplement)] |
geographicalSupplement | [Option](#option)[[GeographicalIdentificationSupplement](#geographicalidentificationsupplement)] |
zipCode       | String                      |
city          | String                      |
state         | [Option](#option)[String]   |
country       | [Option](#option)[String]   |


### AddressReference

Name          | Type                                | Description
--------------| ------------------------------------| --------------------------------------------------------
uid           | [SafeUUID](#safeuuid)               |
address       | RationalAddress                     | cf. valeur précédente de l'enum
checker       | [AddressChecker](#addresschecker)   |
geoLocation   | [GeoLocation](#geolocation)

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
quality       | [Option](#option)[[NonEmptyString](#nonemptystring)] |
number        | [Option](#option)[[NonEmptyString](#nonemptystring)] | the number of the street. ex: 12 
street        | String                              | ex: avenue de Paris 
complement    | [Option](#option)[[NonEmptyString](#nonemptystring)]           |
zipCode       | String                              | zipCode of this `Address` 
city          | String                              | ex: Paris 
state         | [Option](#option)[[NonEmptyString](#nonemptystring)]           |
country       | [Option](#option)[[NonEmptyString](#nonemptystring)]           | ex: France
geoLocation   | [Option](#option)[[GeoLocation](#geolocation)]         | geolocation of the `Address` (with latitude & longitude value) 
checker       | [Option](#option)[[AddressChecker](#addresschecker)]   | used to identify `Address` across external tools (ex: google place ID)
floor         | [Option](#option)[String]           | 
unit          | [Option](#option)[String]           |
digicode      | [Option](#option)[String]           |
entrance      | [Option](#option)[String]           |
elevator      | [Option](#option)[String]           |
staircase     | [Option](#option)[String]           |

## LotAddressCommand

Name          | Type                                | Description
--------------| ------------------------------------| --------------------------------------------------------
quality       | [Option](#option)[[NonEmptyString](#nonemptystring)]           |
number        | [Option](#option)[[NonEmptyString](#nonemptystring)] | the number of the street. ex: 12
street        | String                              | ex: "avenue de Paris"
complement    | [Option](#option)[[NonEmptyString](#nonemptystring)] |
zipCode       | String                              | zipCode of this `Address`
city          | String                              | ex: Paris
state         | [Option](#option)[[NonEmptyString](#nonemptystring)] |
country       | [Option](#option)[[NonEmptyString](#nonemptystring)] | ex: "France"
recipientSupplement | [Option](#option)[[RecipientIdentificationSupplement](#recipientidentificationsupplement)] |
geographicalSupplement | [Option](#option)[[GeographicalIdentificationSupplement](#geographicalidentificationsupplement)] |
geoLocation   | [Option](#option)[[GeoLocation](#geolocation)]         | geolocation of the `Address` (with latitude & longitude value)
checker       | [Option](#option)[[AddressChecker](#addresschecker)]   | used to identify `Address` across external tools (ex: google place ID)
building      | [Option](#option)[[SafeUUID](#safeuuid)] |

## ProviderContactResultView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
result      | Array[[ProviderContactQueryView](#providercontactqueryview)]  | Array of selected `ProviderContactQueryView`s
_links      | Array[[RestNavigationLink](#restnavigationlink)]  | Array of `RestNavigationLink`. Allow building decoupled navigation workflow.

## ProviderContactQueryView

### Fields

Name            | Type                                                  | Description
----------------| ------------------------------------------------------| --------------------------------------------------
uid             | [SafeUUID](#safeuuid)                                 | the uid of the `ProviderContact`
label           | String                                                | label of the `ProviderContact`
providerCompany | [Option[[ProviderCompanyInContact](#providercompanyincontact)]](#option) | an optional reference to a `ProviderCompany`. <br/> Means this `ProviderContact` is a part of this `ProviderCompany`.
activities      | Array[[ProviderContactActivity](#providercontactactivity)]
phones          | Array[String]                                         | 
fax             | Array[String]                                         | 
emails          | Array[String]                                         | 
active          | Boolean                                               | 
_links          | Array[[RestNavigationLink](#restnavigationlink)]      | Array of `RestNavigationLink`. Allow building decoupled navigation workflow.

## ProviderContactDetailedQueryView

### Fields

Name            | Type                                                  | Description
----------------| ------------------------------------------------------| --------------------------------------------------
uid             | [SafeUUID](#safeuuid)                                 | the uid of the `ProviderContact`
label           | String                                                | label of the `ProviderContact`
providerCompany | [Option[[ProviderCompanyInContact](#providercompanyincontact)]](#option) | an optional reference to a `ProviderCompany`. <br/> Means this `ProviderContact` is a part of this `ProviderCompany`.
activities      | Array[[ProviderContactActivity](#providercontactactivity)] | a `ProviderContact` can perform several activities. e.g some job like plumbing.
patrimonies     | Array[[ItemAbstractWithRef](#itemabstractwithref)]    | a `ProviderContact` is able to intervene on several `Patrimony`.
company         | [ItemAbstract](#itemabstract)                         | a `ProviderContact` is private for a given `ClientCompany`. 
phones          | Array[String]                                         | 
fax             | Array[String]                                         | 
emails          | Array[String]                                         | 
active          | Boolean                                               | 
_links          | Array[[RestNavigationLink](#restnavigationlink)]      | Array of `RestNavigationLink`. Allow building decoupled navigation workflow.

## ProviderCompanyInContact

Name            | Type                                                  | Description
----------------| ------------------------------------------------------| --------------------------------------------------
uid             | [SafeUUID](#safeuuid)                                 | the uid of the `ProviderCompany`
name            | String                                                | name of the `ProviderCompany`
siretNumber     | [SIRET](#siret)                                       | siretNumber of the `ProviderCompany` 
  
## ProviderContactActivity  

Name            | Type                                                  | Description
----------------| ------------------------------------------------------| --------------------------------------------------
activityUid     | [SafeUUID](#safeuuid)                                 | the uid of the `Activity`
includedIncidentTypes | Array[[SafeUUID](#safeuuid)]                    | 

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
interventionDelay           | Array[[DelayStat](#delaystat)]  | Time between [`InterventionAccepted`](#interventionaccepted) & [`InterventionStarted`](#interventionstarted)
missionAcceptedDelay        | Array[[DelayStat](#delaystat)]  | Time between [`CallEmittedTo`](#callemittedto) & [`InterventionAccepted`](#interventionaccepted)
repairDelay                 | Array[[DelayStat](#delaystat)]  | Time between [`InterventionAccepted`](#interventionaccepted) & [`InterventionFinished`](#interventionfinished) or `ClosingTicketEvent`
callBeforeMissionAccepted   | Array[[CountStat](#countstat)]  | Count the number of [`CallEmittedTo`](#callemittedto) before [`InterventionAccepted`](#interventionaccepted)
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

## UserEventResultView

### Fields

Name                        | Type                            | Description
----------------------------| --------------------------------| --------------------------------------------------
events                      | Array[[UserEvent](#userevent)]  | The `Event`s resulting of this `Command`

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

## LotEventResultView

### Fields

Name                        | Type                            | Description
----------------------------| --------------------------------| --------------------------------------------------
events                      | Array[[LotEvent](#lotevent)]    | The `Event`s resulting of this `Command`

## PatrimonyContactEventResultView

Name                        | Type                            | Description
----------------------------| --------------------------------| --------------------------------------------------
events                      | Array[[PatrimonyContactEvent](#patrimonycontactevent)]    | The `Event`s resulting of this `Command`

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
         "callPurposeUid":"62043f05-0e0a-462d-9777-16a152bb291a",
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
callPurposeUid    | [Option](#option)[[SafeUUID](#safeuuid)]          | if a referenced `CallPurpose` on Performance Immo was used. (recommended) 
altCallPurpose    | [Map](#map)[String, Array[String]],               |  
additionalData    | [Map](#map)[String, [Option](#option)[String]]    | some addional data you want to display on the detailed `Ticket` page.

## CallerType

`CallerType` is an Enum, i.e type can take different values : 

```haskell
data CallerType = HumanCaller | AutomatonCaller | ReferencedContactCaller
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

### ReferencedContactCaller

A caller that is already identified as a `PatrimonyContact`.

> ReferencedContactCaller example :

```json
{
    "uid":"d5c48f2f-2bcc-40ff-9a5c-4ba5d33419df",
    "callerType":"ReferencedContactCaller"
}
```

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------
uid         | [SafeUUID](#safeuuid)                             | the unique identifier of the contact 
callerType  | Constant                                          | `"ReferencedContactCaller"`

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

## ContactInfo

`ContactInfo` is an Enum, i.e type can take different values : 

```haskell
data ContactInfo = Phone | Fax | Mail
```

### Phone 

> Phone example :

```json
{
    "phone":"0146305674",
    "contactInfoType":"Phone"
}
```

Name              | Type                                              | Description
------------------| --------------------------------------------------| --------------------------
phone             | String                                            | 
contactInfoType   | Constant                                          | `"Phone"`
                        
### Fax 

> Fax example :

```json
{
    "fax":"0146305674",
    "contactInfoType":"Fax"
}
```

Name              | Type                                              | Description
------------------| --------------------------------------------------| --------------------------
fax               | String                                            | 
contactInfoType   | Constant                                          | `"Fax"`

### Mail 

> Mail example :

```json
{
    "mail":"0146305674",
    "contactInfoType":"Mail"
}
```

Name              | Type                                              | Description
------------------| --------------------------------------------------| --------------------------
mail              | String                                            | 
contactInfoType   | Constant                                          | `"Mail"`

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

## TicketAssignee

A `TicketAssignee` is targeted to resolve issue referenced on the Ticket.

`TicketAssignee` is an Enum, i.e type can take different values : 

```haskell
data TicketAssignee = AnonymousAssignee | ReferencedProviderContact | ReferencedProviderCompany
```

### ReferencedProviderContact

A `ReferencedProviderContact` is a `ProviderContact` that can be identified by its uid on Performance-immo app. 

> ReferencedProviderContact example :

```json
{
    "providerUid":"d5c48f2f-2bcc-40ff-9a5c-4ba5d33419df",
    "assigneeType":"ReferencedProviderContact"
}
```

Name              | Type                                              | Description
------------------| --------------------------------------------------| --------------------------
providerUid       | [SafeUUID](#safeuuid)                             | 
assigneeType      | Constant                                          | `"ReferencedProviderContact"`

### ReferencedProviderCompany

A `ReferencedProviderCompany` is a `ProviderCompany` that can be identified by its uid on Performance-immo app.

> ReferencedProviderCompany example :

```json
{
    "providerUid":"d5c48f2f-2bcc-40ff-9a5c-4ba5d33419df",
    "assigneeType":"ReferencedProviderCompany"
}
```

Name              | Type                                              | Description
------------------| --------------------------------------------------| --------------------------
providerUid       | [SafeUUID](#safeuuid)                             |
assigneeType      | Constant                                          | `"ReferencedProviderCompany"`

### AnonymousAssignee

An `AnonymousAssignee` is a `TicketAssignee` that is not referenced on Performance-immo app.

You should not use this value if you want benefit some of PerfImmo killer features. cf. [ProviderContact](#providercontact).

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
    "assigneeType":"AnonymousAssignee"
}
```

Name              | Type                                              | Description
------------------| --------------------------------------------------| --------------------------
name              | [Name](#name)                                     |  
phones            | Array[String]                                     |  
fax               | Array[String]                                     |  
emails            | Array[String]                                     |  
assigneeType      | Constant                                          | `"AnonymousAssignee"`

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

### LotAddressReference

Name              | Type                                              | Description
------------------| --------------------------------------------------| --------------------------
addressReference  | [AddressReference](#addressreference)             | 
building          | [Option](#option)[[SafeUUID](#safeuuid)]          | 

## PatrimonyContactResultView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
result      | Array[[PatrimonyContactQueryView](#patrimonycontactqueryview)]  | Array of selected `PatrimonyContact`s
_links      | Array[[RestNavigationLink](#restnavigationlink)]  | Array of `RestNavigationLink`. Allow building decoupled navigation workflow.

## PatrimonyContactQueryView

### Fields

Name            | Type                                                  | Description
----------------| ------------------------------------------------------| --------------------------------------------------
uid             | [SafeUUID](#safeuuid)                                 | the uid of the `PatrimonyContact`
name            | [Name](#name)                                         | the name of the `PatrimonyContact`
company         | [Option](#option)[String]                             | an optional company's name of the `PatrimonyContact`
address         | [Option](#option)[[PatrimonyContactAddressReference](#patrimonyaddressreference)] | an optional address for this `PatrimonyContact`  
contacts        | [NonEmptyList](#nonemptylist)[[ContactInfo](#contactinfo)] | a non empty list of contact like phone number or email
linkedWith      | [NonEmptyList](#nonemptylist)[[PatrimonyContactEntityLink](#patrimonycontactentitylink)] | a non empty list of link to several `Patrimony` or `Lot`entity. 
_links          | Array[[RestNavigationLink](#restnavigationlink)]      | Array of `RestNavigationLink`. Allow building decoupled navigation workflow.

## PatrimonyContactEntityLink

`PatrimonyContactEntityLink` is an Enum, i.e type can take different values : 

```haskell
data PatrimonyContactEntityLink = LinkToPatrimonyAsCareTaker | LinkToPatrimonyAsHomeOwnerAssociation | LinkToLotAsTenant | LinkToLotAsOwner | LinkToLotAsLandlord 
```

### LinkToPatrimonyAsCareTaker

> LinkToPatrimonyAsCareTaker example :

```json
{
	"patrimonyUid":"d5c48f2f-2bcc-40ff-9a5c-4ba5d33419df",
    "linkType":"LinkToPatrimonyAsCareTaker"
}
```

Name         | Type                                              | Description
-------------| --------------------------------------------------| --------------------------------------------------
patrimonyUid | [SafeUUID](#safeuuid)                             | 
linkType     | Constant                                          | `"LinkToPatrimonyAsCareTaker"`

### LinkToPatrimonyAsHomeOwnerAssociation

> LinkToPatrimonyAsHomeOwnerAssociation example :

```json
{
	"patrimonyUid":"d5c48f2f-2bcc-40ff-9a5c-4ba5d33419df",
	"position":"Member",
    "linkType":"LinkToPatrimonyAsHomeOwnerAssociation"
}
```

Name         | Type                                              | Description
-------------| --------------------------------------------------| --------------------------------------------------
patrimonyUid | [SafeUUID](#safeuuid)                             | 
position     | [HomeOwnerAssociationPosition](#homeownerassociationposition) | 
linkType     | Constant                                          | `"LinkToPatrimonyAsHomeOwnerAssociation"`

### LinkToLotAsTenant

> LinkToLotAsTenant example :

```json
{
	"lotUid":"d5c48f2f-2bcc-40ff-9a5c-4ba5d33419df",
    "linkType":"LinkToLotAsTenant"
}
```

Name         | Type                                              | Description
-------------| --------------------------------------------------| --------------------------------------------------
lotUid       | [SafeUUID](#safeuuid)                             | 
linkType     | Constant                                          | `"LinkToLotAsTenant"`

### LinkToLotAsOwner

> LinkToLotAsOwner example :

```json
{
	"lotUid":"d5c48f2f-2bcc-40ff-9a5c-4ba5d33419df",
    "linkType":"LinkToLotAsOwner"
}
```

Name         | Type                                              | Description
-------------| --------------------------------------------------| --------------------------------------------------
lotUid       | [SafeUUID](#safeuuid)                             | 
linkType     | Constant                                          | `"LinkToLotAsOwner"`

### LinkToLotAsLandlord

> LinkToLotAsLandlord example :

```json
{
	"lotUid":"d5c48f2f-2bcc-40ff-9a5c-4ba5d33419df",
    "linkType":"LinkToLotAsLandlord"
}
```

Name         | Type                                              | Description
-------------| --------------------------------------------------| --------------------------------------------------
lotUid       | [SafeUUID](#safeuuid)                             | 
linkType     | Constant                                          | `"LinkToLotAsLandlord"`

### LinkToNonReferencedLot

> LinkToNonReferencedLot example :

```json
{
	"patrimonyUid":"d5c48f2f-2bcc-40ff-9a5c-4ba5d33419df",
  "linkType":"LinkToNonReferencedLot",
  "linkedAs":"Owner"
}
```

Name         | Type                                              | Description
-------------| --------------------------------------------------| --------------------------------------------------
lotUid       | [SafeUUID](#safeuuid)                             | 
linkedAs     | [LinkedToNonReferencedLotAs](#linkedtononreferencedlotas) | 
linkType     | Constant                                          | `"LinkToNonReferencedLot"`

You should specify a LinkToNonReferencedLot with a [LinkToPatrimonyAsHomeOwnerAssociation.NonMember](#linktopatrimonyashomeownerassociation).

## HomeOwnerAssociationPosition

`HomeOwnerAssociationPosition` is an Enum, i.e type can take different values : 

`"NonMember"` or `"Member"` or `"President"`

```haskell
data HomeOwnerAssociationPosition = NonMember | Member | President 
```

## LinkedToNonReferencedLotAs

`LinkedToNonReferencedLotAs` is an Enum, i.e type can take different values : 

`"Tenant"` or `"Owner"` or `"Landlord"`

```haskell
data LinkedToNonReferencedLotAs = Tenant | Owner | Landlord 
```

## ProviderContactSuggestResultView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
result      | Array[[ProviderContactSuggestView](#providercontactsuggestview)] | Array of suggested `ProviderContact`s

## ProviderContactSuggestView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------
uid         | [SafeUUID](#safeuuid)                             | uid of the `ProviderContact`
label       | String                                            | the `ProviderContact`'s label
activities  | Array[[ProviderContactActivityView](#providercontactactivityview)] |
isDirectlyLinkedWithPatrimony | Boolean                         | is this `ProviderContact` directly related to the `Patrimony`
phones      | Array[String]                                     |
fax         | Array[String]                                     |
emails      | Array[String]                                     |
active      | Boolean                                           | `true` if the `ProviderContact` is active

## ProviderContactActivityView

### Fields

Name                    | Type                                              | Description
------------------------| --------------------------------------------------| --------------------------
activityUid             | [SafeUUID](#safeuuid)                             | 
includedIncidentTypes   | Array[[SafeUUID](#safeuuid)]                      | 

## InterventionPeriodForCommand

`InterventionPeriodForCommand` is an Enum, i.e type can take different values :

```haskell
data InterventionPeriodForCommand = DateTimePeriod | WeekDaysPeriod | SpecificDaysPeriod
```

### DateTimePeriod

> DateTimePeriod example :

```json
{
    "label":"Ma période",
    "startDate": "2018-02-01T08:00:00.000+01:00",
    "endDate": "2018-11-30T018:00:00.000+02:00",
    "periodType": "DateTimePeriod"
}
```

Name         | Type                                              | Description
-------------| --------------------------------------------------| --------------------------------------------------
label        | [NonEmptyString](#nonemptystring)                 |
startDate    | [DateTime](#datetime)                             |
endDate      | [DateTime](#datetime)                             |
periodType   | Constant                                          | `"DateTimePeriod"`

### WeekDaysPeriod

> WeekDaysPeriod example :

```json
{
    "label":"Ma période",
    "periodRanges": [
        {
            "weekDays":["MONDAY", "TUESDAY", "FRIDAY"],
            "timeSlot":{"timeSlotType":"AllDayLong"}
        }
    ],
    "startDate":"2018-02-01",
    "endDate":"2018-11-30",
    "exclusions":[
        {
            "days":["2018-11-28"],
            "timeSlot":{"timeSlotType":"AllDayLong"}
        }
    ],
    "periodType": "WeekDaysPeriod"
}
```

Name         | Type                                              | Description
-------------| --------------------------------------------------| --------------------------------------------------
label        | [NonEmptyString](#nonemptystring)                 |
startDate    | [Option](#option)[[DateTime](#datetime)]          | When the period validity start. If not start valid from always.
endDate      | [Option](#option)[[DateTime](#datetime)]          | When the period validity end. If not never end, always valid.
periodRanges | [NonEmptyList](#nonemptylist)[[PeriodRange](#periodrange)] | A non empty list of week days period when the ProviderContact is available to intervene.
exclusions   | Array[[ExclusionPeriod](#exclusionperiod)]        | A list (can be empty) of exclusions period allowing to precisly define the ProviderContact availibility.
periodType   | Constant                                          | `"WeekDaysPeriod"`

### SpecificDaysPeriod

> SpecificDaysPeriod example :

```json
{
    "label":"Ma période",
    "days":["2018-11-28", "2018-11-29"],
    "timeSlot":{"timeSlotType":"AllDayLong"},
    "periodType": "SpecificDaysPeriod"
}
```

Name         | Type                                              | Description
-------------| --------------------------------------------------| --------------------------------------------------
label        | [NonEmptyString](#nonemptystring)                 |
days         | [NonEmptyList](#nonemptylist)[[LocalDate](#localdate)] | A non empty list of year days when the ProviderContact is available to intervene.
timeSlot     | [TimeSlot](#timeslot)                             | Define the time slot when ProviderConatct is available. (Can be AllDayLong)
periodType   | Constant                                          | `"SpecificDaysPeriod"`

## TimeSlot

`TimeSlot` is an Enum, i.e type can take different values :

```haskell
data TimeSlot = AllDayLong | HourPeriods
```


### AllDayLong

> AllDayLong example :

```json
{
  "timeSlotType" : "AllDayLong"
}
```

Name         | Type                                              | Description
-------------| --------------------------------------------------| --------------------------------------------------
timeSlotType | Constant                                          | `"AllDayLong"`

### HourPeriods

> HourPeriods example :

```json
{
  "periods" : [
      {
          "start" : "00:00:00",
          "end" : "00:01:00"
      }
  ],
  "timeSlotType" : "HourPeriods"
}
```

Name         | Type                                              | Description
-------------| --------------------------------------------------| --------------------------------------------------
periods      | [NonEmptyList](#nonemptylist)[[HourPeriod](#hourperiod)] |
timeSlotType | Constant                                          | `"HourPeriods"`

## HourPeriod

Name         | Type                                              | Description
-------------| --------------------------------------------------| --------------------------------------------------
start        | [LocalTime](#localtime)                           |
end          | [LocalTime](#localtime)                           |

## PeriodRange

Name         | Type                                              | Description
-------------| --------------------------------------------------| --------------------------------------------------
weekDays     | [NonEmptyList](#nonemptylist)[[WeekDay](#weekday)]  | A non empty list of week day.
timeSlot     | [TimeSlot](#timeslot)                             |

case class PeriodRange(weekDays: NonEmptyList[WeekDay], timeSlot: TimeSlot)

## WeekDay

`TimeSlot` is an Enum, i.e type can take different values :

```haskell
data WeekDay = MONDAY | TUESDAY | WEDNESDAY | THURSDAY | FRIDAY | SATURDAY | SUNDAY
```

## ExclusionPeriod

Name         | Type                                              | Description
-------------| --------------------------------------------------| --------------------------------------------------
days         | [NonEmptyList](#nonemptylist)[[LocalDate](#localdate)] |
timeSlot     | [TimeSlot](#timeslot)                             |

## InterventionPeriod

`InterventionPeriod` is an Enum, i.e type can take different values :

```haskell
data InterventionPeriod = DateTimePeriod | WeekDaysPeriod | SpecificDaysPeriod
```

### DateTimePeriod

> DateTimePeriod example :

```json
{
    "uid":"8c12f096-20e6-11ab-8ff7-2c39b4397040",
    "label":"Ma période",
    "startDate": "2018-02-01T08:00:00.000+01:00",
    "endDate": "2018-11-30T018:00:00.000+02:00",
    "periodType": "DateTimePeriod"
}
```

Name         | Type                                              | Description
-------------| --------------------------------------------------| --------------------------------------------------
uid          | [SafeUUID](#safeuuid)                             |
label        | [NonEmptyString](#nonemptystring)                 |
startDate    | [DateTime](#datetime)                             |
endDate      | [DateTime](#datetime)                             |
periodType   | Constant                                          | `"DateTimePeriod"`

### WeekDaysPeriod

> WeekDaysPeriod example :

```json
{
    "uid":"8c12f096-20e6-11ab-8ff7-2c39b4397040",
    "label":"Ma période",
    "periodRanges": [
        {
            "weekDays":["MONDAY", "TUESDAY", "FRIDAY"],
            "timeSlot":{"timeSlotType":"AllDayLong"}
        }
    ],
    "startDate":"2018-02-01",
    "endDate":"2018-11-30",
    "exclusions":[
        {
            "days":["2018-11-28"],
            "timeSlot":{"timeSlotType":"AllDayLong"}
        }
    ],
    "periodType": "WeekDaysPeriod"
}
```

Name         | Type                                              | Description
-------------| --------------------------------------------------| --------------------------------------------------
uid          | [SafeUUID](#safeuuid)                             |
label        | [NonEmptyString](#nonemptystring)                 |
startDate    | [Option](#option)[[DateTime](#datetime)]          | When the period validity start. If not start valid from always.
endDate      | [Option](#option)[[DateTime](#datetime)]          | When the period validity end. If not never end, always valid.
periodRanges | [NonEmptyList](#nonemptylist)[[PeriodRange](#periodrange)] | A non empty list of week days period when the ProviderContact is available to intervene.
exclusions   | Array[[ExclusionPeriod](#exclusionperiod)]        | A list (can be empty) of exclusions period allowing to precisly define the ProviderContact availibility.
periodType   | Constant                                          | `"WeekDaysPeriod"`

### SpecificDaysPeriod

> SpecificDaysPeriod example :

```json
{
    "uid":"8c12f096-20e6-11ab-8ff7-2c39b4397040",
    "label":"Ma période",
    "days":["2018-11-28", "2018-11-29"],
    "timeSlot":{"timeSlotType":"AllDayLong"},
    "periodType": "SpecificDaysPeriod"
}
```

Name         | Type                                              | Description
-------------| --------------------------------------------------| --------------------------------------------------
uid          | [SafeUUID](#safeuuid)                             |
label        | [NonEmptyString](#nonemptystring)                 |
days         | [NonEmptyList](#nonemptylist)[[LocalDate](#localdate)] | A non empty list of year days when the ProviderContact is available to intervene.
timeSlot     | [TimeSlot](#timeslot)                             | Define the time slot when ProviderConatct is available. (Can be AllDayLong)
periodType   | Constant                                          | `"SpecificDaysPeriod"`

## ProviderContactActivityCmd

Name                  | Type                                              | Description
----------------------| --------------------------------------------------| --------------------------------------------------
activityUidUid        | [SafeUUID](#safeuuid)                             | the uid of the `Activity` assigned to this `ProviderContact`
includedIncidentTypes | Array[[SafeUUID](#safeuuid)]                      | the list of incident type that is managed for this Activity by this `ProviderContact`

## ProviderContractContractor

`ProviderContractContractor` is an Enum, i.e type can take different values :

```haskell
data ProviderContractContractor = PatrimonyContractor
```

### PatrimonyContractor

> PatrimonyContractor example :

```json
{
    "patrimonyUid":"8c12f096-20e6-11ab-8ff7-2c39b4397040",
    "contractorType": "PatrimonyContractor"
}
```

Name             | Type                                              | Description
-----------------| --------------------------------------------------| --------------------------------------------------
patrimonyUid     | [SafeUUID](#safeuuid)                             |
contractorType   | Constant                                          | `"PatrimonyContractor"`

## ContractForProviderContact

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
contractUid         | [SafeUUID](#safeuuid)                                |
label               | [NonEmptyString](#nonemptystring)                    |
contractNumber      | [Option](#option)[[NonEmptyString](#nonemptystring)] |
validityPeriod      | [Option](#option)[[NonEmptyString](#nonemptystring)] |
phoneNumbers        | Array[[PhoneNumber](#phonenumber)]                   |
instructions        | [Option](#option)[[NonEmptyString](#nonemptystring)] |
commentaries        | [Option](#option)[[NonEmptyString](#nonemptystring)] |
activities          | [NonEmptyList](#nonemptylist)[[SafeUUID](#safeuuid)] |
contractor          | [ProviderContractContractor](#providercontractcontractor) | with which entity the `ProviderContact` sign a Contract (ex: with a `Patrimony`)

## AdditionInfosEntityLink

`AdditionInfosEntityLink` is an Enum, i.e type can take different values :

```haskell
data AdditionInfosEntityLink = ProviderContactContract
```

### ProviderContactContract

Link infos with the contract of a `ProviderContact`.

The uid needed is the one from the contract.

> ProviderContactContract example :

```json
{
    "uid":"8c12f096-20e6-11ab-8ff7-2c39b4397040",
    "type": "ProviderContactContract"
}
```

Name             | Type                                              | Description
-----------------| --------------------------------------------------| --------------------------------------------------
uid              | [SafeUUID](#safeuuid)                             | the uid of the contract where you link these additional infos.
type             | Constant                                          | `"ProviderContactContract"`

## SimplifiedRequestResultView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
result      | Array[[SimplifiedRequestSearchView](#simplifiedrequestsearchview)] | Array of selected `SimplifiedRequest`s
aggergations| [SRAggregations](#sraggregations)                 | Aggregations of several params.
_links      | Array[[RestNavigationLink](#restnavigationlink)]  |

## SimplifiedRequestSearchView

### Fields

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
uid                 | [SafeUUID](#safeuuid)                         |
state               | ENUM                                          | `Declared` ou `Seen` ou `Qualified`
ticketUid           | [Option](#option)[[SafeUUID](#safeuuid)]      | if present, a `Ticket` was opened from this `SimplifiedRequest`
category            | [OtpCategory](#otpcategory)                   |
patrimony           | [PatrimonyAbstract](#patrimonyabstract)       |
requestDate         | [DateTime](#datetime)                         |
_links              | Array[[RestNavigationLink](#restnavigationlink)] |

## SimplifiedRequestDetailedView

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
uid                 | [SafeUUID](#safeuuid)                         |
state               | ENUM                                          | `Declared` ou `Seen` ou `Qualified`
category            | [OtpCategory](#otpcategory)                   |
linkedEntities      | [LinkedEntities](#linkedentities)             |
requestDate         | [DateTime](#datetime)                         |
description         | [FormattedText](#formattedtext)[[NonEmptyString](#nonemptystring)] |
requester           | [CallerTicketQueryView](#callerticketqueryview) |
seen                | [Option](#option)[[SimplifiedRequestSeenView](#simplifiedrequestseenview)]             |
qualified           | [Option](#option)[[SimplifiedRequestQualifiedByExpertView](#simplifiedrequestqualifiedbyexpertview)] |
_links              | Array[[RestNavigationLink](#restnavigationlink)] |

## CallerTicketQueryView

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
uid                 | [Option](#option)[[SafeUUID](#safeuuid)]      |
name                | String                                        |
medium              | [Option](#option)[Array[[ContactMediumView](#contactmediumview)] |
comment             | [Option](#option)[String]                     |
category            | [OtpCategory](#otpcategory)                   |
callerInfos         | [CallerInfos](#callerinfos)                   |
status              | [Option](#option)[[NonEmptyString](#nonemptystring)] | description of the caller

## CallerInfos 

`CallerInfos` is an Enum, i.e type can take different values : 

```haskell
data CallerInfos = PatrimonyContactCallerInfos | ClientCompanyUserCallerInfos | NonReferencedCallerInfos
```

### PatrimonyContactCallerInfos

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
linkedWith  | Array[[PatrimonyContactEntityQueryLink](#patrimonycontactentityquerylink)]                                            | 

### ClientCompanyUserCallerInfos

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
companyUid  | [SafeUUID](#safeuuid)                             | 
userType    | [ClientCompanyUserType](#clientcompanyusertype)   | 

### NonReferencedCallerInfos

TODO

## SimplifiedRequestSeenView

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
date        | [DateTime](#datetime)                             | 
personInChargeOf | [UserWhoActOnSimplifiedRequestView](#userwhoactonsimplifiedrequestview)   |

## SimplifiedRequestQualifiedByExpertView

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
ticketUid   | [SafeUUID](#safeuuid)                             | 
qualifier | [UserWhoActOnSimplifiedRequestView](#userwhoactonsimplifiedrequestview)   |
date        | [DateTime](#datetime)                             | 

## PatrimonyContactEntityQueryLink

`PatrimonyContactEntityQueryLink` is an Enum, i.e type can take different values : 

```haskell
data PatrimonyContactEntityQueryLink = LinkToPatrimonyAsCareTaker | LinkToPatrimonyAsHomeOwnerAssociation | LinkToLotAsTenant | LinkToLotAsOwner | LinkToLotAsLandlord | LinkToNonReferencedLot
```

### LinkToPatrimonyAsCareTaker

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
patrimony   | [AbstractEntityWithReference](#abstractentitywithreference) | 
linkType    | Constant                                          | `"LinkToPatrimonyAsCareTaker"`

### LinkToPatrimonyAsHomeOwnerAssociation

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
patrimony   | [AbstractEntityWithReference](#abstractentitywithreference) | 
position    | [HomeOwnerAssociationPosition](#homeownerassociationposition) | 
linkType    | Constant                                          | `"LinkToPatrimonyAsHomeOwnerAssociation"`

### LinkToLotAsTenant

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
lot         | [AbstractEntityWithReference](#abstractentitywithreference) | 
patrimony   | [AbstractEntityWithOnlyUid](#abstractentitywithonlyuid) | 
linkType    | Constant                                          | `"LinkToLotAsTenant"`

### LinkToLotAsOwner

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
lot         | [AbstractEntityWithReference](#abstractentitywithreference) | 
patrimony   | [AbstractEntityWithOnlyUid](#abstractentitywithonlyuid) | 
linkType    | Constant                                          | `"LinkToLotAsOwner"`

### LinkToLotAsLandlord

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
lot         | [AbstractEntityWithReference](#abstractentitywithreference) | 
patrimony   | [AbstractEntityWithOnlyUid](#abstractentitywithonlyuid) | 
linkType    | Constant                                          | `"LinkToLotAsLandlord"`

### LinkToNonReferencedLot

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
patrimony   | [AbstractEntityWithReference](#abstractentitywithreference) | 
linkedAs    | [LinkedToNonReferencedLotAs](#linkedtononreferencedlotas) | 
linkType    | Constant                                          | `"LinkToLotAsLandlord"`		
		
## AbstractEntityWithReference

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
uid         | [SafeUUID](#safeuuid)                             | 
ref         | String                                            | 
label       | [Option](#option)[String]                         |

## AbstractEntityWithOnlyUid

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------------------------------
uid         | [SafeUUID](#safeuuid)                             |

## UserWhoActOnSimplifiedRequestView

TODO

## ClientCompanyUserType

TODO

## LinkedToNonReferencedLotAs
 TODO

## SRAggregations

Name            | Type                                              | Description
----------------| --------------------------------------------------| -----------------
patrimonies     | Array[[Aggreg ation](#aggregation)]                | 
states          | Array[[Aggregation](#aggregation)]                |

## OtpCategory

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
uid                 | [SafeUUID](#safeuuid)                         |
label               | [NonEmptyString](#nonemptystring)             |
iconId              | [NonEmptyString](#nonemptystring)             |

## LinkedEntities

Name                | Type                                          | Description
------------------- | ----------------------------------------------| --------------------------------------------------
patrimony           | [PatrimonyAbstract](#patrimonyabstract)       |
company             | [ClientCompanyAbstract](#clientcompanyabstract) |
holdingUid          | [Option](#option)[[SafeUUID](#safeuuid)]      |
agencies            | Array[[AgencyAbstract](#agencyabstract)]      |
callCenters         | Array[[SafeUUID](#safeuuid)]                  |
