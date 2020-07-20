---
title: Konfiguration av Edge
seo-title: Edge-konfiguration för Experience Platform Web SDK
description: 'Lär dig hur du konfigurerar Experience Platform Edge-nätverket. '
seo-description: 'Lär dig hur du konfigurerar Experience Platform Edge-nätverket. '
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 1%

---


# Konfigurera Edge

Konfigurationen för Adobe Experience Platform [!DNL Web SDK] delas mellan två platser. Kommandot [](configuring-the-sdk.md) configure i SDK styr saker som måste hanteras på klienten, till exempel `edgeDomain`. Edge-konfigurationen hanterar all annan konfiguration för SDK. När en begäran skickas till Adobe Experience Platform [!DNL Edge Network]används den för att `edgeConfigId` referera till konfigurationen på serversidan. På så sätt kan du uppdatera konfigurationen utan att behöva göra kodändringar på webbplatsen.

## Skapa ett Edge Configuration ID

Konfiguration-ID för Edge kan skapas i Adobe [!DNL Launch] med hjälp av edge-konfigurationsverktyget. Med det här verktyget kan du skapa både edge-konfigurationen och miljöer i dessa konfigurationer.

![navigering för konturkonfigurationsverktyg](../../assets/edge_configuration_nav.png)

>[!NOTE]
>
>
>
>Kunder på tillåtelselista kan använda kantkonfigurationsverktyget oavsett om de använder [!DNL Launch] som tagghanterare eller inte. Dessutom kräver användare framkallningsbehörigheter i [!DNL Launch]. Mer information finns i artikeln [Användarbehörigheter](https://docs.adobe.com/content/help/en/launch/using/reference/admin/user-permissions.html) i [!DNL Launch] dokumentationen.

Du kan skapa en kantkonfiguration genom att klicka på **[!UICONTROL New Edge Configuration]** i skärmens övre högra hörn. När du har angett ett namn och en beskrivning ombeds du ange standardinställningarna för varje miljö.

### Standardmiljöinställningar

Dessa standardinställningar används för att skapa de tre första miljöerna med identiska inställningar. Dessa tre miljöer är *dev*, *stage* och *prod*. De matchar de tre standardmiljöerna i [!DNL Launch]. När du skapar ett [!DNL Launch] bibliotek till en utvecklingsmiljö använder biblioteket automatiskt dev-miljön från din konfiguration. Du kan redigera inställningar i enskilda miljöer så mycket du vill.

Det ID som används i SDK som `edgeConfigId` är ett sammansatt ID som anger konfigurationen och miljön. Om ingen miljö finns används produktionsmiljön.

### Miljöinställningar

Nedan finns alla inställningar som är tillgängliga för en miljö. De flesta avsnitt kan aktiveras eller inaktiveras. Inställningarna sparas men är inte aktiva när de är inaktiverade.

#### [!UICONTROL Identity]

Identitetsavsnittet är det enda avsnitt som alltid är på. Det finns två tillgängliga inställningar: [!UICONTROL ID Syncs Enabled] och [!UICONTROL ID Sync Container ID].

![Identitetsavsnittet i konfigurationsgränssnittet](../../assets/edge_configuration_identity.png)

##### [!UICONTROL ID Sync Enabled]

Styr huruvida SDK utför identitetssynkroniseringar med tredjepartspartners eller inte.

##### [!UICONTROL ID Sync Container ID]

ID-synkroniseringar kan grupperas i behållare så att olika ID-synkroniseringar kan köras vid olika tidpunkter. Detta styr vilken behållare för ID-synkronisering som körs för ett givet konfigurations-ID.

#### Adobe Experience Platform

Med inställningarna som anges här kan du skicka data till Adobe Experience Platform. Du bör bara aktivera det här avsnittet om du har köpt Adobe Experience Platform.

![Adobe Experience Platform-inställningsblock](../../assets/edge_configuration_aep.png)

##### [!UICONTROL Sandbox]

Sandlådor är platser i Adobe Experience Platform som gör att kunderna kan isolera sina data och implementeringar från varandra. Mer information om hur de fungerar finns i dokumentationen [för](../../sandboxes/home.md)sandlådor.

##### [!UICONTROL Streaming Inlet]

Ett inlopp för direktuppspelning är en HTTP-källa i Adobe Experience Platform. Dessa skapas under fliken [!UICONTROL Sources] i Adobe Experience Platform som ett HTTP-API.

##### [!UICONTROL Event Dataset]

Edge-konfigurationer har stöd för att skicka data till datauppsättningar som har ett klassschema [!UICONTROL Experience Event].

#### Adobe Target

Om du vill konfigurera Adobe Target måste du ange en klientkod. De andra fälten är valfria.

![Adobe Target-inställningsblock](../../assets/edge_configuration_target.png)

>[!NOTE]
>
>
>
>Organisationen som är associerad med klientkoden måste matcha organisationen där konfigurations-ID skapas.

##### [!UICONTROL Client Code]

Unikt ID för ett målkonto. Du hittar detta genom att navigera till [!UICONTROL Adobe Target] > [!UICONTROL Setup]> [!UICONTROL Implementation] > [!UICONTROL edit settings] bredvid [!UICONTROL download] knappen för antingen [!UICONTROL at.js] eller [!UICONTROL mbox.js]

##### [!UICONTROL Property Token]

[!DNL Target] låter kunderna styra behörigheter genom att använda egenskaper. Mer information finns under [Enterprise Permissions](https://docs.adobe.com/content/help/en/target/using/administer/manage-users/enterprise/properties-overview.html) (Enterprise-behörigheter) i [!DNL Target] dokumentationen.

Egenskapstoken finns i [!UICONTROL Adobe Target] > [!UICONTROL setup] > [!UICONTROL Properties]

##### [!UICONTROL Target Environment ID]

[Med miljöer](https://docs.adobe.com/content/help/en/target/using/administer/hosts.html) i Adobe Target kan ni hantera implementeringen i alla utvecklingsfaser. Den här inställningen anger vilken miljö du ska använda för varje miljö.

Adobe rekommenderar att du ställer in detta på olika sätt för var och en av dina `dev`- `stage`och `prod` edge-konfigurationsmiljöer för att göra det enkelt. Om du redan har [!UICONTROL Adobe Target environments] definierat dem kan du använda dem.

#### Adobe Audience Manager

Allt som behövs för att skicka data till Adobe Audience Manager är att aktivera det här avsnittet. De andra inställningarna är valfria men rekommenderas.

![Inställningsblocket Adobe Audience Manage](../../assets/edge_configuration_aam.png)

##### [!UICONTROL Cookie Destinations Enabled]

Gör att SDK kan dela segmentinformation via [cookie-mål](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) från [!DNL Audience Manager].

##### [!UICONTROL URL Destinations Enabled]

Tillåter SDK att dela segmentinformation via [URL-mål](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html). Dessa är konfigurerade i [!DNL Audience Manager].

#### Adobe Analytics

Kontrollerar om data skickas till Adobe Analytics. Mer information finns i [Analytics Overview](../solution-specific/analytics/analytics-overview.md).

![Adobe Analytics Settings Block](../../assets/edge_configuration_aa.png)

##### [!UICONTROL Report Suite ID]

Rapportsviten finns i avsnittet Adobe Analytics Admin under [!UICONTROL Admin > ReportSuites]. Om flera rapportsviter anges kopieras data till varje rapportserie.
