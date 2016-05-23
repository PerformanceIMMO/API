# Companies

## Get all Companies

### HTTP Request

**`GET`** `/api/v1/companies`

### Parameters

Name            | In    | Type                          | Default   | Description
--------------- | ------| ------------------------------| ----------| -------------
range           | query | String                        | 0-100     | range selector for result pagination ex: `range=0-19` (starRange should be > endRange)
holdinguid      | query | Option[[SafeUUID](#safeuuid)] | None      | uid of ClientAccountHolding. If this param is setted, return ClientAccountHolding's subsidiairies list. **This param is incompatible with `companytype`.**
companytype     | query | Option[String]                | None      | If this param is setted, return CallCenter's list. **This param is incompatible with `holdinguid`.**

### Responses

Http code | Type                        | Description
----------| ----------------------------| ----------------------------
200       | Array[[CompanyQueryView](#companyqueryview)]    | All resources's elements are returned.
206       | Array[[CompanyQueryView](#companyqueryview)]    | Partial Content. See `Content-Range` header for use pagination.
400       | Error                                           | Bad request, occurs most often when parameters passed are invalid.

## Get a specific Company

### HTTP Request

**`GET`** `/api/v1/companies/:company_uid`

### Parameters

Name            | In    | Type                          | Default   | Description
--------------- | ------| ------------------------------| ----------| -------------
company_uid     | path  | [SafeUUID](#safeuuid)         |           | uid of the requested `Company`

### Responses

Http code | Type                | Description
----------| --------------------| ----------------------------
200       | [CompanyQueryView](#companyqueryview)   | The `Company` requested 
400       | Error                                   | Bad request, occurs most often when parameters passed are invalid.

## Get Agencies of a Company

**`GET`** `/api/v1/companies/:company_uid/agencies`

cqrs.queries.application.controllers.CompaniesQueryAPI.agencies(range: Option[String], uid: SafeUUID)

## Get Users of a Company

**`GET`** `/api/v1/companies/:company_uid/users`

cqrs.queries.application.controllers.CompaniesQueryAPI.companyUsers(range: Option[String], companyUid: SafeUUID)

## Get subsidiaries of a Company

**`GET`** `/api/v1/companies/:company_uid/subsidiaries`

cqrs.queries.application.controllers.CompaniesQueryAPI.subsidiaries(range: Option[String], companyUid: SafeUUID)

## Create Company

## Increment Company

