---
title: Profilsynkronisering i realtid för mbox3rdPartyId
description: Lär dig använda mbox3rdPartyId med Adobe Experience Platform Web SDK.
keywords: personalisering;mål;adobe target;renderDecision;sendEvent;mbox3rdPartyId;
exl-id: 677d1054-0769-4ec6-811e-e02d4b247c2a
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 1%

---

# Vad är `mbox3rdPartyId`

Mbox3rdPartyId i Adobe Target är ditt företags besökar-ID, till exempel medlemskaps-ID för ditt företags lojalitetsprogram.

När en besökare loggar in på ett företags webbplats skapar företaget vanligtvis ett ID som är knutet till besökarens konto, förmånskort, medlemsnummer eller andra tillämpliga identifierare för det företaget. [Läs mer](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html#)


## Så här använder du `mbox3rdPartyId` med Web SDK

### Steg 1: Konfigurera `Target Third Party ID Namespace`

Konfigurera `Target Third Party ID Namespace` i [Datastream](../../../datastreams/overview.md) med det ID-namnområde som du vill använda som ett ID för en tredje part i en mbox.
[Läs mer om ID-namnutrymmen](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=sv)

![Plattformsgränssnitt som visar namnområdesfältet för mål-ID för tredje part.](assets/mbox3rdpartyid.png)

### Steg 2: Skicka `mbox3rdpartyId` till mål

Skicka `mbox3rdpartyId` till mål i kommandot `sendEvent` med ID-namnområdet som du konfigurerade i steg 1.
[Läs mer om att skicka ID:n](../../identity/overview.md#syncing-identities)

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Replace `ID_NAMESPACE` with the namespace you have configured in Step 1.
        {
          "id": "1234",
          "authenticatedState": "authenticated"
        }
      ]
    }
  }
});
```
