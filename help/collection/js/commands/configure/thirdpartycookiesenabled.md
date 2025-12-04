---
title: thirdPartyCookiesEnabled
description: Tillåt användning av cookies från tredje part för att identifiera besökare.
exl-id: f241a9ae-a892-46a5-b0dd-5ac72a44d4ac
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---

# `thirdPartyCookiesEnabled`

Egenskapen `thirdPartyCookiesEnabled` är en boolesk egenskap som avgör om Web SDK anger cookies i en tredjepartskontext. Det här alternativet är användbart om du vill identifiera besökare mellan underdomäner eller domäner som din organisation äger. Många moderna webbläsare begränsar dock inställningen och förfallotiden för cookies från tredje part. Om en besökares webbläsare inte stöder cookies från tredje part gör den här egenskapen ingenting.

Egenskapen `thirdPartyCookiesEnabled` styr också om [`CORE ID`](/help/collection/use-cases/identity/id-overview.md#tracking-coreid-web-sdk) kan begäras för [`getIdentity`](../getidentity.md) anrop.

När det här alternativet är aktiverat använder SDK Adobe Audience Manager för att identifiera besökare. När det här alternativet är inaktiverat inaktiveras anropet till Audience Manager. Mer information finns i [Förstå anrop till Demdex-domänen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/demdex-calls.html) i användarhandboken för Audience Manager.

Ange det booleska värdet `thirdPartyCookiesEnabled` när du kör kommandot `configure`. Om du utelämnar den här egenskapen när du konfigurerar Web SDK blir standardvärdet `true`. Ange det här värdet till `false` om du inte vill att Web SDK ska använda Audience Manager för att identifiera besökare.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  thirdPartyCookiesEnabled: false
});
```

## Aktivera cookies från tredje part med hjälp av taggtillägget Web SDK

Den här inställningen kan konfigureras i Web SDK-taggtillägget med hjälp av [Identitetskonfigurationsinställningar](/help/tags/extensions/client/web-sdk/configure/identity.md#use-third-party-cookies).
