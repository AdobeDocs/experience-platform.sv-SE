---
title: Översikt över Capillary Streaming Events
description: Lär dig att strömma data från Capillary till Experience Platform.
last-substantial-update: 2025-09-23T00:00:00Z
badge: Beta
exl-id: 3b8eb2f6-3b4a-4b91-89d4-b6d9027c6ab4
source-git-commit: 91d6206c6ce387fde365fa72dc79ca79fc0e46fa
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# [!DNL Capillary Streaming Events]

>[!AVAILABILITY]
>
>Källan [!DNL Capillary Streaming Events] är i betaversion. Läs [villkoren](../../home.md#terms-and-conditions) i källresursöversikten om du vill ha mer information om hur du använder betatecknade källor.

[!DNL Capillary Technologies] är en ledande lojalitets- och engagemangsplattform som är betrodd av över 300 varumärken runt om i världen. Använd [!DNL Capillary Streaming Events]-källan för att göra det möjligt för ditt företag att strömma kundprofiler, lojalitetsdata och transaktionshändelser från [!DNL Capillary] till Adobe Experience Platform. Anslut [!DNL Capillary]-källan för att aktivera personalisering i realtid, avancerad målgruppssegmentering och flerkanalskampanjer.

Genom att integrera [!DNL Capillary] med Experience Platform kan du:

* Synkronisera **förmånspunkter, nivåer och belöningar** i realtid.
* Skicka **transaktionsdata** till Experience Platform för analys och aktivering.
* Använd Real-Time CDP, Experience Platform och Adobe Journey Optimizer för segmentering, resesamordning och personalisering.

## Förhandskrav

Innan du ansluter [!DNL Capillary] till Adobe Experience Platform bör du kontrollera att du har:

* Ett giltigt **Adobe-organisations-ID** och åtkomst till en aktiverad Experience Platform-sandlåda.
* **[!DNL Capillary]källautentiseringsuppgifter** (klient-ID och klienthemlighet).
* Behörigheter som krävs i Adobe Admin Console för att skapa källor och dataflöden.

### Samla in nödvändiga inloggningsuppgifter

Du måste ange värden för följande autentiseringsuppgifter för att kunna ansluta ditt [!DNL Capillary]-konto till Experience Platform:

| Autentiseringsuppgifter | Beskrivning | Exempel |
| --- | --- | --- |
| Klient-ID | Klient-ID för källan [!DNL Capillary]. | `321c8a8fee0d4a06838d46f9d3109e8a` |
| Klienthemlighet | Klienthemligheten som utfärdas med klient-ID | `xxxxxxxxxxxxxxxxxx` |
| Organisations-ID | Ditt Adobe-organisations-ID | `0A7D42FC5DB9D3360A495FD3@AdobeOrg` |

Mer information om hur du genererar åtkomsttoken finns i [Adobe-autentiseringsguiden](https://developer.adobe.com/developer-console/docs/guides/authentication/).

### Generera en åtkomsttoken

Använd sedan ditt klient-ID och klienthemlighet för att generera en åtkomsttoken från Adobe.

**Begäran**

```shell
curl -X POST 'https://ims-na1.adobelogin.com/ims/token' \
  -d 'client_id={CLIENT_ID}' \
  -d 'client_secret={CLIENT_SECRET}' \
  -d 'grant_type=client_credentials' \
  -d 'scope=openid AdobeID read_organizations additional_info.projectedProductContext session'
```

**Svar**

```json
{
  "access_token": "eyJhbGciOi...",
  "token_type": "bearer",
  "expires_in": 86399994
}
```

## Nästa steg

När du har slutfört kravkonfigurationen för [!DNL Capillary] kan du läsa följande dokumentation för att lära dig hur du kan ansluta ditt konto och starta direktuppspelning av data från [!DNL Capillary] till Experience Platform.

* [Anslut [!DNL Capillary Streaming Events] till Experience Platform med API:t](../../tutorials/api/create/loyalty/capillary.md)
* [Anslut [!DNL Capillary Streaming Events] till Experience Platform med användargränssnittet](../../tutorials/ui/create/loyalty/capillary.md)
