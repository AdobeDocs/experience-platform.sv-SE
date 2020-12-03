---
keywords: advertising; bing;
title: Microsoft Bing-mål
seo-title: Med Microsoft Bing-målet kan du skicka profildata till Microsoft Display Advertising.
description: Med Microsoft Bing-målet kan ni genomföra återannonsering och målgruppsanpassade digitala kampanjer i Microsoft Display Advertising.
seo-description: Med Microsoft Bing-målet kan ni genomföra återannonsering och målgruppsanpassade digitala kampanjer i Microsoft Display Advertising.
translation-type: tm+mt
source-git-commit: 0bb1622895b1e0f97fc47b5c61d456bc369746c8
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 1%

---


# [!DNL Microsoft Bing] mål

## Översikt {#overview}

Målet hjälper dig att [!DNL Microsoft Bing] skicka profildata till [!DNL Microsoft Display Advertising].

Om du vill skicka profildata till [!DNL Microsoft Bing]måste du först ansluta till målet.

## Destinationsspecifikationer {#destination-specs}

Observera följande information som är specifik för [!DNL Microsoft Bing] målet:

* Du kan skicka följande [identiteter](../../../identity-service/namespaces.md) till [!DNL Microsoft Bing] mål: [!DNL Microsoft ID].

## Användningsfall {#use-cases}

Som marknadsförare vill jag kunna använda segment som är inbyggda i för [!DNL Microsoft Advertising IDs] att rikta in mig på användare via webbannonsering i alla [!DNL Microsoft Advertising] kanaler.

## Exporttyp {#export-type}

**[!DNL Segment Export]** - du exporterar alla medlemmar i ett segment (publik) till [!DNL Microsoft Bing] målet.

## Förutsättningar {#prerequisites}

När du konfigurerar målet måste du ange följande information:

* [!UICONTROL Account ID]: detta är ditt [!DNL Bing Ads CID]heltalsformat.

## Anslut till mål {#connect-destination}

In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, select [!DNL Microsoft Bing], and select **[!UICONTROL Configure]**.

![Konfigurera Microsoft Bing-mål](../../assets/catalog/advertising/bing/configure.png)

>[!NOTE]
>
>Om det redan finns en anslutning till det här målet kan du se en **[!UICONTROL Activate]** knapp på målkortet. Mer information om skillnaden mellan **[!UICONTROL Activate]** och **[!UICONTROL Configure]** finns i avsnittet [Katalog](../../ui/destinations-workspace.md#catalog) i dokumentationen för målarbetsytan.
>
>![Aktivera Microsoft Bing-mål](../../assets/catalog/advertising/bing/activate.png)

I [!UICONTROL Authentication] steget måste du ange information om målanslutningen:

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Account ID]**: Din [!DNL Bing Ads CID].
* **[!UICONTROL Marketing use case]**: Fall av marknadsanvändning anger avsikten för vilken data ska exporteras till destinationen. Du kan välja bland Adobe-definierade användningsfall för marknadsföring eller skapa ett eget marknadsföringsexempel. Mer information om användningsfall för marknadsföring finns på sidan [Datastyrning i Adobe Experience Platform](../../../rtcdp/privacy/data-governance-overview.md#destinations) . Mer information om de enskilda Adobe-definierade användningsfallen för marknadsföring finns i översikten över [dataanvändningspolicyn](../../../data-governance/policies/overview.md#core-actions).

![Autentisering av Microsoft Bing-mål](../../assets/catalog/advertising/bing/authentication.png)

Klicka på **[!UICONTROL Create destination]**. Målet har skapats. Du kan klicka [!UICONTROL Save & Exit] om du vill aktivera segment senare eller klicka om du vill fortsätta med arbetsflödet och välja segment [!UICONTROL Next] som ska aktiveras. I båda fallen finns mer information i nästa avsnitt, [Aktivera segment](#activate-segments), för resten av arbetsflödet.

## Aktivera segment {#activate-segments}

Mer information om arbetsflödet för [aktivering finns i Aktivera profiler och segment till ett mål](../../ui/activate-destinations.md#select-attributes) .

I steget [Segmentschema](../../ui/activate-destinations.md#segment-schedule) måste du manuellt mappa dina segment till motsvarande ID eller egna namn i målet.

När du mappar segment rekommenderar vi att du använder [!DNL Platform] segmentnamnet eller en kortare form av det för att underlätta användningen. Segment-ID:t eller namnet i målet behöver dock inte matcha det i ditt [!DNL Platform] konto. Alla värden som du infogar i mappningsfältet återspeglas av målet.

![Segmentmappnings-ID](../../assets/common/segment-mapping-id.png)

## Exporterade data {#exported-data}

Kontrollera ditt [!DNL Microsoft Bing] konto om du vill verifiera om data har exporterats till [!DNL Microsoft Bing Ads] målet. Om aktiveringen lyckades fylls målgrupperna i ditt konto.