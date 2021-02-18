---
title: Hämta Experience Cloud-ID:n med Adobe Experience Platform Web SDK
description: Lär dig hur du hämtar Adobe Experience Cloud-ID:n (ECID) med Adobe Experience Platform Web SDK.
seo-description: Lär dig hur du skaffar Adobe Experience Cloud ID.
keywords: Identitet;Första parts identitet;Identitetstjänst;Tredjepartsidentitet;ID-migrering;Besökar-ID;Tredjepartsidentitet;Tredje parts-cookiesEnabled;idMigrationEnabled;getIdentity;Syncing Identities;syncIdentity;sendEvent;identityMap;primär;ecid;Identity Namespace id;authenticationState;hashEnabled;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---


# Hämta Adobe Experience Cloud ID:n

Adobe Experience Platform Web SDK använder [Adobe Identity Service](../../identity-service/ecid.md). Detta garanterar att varje enhet har en unik identifierare som är beständig på enheten så att aktiviteten mellan sidorna kan knytas ihop.

## Första parts identitet

[!DNL Identity Service] lagrar identiteten i en cookie i en förstapartsdomän. [!DNL Identity Service] försöker ange cookien med hjälp av en HTTP-rubrik på domänen. Om det misslyckas återgår [!DNL Identity Service] till att ställa in cookies via Javascript. Adobe rekommenderar att du konfigurerar en CNAME för att säkerställa att dina cookies inte begränsas av ITP-begränsningar på klientsidan.

## Tredjepartsidentitet

[!DNL Identity Service] kan synkronisera ett ID med en tredjepartsdomän (demdex.net) för att aktivera spårning över webbplatser. När detta är aktiverat görs den första begäran om besökare (till exempel någon som saknar ett ECID) till demdex.net. Detta görs endast i webbläsare som tillåter det (till exempel Chrome) och styrs av parametern `thirdPartyCookiesEnabled` i konfigurationen. Om du vill inaktivera den här funktionen tillsammans anger du `thirdPartyCookiesEnabled` till false.

## ID-migrering

När du migrerar från med Visitor API kan du även migrera befintliga AMCV-cookies. Om du vill aktivera ECID-migrering anger du parametern `idMigrationEnabled` i konfigurationen. ID-migrering aktiverar följande användningsfall:

* När vissa sidor i en domän använder Visitor API och andra sidor använder denna SDK. Som stöd för detta fall läser SDK befintliga AMCV-cookies och skriver en ny cookie med det befintliga ECID:t. Dessutom skriver SDK AMCV-cookies så att efterföljande sidor som är instrumenterade med Visitor API har samma ECID om ECID hämtas först på en sida som är instrumenterad med SDK.
* När Adobe Experience Platform Web SDK har konfigurerats på en sida som även har Visitor API. Om AMCV-cookien inte är inställd söker SDK efter besökar-API:t på sidan och anropar den för att hämta ECID.
* När hela webbplatsen använder Adobe Experience Platform Web SDK och inte har något Visitor-API är det bra att migrera ECID:n så att informationen om den returnerade besökaren behålls. När SDK har distribuerats med `idMigrationEnabled` under en tidsperiod så att de flesta besökarcookies migreras, kan inställningen inaktiveras.

## Uppdaterar egenskaper för migrering

När XDM-formaterade data skickas till Audience Manager måste dessa data konverteras till signaler när de migreras. Dina egenskaper måste uppdateras för att återspegla de nya nycklarna som finns i XDM. Den här processen blir enklare om du använder [BAAAM-verktyget](https://docs.adobe.com/content/help/en/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management) som Audience Manager har skapat.

## Vidarebefordran på serversidan

Om vidarebefordran på serversidan är aktiverat och använder `appmeasurement.js`. och `visitor.js` kan du behålla vidarebefordringsfunktionen på serversidan aktiverad och detta orsakar inga problem. I serverdelen hämtar Adobe alla AAM segment och lägger till dem i anropet till Analytics. Om anropet till Analytics innehåller dessa segment kommer Analytics inte att anropa Audience Manager för att vidarebefordra data, så det finns ingen dubbel datainsamling. Du behöver heller inte använda platstips när du använder Web SDK eftersom samma segmenteringsslutpunkter anropas i serverdelen.

## Hämtar besökar-ID

Om du vill använda det här unika ID:t använder du kommandot `getIdentity`. `getIdentity` returnerar det befintliga ECID:t för den aktuella besökaren. För förstagångsbesökare som ännu inte har ett ECID genereras ett nytt ECID med det här kommandot.

>[!NOTE]
>
>Den här metoden används vanligtvis med anpassade lösningar som kräver läsning av [!DNL Experience Cloud]-ID:t. Den används inte av en standardimplementering.

```javascript
alloy("getIdentity")
  .then(function(result) {
    // The command succeeded.
    console.log(result.identity.ECID);
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information.
  });
```

## Synkroniserar identiteter

>[!NOTE]
>
>Metoden `syncIdentity` har tagits bort i version 2.1.0, förutom hash-funktionen. Om du använder version 2.1.0+ och vill synkronisera identiteter kan du skicka dem direkt i alternativet `xdm` i kommandot `sendEvent`, under fältet `identityMap`.

Dessutom kan du med [!DNL Identity Service] synkronisera dina egna identifierare med ECID med hjälp av kommandot `syncIdentity`.

>[!NOTE]
>
>Vi rekommenderar att du skickar alla tillgängliga identiteter för varje `sendEvent`-kommando. Detta frigör en rad användningsfall, inklusive personalisering. Nu när du kan skicka dessa identiteter i kommandot `sendEvent` kan de placeras direkt i ditt DataLayer.

Genom att synkronisera identiteter kan du identifiera en enhet/användare med flera identiteter, ange deras autentiseringstillstånd och avgöra vilken identifierare som betraktas som den primära. Om ingen identifierare har angetts som `primary` blir det primära standardvärdet `ECID`.

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Notice how each namespace can contain multiple identifiers.
        {
          "id": "1234",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    }
  }
});
```

Varje egenskap i `identityMap` representerar identiteter som tillhör ett visst [identitetsnamnutrymme](../../identity-service/namespaces.md). Egenskapsnamnet ska vara identitetsnamnutrymmessymbolen, som du hittar i användargränssnittet i Adobe Experience Platform under &quot;[!UICONTROL Identities]&quot;. Egenskapsvärdet ska vara en array med identiteter som gäller det identitetsnamnutrymmet.

Varje identitetsobjekt i identitetsarrayen är strukturerat på följande sätt:

### `id`

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ----------------- |
| Sträng | Ja | ingen |

Detta är det ID som du vill synkronisera för det angivna namnutrymmet.

### `authenticationState`

| **Typ** | **Obligatoriskt** | **Standardvärde** | **Möjliga värden** |
| -------- | ------------ | ----------------- | ------------------------------------ |
| Sträng | Ja | tvetydig | tvetydig, autentiserad och utloggad |

Autentiseringstillståndet för ID:t.

### `primary`

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ----------------- |
| Boolean | valfri | falskt |

Avgör om den här identiteten ska användas som ett primärt fragment i den enhetliga profilen. Som standard anges ECID som användarens primära identifierare.
