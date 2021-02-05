---
keywords: Reklam. skrivbordet,
title: The Trade Desk Connection Destination
description: 'Trade Desk är en självbetjäningsplattform för annonsköpare som kan genomföra återannonsering och målgruppsanpassade digitala kampanjer för olika annonser, videoklipp och mobila inventeringskällor. '
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---


# [!DNL The Trade Desk] anslutning

[!DNL The Trade Desk] mål hjälper dig att skicka profildata till  [!DNL The Trade Desk].

[!DNL The Trade Desk] är en självbetjäningsplattform för annonsköpare som vill genomföra återannonsering och målgruppsanpassade digitala kampanjer för alla annonser, videoklipp och mobila inventeringskällor.

Om du vill skicka profildata till [!DNL The Trade Desk] måste du först ansluta till målet.

## Målspecifikationer {#destination-specs}

Observera följande information som är specifik för [!DNL The Trade Desk]-målet:

* Du kan skicka följande [identiteter](../../../identity-service/namespaces.md) till [!DNL The Trade Desk] mål: [!DNL The Trade Desk ID], [!DNL IDFA], [!DNL GAID].

## Användningsfall {#use-cases}

Som marknadsförare vill jag kunna använda segment som är inbyggda i [!DNL Trade Desk IDs] eller enhets-ID:n för att skapa återmarknadsföring eller målgruppsanpassade digitala kampanjer.

## Exporttyp {#export-type}

**[!DNL Segment export]** - du exporterar alla medlemmar i ett segment (publik) till målet.

## Anslut till målet {#connect-destination}

I **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** väljer du [!DNL The Trade Desk] och väljer **[!UICONTROL Configure]**.

![Konfigurera Trade Desk-målet](../../assets/catalog/advertising/tradedesk/configure.png)

>[!NOTE]
>
>Om det redan finns en anslutning till det här målet kan du se en **[!UICONTROL Activate]**-knapp på målkortet. Mer information om skillnaden mellan **[!UICONTROL Activate]** och **[!UICONTROL Configure]** finns i avsnittet [Katalog](../../ui/destinations-workspace.md#catalog) i dokumentationen för målarbetsytan.
>
>![Aktivera målet för handelsavdelningen](../../assets/catalog/advertising/tradedesk/activate.png)

I steget [!UICONTROL Authentication] måste du ange [!DNL The Trade Desk] anslutningsinformation:

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Account ID]**: Din [!DNL Trade Desk] [!UICONTROL Account ID].
* **[!UICONTROL Client Secret]**: Den  `clientSecret` parameter som används i  [!DNL OAuth2] klientautentiseringsuppgifterna.
* **[!UICONTROL Server Location]**: Fråga din  [!DNL The Trade Desk] representant vilken regional server du ska använda. Det här är de tillgängliga regionala servrarna du kan välja mellan:

   * **[!UICONTROL Europe]**
   * **[!UICONTROL Singapore]**
   * **[!UICONTROL Tokyo]**
   * **[!UICONTROL North America East]**
   * **[!UICONTROL North America West]**
   * **[!UICONTROL Latin America]**

* **[!UICONTROL Marketing use case]**: Fall av marknadsanvändning anger avsikten för vilken data ska exporteras till destinationen. Du kan välja bland Adobe-definierade användningsfall för marknadsföring eller skapa ett eget marknadsföringsexempel. Mer information om användningsfall för marknadsföring finns på sidan [Datastyrning i Adobe Experience Platform](../../../data-governance/policies/overview.md). Mer information om de enskilda Adobe-definierade användningsfallen för marknadsföring finns i [Översikt över dataanvändningsprinciper](../../../data-governance/policies/overview.md).

![The Trade Desk Authentication Step](../../assets/catalog/advertising/tradedesk/authenticate.png)

Klicka på **[!UICONTROL Create destination]**. Målet har skapats. Du kan klicka på [!UICONTROL Save & Exit] om du vill aktivera segment senare eller välja [!UICONTROL Next] om du vill fortsätta arbetsflödet och välja segment som ska aktiveras. I båda fallen ska du läsa nästa avsnitt, [Aktivera segment](#activate-segments), för resten av arbetsflödet.

## Aktivera segment {#activate-segments}

Mer information om arbetsflödet för segmentaktivering finns i [Aktivera profiler och segment till ett mål](../../ui/activate-destinations.md#select-attributes).

I steget [Segmentschema](../../ui/activate-destinations.md#segment-schedule) måste du manuellt mappa dina segment till deras motsvarande ID eller egna namn i målet.

När du mappar segment rekommenderar vi att du använder segmentnamnet [!DNL Platform] eller en kortare form av det för att underlätta användningen. Segment-ID:t eller namnet i målet behöver dock inte matcha det i ditt [!DNL Platform]-konto. Alla värden som du infogar i mappningsfältet återspeglas av målet.

Om du använder flera enhetsmappningar (cookie-ID, [!DNL IDFA], [!DNL GAID]) måste du använda samma mappningsvärde för alla tre mappningarna. [!DNL The Trade Desk] sammanfogar alla till ett enda segment med en uppdelning på enhetsnivå.

![Segmentmappnings-ID](../../assets/common/segment-mapping-id.png)

## Exporterade data {#exported-data}

Kontrollera ditt [!DNL The Trade Desk]-konto om du vill verifiera om data har exporterats till [!DNL The Trade Desk]-målet. Om aktiveringen lyckades fylls målgrupperna i ditt konto.
