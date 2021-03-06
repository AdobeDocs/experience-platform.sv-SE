---
title: Hemligheter i reaktors-API
description: Lär dig grunderna i hur du konfigurerar hemligheter i Reaktors API för användning vid vidarebefordran av händelser.
source-git-commit: 6822199c3ecf4414893a8b8dfc650e3da40a6470
workflow-type: tm+mt
source-wordcount: '1111'
ht-degree: 1%

---

# Hemligheter i reaktors-API

I Reaktors-API är en hemlighet en resurs som representerar autentiseringsuppgifter. Hemligheter används vid vidarebefordran av händelser för att autentisera till ett annat system för säkert datautbyte. Därför kan hemligheter bara skapas i egenskaper för händelsevidarebefordran (egenskaper vars `platform` attribute is set to `edge`).

Det finns för närvarande tre hemliga typer som stöds angivna i `type_of` attribute:

| Hemlig typ | Beskrivning |
| --- | --- |
| `token` | En enda teckensträng som representerar ett autentiseringstokenvärde som är känt och begripligt för båda systemen. |
| `simple-http` | Innehåller två strängattribut för ett användarnamn och ett lösenord. |
| `oauth2` | Innehåller flera attribut som stöder [OAuth](https://datatracker.ietf.org/doc/html/rfc6749) autentiseringsspecifikation. Vidarebefordran av händelser ber dig om den information som krävs och hanterar sedan förnyelsen av dessa token för dig inom ett angivet intervall. |

{style=&quot;table-layout:auto&quot;}

Den här guiden ger en översikt på hög nivå över hur du konfigurerar hemligheter för användning vid vidarebefordran av händelser. Detaljerad vägledning om hur du hanterar hemligheter i Reaktors-API:t, inklusive exempel-JSON för en hems struktur, finns i [Slutpunktshandbok för hemligheter](../endpoints/secrets.md).

## Autentiseringsuppgifter

Varje hemlighet innehåller `credentials` som innehåller sina respektive autentiseringsvärden. Varje typ av hemlighet har olika obligatoriska attribut, vilket visas i avsnitten nedan.

### `token`

Hemligheter med en `type_of` värde för `token` kräver endast ett attribut under `credentials`:

| Attribut för autentiseringsuppgifter | Datatyp | Beskrivning |
| --- | --- | --- |
| `token` | Sträng | En hemlig token som förstås av målsystemet. |

{style=&quot;table-layout:auto&quot;}

Token lagras som ett statiskt värde, och därför är hemligheten `expires_at` och `refresh_at` egenskaper anges till `null` när hemligheten skapas.

### `simple-http`

Hemligheter med en `type_of` värde för `simple-http` kräver följande attribut under `credentials`:

| Attribut för autentiseringsuppgifter | Datatyp | Beskrivning |
| --- | --- | --- |
| `username` | Sträng | Ett användarnamn. |
| `password` | Sträng | Ett lösenord. Detta värde ingår inte i API-svaret. |

{style=&quot;table-layout:auto&quot;}

När hemligheten skapas byts de två attributen ut med en BASE64-kodning av `username:password`. Efter utbytet är hemligheten `expires_at` och `refresh_at` egenskaper anges till `null`.

### `oauth2`

>[!NOTE]
>
>För närvarande är det bara [Typ av klientautentiseringsuppgifter](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) stöds för OAuth-hemligheter.

Hemligheter med en `type_of` värde för `oauth2` kräver följande attribut under `credentials`:

| Attribut för autentiseringsuppgifter | Datatyp | Beskrivning |
| --- | --- | --- |
| `client_id` | Sträng | Klient-ID för OAuth-integreringen. |
| `client_secret` | Sträng | Klienthemligheten för OAuth-integreringen. Detta värde ingår inte i API-svaret. |
| `authorization_url` | Sträng | Auktoriserings-URL:en för OAuth-integreringen. |
| `refresh_offset` | Heltal | *(Valfritt)* Värdet i sekunder som uppdateringsåtgärden ska förskjutas med. Om det här attributet utelämnas när hemligheten skapas ställs värdet in på `14400` (fyra timmar) som standard. |
| `options` | Objekt | *(Valfritt)* Anger ytterligare alternativ för OAuth-integrering:<ul><li>`scope`: En sträng som representerar [OAuth 2.0-scope](https://oauth.net/2/scope/) för inloggningsuppgifterna.</li><li>`audience`: En sträng som representerar en [Åtkomsttoken för Auth0](https://auth0.com/docs/protocols/protocol-oauth2).</li></ul> |

När en `oauth2` hemligheten skapas eller uppdateras, `client_id` och `client_secret` (och möjligt `options`) byts ut i en POST till `authorization_url`, enligt klientautentiseringsflödet i OAuth-protokollet.

>[!NOTE]
>
>Svarstexten för auktoriseringstjänsten förväntas vara kompatibel med OAuth-protokollet.

Om auktoriseringstjänsten svarar med `200 OK` och ett JSON- svarsorgan analyseras kroppen och `access_token` kommer till kantmiljön och `expires_in` används för att beräkna `expires_at` och `refresh_at` attribut för hemligheten. Om det inte finns någon miljökoppling på hemligheten, `access_token` kasseras.

Ett utbyte av autentiseringsuppgifter anses vara lyckat under följande förhållanden:

* `expires_in` är större än `28800` (åtta timmar).
* `refresh_offset` är mindre än värdet för `expires_in` minus `14400` (fyra timmar). Om `expires_in` är `36000` (tio timmar) och `refresh_offset` är `28800` (åtta timmar), betraktas utbytet som misslyckat eftersom `28800` är större än `36000` - `14400` (`21600`).

Om utbytet lyckas anges hemmens statusattribut till `succeeded` och värden för `expires_at` och `refresh_at` är inställda:

* `expires_at` är den aktuella UTC-tiden plus värdet för `expires_in`.
* `refresh_at` är den aktuella UTC-tiden plus värdet för `expires_in`, minus värdet för `refresh_offset`. Om `expires_in` är `43200` (tolv timmar) och `refresh_offset` är `14400` (fyra timmar), `refresh_at` egenskapen skulle anges till `28800` (åtta timmar) efter aktuell UTC-tid.

Om bytet av någon anledning misslyckas `status_details` i `meta` objektuppdateringar med relevant information.

### Uppdatera en `oauth2` hemlig

Om en `oauth2` hemligheten har tilldelats en miljö och dess status är `succeeded` (inloggningsuppgifterna har bytts ut utan fel), utförs ett nytt utbyte automatiskt på `refresh_at`.

Om utbytet lyckas `refresh_status` i `meta` objektet är inställt på `succeeded` while `expires_at`, `refresh_at`och `activated_at` uppdateras därefter.

Om utbytet misslyckas görs ett försök att utföra åtgärden tre gånger till, med det senaste försöket högst två timmar innan åtkomsttoken upphör att gälla. Om alla försök misslyckas `refresh_status_details` attribut från `meta` objektuppdateringar med relevant information.

## Miljörelation

När du skapar en hemlighet måste du ange [miljö](../endpoints/environments.md) där den kommer att finnas. Hemligheter sätts omedelbart in i den miljö där de skapas.

En hemlighet kan bara associeras med en miljö. När förhållandet mellan en hemlighet och en miljö väl har etablerats kan hemligheten inte rensas från miljön och hemligheten kan inte kopplas till en annan miljö.

>[!NOTE]
>
>Det enda undantaget till den här regeln är om miljön i fråga tas bort. I det här fallet är relationen rensad och hemligheten kan tilldelas en annan miljö.

När en hems autentiseringsuppgifter har bytts ut, för att en hemlighet ska kopplas till en miljö, kan växlingsartefakten (tokensträngen för `token`, den Base64-kodade strängen för `simple-http`eller åtkomsttoken för `oauth2`) sparas säkert i miljön.

När växlingsartefakten har sparats i miljön är hemligheten `activated_at` är inställt på aktuell UTC-tid och kan nu refereras med ett dataelement. Se [nästa avsnitt](#referencing-secrets) för mer information om att referera till hemligheter.

## Referera hemligheter {#referencing-secrets}

Om du vill referera till en hemlighet måste du skapa ett dataelement av typen[!UICONTROL Secret]&quot; (tillhandahålls av [[!UICONTROL Core] extension](../../extensions/web/core/overview.md)) på en händelsevidarebefordringsegenskap. När du konfigurerar det här dataelementet uppmanas du att ange vilken hemlighet som ska användas för varje miljö. Sedan kan du skapa regler som refererar till ett hemligt dataelement, till exempel i huvudet för ett HTTP-anrop.

![Hemligt dataelement](../../images/api/guides/secrets/data-element.png)

>[!NOTE]
>
>Om du vill lägga till ett hemligt dataelement i ett bibliotek måste du ha minst ett `succeeded` hemlighet som är associerad med miljön som biblioteket byggs på. Om ett bibliotek till exempel har ett hemligt dataelement som inte har ett `succeeded` hemlighet konfigurerad för [!UICONTROL Staging Secret] om du försöker skapa det biblioteket i testmiljön uppstår ett fel.

Vid körning ersätts det hemliga dataelementet med motsvarande hemliga utbytesartefakt som sparats i miljön.

## Nästa steg

Den här guiden behandlar grunderna i att arbeta med hemligheter i Reaktors API. Mer information om hur du hanterar hemligheter med API-anrop finns i [Slutpunktshandbok för hemligheter](../endpoints/secrets.md).
