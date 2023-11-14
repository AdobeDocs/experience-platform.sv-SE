---
title: Använda Adobe Journey Optimizer med Platform Web SDK
description: Lär dig hur du återger anpassat innehåll med Experience Platform Web SDK med Adobe Journey Optimizer
keywords: ajo;ajo web;adobe travel optimizer;renderDecision;surfaces;Decision;propositions;scope;schema
exl-id: 3f28e2bc-2c4b-4400-8f69-c7316449ff4f
source-git-commit: 5f2358c2e102c66a13746004ad73e2766e933705
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---

# Använda [!DNL Adobe Journey Optimizer] med [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] kan leverera och återge personaliserade upplevelser som hanteras i [!DNL Adobe Journey Optimizer] till webbkanalen. Du kan använda en WYSIWYG-redigerare, [!DNL Adobe Journey Optimizer] [WebbCampaign-gränssnitt](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html)för att skapa, aktivera och leverera [!DNL Journey Optimizer Web] kampanjer och personaliseringsupplevelser.

>[!IMPORTANT]
>
>Läs [Dokumentation för Adobe Journey Optimizer Web Channel](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/get-started-web.html) för information om hur du kommer igång med [!DNL Journey Optimizer Web] skapa och rapportera.

## Terminologi {#terminology}

**[!UICONTROL Surface]**: En webbyta är en webbegenskap som identifieras av en URL där [!DNL Adobe Journey Optimizer] upplevelseinnehåll kommer att levereras.

**[!UICONTROL Propositions]**: I [!DNL Adobe Journey Optimizer], korrelerar förslag till upplevelsen som väljs från en [!DNL Journey Optimizer Campaign].

## Aktivering [!DNL Adobe Journey Optimizer] {#enable-ajo}

Börja använda [!DNL Adobe Journey Optimizer]följer du stegen nedan.

