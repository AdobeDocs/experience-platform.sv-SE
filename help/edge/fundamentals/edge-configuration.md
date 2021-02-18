---
title: Skapa en Edge-konfiguration för Experience Platform Web SDK
description: 'Lär dig hur du konfigurerar Experience Platform Edge-nätverket. '
keywords: konfiguration;edge;edge configuration id;Environment Settings;edgeConfigId;identity;id sync enabled;ID Sync Container ID;Sandbox;Streaming Inlet;Event Dataset;target;client code;Property Token;Target Environment ID;Cookie Destinations;url Destinations;Analytics Settings Blockreport suite id;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 0%

---


# Skapa en kantkonfiguration

Konfigurationen för Adobe Experience Platform Web SDK är uppdelad på två platser. [konfigurationskommandot](configuring-the-sdk.md) i SDK styr saker som måste hanteras på klienten, till exempel `edgeDomain`. Edge-konfigurationen hanterar all annan konfiguration för SDK. När en begäran skickas till Adobe Experience Platform Edge Network används `edgeConfigId` för att referera till konfigurationen på serversidan. På så sätt kan du uppdatera konfigurationen utan att behöva göra kodändringar på webbplatsen.

Din organisation måste etableras för den här funktionen. Kontakta din Customer Success Manager (CSM) för att komma igång med tillåtelselista.

## Skapa en Edge-konfiguration

Kantkonfigurationer kan skapas i Adobe [!DNL Experience Platform Launch] med hjälp av edge-konfigurationsverktyget.

![navigering för konturkonfigurationsverktyg](../../assets/edge_configuration_nav.png)

