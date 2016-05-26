# ProviderContacts

<aside class="warning">
	You must be authenticated to use these API.
</aside>

## Create ProviderContact

POST         /api/vEvent/providerContacts                                   cqrs.commands.application.controllers.ProvidersContactCommandAPI.create

case class AddProviderContact(processUid: SafeUUID,
                              aggregateUid: SafeUUID,
                              date: DateTime,
                              name: Name,
                              phones: List[String],
                              fax: List[String],
                              emails: List[String],
                              sentDate: DateTime) extends ProviderContactCommand

## Increment ProviderContact State

PATCH        /api/vEvent/providerContacts/:aggregateUid                     cqrs.commands.application.controllers.ProvidersContactCommandAPI.increment(aggregateUid: String)

case class UpdateProviderContact(processUid: SafeUUID,
                                 aggregateUid: SafeUUID,
                                 name: Name,
                                 phones: List[String],
                                 fax: List[String],
                                 emails: List[String],
                                 date: DateTime,
                                 sentDate: DateTime) extends OtherProviderContactCommand

case class DisableProviderContact(processUid: SafeUUID,
                                  aggregateUid: SafeUUID,
                                  date: DateTime,
                                  sentDate: DateTime) extends OtherProviderContactCommand

case class EnableProviderContact(processUid: SafeUUID,
                                 aggregateUid: SafeUUID,
                                 date: DateTime,
                                 sentDate: DateTime) extends OtherProviderContactCommand