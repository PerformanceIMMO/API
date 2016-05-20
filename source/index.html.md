---
title: Performance Immo API Reference

language_tabs:
  - shell
  - ruby
  - python

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Bienvenue dans la documentation des APIs de Performance Immo ! 

Performance immo a fait le choix technique d'utiliser des API basées sur le protocole HTTP pour communiquer avec 
ses différents partenaires.

Cette document s'organise principalement autour de deux axes :
 
 * [Un axe architectural](#architecture-des-api)
 * [Un axe métier](#ressources-m-tier)

La documentation est en cours de construction, donc s'il vous manque des informations ou que certaines choses ne sont 
pas clairs, n'hésitez pas à nous contacter, nous nous ferons un plaisir de vous répondre. 

Si vous trouvez dans la documentation des manques ou des erreurs, nous vous remercions d'avance de nous les communiquer 
pour que nous puissions les corriger le plus rapidement possible.

## Host des API

Le **`host`** (ou base url) des API est spécifique à chaque client de Performance Immo.

Pour connaitre votre host spécifique, addressez-vous à votre contact technique (sur votre fil slack de préférence).

Toutes les API de Performance Immo sont uniquement accessible via **`https`**, garantissant un niveau minimum de sécurité 
et de confidentialité.

Dans toute la suite du document, nous ne préciserons que les path spécifiques à chaque action, sans rappeler 
à chaque fois le protocole ou le host **`https://monapi.com`**. 
Pensez-bien de votre côté à toujours rajouter ces informations dans vos requêtes.

Chaque requête http; autre que `GET`; requiert l'envoi de json. N'oubliez pas de spécifier le header 
**`Content-Type: application/json`** dans chacune de vos requêtes.

# Architecture des API

Ces API sont divisées en 3 catégories :

* [API évènementielle d'écriture](#apis-v-nementielle-d-39-criture)
* [API REST de lecture](#apis-de-lecture)
* API de notifications (en construction)

# Ressources métier

Les différentes ressources métier se retrouvent dans les différentes catégories d'API décrites ci-dessus.

Cependant, à la différences d'API REST "classique" le format de représentation de ces entités sera très différent 
d'une catégorie d'API à l'autre.

## Company

## ProviderContact

## Tickets

## Patrimony

## Lots

## User

# Authentication

> To authorize, use this code:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# APIs de lecture

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

# APIs évènementielle d'écriture

## Présentation

Ainsi nous fournissons plusieurs API pour que nos partenaires puissent nous envoyer les informations nécessaire au fonctionnement de la plateforme avec leurs données clientes.

Aujourd'hui il existe 3 principales entités qui correspondent à 3 API :

    Pour renseigner les Companies (les comptes clients et leur agences) /api/vEvent/companies
    Pour renseigner les contacts de fournisseur de service /api/vEvent/providerContacts
    Pour renseigner les Tickets (ou dossiers) relatifs à un suivi de problème sur un patrimoine /api/vEvent/tickets

Précédemment, nous vous avons aprlé d'API évènementielle. Qu'est-ce que cela implique ?

Au lieu de nous transmettre l'état des différentes entités (company, providerContact, ticket, ...), nous vous fournissons une interface mettant à disposition une liste d'évènements (ex: TicketOpened), associées à une entité donnée, vous permettant de nous envoyer un incrément de cet état.
Pour expliquer cela autrement, la communication des données concernant une entité passe par la description d'une cause (un évènement) à un changement, plutôt que juste le changement lui-même.

Nous vous fournissons, plus bas dans ce document, la liste des évènements (ainsi que le format de données pour chacun d'entre eux) pour chaque entités.