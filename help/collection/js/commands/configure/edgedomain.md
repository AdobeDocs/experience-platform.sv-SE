---
title: edgeDomain
description: Avgör vilken domän du vill skicka data till.
exl-id: 6beb5116-cd23-42fd-934c-5cf84d1d7153
source-git-commit: 2d3c31e399989652a0472bbe2174ca8d8554ba30
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 1%

---

# `edgeDomain`

Med egenskapen `edgeDomain` kan du ändra den domän som Web SDK skickar data till. Användning av en anpassad domän kan minska effekten av annonsblockerare.

>[!NOTE]
>
>Den här egenskapen ändrar inte var cookies anges. SDK anger alltid [cookies från första part](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html), oavsett var data skickas.

Vilket värde du använder för `edgeDomain` beror på ditt deltagande i det [Adobe-hanterade certifikatprogrammet](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/adobe-managed-cert):

**Om din organisation deltar i det Adobe-hanterade certifikatprogrammet** anger du värdet till den förstapartsdomän som valdes när certifikatet konfigurerades. Vanligtvis är det här värdet en underdomän som ägs av din organisation. Exempel: `data.example.com`. CNAME-poster i din organisation vidarebefordrar dessa data till Adobe.

**Om din organisation inte deltar i certifikatprogrammet** anger du värdet till en underdomän till `data.adobedc.net`. Adobe rekommenderar att du använder din organisations Adobe-tilldelade IMS-företags-ID för att få en konsekvent hantering. Exempel: `example.data.adobedc.net`. Följ de här stegen för att fastställa ditt företags-ID för IMS:

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Tryck på `[Cmd]` + `[I]` (macOS) eller `[Ctrl]` + `[I]` (Windows) någonstans i Experience Cloud-gränssnittet.
1. En **[!UICONTROL User data debugger]** visas. Klicka på fliken **[!UICONTROL Assigned orgs]**.  
1. Utöka den önskade IMS-organisationen.
1. Leta reda på fältet **[!UICONTROL Tenant]**. Det här värdet är den rekommenderade underdomänen till `data.adobedc.net` att använda.

Ange strängen `edgeDomain` när du kör kommandot `configure`. Om du utelämnar den här egenskapen när du konfigurerar SDK blir standardvärdet `edge.adobedc.net`. Standardvärdet är godtagbart, men Adobe anser att det är bäst att ange ett organisationsspecifikt värde.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  edgeDomain: "data.example.com"
});
```

## Edge domain using the Web SDK tag extension

Taggtillägget som motsvarar den här egenskapen är fältet **[!UICONTROL Edge domain]** under [ SDK instanskonfigurationsinställningar ](/help/tags/extensions/client/web-sdk/configure/general.md) när tillägget konfigureras.
