---
title: Hämtar Experience Cloud ID
seo-title: Adobe Experience Platform Web SDK Hämtar Experience Cloud-ID
description: Lär dig hur du skaffar Adobe Experience Cloud ID.
seo-description: Lär dig hur du skaffar Adobe Experience Cloud ID.
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 2%

---


# Identitet - Hämtar Experience Cloud-ID

Adobe Experience Platform [!DNL Web SDK] använder [Adobe Identity Service](../../identity-service/ecid.md). Detta garanterar att varje enhet har en unik identifierare som är beständig på enheten så att aktiviteten mellan sidorna kan knytas ihop.

## Identitet för första part

Identiteten [!DNL Identity Service] lagras i en cookie i en förstapartsdomän. Försökte [!DNL Identity Service] ange cookien med hjälp av en HTTP-rubrik på domänen. Om detta misslyckas återgår [!DNL Identity Service] programmet till att ställa in cookies via Javascript. Adobe rekommenderar att du konfigurerar en CNAME så att dina cookies inte begränsas av ITP-begränsningar på klientsidan.

## Tredjepartsidentitet

Det [!DNL Identity Service] går att synkronisera ett ID med en tredje parts domän (demdex.net) för att aktivera spårning över webbplatser. När detta är aktiverat görs den första begäran om besökare (t.ex. någon som saknar ett ECID) till demdex.net. Detta görs endast i webbläsare som tillåter det (t.ex. Chrome) och styrs av parametern `thirdPartyCookiesEnabled` i konfigurationen. Om du vill inaktivera den här funktionen tillsammans anger du false `thirdPartyCookiesEnabled` för den.

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

Dessutom [!DNL Identity Service] kan du synkronisera dina egna identifierare med ECID med hjälp av `syncIdentity` kommandot .

```javascript
alloy("syncIdentity",{
    identity:{
      "AppNexus":{
        "id":"123456,
        "authenticationState":"ambiguous",
        "primary":false,
        "hashEnabled": true,
      }
    }
})
```

### Alternativ för synkronisering av identiteter

#### Symbol för namnområde för identitet

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ----------------- |
| Sträng | Ja | ingen |

Nyckeln för objektet är [Identity Namespace](../../identity-service/namespaces.md) Symbol. Du hittar det här i användargränssnittet i Adobe Experience Platform under [!UICONTROL Identities].

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
