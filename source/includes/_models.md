# Models

## Option

Means that filed is optional. If parameter has no value, it is not present in the json payload.

<aside class="warning">
	<code> { "field1":"toto", field2:"" } is not equivalent to { "field1":"toto" } </code>
</aside>

## NonEmptyList

An json `array`that can't be empty.

## SafeUUID

Identifiant garanti unique en utilisant la norme [GUUID](https://fr.wikipedia.org/wiki/Globally_Unique_Identifier)    

S'exprime sous forme de chaîne de caractères avec une contrainte sur le format.

ex: `8074964f-c633-3c2a-055f-bbaf8ca8181b`

## CompanyQueryView

### Fields

Name        | Type                                              | Description
------------| --------------------------------------------------| --------------------------
uid         | [SafeUUID](#safeuuid)                             | id of the `Company`
label       | String                                            | the `Company`'s label
isActive    | Boolean                                           | `true` if the `Company` is active
holding     | [Option](#option)[HoldingQueryView](#holdingqueryview)       | a reference to `Company`'s holding if has it
companyType | String                                            | enum : `"CallCenter"` or `"ClientAccountHolding"` or `"ClientAccount"`

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

## HoldingQueryView 

Name        | Type                                              | Mandatory | Description
------------| --------------------------------------------------| ----------| -----------------
uid         | [SafeUUID](#safeuuid)                             | true      | the holding's uid
label       | String                                            | true      | the holding's label

## CompanyUserQueryView

Name        | Type                                              | Mandatory | Description
------------| --------------------------------------------------| ----------| -----------------
uid         | [SafeUUID](#safeuuid)                             | true      | the `Company`'s uid
label       | String                                            | true      | the `Company`'s label

## AgencyUserQueryView

Name        | Type                                              | Mandatory | Description
------------| --------------------------------------------------| ----------| -----------------
uid         | [SafeUUID](#safeuuid)                             | true      | the `Agency`'s uid
label       | String                                            | true      | the `Agency`'s label
