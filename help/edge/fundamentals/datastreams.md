---
title: Konfigurera ditt datastream för Experience Platform Web SDK
description: 'Lär dig hur du konfigurerar datastreams. '
keywords: konfiguration;datastreams;datastreamId;edge;datastream id;Environment Settings;edgeConfigId;identity;id sync enabled;ID Sync Container ID;Sandbox;Streaming Inlet;Event Dataset;target;client code;Property Token;Target Environment ID;Cookie Destinations;url Destinations;Analytics Settings Blockreport suite;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 1ff52944be6e9475f57c62793b0e4c671ff8786b
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Konfigurera ett datastream

Konfigurationen för Adobe Experience Platform Web SDK är uppdelad på två platser. The [konfigurera, kommando](configuring-the-sdk.md) i SDK styr saker som måste hanteras på klienten, som `edgeDomain`. Datastreams hanterar alla andra konfigurationer för SDK. När en begäran skickas till Adobe Experience Platform Edge Network `edgeConfigId` används för att referera till konfigurationen på serversidan. På så sätt kan du uppdatera konfigurationen utan att behöva göra kodändringar på webbplatsen.

Din organisation måste etableras för den här funktionen. Kontakta din Customer Success Manager (CSM) för att komma igång med tillåtelselista.

## Skapa en datastream-konfiguration

Du kan skapa och hantera datastammar i användargränssnittet för datainsamling genom att välja **[!UICONTROL Datastreams]** i den vänstra navigeringen.

![navigering för datastreams-verktyg](../images/datastreams/config.png)

>[!NOTE]
>
>Medan du kan komma åt [!UICONTROL Datastreams] oavsett om du använder plattformens tagghanteringsfunktioner eller inte måste du ha utvecklarbehörighet för att kunna hantera dataströmmar själva. Se [användarbehörigheter](../../tags/ui/administration/user-permissions.md) artikel i taggdokumentationen om du vill ha mer information.

Skapa ett datastream genom att klicka på **[!UICONTROL New Datastream]** i skärmens övre högra hörn. När du har angett ett namn och en beskrivning ombeds du ange standardinställningarna för varje miljö. Tillgängliga inställningar anges nedan.

När du skapar en datastream skapas tre miljöer automatiskt med identiska inställningar. Dessa tre miljöer *dev*, *stage* och *prod*. De matchar de tre standardmiljöerna för taggar. När du skapar ett taggbibliotek i en utvecklingsmiljö använder biblioteket automatiskt dev-miljön från din konfiguration. Du kan redigera inställningar i enskilda miljöer så mycket du vill.

Det ID som används i SDK som `edgeConfigId` är ett sammansatt ID som anger konfigurationen och miljön (till exempel `1c86778b-cdba-4684-9903-750e52912ad1:stage`). Om det inte finns någon miljö i det sammansatta ID:t (till exempel `stage` i föregående exempel) används produktionsmiljön.

Nedan visas de tillgängliga inställningarna för varje konfigurationsmiljö. De flesta avsnitt kan aktiveras eller inaktiveras. Inställningarna sparas men är inte aktiva när de är inaktiverade.

## [!UICONTROL Third Party ID] inställningar

Avsnittet med tredje parts-ID är det enda avsnitt som alltid är aktivt. Det finns två tillgängliga inställningar: &quot;[!UICONTROL Third Party ID Sync Enabled]&quot; och &quot;[!UICONTROL Third Party ID Sync Container ID]&quot;.

![Identitetsavsnittet i konfigurationsgränssnittet](../images/datastreams/edge_configuration_identity.png)

### [!UICONTROL Third Party ID Sync Enabled]

Styr huruvida SDK utför identitetssynkroniseringar med tredjepartspartners eller inte.

### [!UICONTROL Third Party ID Sync Container ID]

ID-synkroniseringar kan grupperas i behållare så att olika ID-synkroniseringar kan köras vid olika tidpunkter. Detta styr vilken behållare för ID-synkronisering som körs för ett givet konfigurations-ID.

## Adobe Experience Platform-inställningar

Med inställningarna som anges här kan du skicka data till Adobe Experience Platform. Du bör bara aktivera det här avsnittet om du har köpt Adobe Experience Platform.

![Adobe Experience Platform inställningsblock](../images/datastreams/platform-config.png)

