# Users

There are different type of Users in the PerfImmo application.
These different type is made to answer to different situation compared to Client entities

- ClientAccountManager

An admin user account to manage all the stuff of a `ClientCompany`.

- Executive

An user in charge of manage one or several `Agencies`.

- PatrimonyManager

An user in charge of manage several `Patrimonies`

## Reference User

> HTTP command example :

```shell
curl -XPOST \
-H "Cookie: PI_SESSION=..." \
-H "Content-Type: application/json" \
-d {
 "processUid":"8c12f096-20e6-11ab-8ff7-2c39b4397040",
 "login":"monlogin@perfimmo.com"
 "firstName":"John",
 "lastName":"Doe",
 "companyUid":"6ed010a1-7481-4b38-87da-c219fc31ba64",
 "managedAgencies": ["16fc6e5e-163d-799c-89ef-a764f2090d74"],
 "commandType":"ReferenceExecutive"
} \
https://base_url/api/vEvent/users
```

> HTTP response example :

```http
HTTP/1.1 201 Created
```
```json
{
    "events":[
        {
            "processUid":"8c12f096-20e6-11ab-8ff7-2c39b4397040",
            "aggregateUid":"7634c414-8822-e29d-fe2b-0a18b3174369",
            "sentDate":"2016-02-29T12:05:32+02:00",
            "login":"monlogin@perfimmo.com",
            "firstName":"John",
            "lastName":"Doe",
            "companyUid":"6ed010a1-7481-4b38-87da-c219fc31ba64",
            "managedAgencies": ["16fc6e5e-163d-799c-89ef-a764f2090d74"],
            "eventType":"ExecutiveReferenced"
        }
    ]
}
```

**`POST`** `/api/vEvent/users`

### Parameters

Name            | In    | Type                                                  | Default   | Description
--------------- | ------| ------------------------------------------------------| ----------| -------------
                | body  | [ReferenceUserCommand](#referenceusercommand)         |           |


### Responses

Http code | Type                                                              | Description
----------| ------------------------------------------------------------------| ----------------------------
201       | [UserEventResultView](#usereventresultview)                       | The `Event`s resulting of this `Command`
400       | [UserEventError](#usereventerror)                                 | Bad request, occurs most often when parameters passed are invalid, or if data in command is not coherent.

## Increment User state

**`PATCH`** `/api/vEvent/users/user_uid`

### Parameters

Name            | In    | Type                                                  | Default   | Description
--------------- | ------| ------------------------------------------------------| ----------| -------------
                | body  | [IncrementUserCommand](#incrementusercommand)         |           |


### Responses

Http code | Type                                                              | Description
----------| ------------------------------------------------------------------| ----------------------------
200       | [UserEventResultView](#usereventresultview)                       | The `Event`s resulting of this `Command`
400       | [UserEventError](#usereventerror)                                 | Bad request, occurs most often when parameters passed are invalid, or if data in command is not coherent.