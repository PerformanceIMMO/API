# Events

## ProviderContactEvent

### ProviderContactAdded

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

### ProviderContactDissociatedFromAgency

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

```json
{
    "processUid":"8c12f096-20e6-11ab-8ff7-2c39b4397040",
    "aggregateUid":"7634c414-8822-e29d-fe2b-0a18b3174369",
    "date":"2016-02-29T12:05:32+02:00",
    "sentDate":"2016-02-29T12:05:32+02:00",
    "eventType":"ProviderContactEnabled"
}
```