1. Gå igenom [krav](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html#prerequesites) från [!DNL Adobe Journey Optimizer] [Web Experiences Guide](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html), särskilt:
   * Konfigurera [!DNL Adobe Experience Cloud Visual Editing Helper].
   * Aktivera [!DNL Adobe Journey Optimizer] i [datastream](../../../datastreams/overview.md).
   * Aktivera [!UICONTROL Active-On-Edge Merge Policy] alternativ.

2. Lägg till `renderDecisions` alternativ för dina händelser. Ange `renderDecisions` till `true` för automatisk återgivning av levererade Journey Optimizer-innehållsutkast på webbsidor.

   ```javascript
   alloy("sendEvent", {
       ...,
       "renderDecisions": true
   })
   ```

3. Du kan också ange ytterligare ytor i händelserna. Som standard genererar Web SDK automatiskt webbytan för den aktuella webbsidan och tar med den i begäran till Edge Network. Om det behövs kan ytterligare ytor inkluderas i begäran genom att ange dessa i `personalization.surfaces` alternativ för `sendEvent` eller i motsvarande **[!UICONTROL Surfaces]** [[!UICONTROL Send event] åtgärd](../../../tags/extensions/client/web-sdk/action-types.md#send-event) konfiguration av Web SDK-tillägget.

   ```javascript
   alloy("sendEvent", {
       ...
       "personalization": {
       "surfaces": [ "web://my.site.com/about.html", "web://my.site.com/contact.html" ]
       }
   })
   ```

   ![extension-add-surface](./assets/extension-add-surface.png)

   Händelsetytor ingår i `query.personalization.surfaces` begärandefält:

   ```json
   {
   "events": [
       {
           "query": {
               "personalization": {
               "schemas": [
                   ...
               ],
               "decisionScopes": [
                   "__view__"
               ],
               "surfaces": [
                   "web://ajostage.weebly.com/"
               ]
               }
           },
           ...
       }
   ]
   }
   ```

4. På samma sätt som andra personaliseringsfunktioner kan du lägga till en **[dölja fragment](../manage-flicker.md)** om du bara vill dölja vissa delar av sidan när du hämtar upplevelser.

## Skapa Adobe Journey Optimizer webbupplevelser {#create-ajo-web-experiences}

Följ [skapa webbkampanjer](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html#create-web-campaign) instruktionerna från [!DNL Adobe Journey Optimizer] [Web Experiences Guide](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) att skapa [!DNL Journey Optimizer Web] kampanjer och upplevelser.

## Återge personaliserat innehåll {#rendering-personalized-content}

Läs dokumentationen om [återge personaliserat innehåll](../rendering-personalization-content.md) för mer information.

Adobe Journey Optimizer-förslag för webbsidor behandlas på ungefär samma sätt som `__view__` förslag om beslutsomfattning. I synnerhet när `renderDecisions` option is set to `true` i `sendEvent` kommer dessa att återges automatiskt av Web SDK.

Exempel på Journey Optimizer-innehåll:

```json
{
    "scope": "web://ajostage.weebly.com/",
    "scopeDetails": {
        "correlationID": "ccfaf19c-6360-4aea-b464-0cf924db5da7",
        "characteristics": {
            "eventToken": "eyJtZXNzYWdlRXhlY3V0aW9uIjp7Im1lc3NhZ2VFeGVjdXRpb25JRCI6ImEzNDYxYTMzLTc5MjktNGQyNS1hNmMxLTVkYzM2YWY1NzRmMyIsIm1lc3NhZ2VJRCI6ImNjZmFmMTljLTYzNjAtNGFlYS1iNDY0LTBjZjkyNGRiNWRhNyIsIm1lc3NhZ2VUeXBlIjoibWFya2V0aW5nIiwiY2FtcGFpZ25JRCI6IjEzN2JmMzllLWM1ODgtNGI1My1iODQxLTJiMWZiZDYxM2JkYiIsImNhbXBhaWduVmVyc2lvbklEIjoiMTA1NzY1MmEtZWYwNS00YjE3LWExMmUtY2FlOTQyOTFhMWFjIiwiY2FtcGFpZ25BY3Rpb25JRCI6ImViNTlmODQ4LTk5ZDYtNGE1OC05YmU4LTk4MjIxODU0NmYzNiIsIm1lc3NhZ2VQdWJsaWNhdGlvbklEIjoiYzg2NzFjZmItNDdjYS00YTVjLTg4Y2YtNzYwZDFlZjU1MzQyIn0sIm1lc3NhZ2VQcm9maWxlIjp7ImNoYW5uZWwiOnsiX2lkIjoiaHR0cHM6Ly9ucy5hZG9iZS5jb20veGRtL2NoYW5uZWxzL3dlYiIsIl90eXBlIjoiaHR0cHM6Ly9ucy5hZG9iZS5jb20veGRtL2NoYW5uZWwtdHlwZXMvd2ViIn0sIm1lc3NhZ2VQcm9maWxlSUQiOiI2YTViY2I3ZC02MmYxLTQ5NDItODRkMC02MzE5ZjM5Zjk1ZGUifX0="
        },
        "decisionProvider": "AJO",
        "activity": {
            "id": "137bf39e-c588-4b53-b841-2b1fbd613bdb#eb59f848-99d6-4a58-9be8-982218546f36"
        }
    },
    "id": "002321c0-dff5-4153-b171-a9dfb70b9750",
    "items": [
        {
            "schema": "https://ns.adobe.com/personalization/dom-action",
            "data": {
                "uiData": {
                    "tagType": "Text",
                    "actionType": "changed"
                },
                "content": "Welcome AJO!",
                "prehidingSelector": "#wsite-content > DIV:nth-of-type(2) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(3) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)",
                "type": "setHtml",
                "selector": "#wsite-content > DIV.wsite-section-wrap:eq(1) > DIV.wsite-section:eq(0) > DIV.wsite-section-content:eq(0) > DIV.container:eq(0) > DIV.wsite-section-elements:eq(0) > DIV.paragraph:eq(0) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)"
            },
            "id": "0a522f66-9e6a-4ded-b1d0-e9167f103290"
        },
        {
            "schema": "https://ns.adobe.com/personalization/dom-action",
            "data": {
                "uiData": {
                    "tagType": "Text",
                    "actionType": "changed"
                },
                "content": {
                    "font-weight": "bold"
                },
                "prehidingSelector": "#wsite-content > DIV:nth-of-type(2) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(3) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)",
                "type": "setStyle",
                "selector": "#wsite-content > DIV.wsite-section-wrap:eq(1) > DIV.wsite-section:eq(0) > DIV.wsite-section-content:eq(0) > DIV.container:eq(0) > DIV.wsite-section-elements:eq(0) > DIV.paragraph:eq(0) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)"
            },
            "id": "66216ca5-5d0f-4239-a8c8-6bc4a5a7cbdb"
        }
    ]
}
```

## Felsökning {#debugging}

Om du vill felsöka Adobe Journey Optimizer personaliseringsimplementeringar använder du [[!DNL Web SDK] felsökning](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/debugging.html). [!DNL Adobe Journey Optimizer] felsökningsspårningar är tillgängliga vid felsökning med [[!DNL Adobe Experience Platform Assurance]](https://developer.adobe.com/client-sdks/documentation/platform-assurance/). Sök efter händelser med `AJO:` prefix.

![trust-ajo-trace](./assets/assurance-ajo-trace.png)
