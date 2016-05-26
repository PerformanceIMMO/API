---
title: Performance Immo API Reference

language_tabs:
  - shell

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - companies
  - providerContacts
  - tickets
  - patrimonies
  - lots
  - operators
  - users
  - models
  - errors

search: true
---

# Introduction

Bienvenue dans la documentation des APIs de Performance Immo ! 

Performance immo a fait le choix technique d'utiliser des API basées sur le protocole HTTP pour communiquer avec 
ses différents partenaires.

Cette documentation s'organise principalement autour de deux axes :
 
 * [Un axe architectural](#architecture-des-api)
 * [Un axe métier](#ressources-m-tier)
 
Chaque type d'API définiera le format qu'il gère pour chaque ressource métier.

La documentation est en cours de construction, donc s'il vous manque des informations ou que certaines choses ne sont 
pas clairs, n'hésitez pas à nous contacter, nous nous ferons un plaisir de vous répondre. 

Si vous trouvez des manques ou des erreurs, nous vous remercions d'avance de nous les communiquer 
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

## Encoding

Le seul enconding accepté pour utiliser les API est `utf-8`.

Faites bien attention à transmettre les données avec cet encoding si vous ne voulez pas avoir de mauvaises surprises.

## Range

> Request example

```http
HTTP/1.1 206 Partial Content
Content-Range: 0-10/256
Accept-Range: 100
```
```http
HTTP/1.1 200 OK
Content-Range: 0-9/10
Accept-Range: 100
```

`range=0-10` is a query parameter that is available in several query API, for collection resources.
It allow to paginate requests.

It is a formatted String that is composed by 3 elements :

* startIndex (start from 0)
* a separator `-`
* endIndex (start from 0)

`startIndex` should be >= `endIndex`.

The request answer by :

* `200 OK` - All the elements of the resources are returned.
* `206 Partial Content` - Only a part of the resources are returned. 

To know what part of the collection is sent, See `Content-Range` header response.

`Content-Range offset – limit / count`
        
* offset : index of the first element returned by the request.
* limit : index of the last element returned by the request.
* count : number of element in the entire collection.

cf. [pagination the doc](http://blog.octo.com/designer-une-api-rest/#pagination) for more explanation.


# Architecture des API

Ces API sont divisées en 3 catégories :

* [API évènementielle d'écriture](#apis-v-nementielle-d-39-criture)
* [API REST de lecture](#apis-de-lecture)
* API de notifications (en construction)

# Ressources métier

Les différentes ressources métier se retrouvent dans les différentes catégories d'API décrites ci-dessus.

Cependant, à la différences d'API REST "classique" le format de représentation de ces entités sera très différent 
d'une catégorie d'API à l'autre.

Dans cette partie, nous définissons la signification métier de chaque ressource. Pour une description concrète de 
ces ressources, reportez-vous aux API spécifiques les concerant. 

## Company

Une `Company` représente une entreprise présente sur la plateforme Performance Immo.

Elle peut prendre 3 formes :

* CallCenter
* ClientAccountHolding
* ClientAccount

### CallCenter

Un `CallCenter` représente un centre d'appel, qui ouvre des tickets. Chaque entité `Company` autre que `CallCenter 
doit possèder une référence vers un `CallCenter`.

### ClientAccountHolding

Un `ClientAccountHolding`représente une entreprise qui possède des filiales, représentées par des `ClientAccount`.

Il doit référencer un `CallCenter`.

### ClientAccount

Un `ClientAccount` représente la structure qui gère un patrimoine immobilier.

Il doit référencer un `CallCenter`et peut référencer un `ClientAccountHolding`.

Il est componser de une ou plusieurs `Agency`, qui elles représentent un groupement (géographique ou autre) permettant 
la ségrégation d'informations sur Performance Immo. Par exemple, pour restreindre l'accès 
à certains `Ticket` ou à un certain `Patrimony`.

## ProviderContact

Un `ProviderContact` est un contact qui a possiblement à intervenir sur un incident.

Si vous souhaitez bénéficier des informations fournisseurs sur la plateforme, de statistiques, vous devez les référencer 
via les API d'écriture.

## Ticket

Un `Ticket` est une déclaration d'incident. Il permet de suivre l'évolution du traitement de cet incident, 
de sa découverte jusqu'à sa résolution.
 
Il contient plusieurs informations, statistiques sur le déroulement de la résolution de l'incident, 
représenté notament par un journal d'évènement. 

## Patrimony

`Patrimony` représente le patrimoine géré par les gestionnaires d'un `ClientAccount`.

`Patrimony` est relié à une ou plusieurs `Agency` d'un `ClientAccount`

## Lot

`Lot` représente un lot immobiliier physique (un appartement, une maison individuelle, un parking, ...)/

`Lot` est relié à un `Patrimony`.

## Operator

`Operator` resprésente un acteur agissant sur le `Ticket`. Par exemple un opérateur répondant au téléphone 
et saisissant uen ouverture de `Ticket`.

Si vous souhaitez bénéficier des informations `Operator` sur la plateforme, de statistiques, vous devez les référencer 
via les API d'écriture.

## User

`User` représente un utilisateur de la plateforme Performance Immo.

Il existe plusieurs types de `User` :

* CallCenterUser - cadre de centre d'appel. Il est relié à un `CallCenter`. Il peut gérer tout ce qui est lié à ce `CallCenter` (`ClientAccount`, `Ticket`, etc...)
* ClientAccountManager - cadre de compte Client. Il est relié à un `ClientAccount`. Il peut gérer tout ce qui est lié à ce `ClientAccount` (`Ticket`, `Patrimony`, etc...)
* Executive - Cadre d'agence. Il est relié à une ou plusieurs `Agency` et à un `ClientAccount`. Il peut gérer tout ce qui est lié avec ses agences (`Ticket`, `Patrimony`, etc...)

# Authentification

L'existence de 2 types d'API distincte (évènementielle en écriture et REST en lecture) qui implique deux systèmes d'authentification.
 
<aside class="notice">
Ce système à 2 authentifications suivant l'API sera prochainement supprimé.
</aside> 

## API évènementielle

> To login, use this code:

```shell
curl -XPOST \ 
> -H "Content-Type: application/json" \
> -d '{"login":my_api_login, "password":my_api_password}' \
> https://my_base_uri/api/vEvent/login
```

> Response example :

```http
HTTP/1.1 200 OK
Cookie: PI_SESSION=dqsmùlkdqsùmlkdsùmlkdqùsmlkdùmqslkdùmqsLkd
```

> In your next request add :

```shell
curl -H "Cookie: PI_SESSION=dqsmùlkdqsùmlkdsùmlkdqùsmlkdùmqslkdùmqsLkd" \
> ...
```

### HTTP Request

`POST /api/vEvent/login`

### Parameters

Name | In | Type | Description
-------------- | -------------- | -------------- | ------------
login | body | String | 
password | body | String | 

### Responses

Http code | Type | Description
----------| ------| -----------
200       | Empty | Retourne le cookie de session `PI_SESSION` dans le header de la réponse
400       | Error | Bad request, occurs most often when parameters passed are invalid or if User not found


Rajouter le header `Cookie: PI_SESSION=value_returned_by_server` dans les prochaines requêtes pour être authentifié.

<aside class="notice">
Les API évènementielles de performance immo sont accessible uniquement à des utilisateurs authentifiés. 
</aside>

<aside class="notice">
La session a par défaut une durée de vie de 12 h (il faut donc prévoir un mécanisme de reconnexion), 
et un idleTime de 1h (= si pas d'activité pendant 1h, la session expire).
</aside>

## API REST

> To login, use this code:

```shell
curl -XPOST \ 
> --header "Content-Type: application/json" \
> -d '{"login":my_api_login, "password":my_api_password}' \
> https://my_base_uri/api/v1/login
```

> In your next request add

```shell
curl --header "Content-Type: application/json" \
> ...
```

### HTTP Request

`POST /api/v1/login`

### Parameters

Name | In | Type | Description
-------------- | -------------- | -------------- | ------------
login | body | String | 
password | body | String | 

### Responses

Http code | Type | Description
----------| ------| -----------
200       | Empty | Retourne le cookie de session `PI_SESSION` dans le header de la réponse
400       | Error | Bad request, occurs most often when parameters passed are invalid or if User not found


Rajouter le header `Cookie: PI_SESSION=value_returned_by_server` dans les prochaines requêtes pour être authentifié.

<aside class="notice">
Les API évènementielles de performance immo sont accessible uniquement à des utilisateurs authentifiés. 
</aside>

<aside class="notice">
La session a par défaut une durée de vie de 12 h (il faut donc prévoir un mécanisme de reconnexion), 
et un idleTime de 1h (= si pas d'activité pendant 1h, la session expire).
</aside>

# APIs évènementielle d'écriture

## Présentation

L'utilisation d'une API évènementielle implique qu'au lieu de nous transmettre l'état des différentes entités 
(`Company`, `ProviderContact`, `Ticket`, ...), nous vous fournissons une interface mettant à disposition une liste 
d'évènements (ex: `TicketOpened`), associées à une entité donnée, vous permettant de nous envoyer un incrément de cet état.

Pour expliquer cela autrement, la communication des données concernant une entité passe par la description 
d'une cause (un évènement) à un changement, plutôt que juste le changement lui-même.

Nous vous fournissons, plus bas dans ce document, la liste des évènements 
(ainsi que le format de données pour chacun d'entre eux) pour chaque entités.