| Fält | Beskrivning |
| --- | --- |
| [!UICONTROL Sandbox] | **(Obligatoriskt)** Välj den plattformssandlåda som du vill skicka data till. Sandlådor är virtuella partitioner i Adobe Experience Platform som gör att du kan isolera data och implementeringar från andra i din organisation.<br><br>Om du skapar en datastam utan att markera en sandlåda kan du fortfarande markera en sandlåda senare.<br><br>När en datastream har skapats och en sandlåda har markerats går det inte att ändra sandlådan. The [!UICONTROL Sandbox] markeringsfältet är därför inte tillgängligt när du redigerar en befintlig datastam med en markerad sandlåda.<br><br> The [!UICONTROL Sandbox] markeringsfältet är därför inte tillgängligt när du redigerar ett befintligt datastream.<br><br>Mer information om sandlådornas roll i Experience Platform finns i [dokumentation för sandlådor](../../sandboxes/home.md). |
| [!UICONTROL Event Dataset] | **(Obligatoriskt)** Välj den plattformsdatauppsättning som kundhändelsedata ska direktuppspelas till. Det här schemat måste använda [Klassen XDM ExperienceEvent](../../xdm/classes/experienceevent.md). |
| [!UICONTROL Profile Dataset] | Välj den plattformsdatauppsättning som kundattributdata ska skickas till. Det här schemat måste använda [Klassen XDM Individuell profil](../../xdm/classes/individual-profile.md). |
| [!UICONTROL Offer Decisioning] | Markera den här kryssrutan om du vill aktivera Offer decisioning för en implementering av en Platform Web SDK. Se guiden [använda Offer decisioning med Platform Web SDK](../personalization/offer-decisioning/offer-decisioning-overview.md) om du vill ha mer information om implementeringen. Mer information om Offer decisioning finns i [Adobe Journey Optimizer-dokumentation](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started/starting-offer-decisioning.html). |
| [!UICONTROL Edge Segmentation] | Markera den här kryssrutan för att aktivera [kantsegmentering](../../segmentation/ui/edge-segmentation.md) för denna datastream. När Platform Web SDK skickar data via en datastam som är aktiverad för kantsegmentering, skickas alla uppdaterade segmentmedlemskap för den aktuella profilen tillbaka som svar.<br><br>Det här alternativet kan användas i kombination med [!UICONTROL Personalization Destinations] for [exempel på användning av personalisering på nästa sida](../../destinations/ui/configure-personalization-destinations.md). |
| [!UICONTROL Personalization Destinations] | Vid användning i kombination med [!UICONTROL Edge Segmentation] kan datastream ansluta till personaliseringsmotorer som Adobe Target. Se måldokumentationen för specifika steg om [konfigurera personaliseringsmål](../../destinations/ui/configure-personalization-destinations.md). |

## Adobe Target-inställningar

Om du vill konfigurera Adobe Target måste du ange en klientkod. De andra fälten är valfria.

![Adobe Target inställningsblock](../images/datastreams/edge_configuration_target.png)

>[!NOTE]
>
>Organisationen som är associerad med klientkoden måste matcha organisationen där konfigurations-ID skapas.

### [!UICONTROL Client Code]

Unikt ID för ett målkonto. Om du vill hitta det här kan du navigera till [!UICONTROL Adobe Target] > [!UICONTROL Setup]> [!UICONTROL Implementation] > [!UICONTROL edit settings] bredvid [!UICONTROL download] knapp för [!UICONTROL at.js] eller [!UICONTROL mbox.js]

### [!UICONTROL Property Token]

[!DNL Target] låter kunderna styra behörigheter genom att använda egenskaper. Mer information finns i [Enterprise permissions](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html) i [!DNL Target] dokumentation.

Egenskapstoken finns i [!UICONTROL Adobe Target] > [!UICONTROL setup] > [!UICONTROL Properties]

### [!UICONTROL Target Environment ID]

[Miljö](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) i Adobe Target hjälper er att hantera implementeringen i alla utvecklingsfaser. Den här inställningen anger vilken miljö du ska använda för varje miljö.

Adobe rekommenderar att du anger detta på olika sätt för var och en av dina `dev`, `stage`och `prod` datastream-miljöer för att hålla saker och ting enkla. Om du redan har definierat Adobe Target-miljöer kan du använda dessa.

## Adobe Audience Manager-inställningar

Allt som behövs för att skicka data till Adobe Audience Manager är att aktivera det här avsnittet. De andra inställningarna är valfria men rekommenderas.

![Inställningsblock för hantering av målgruppshantering i Adobe](../images/datastreams/edge_configuration_aam.png)

### [!UICONTROL Cookie Destinations Enabled]

Gör att SDK kan dela segmentinformation via [Cookie-destinationer](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) från [!DNL Audience Manager].

### [!UICONTROL URL Destinations Enabled]

Gör att SDK kan dela segmentinformation via [URL-mål](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html). Dessa konfigureras i [!DNL Audience Manager].

## Adobe Analytics-inställningar

Kontrollerar om data skickas till Adobe Analytics. Mer information finns i [Analysöversikt](../data-collection/adobe-analytics/analytics-overview.md).

![Adobe Analytics Settings Block](../images/datastreams/edge_configuration_aa.png)

### [!UICONTROL Report Suite ID]

Rapportsviten finns i avsnittet Adobe Analytics Admin under [!UICONTROL Admin > ReportSuites]. Om flera rapportsviter anges kopieras data till varje rapportserie.
