---
title: Översikt över API-tillägg för metakonvertering
description: Läs mer om Meta Conversions API-tillägget för händelsevidarebefordran i Adobe Experience Platform.
source-git-commit: a47e35a1b8c7ce2b0fa4ffe30fcdc7d22fc0f4c5
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 0%

---

# [!DNL Meta Conversions API] tilläggsöversikt

The [[!DNL Meta Conversions API]](https://developers.facebook.com/docs/marketing-api/conversions-api/) kan ni koppla marknadsföringsdata på serversidan till [!DNL Meta] för att optimera er annonsinriktning, minska kostnaden per åtgärd och mäta resultaten. Händelser är länkade till en [[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) ID och behandlas på ett liknande sätt som händelser på klientsidan.

Använda [!DNL Meta Conversions API] kan du utnyttja API:ts funktioner i [händelsevidarebefordran](../../../ui/event-forwarding/overview.md) regler att skicka data till [!DNL Meta] från Adobe Experience Platform Edge Network. Det här dokumentet beskriver hur du installerar tillägget och använder dess funktioner vid en händelsevidarebefordring [regel](../../../ui/managing-resources/rules.md).

>[!NOTE]
>
>Om du försöker skicka händelser till [!DNL Meta] från klientsidan i stället för från serversidan använder du [[!DNL Meta Pixiel] taggtillägg](../../client/meta/overview.md) i stället.

## Förutsättningar

För att kunna använda tillägget måste du ha tillgång till händelsevidarebefordran och en giltig [!DNL Meta] konto med tillgång till [!DNL Ad Manager] och [!DNL Event Manager]. Du måste kopiera ID:t för en befintlig [[!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755?id=1205376682832142) (eller [skapa en ny [!DNL Pixel]](https://www.facebook.com/business/help/952192354843755) i stället) så att tillägget kan konfigureras för ditt konto.

## Installera tillägget

Så här installerar du [!DNL Meta Conversions API] navigerar du till användargränssnittet för datainsamling eller användargränssnittet för Experience Platform och väljer **[!UICONTROL Event Forwarding]** från vänster navigering. Här väljer du en egenskap som tillägget ska läggas till i eller skapar en ny egenskap i stället.

När du har markerat eller skapat den önskade egenskapen väljer du **[!UICONTROL Extensions]** i den vänstra navigeringen väljer du **[!UICONTROL Catalog]** -fliken. Sök efter [!UICONTROL Meta Conversions API] kort, välj **[!UICONTROL Install]**.

![The [!UICONTROL Install] knappen som markeras för [!UICONTROL Meta Conversions API] i användargränssnittet för datainsamling.](../../../images/extensions/server/meta/install.png)

I konfigurationsvyn som visas måste du ange [!DNL Pixel] ID som du kopierade tidigare för att länka tillägget till ditt konto. Du kan klistra in ID:t direkt i indata eller använda ett dataelement i stället.

Du måste också ange en åtkomsttoken för att kunna använda [!DNL Conversions API] specifikt. Se [!DNL Conversions API] dokumentation om [generera en åtkomsttoken](https://developers.facebook.com/docs/marketing-api/conversions-api/get-started#access-token) om du vill se steg för hur du får fram det här värdet.

När du är klar väljer du **[!UICONTROL Save]**

![The [!DNL Pixel] ID som anges som ett dataelement i tilläggskonfigurationsvyn.](../../../images/extensions/server/meta/configure.png)

Tillägget är installerat och du kan nu använda dess funktioner i taggreglerna.

## Konfigurera en regel för vidarebefordran av händelser {#rule}

Börja skapa en ny regel för vidarebefordring av händelser och konfigurera villkoren efter behov. När du väljer åtgärder för regeln väljer du **[!UICONTROL Meta Conversions API Extension]** för tillägget väljer du **[!UICONTROL Send Conversions API Event]** för åtgärdstypen.

![The [!UICONTROL Send Page View] åtgärdstypen som väljs för en regel i användargränssnittet för datainsamling.](../../../images/extensions/server/meta/select-action.png)

Det visas kontroller som gör att du kan konfigurera händelsedata som ska skickas till [!DNL Meta] via [!DNL Conversions API]. Dessa alternativ kan anges direkt i de angivna inmatningarna eller så kan du välja befintliga dataelement som ska representera värdena i stället. Konfigurationsalternativen är uppdelade i fyra huvudavsnitt enligt nedan.

| Konfig.avsnitt | Beskrivning |
| --- | --- |
| [!UICONTROL Server Event Parameters] | Allmän information om händelsen, inklusive tidpunkten då den inträffade och källåtgärden som utlöste den. Se [[!DNL Conversions API] dokumentation](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event) om du vill ha mer information om de här parametrarna.<br><br>Du kan också välja att **[!UICONTROL Enable Limited Data Use]** för att hjälpa till att följa kundernas avval. Se [!DNL Conversions API] dokumentation om [databearbetningsalternativ](https://developers.facebook.com/docs/marketing-apis/data-processing-options/) om du vill ha mer information om den här funktionen. |
| [!UICONTROL Customer Information Parameters] | Användar-ID-data som används för att tilldela händelsen till en kund. Vissa av dessa värden måste hashas innan de kan skickas till API:t. Se [[!DNL Conversions API] dokumentation](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/customer-information-parameters) om du vill ha mer information om de här parametrarna. |
| [!UICONTROL Custom Data] | Ytterligare data som ska användas för annonsleveransoptimering, tillhandahålls i form av ett JSON-objekt. Se [[!DNL Conversions API] dokumentation](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/custom-data) om du vill ha mer information om godkända egenskaper för det här objektet.<br><br>Om du skickar en köphändelse måste du använda det här avsnittet för att ange de attribut som krävs `currency` och `value`. |
| [!UICONTROL Test Event] | Det här alternativet används för att verifiera om konfigurationen gör att serverhändelser tas emot av [!DNL Meta] som förväntat. Om du vill använda den här funktionen väljer du **[!UICONTROL Send as Test Event]** och ange sedan en testhändelsekod i indata nedan. När regeln för vidarebefordran av händelser har distribuerats och du har konfigurerat tillägget och åtgärden korrekt, bör du se aktiviteter som visas i **[!DNL Test Events]** visa i [!DNL Meta Events Manager]. |

{style=&quot;table-layout:auto&quot;}

När du är klar väljer du **[!UICONTROL Keep Changes]** för att lägga till åtgärden i regelkonfigurationen.

![[!UICONTROL Keep Changes] väljs för åtgärdskonfigurationen.](../../../images/extensions/server/meta/keep-changes.png)

När du är nöjd med regeln väljer du **[!UICONTROL Save to Library]**. Publicera slutligen en ny händelsevidarebefordring [bygga](../../../ui/publishing/builds.md) för att aktivera ändringar som gjorts i biblioteket.

## Nästa steg

I den här guiden beskrivs hur du skickar händelsedata på serversidan till [!DNL Meta] med [!DNL Meta Conversions API] tillägg. Mer information om taggar och vidarebefordran av händelser finns i [taggöversikt](../../../home.md).
