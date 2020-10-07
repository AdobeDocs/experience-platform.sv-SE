---
title: Hämtar Experience Cloud ID
seo-title: Adobe Experience Platform Web SDK Hämtar Experience Cloud-ID
description: Lär dig hur du skaffar Adobe Experience Cloud ID.
seo-description: Lär dig hur du skaffar Adobe Experience Cloud ID.
keywords: Identity;First Party Identity;Identity Service;3rd Party Identity;ID Migration;Visitor ID;third party identity;thirdPartyCookiesEnabled;idMigrationEnabled;getIdentity;Syncing Identities;syncIdentity;sendEvent;identityMap;primary;ecid;Identity Namespace;namespace id;authenticationState;hashEnabled;
translation-type: tm+mt
source-git-commit: 34cfcaac276bf2645a0365a0dfa71c4ead6e2ecb
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 1%

---


# Identitet - Hämtar Experience Cloud-ID

Adobe Experience Platform [!DNL Web SDK] använder [Adobe Identity Service](../../identity-service/ecid.md). Detta garanterar att varje enhet har en unik identifierare som är beständig på enheten så att aktiviteten mellan sidorna kan knytas ihop.

## Identitet för första part

Identiteten [!DNL Identity Service] lagras i en cookie i en förstapartsdomän. Försökte [!DNL Identity Service] ange cookien med hjälp av en HTTP-rubrik på domänen. Om detta misslyckas återgår [!DNL Identity Service] programmet till att ställa in cookies via Javascript. Adobe rekommenderar att du konfigurerar en CNAME för att säkerställa att dina cookies inte begränsas av ITP-begränsningar på klientsidan.

## Tredjepartsidentitet

Det [!DNL Identity Service] går att synkronisera ett ID med en tredje parts domän (demdex.net) för att aktivera spårning över webbplatser. När detta är aktiverat görs den första begäran om besökare (t.ex. någon som saknar ett ECID) till demdex.net. Detta görs endast i webbläsare som tillåter det (t.ex. Chrome) och styrs av parametern `thirdPartyCookiesEnabled` i konfigurationen. Om du vill inaktivera den här funktionen tillsammans anger du false `thirdPartyCookiesEnabled` för den.

## ID-migrering

När du migrerar från med Visitor API kan du även migrera befintliga AMCV-cookies. Om du vill aktivera ECID-migrering anger du parametern `idMigrationEnabled` i konfigurationen. ID-migreringen är konfigurerad för att aktivera vissa användningsfall:

* När vissa sidor i en domän använder Visitor API och andra sidor använder denna SDK. Som stöd för detta fall läser SDK befintliga AMCV-cookies och skriver en ny cookie med det befintliga ECID:t. Dessutom skriver SDK AMCV-cookies så att efterföljande sidor som är instrumenterade med Visitor API har samma ECID om ECID hämtas först på en sida som är instrumenterad med AEP Web SDK.
* När AEP Web SDK har konfigurerats på en sida som även har Visitor API. Om AMCV-cookien inte är inställd söker SDK efter besökar-API:t på sidan och anropar den för att hämta ECID.
* När hela webbplatsen använder AEP Web SDK och inte har något Visitor-API är det bra att migrera ECID:n så att informationen om den returnerade besökaren behålls. När SDK har distribuerats `idMigrationEnabled` under en tidsperiod så att de flesta besöks-cookies migreras, kan inställningen inaktiveras.

## Hämtar besökar-ID

Om du vill använda det här unika ID:t använder du `getIdentity` kommandot. `getIdentity` returnerar det befintliga ECID:t för den aktuella besökaren. För förstagångsbesökare som ännu inte har ett ECID genereras ett nytt ECID med det här kommandot.

>[!NOTE]
>
>Den här metoden används vanligtvis med anpassade lösningar som kräver att du läser [!DNL Experience Cloud] ID:t. Den används inte av en standardimplementering.

```javascript
alloy("getIdentity")
  .then(function(result.identity.ECID) {
    // This function will get called with Adobe Experience Cloud Id when the command promise is resolved
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information
  })
```

## Synkroniserar identiteter

>[!NOTE]
>
>Metoden har tagits bort i version 2.1.0, förutom hash-funktionen. `syncIdentity` Om du använder version 2.1.0+ och vill synkronisera identiteter kan du skicka dem direkt med alternativet `xdm` för `sendEvent` kommandot, under `identityMap` fältet.

Dessutom [!DNL Identity Service] kan du synkronisera dina egna identifierare med ECID med hjälp av `syncIdentity` kommandot .

>[!NOTE]
>
>Vi rekommenderar att du skickar alla tillgängliga identiteter för varje `sendEvent` kommando. Detta frigör en rad användningsfall, inklusive personalisering. Nu när du kan skicka dessa identiteter i `sendEvent` kommandot kan de placeras direkt i ditt DataLayer.

Genom att synkronisera identiteter kan du identifiera en enhet/användare med flera identiteter, ange deras autentiseringstillstånd och avgöra vilken identifierare som betraktas som den primära. Om ingen identifierare har angetts som `primary`är standardinställningen `ECID`.

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
})
```


### Alternativ för synkronisering av identiteter

#### Symbol för namnområde för identitet

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ----------------- |
| Sträng | Ja | ingen |

Nyckeln för objektet är [Identity Namespace](../../identity-service/namespaces.md) Symbol. I Adobe Experience Platform användargränssnitt hittar du det under &quot;[!UICONTROL Identities]&quot;.

#### `id`

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ----------------- |
| Sträng | Ja | ingen |

Detta är det ID som du vill synkronisera för det angivna namnutrymmet.

#### `authenticationState`

| **Typ** | **Obligatoriskt** | **Standardvärde** | **Möjliga värden** |
| -------- | ------------ | ----------------- | ------------------------------------ |
| Sträng | Ja | tvetydig | tvetydig, autentiserad och utloggad |

Autentiseringstillståndet för ID:t.

#### `primary`

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ----------------- |
| Boolean | valfri | falskt |

Avgör om den här identiteten ska användas som ett primärt fragment i den enhetliga profilen. Som standard anges ECID som användarens primära identifierare.

#### `hashEnabled`

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ----------------- |
| Boolean | valfri | falskt |

Om alternativet är aktiverat kommer det att hash-koda identiteten med SHA256-hash.