>[!NOTE]
>
>Kunder på tillåtelselista kan använda kantkonfigurationsverktyget oavsett om de använder [!DNL Experience Platform Launch] som tagghanterare eller inte. Dessutom kräver användare framkallningsbehörighet i [!DNL Experience Platform Launch]. Mer information finns i artikeln [Användarbehörigheter](https://docs.adobe.com/content/help/en/launch/using/reference/admin/user-permissions.html) i [!DNL Experience Platform Launch]-dokumentationen.

Skapa en kantkonfiguration genom att klicka på **[!UICONTROL New Edge Configuration]** i skärmens övre högra del. När du har angett ett namn och en beskrivning ombeds du ange standardinställningarna för varje miljö. Tillgängliga inställningar anges nedan.

När du skapar en kantkonfiguration skapas automatiskt tre miljöer med identiska inställningar. Dessa tre miljöer är *dev*, *stage* och *prod*. De matchar de tre standardmiljöerna i [!DNL Experience Platform Launch]. När du skapar ett [!DNL Experience Platform Launch]-bibliotek i en dev-miljö använder biblioteket automatiskt dev-miljön från din konfiguration. Du kan redigera inställningar i enskilda miljöer så mycket du vill.

Det ID som används i SDK som `edgeConfigId` är ett sammansatt ID som anger konfigurationen och miljön (till exempel `1c86778b-cdba-4684-9903-750e52912ad1:stage`). Om det inte finns någon miljö i det sammansatta ID:t (till exempel `stage` i föregående exempel) används produktionsmiljön.

Här nedan hittar du de tillgängliga inställningarna för varje konfigurationsmiljö. De flesta avsnitt kan aktiveras eller inaktiveras. Inställningarna sparas men är inte aktiva när de är inaktiverade.

## [!UICONTROL Identity] Inställningar

Identitetsavsnittet är det enda avsnitt som alltid är på. Det finns två tillgängliga inställningar: &quot;[!UICONTROL ID Syncs Enabled]&quot; och &quot;[!UICONTROL ID Sync Container ID]&quot;.

![Identitetsavsnittet i konfigurationsgränssnittet](../../assets/edge_configuration_identity.png)

### [!UICONTROL ID Sync Enabled]

Styr huruvida SDK utför identitetssynkroniseringar med tredjepartspartners eller inte.

### [!UICONTROL ID Sync Container ID]

ID-synkroniseringar kan grupperas i behållare så att olika ID-synkroniseringar kan köras vid olika tidpunkter. Detta styr vilken behållare för ID-synkronisering som körs för ett givet konfigurations-ID.

## Adobe Experience Platform-inställningar

Med inställningarna som anges här kan du skicka data till Adobe Experience Platform. Du bör bara aktivera det här avsnittet om du har köpt Adobe Experience Platform.

![Adobe Experience Platform inställningsblock](../../assets/edge_configuration_aep.png)

### [!UICONTROL Sandbox]

Sandlådor är platser i Adobe Experience Platform som gör att kunderna kan isolera sina data och implementeringar från varandra. Mer information om hur de fungerar finns i [dokumentationen till sandlådor](../../sandboxes/home.md).

### [!UICONTROL Streaming Inlet]

Ett inlopp för direktuppspelning är en HTTP-källa i Adobe Experience Platform. Dessa skapas under fliken [!UICONTROL Sources] i Adobe Experience Platform som ett HTTP-API.

### [!UICONTROL Event Dataset]

Edge-konfigurationer har stöd för att skicka data till datauppsättningar som har ett schema av klassen [!UICONTROL Experience Event].

## Adobe Target-inställningar

Om du vill konfigurera Adobe Target måste du ange en klientkod. De andra fälten är valfria.

![Adobe Target inställningsblock](../../assets/edge_configuration_target.png)

>[!NOTE]
>
>Organisationen som är associerad med klientkoden måste matcha organisationen där konfigurations-ID skapas.

### [!UICONTROL Client Code]

Unikt ID för ett målkonto. Du hittar detta genom att navigera till [!UICONTROL Adobe Target] > [!UICONTROL Setup]> [!UICONTROL Implementation] > [!UICONTROL edit settings] bredvid knappen [!UICONTROL download] för antingen [!UICONTROL at.js] eller [!UICONTROL mbox.js]

### [!UICONTROL Property Token]

[!DNL Target] låter kunderna styra behörigheter genom att använda egenskaper. Mer information finns i avsnittet [Enterprise Permissions](https://docs.adobe.com/content/help/en/target/using/administer/manage-users/enterprise/properties-overview.html) i [!DNL Target]-dokumentationen.

Egenskapstoken finns i [!UICONTROL Adobe Target] > [!UICONTROL setup] > [!UICONTROL Properties]

### [!UICONTROL Target Environment ID]

[Med ](https://docs.adobe.com/content/help/en/target/using/administer/hosts.html) Adobe Target kan du hantera implementeringen i alla utvecklingsfaser. Den här inställningen anger vilken miljö du ska använda för varje miljö.

Adobe rekommenderar att du anger detta annorlunda för var och en av edge-konfigurationsmiljöerna `dev`, `stage` och `prod` för att göra saker och ting enkla. Om du redan har definierat Adobe Target-miljöer kan du använda dessa.

## Adobe Audience Manager-inställningar

Allt som behövs för att skicka data till Adobe Audience Manager är att aktivera det här avsnittet. De andra inställningarna är valfria men rekommenderas.

![Inställningsblock för hantering av målgruppshantering i Adobe](../../assets/edge_configuration_aam.png)

### [!UICONTROL Cookie Destinations Enabled]

Tillåter SDK att dela segmentinformation via [Cookie-mål](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) från [!DNL Audience Manager].

### [!UICONTROL URL Destinations Enabled]

Tillåter SDK att dela segmentinformation via [URL-mål](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html). Dessa konfigureras i [!DNL Audience Manager].

## Adobe Analytics-inställningar

Kontrollerar om data skickas till Adobe Analytics. Ytterligare information finns i [Analysöversikt](../data-collection/adobe-analytics/analytics-overview.md).

![Adobe Analytics Settings Block](../../assets/edge_configuration_aa.png)

### [!UICONTROL Report Suite ID]

Rapportsviten finns i avsnittet Adobe Analytics Admin under [!UICONTROL Admin > ReportSuites]. Om flera rapportsviter anges kopieras data till varje rapportserie.
