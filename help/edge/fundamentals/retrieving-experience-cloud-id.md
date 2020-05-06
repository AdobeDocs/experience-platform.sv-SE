---
title: Hämtar Experience Cloud-ID
seo-title: Adobe Experience Platform Web SDK Hämta Experience Cloud-ID
description: Lär dig hur du skaffar Adobe Experience Cloud ID.
seo-description: Lär dig hur du skaffar Adobe Experience Cloud ID.
translation-type: tm+mt
source-git-commit: fc48c11cb1f8a88f9fec8a36646f59f39ac3819f
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# (Beta) Hämtar Experience Cloud ID

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK är för närvarande en betaversion och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

Adobe Experience Cloud använder ett unikt ID för varje kund. Om du vill använda det här unika ID:t använder du `getIdentity` kommandot. `getIdentity` returnerar det befintliga ECID:t för den aktuella besökaren. För förstagångsbesökare som ännu inte har ett ECID genereras ett nytt ECID med det här kommandot.

>[!NOTE]
>
>Den här metoden används vanligtvis med anpassade lösningar som kräver att Experience Cloud ID läses. Den används inte av en standardimplementering.

```javascript
alloy("getIdentity")
  .then(function(ecid) {
    // This function will get called with Adobe Experience Cloud Id when the command promise is resolved
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information
  })
```
