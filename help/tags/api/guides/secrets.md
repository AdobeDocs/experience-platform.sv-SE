---
title: Hemligheter i reaktors-API
description: Lär dig grunderna i hur du konfigurerar hemligheter i Reaktors API för användning vid vidarebefordran av händelser.
exl-id: 0298c0cd-9fba-4b54-86db-5d2d8f9ade54
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '1202'
ht-degree: 0%

---

# Hemligheter i reaktors-API

I Reaktors-API är en hemlighet en resurs som representerar autentiseringsuppgifter. Hemligheter används vid vidarebefordran av händelser för att autentisera till ett annat system för säkert datautbyte. Det innebär att hemligheter bara kan skapas i egenskaper för händelsevidarebefordran (egenskaper vars `platform`-attribut är inställt på `edge`).

Det finns för närvarande tre hemliga typer som stöds angivna i attributet `type_of`:

| Hemlig typ | Beskrivning |
| --- | --- |
| `token` | En enda teckensträng som representerar ett autentiseringstokenvärde som är känt och begripligt för båda systemen. |
| `simple-http` | Innehåller två strängattribut för ett användarnamn respektive ett lösenord. |
| `oauth2-client_credentials` | Innehåller flera attribut som stöder autentiseringsspecifikationen [OAuth](https://datatracker.ietf.org/doc/html/rfc6749). Vidarebefordran av händelser ber dig om den information som krävs och hanterar sedan förnyelsen av dessa token för dig inom ett angivet intervall. |

{style="table-layout:auto"}

Den här guiden ger en översikt på hög nivå över hur du konfigurerar hemligheter för användning vid vidarebefordran av händelser. Detaljerad vägledning om hur du hanterar hemligheter i Reaktors-API:t, inklusive exempel-JSON för en hemals struktur, finns i [Slutpunktshandboken för hemligheter](../endpoints/secrets.md).

## Referenser

Varje hemlighet innehåller ett `credentials`-attribut som innehåller sina respektive autentiseringsvärden. När [skapar en hemlighet i API](../endpoints/secrets.md#create) har varje typ av hemlighet olika obligatoriska attribut som visas i avsnitten nedan:

* [&quot;token&quot;](#token)
* [`simple-http`](#simple-http)
* [`oauth2-client_credentials`](#oauth2-client_credentials)
* [`oauth2-google`](#oauth2-google)

### `token` {#token}

För hemligheter med värdet `type_of` på `token` krävs endast ett attribut under `credentials`:

| Attribut för autentiseringsuppgifter | Datatyp | Beskrivning |
| --- | --- | --- |
| `token` | Sträng | En hemlig token som förstås av målsystemet. |

{style="table-layout:auto"}

Token lagras som ett statiskt värde och därför ställs hemlighetens `expires_at`- och `refresh_at`-egenskaper in på `null` när hemligheten skapas.

### `simple-http` {#simple-http}

För hemligheter med värdet `type_of` `simple-http` krävs följande attribut under `credentials`:

| Attribut för autentiseringsuppgifter | Datatyp | Beskrivning |
| --- | --- | --- |
| `username` | Sträng | Ett användarnamn. |
| `password` | Sträng | Ett lösenord. Det här värdet ingår inte i API-svaret. |

{style="table-layout:auto"}

När hemligheten skapas byts de två attributen ut med BASE64-kodningen `username:password`. Efter utbytet ställs hemlighetens `expires_at`- och `refresh_at`-egenskaper in på `null`.

### `oauth2-client_credentials` {#oauth2-client_credentials}

För hemligheter med värdet `type_of` `oauth2-client_credentials` krävs följande attribut under `credentials`:

| Attribut för autentiseringsuppgifter | Datatyp | Beskrivning |
| --- | --- | --- |
| `client_id` | Sträng | Klient-ID för OAuth-integreringen. |
| `client_secret` | Sträng | Klienthemligheten för OAuth-integreringen. Det här värdet ingår inte i API-svaret. |
| `token_url` | Sträng | Auktoriserings-URL:en för OAuth-integreringen. |
| `refresh_offset` | Heltal | *(Valfritt)* Värdet i sekunder som uppdateringsåtgärden ska förskjutas med. Om det här attributet utelämnas när hemligheten skapas ställs värdet in på `14400` (fyra timmar) som standard. |
| `options` | Objekt | *(Valfritt)* Anger ytterligare alternativ för OAuth-integrering:<ul><li>`scope`: En sträng som representerar [ OAuth 2.0-omfånget ](https://oauth.net/2/scope/) för autentiseringsuppgifterna.</li><li>`audience`: En sträng som representerar en [Auth0-åtkomsttoken](https://auth0.com/docs/protocols/protocol-oauth2).</li></ul> |

När en `oauth2-client_credentials`-hemlighet skapas eller uppdateras, byts `client_id` och `client_secret` (och eventuellt `options`) ut i en POST till `token_url`, enligt klientautentiseringsflödet i OAuth-protokollet.

>[!NOTE]
>
>Svarstexten för auktoriseringstjänsten förväntas vara kompatibel med OAuth-protokollet.

Om auktoriseringstjänsten svarar med `200 OK` och en JSON-svarstext, tolkas brödtexten och `access_token` skickas till kantmiljön och `expires_in` används för att beräkna attributen `expires_at` och `refresh_at` för hemligheten. Om det inte finns någon miljöassociation för hemligheten, ignoreras `access_token`.

Ett utbyte av autentiseringsuppgifter anses vara lyckat under följande förhållanden:

* `expires_in` är större än `28800` (åtta timmar).
* `refresh_offset` är mindre än värdet `expires_in` minus `14400` (fyra timmar). Om `expires_in` till exempel är `36000` (tio timmar) och `refresh_offset` är `28800` (åtta timmar), anses utbytet vara misslyckat eftersom `28800` är större än `36000` - `14400` (`21600`).

Om utbytet lyckas anges hemmens statusattribut till `succeeded` och värdena för `expires_at` och `refresh_at` anges:

* `expires_at` är den aktuella UTC-tiden plus värdet `expires_in`.
* `refresh_at` är den aktuella UTC-tiden plus värdet `expires_in` minus värdet `refresh_offset`. Om `expires_in` till exempel är `43200` (tolv timmar) och `refresh_offset` är `14400` (fyra timmar), kommer egenskapen `refresh_at` att anges till `28800` (åtta timmar) efter den aktuella UTC-tiden.

Om utbytet misslyckas av någon anledning uppdateras attributet `status_details` i objektet `meta` med relevant information.

#### Uppdaterar en `oauth2-client_credentials`-hemlighet

Om en `oauth2-client_credentials`-hemlighet har tilldelats en miljö och dess status är `succeeded` (autentiseringsuppgifterna har bytts ut), utförs en ny utväxling automatiskt `refresh_at`.

Om utbytet lyckas ställs attributet `refresh_status` i objektet `meta` in på `succeeded` while `expires_at`, `refresh_at` och `activated_at` in på motsvarande sätt.

Om utbytet misslyckas görs ett försök att utföra åtgärden tre gånger till, med det senaste försöket högst två timmar innan åtkomsttoken upphör att gälla. Om alla försök misslyckas uppdateras attributet `refresh_status_details` från objektet `meta` med relevant information.

### `oauth2-google` {#oauth2-google}

För hemligheter med värdet `type_of` på `oauth2-google` krävs följande attribut under `credentials`:

| Attribut för autentiseringsuppgifter | Datatyp | Beskrivning |
| --- | --- | --- |
| `scopes` | Array | Visar Google produktomfång för autentisering. Följande omfattningar stöds:<ul><li>[Google Ads](https://developers.google.com/google-ads/api/docs/oauth/overview): `https://www.googleapis.com/auth/adwords`</li><li>[Google Pub/Sub](https://cloud.google.com/pubsub/docs/reference/service_apis_overview): `https://www.googleapis.com/auth/pubsub`</li></ul> |

När hemligheten `oauth2-google` har skapats innehåller svaret en `meta.authorization_url`-egenskap. Du måste kopiera och klistra in den här URL:en i en webbläsare för att slutföra autentiseringsflödet i Google.

#### Auktorisera om en `oauth2-google`-hemlighet

Auktoriserings-URL:en för en `oauth2-google`-hemlighet går ut en timme efter att hemligheten har skapats (vilket anges av `meta.authorization_url_expires_at`). Därefter måste hemligheten auktoriseras på nytt för att autentiseringsprocessen ska kunna förnyas.

Mer information om hur du återauktoriserar en `oauth2-google`-hemlighet genom att göra en PATCH-begäran till Reactor API finns i [Slutpunktshandboken ](../endpoints/secrets.md#reauthorize).

## Miljörelation

När du skapar en hemlighet måste du ange i vilken [miljö](../endpoints/environments.md) den ska finnas. Hemligheter sätts omedelbart in i den miljö där de skapas.

En hemlighet kan bara associeras med en miljö. När förhållandet mellan en hemlighet och en miljö väl har etablerats kan hemligheten inte rensas från miljön och hemligheten kan inte kopplas till en annan miljö.

>[!NOTE]
>
>Det enda undantaget till den här regeln är om miljön i fråga tas bort. I det här fallet är relationen rensad och hemligheten kan tilldelas en annan miljö.

När en hems autentiseringsuppgifter har bytts ut och en hemlighet ska kopplas till en miljö, sparas växlingsartefakten (tokensträngen för `token`, Base64-kodad sträng för `simple-http` eller åtkomsttoken för `oauth2-client_credentials`) säkert i miljön.

När växlingsartefakten har sparats i miljön anges hemlighetens `activated_at`-attribut till aktuell UTC-tid och kan nu refereras med ett dataelement. Mer information om att referera till hemligheter finns i [nästa avsnitt](#referencing-secrets).

## Referera till hemligheter {#referencing-secrets}

För att kunna referera till en hemlighet måste du skapa ett dataelement av typen [!UICONTROL Secret] (tillhandahålls av [[!UICONTROL Core] extension](../../extensions/client/core/overview.md)) för en händelsevidarebefordringsegenskap. När du konfigurerar det här dataelementet uppmanas du att ange vilken hemlighet som ska användas för varje miljö. Sedan kan du skapa regler som refererar till ett hemligt dataelement, till exempel i huvudet för ett HTTP-anrop.

![Hemligt dataelement](../../images/api/guides/secrets/data-element.png)

>[!NOTE]
>
>Om du vill lägga till ett hemligt dataelement i ett bibliotek måste du ha minst en `succeeded`-hemlighet associerad med miljön som biblioteket byggs på. Om ett bibliotek till exempel har ett hemligt dataelement som inte har någon `succeeded`-hemlighet konfigurerad för avsnittet [!UICONTROL Staging Secret], kommer ett försök att skapa biblioteket i mellanlagringsmiljön att resultera i ett fel.

Vid körning ersätts det hemliga dataelementet med motsvarande hemliga utbytesartefakt som sparats i miljön.

## Nästa steg

Den här guiden behandlar grunderna i att arbeta med hemligheter i Reaktors API. Mer information om hur du hanterar hemligheter med API-anrop finns i [Slutpunktshandboken för hemligheter](../endpoints/secrets.md).
