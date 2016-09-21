# Event Errors

## CompanyEventError

Name               | Type   | Description
-------------------| -------| --------------------------------------------------
errorType          | Enum   | code describing the type of the error
message            | String | a message describing the error  

### CompanyGenericError

<aside class="warning"> Will be removed soon </aside>

### CommandAlreadySent 

The `Command` have been already sent & computed, i.e an existing `Event` already have the same `processUid` & `aggregateUid` 

### ImpossibleToCreateExistingCompany

The `Company` already exist.

### ImpossibleToPerfomCommandOnNonExistingCompany

The `Command` reference a `Company` that don't exist in database.

### ImpossibleToCreateExistingAgency

The `Agency` already exist.

### ImpossibleToPerformCommandOnNonExistingAgency

The `Command` reference a `Agency` that don't exist in database.

### ImpossibleToCancelCanceledCompany

This `Company` is laready Canceled.

### ImpossibleToCancelCallCenter

It is not allowed to cancel a `CallCenter`.

### ImpossibleToCreateAgencyInAnotherCompanyThatClientAccount

You can only create `Agency` in `ClientAccount`.

## PatrimonyEventError

Name               | Type   | Description
-------------------| -------| --------------------------------------------------
errorType          | Enum   | code describing the type of the error
message            | String | a message describing the error

### PatrimonyGenericError

<aside class="warning"> Will be removed soon </aside>

### CommandAlreadySent

The `Command` have been already sent & computed, i.e an existing `Event` already have the same `processUid` & `aggregateUid`

### ImpossibleToCreateExistingPatrimony

### ImpossibleToPerformCommandOnNonExistingPatrimony

### ImpossibleToReferenceAlreadyExistingBuilding

### ImpossibleToAddAlreadyExistingComplementaryAddressToPatrimony

### ImpossibleToRemoveNonExistingComplementaryAddressFromPatrimony

### ImpossibleToAssociatePatrimonyInAgencyForAlreadyAssociatedAgency

### ImpossibleToDissociatePatrimonyFromAgencyThatDoesntExist

### ImpossibleToDissociatePatrimonyFromAgencyRemainOnlyOneAgency

## ProviderContactEventError

Name               | Type   | Description
-------------------| -------| --------------------------------------------------
errorType          | Enum   | code describing the type of the error
message            | String | a message describing the error

### CommandAlreadySent 

The `Command` have been already sent & computed, i.e an existing `Event` already have the same `processUid` & `aggregateUid`

### ImpossibleToAddExistingProviderContact

### ImpossibleToPerfomCommandOnNonExistingProviderContactCommand

### ImpossibleToAssociateToAgencyThatIsAlreadyAssociated

## TicketEventError

