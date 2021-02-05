---
keywords: Experience Platform;hem;populära ämnen;Adobe Experience Platform;användarhandbok;användarhandbok;användarhandbok för plattformen;introduktion till plattformen;instrumentpanel;
solution: Experience Platform
title: Experience Platform - översikt
topic: ui guide
description: 'Adobe Experience Platform '
translation-type: tm+mt
source-git-commit: 5575d5e45bddcc007dcf78720cd7a7e20475f78c
workflow-type: tm+mt
source-wordcount: '1695'
ht-degree: 0%

---


# Adobe Experience Platform UI Guide

Den här guiden är en introduktion till hur du använder Adobe Experience Platform användargränssnitt, förklarar vad de olika komponenterna används för och ger länkar till ytterligare dokumentation för mer information.

Läs översikten [Experience Platform](home.md) om du vill veta mer om Adobe Experience Platform.

## Hemskärm

När du har loggat in på Adobe Experience Platform finns du på [!UICONTROL Home]-sidan, som består av [metrics dashboard](#metrics), [nyligen använda data](#recent-data) och [rekommenderat utbildningsavsnitt](#recommended-learning).

![](images/user-guide/homepage.png)

### Mätvärden

Kontrollpanelen för mätvärden innehåller kort som ger dig information om datauppsättningar, profiler, segment och mål inom organisationen.

![](images/user-guide/homepage-dashboard.png)

Avsnittet **[!UICONTROL Datasets]** visar antalet datauppsättningar i IMS-organisationen. Numret uppdateras när en ny datauppsättning skapas. Mer information om datauppsättningar finns i översikten [över datauppsättningar](../catalog/datasets/overview.md).

I **[!UICONTROL Profiles]**-avsnittet visas det totala antalet personer med profiler inom IMS-organisationen, exklusive profilfragment. Det totala antalet personer representerar den totala adresserbara publiken och uppdateras en gång var 24:e timme. Mer information om profiler finns i [Kundprofilöversikt i realtid](../profile/home.md).

Avsnittet **[!UICONTROL Segments]** visar det totala antalet segment som skapats i IMS-organisationen. Numret uppdateras när ett nytt segment skapas. Mer information om segment finns i [Översikt över segmenteringstjänsten](../segmentation/home.md).

Avsnittet **[!UICONTROL Destinations]** visar det totala antalet mål som skapats för IMS-organisationen. Numret uppdateras när ett nytt mål skapas. Mer information om mål finns i [målöversikten](../destinations/home.md).

### Senaste data

Den senaste datapanelen innehåller information om nyligen skapade datauppsättningar, källor, segment och mål.

![](images/user-guide/homepage-recent.png)

I **[!UICONTROL Recent datasets]**-avsnittet visas de fem senast skapade datauppsättningarna i din IMS-organisation. Den här listan uppdateras varje gång en ny datauppsättning skapas. Du kan välja en datauppsättning i listan om du vill visa mer information om den angivna datauppsättningen eller välja **[!UICONTROL View all]** om du vill visa en lista över alla skapade datauppsättningar. Mer information om datauppsättningar finns i översikten [över datauppsättningar](../catalog/datasets/overview.md).

I **[!UICONTROL Recent sources]**-avsnittet visas de fem senast skapade källanslutningarna i IMS-organisationen. Listan uppdateras varje gång en ny källkoppling skapas. Du kan välja en källanslutning i listan om du vill visa mer information om den angivna kopplingen eller välja **[!UICONTROL View all]** om du vill se en lista över alla skapade källanslutningar. Mer information om källor finns i resursöversikten [](../sources/home.md).

I **[!UICONTROL Recent segments]**-avsnittet visas de fem senast skapade segmentdefinitionerna i din IMS-organisation. Listan uppdateras varje gång en ny segmentdefinition skapas. Du kan välja en segmentdefinition i listan om du vill visa mer information om den angivna segmentdefinitionen eller välja **[!UICONTROL View all]** om du vill se en lista över alla skapade segmentdefinitioner. Mer information om segment finns i [Översikt över segmenteringstjänsten](../segmentation/home.md).

I **[!UICONTROL Recent destinations]**-avsnittet visas de fem senast skapade destinationerna i din IMS-organisation. Listan uppdateras varje gång ett nytt mål skapas. Du kan välja ett mål i listan om du vill visa mer information om det angivna målet eller välja **[!UICONTROL View all]** om du vill se en lista över alla skapade mål. Mer information om mål finns i [målöversikten](../destinations/home.md).

### Rekommenderad utbildning

Avsnittet **[!UICONTROL Recommended learning]** innehåller länkar till användbar dokumentation för att komma igång med Adobe Experience Platform.

![](images/user-guide/homepage-recommended.png)

## Övre navigeringsfältet

Det övre navigeringsfältet i plattformsgränssnittet visar den IMS-organisation som du är inloggad på och innehåller flera viktiga kontroller.

Till vänster i navigeringsfältet finns Adobe Experience Platform logotyp. Om du väljer det här alternativet när som helst kommer du tillbaka till startskärmen för användargränssnittet för plattformen.

![](./images/user-guide/homepage-top-nav-bar.png)

### IMS-organisationsväljare

Det första objektet till höger om det övre navigeringsfältet är **IMS Organization-växlaren**.

![](./images/user-guide/homepage-ims-org.png)

Om du väljer väljaren öppnas en listruta med IMS-organisationer som du har tillgång till, om det finns några. Välj ett alternativ i listan för att växla till den IMS-organisationen.

![](./images/user-guide/homepage-ims-org-switcher.png)

### Byt program

Nästa objekt till höger om den översta navigeringen är **programväxlaren**, som representeras av ikonen ![programväljaren](./images/user-guide/app-switcher-icon.png). När du väljer den här ikonen kan du växla mellan de Adobe-program som din IMS-organisation har åtkomst till, till exempel Experience Platform, Analytics, Assets och Launch.

### Hjälp

Till höger om programväljaren finns **hjälp- och supportmenyn**, som representeras av ikonen ![frågetecken/hjälp](./images/user-guide/help-icon.png). När du väljer den här ikonen visas en snabbmeny med flera hjälp- och supportresurser. På fliken **[!UICONTROL Help]** visas en lista med relevant dokumentation för sidan som du är på. På fliken **[!UICONTROL Support]** kan du skapa en supportanmälan med Adobe supportteam. På fliken **[!UICONTROL Feedback]** kan du skicka feedback om Platform till Adobe.

![](images/user-guide/homepage-help-clicked.png)

### Meddelanden

I **meddelandeavsnittet**, som representeras av ikonen ![bell/Notifications and Announcements](images/user-guide/notification-icon.png). Fliken **[!UICONTROL Notifications]** visar viktig information om produkten och andra relevanta uppdateringar, medan fliken **[!UICONTROL Announcements]** visar information om serviceunderhåll.

### Användarprofil

Det sista objektet i det övre navigeringsfältet är **användarinställningarna**, som representeras av ikonen ![användarinställningar/Användarprofil](images/user-guide/profile-icon.png). Välj den här ikonen om du vill redigera dina inställningar eller logga ut.

### Sandlådor

Direkt nedanför det övre navigeringsfältet finns sandlådefältet. I det här fältet visas vilken sandlåda du använder för plattformen. Mer information om sandlådor finns i [översikten över sandlådor](../sandboxes/home.md).

## Vänster navigering {#left-nav}

Navigeringen till vänster på skärmen visar alla olika tjänster som stöds i plattformsgränssnittet.

>[!IMPORTANT]
>
>Vissa avsnitt i det vänstra navigeringsfältet kanske inte visas eller är nedtonade. Det beror på att du inte har tillgång till dessa funktioner. Kontakta systemadministratören om du anser att du bör ha tillgång till dessa avsnitt.

![](images/user-guide/homepage-left.png)

I **[!UICONTROL Home]**-avsnittet kan du gå tillbaka till startsidan för plattformsgränssnittet.

Avsnittet **[!UICONTROL Workflows]** innehåller en lista med arbetsflöden i flera steg för att utföra åtgärder inom plattformen. Mer information om arbetsflöden finns i översikten [arbetsflöden](./workflows.md).

### [!UICONTROL Connections]

I **[!UICONTROL Sources]**-avsnittet kan du skapa, uppdatera och ta bort källanslutningar, så att du kan importera data från externa källor till plattformen. Mer information om källor finns i resursöversikten [](../sources/home.md).

Med **[!UICONTROL Destinations]**-avsnittet kan du skapa, uppdatera och ta bort mål, så att du kan exportera data från plattformen till många externa mål. Mer information om mål finns i [målöversikten](../destinations/home.md).

### [!UICONTROL Customer]

I **[!UICONTROL Profiles]**-avsnittet kan du bläddra bland kundprofiler, visa profilmått, skapa och hantera sammanfogningspolicyer och visa unionskartor. Läs [[!DNL Profile] användarhandboken](../profile/ui/user-guide.md) om du vill veta mer om hur du använder avsnittet [!UICONTROL Profiles]. Mer information om kundprofil i realtid finns i [Kundprofilöversikt i realtid](../profile/home.md).

I **[!UICONTROL Segments]**-avsnittet kan du skapa och hantera segmentdefinitioner. Läs [användarhandboken för segmentering](../segmentation/ui/overview.md) om du vill veta mer om hur du använder avsnittet [!UICONTROL Segments]. Mer information om segmenteringstjänsten finns i [Översikt över segmenteringstjänsten](../segmentation/home.md).

I **[!UICONTROL Identities]**-avsnittet kan du skapa och hantera identitetsnamnutrymmen. Mer information om [!UICONTROL Identities]-avsnittet, inklusive information om identitetsnamnutrymmen och hur du använder identiteter i plattformsgränssnittet, finns i [översikten över identitetsnamnrymden](../identity-service/namespaces.md).

### [!UICONTROL Privacy]

I **[!UICONTROL Policies]**-avsnittet kan du skapa och hantera dataanvändningsprinciper. Läs [användarhandboken för dataanvändningsprinciper](../data-governance/policies/user-guide.md) om du vill veta mer om hur du använder avsnittet Profiler. Mer information om dataanvändningsprinciper finns i [översikten över dataanvändningsprinciper](../data-governance/policies/overview.md).

I **[!UICONTROL Requests]**-avsnittet kan du skapa och hantera sekretessförfrågningar. Observera att du måste vara tillåtslista för att få tillgång till Privacy Servicens användargränssnitt. Läs [användarhandboken för Privacy Service](../privacy-service/ui/user-guide.md) om du vill veta mer om hur du använder avsnittet med förfrågningar. Mer information om Privacy Service finns i [Privacy Servicen overview](../privacy-service/home.md).

### [!UICONTROL Data Science]

Avsnittet **[!UICONTROL Notebooks]** ger åtkomst till JupyterLab, en interaktiv utvecklingsmiljö där du kan utforska, analysera och modellera data. Läs [användarhandboken för JupyterLab](../data-science-workspace/jupyterlab/overview.md) om du vill veta mer om hur du använder avsnittet Anteckningsböcker. Mer information om arbetsytan Datavetenskap finns i [översikten över arbetsytan Datavetenskap](../data-science-workspace/home.md)

Med **[!UICONTROL Models]**-delen kan du utnyttja maskininlärning och artificiell intelligens för att skapa, utveckla, utbilda och trimma modeller för att göra prognoser. Mer information om modellavsnittet finns i självstudiekursen om [utbildning och utvärdering av en modell](../data-science-workspace/models-recipes/train-evaluate-model-ui.md).

Med **[!UICONTROL Services]**-sektionen kan du hantera publicerade modeller för schemalagd utbildning och poängsättning, eller utnyttja Adobe Intelligent Services, en uppsättning AI-tjänster som levererar personaliserade kundupplevelser i realtid. Mer information om tjänstavsnittet finns i [Publicera en modell som en självstudiekurs](../data-science-workspace/models-recipes/publish-model-service-ui.md).

### [!UICONTROL Data management]

I **[!UICONTROL Schemas]**-avsnittet kan du skapa och hantera XDM-scheman (Experience Data Model). Om du vill veta mer om scheman kan du läsa självstudiekursen om att [skapa ett schema](../xdm/tutorials/create-schema-ui.md). Mer information om XDM finns i [XDM-systemöversikt](../xdm/home.md).

Med **[!UICONTROL Datasets]**-avsnittet kan du skapa och hantera datauppsättningar. Mer information om datauppsättningar finns i [användarhandboken för datauppsättningar](../catalog/datasets/user-guide.md).

I **[!UICONTROL Queries]**-avsnittet kan du skapa och hantera frågor, logga SQL-frågor som skapats av Adobe Experience Platform Query Service och visa dina PostgreSQL-autentiseringsuppgifter. Mer information om frågor finns i [användarhandboken för frågetjänsten](../query-service/ui/overview.md).

Med **[!UICONTROL Monitoring]**-avsnittet kan du övervaka inmatning av grupper och strömning. Mer information om övervakning finns i [användarhandboken för övervakning av dataöverföring](../ingestion/quality/monitor-data-ingestion.md).

### [!UICONTROL Decisioning]

Offer Decisioning är en programtjänst som är integrerad med Adobe Experience Platform. Ni kan utnyttja Experience Platform för att leverera det bästa erbjudandet och upplevelsen till era kunder via alla kontaktytor vid rätt tidpunkt. Om du vill veta mer om Offer Decisioning, t.ex. om du arbetar med [!UICONTROL Offers] och [!UICONTROL Activities] går du till [Offer Decisioning dokumentation](https://experienceleague.adobe.com/docs/offer-decisioning.html).

### [!UICONTROL Administration]

Användargränssnittet för plattformen (UI) är en kontrollpanel där du kan visa viktig information om din organisations licensanvändning, som den har hämtats under en ögonblicksbild. Du kommer åt detta genom att välja **[!UICONTROL License usage]** i navigeringen. Mer information om kontrollpanelen för licensanvändning finns i handboken [på kontrollpanelen för licensanvändning](license-usage-dashboard.md).

>[!IMPORTANT]
>
>Kontrollpanelsfunktionen för licensanvändning är för närvarande alfabetisk och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

## Nästa steg

Genom att läsa den här guiden har du nu introducerats på startsidan och viktiga navigeringselement i användargränssnittet för plattformen. Mer detaljerad information om hur du arbetar i användargränssnittet finns i dokumentationen för respektive plattformstjänst. Länkar till den här dokumentationen finns i avsnittet [vänster navigering](#left-nav) som hittades tidigare i det här dokumentet.