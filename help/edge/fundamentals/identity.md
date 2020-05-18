---
title: Hämtar Experience Cloud-ID
seo-title: Adobe Experience Platform Web SDK Hämta Experience Cloud-ID
description: Lär dig hur du skaffar Adobe Experience Cloud ID.
seo-description: Lär dig hur du skaffar Adobe Experience Cloud ID.
translation-type: tm+mt
source-git-commit: a9dd5fd93397e57d0876bec334d54c517fa86939
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---


# Hämtar Experience Cloud-ID

Adobe Experience Platform Web SDK använder [Adobe Identity Service](../../identity-service/ecid.md). Detta garanterar att varje enhet har en unik identifierare som är beständig på enheten så att aktiviteten mellan sidorna kan knytas ihop.

## Identitet för första part

ID-tjänsten lagrar identiteten i en cookie i en förstapartsdomän. ID-tjänsterna försöker att ange cookien med hjälp av en HTTP-rubrik på domänen om detta misslyckas, eftersom ID-tjänsten återgår till att ange cookies via Javascript. Adobe rekommenderar att du konfigurerar en CNAME för att säkerställa att dina cookies inte begränsas av ITP-begränsningar på klientsidan.

## Tredjepartsidentitet

ID-tjänsterna kan synkronisera ett ID med en tredje parts domän (demdex.net) för att aktivera spårning över webbplatsen. När detta är aktiverat görs den första begäran om besökare (t.ex. någon som saknar ett ECID) till demdex.net. Detta görs endast i webbläsare som tillåter det (t.ex. Chrome) och styrs av parametern `thirdPartyCookiesEnabled` i konfigurationen. Om du vill inaktivera den här funktionen tillsammans, inställd `thirdPartyCookiesEnabled` på false.

## Hämtar besökar-ID

Om du vill använda det här unika ID:t använder du `getIdentity` kommandot. `getIdentity` returnerar det befintliga ECID:t för den aktuella besökaren. För förstagångsbesökare som ännu inte har ett ECID genereras ett nytt ECID med det här kommandot.

>[!NOTE]
>
>Den här metoden används vanligtvis med anpassade lösningar som kräver att Experience Cloud ID läses. Den används inte av en standardimplementering.

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

Med identitetstjänsten kan du dessutom synkronisera dina egna identifierare med ECID med hjälp av `syncIdentity` kommandot.

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

Nyckeln för objektet är [Identity Namespace](../../identity-service/namespaces.md) Symbol. Det listas i Adobe Experience Platform-gränssnittet under Identiteter.

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
| Boolean | valfri | false |

Ska den här identiteten användas som ett primärt fragment i den enhetliga profilen. Som standard är ECID angivet som användarens primära identifierare.

#### `hashEnabled`

| **Typ** | **Obligatoriskt** | **Standardvärde** |
| -------- | ------------ | ----------------- |
| Boolean | valfri | false |

Om det här alternativet är aktiverat kommer det att hash-koda identiteten med SHA256-hash.
