---
keywords: Experience Platform;hem;populära ämnen;Adobe Experience Platform;användarhandbok;användarhandbok;användarhandbok för plattformen;introduktion till plattformen;instrumentpanel;
solution: Experience Platform
title: Experience Platform - översikt
description: Adobe Experience Platform
exl-id: 47f9a3fb-731d-4ade-8069-faaa18f224dc
source-git-commit: 9844a7bf5e7198e7d5112ec924220aba71cdc14b
workflow-type: tm+mt
source-wordcount: '1880'
ht-degree: 0%

---

# Adobe Experience Platform UI Guide

Den här guiden är en introduktion till hur du använder Adobe Experience Platform användargränssnitt, förklarar vad de olika komponenterna används för och ger länkar till ytterligare dokumentation för mer information.

Mer information om Adobe Experience Platform finns i översikten [Experience Platform](home.md).

## Hemskärm

När du har loggat in på Adobe Experience Platform finns du på sidan [!UICONTROL Home], som består av avsnitten [metrics dashboard](#metrics), [recent data](#recent-data) och [recommended learning](#recommended-learning).

![](images/user-guide/homepage.png)

### Mätvärden

Kontrollpanelen för mätvärden innehåller kort som ger dig information om datauppsättningar, profiler, segment och mål inom organisationen.

![](images/user-guide/homepage-dashboard.png)

Avsnittet **[!UICONTROL Datasets]** visar antalet datauppsättningar i organisationen. Numret uppdateras när en ny datauppsättning skapas. Mer information om datauppsättningar finns i [översikten över datauppsättningar](../catalog/datasets/overview.md).

Avsnittet **[!UICONTROL Profiles]** visar det totala antalet personer med profiler inom organisationen, exklusive profilfragment. Det totala antalet personer representerar den totala adresserbara publiken och uppdateras en gång var 24:e timme. Mer information om profiler finns i [Översikt över kundprofiler i realtid](../profile/home.md).

Avsnittet **[!UICONTROL Segments]** visar det totala antalet segment som skapats i organisationen. Numret uppdateras när ett nytt segment skapas. Mer information om segment finns i [Översikt över segmenteringstjänsten](../segmentation/home.md).

Avsnittet **[!UICONTROL Destinations]** visar det totala antalet mål som skapats för organisationen. Numret uppdateras när ett nytt mål skapas. Mer information om mål finns i [målöversikten](../destinations/home.md).

### Senaste data

Den senaste datapanelen innehåller information om nyligen skapade datauppsättningar, källor, segment och mål.

![](images/user-guide/homepage-recent.png)

I avsnittet **[!UICONTROL Recent datasets]** visas de fem senast skapade datauppsättningarna i din organisation. Den här listan uppdateras varje gång en ny datauppsättning skapas. Du kan välja en datauppsättning från listan för att visa Du kan hitta mer information om den angivna datauppsättningen eller välja **[!UICONTROL View all]** för att visa en lista över alla skapade datauppsättningar. Mer information om datauppsättningar finns i [översikten över datauppsättningar](../catalog/datasets/overview.md).

I avsnittet **[!UICONTROL Recent sources]** visas de fem senast skapade källanslutningarna i din organisation. Listan uppdateras varje gång en ny källkoppling skapas. Du kan välja en källanslutning i listan för att visa Du kan hitta mer information om den angivna kopplingen eller välja **[!UICONTROL View all]** för att visa en lista över alla skapade källanslutningar. Du hittar mer information om källor i [Källöversikten](../sources/home.md).

I avsnittet **[!UICONTROL Recent segments]** visas de fem senast skapade segmentdefinitionerna i din organisation. Listan uppdateras varje gång en ny segmentdefinition skapas. Du kan välja en segmentdefinition i listan för att visa Du kan hitta mer information om den angivna segmentdefinitionen eller välja **[!UICONTROL View all]** för att visa en lista över alla skapade segmentdefinitioner. Mer information om segment finns i [Översikt över segmenteringstjänsten](../segmentation/home.md).

I avsnittet **[!UICONTROL Recent destinations]** visas de fem senast skapade destinationerna i din organisation. Listan uppdateras varje gång ett nytt mål skapas. Du kan välja ett mål i listan för att visa Du kan hitta mer information om det angivna målet eller välja **[!UICONTROL View all]** för att visa en lista över alla skapade mål. Mer information om mål finns i [målöversikten](../destinations/home.md).

### Rekommenderad utbildning

Avsnittet **[!UICONTROL Recommended learning]** innehåller länkar till användbar dokumentation för att komma igång med Adobe Experience Platform.

![](images/user-guide/homepage-recommended.png)

## Övre navigeringsfältet

I det övre navigeringsfältet i plattformsgränssnittet visas den organisation som du är inloggad på och det finns flera viktiga kontroller.

Till vänster i navigeringsfältet finns Adobe Experience Platform logotyp. När du väljer den här logotypen kommer du tillbaka till startskärmen för användargränssnittet för plattformen.

![](./images/user-guide/homepage-top-nav-bar.png)

### Organisationsväljare

Det första objektet till höger om det övre navigeringsfältet är **Organisationsväljaren**.

![](./images/user-guide/homepage-ims-org-switcher.png)

När du väljer väljaren öppnas en listruta med organisationer som du har tillgång till, om det finns några. Om du vill byta till en annan organisation väljer du ett alternativ i listan.

### Byt program

Nästa objekt till höger om den översta navigeringen är **programväljaren**, som representeras av ikonen ![för programväljaren](/help/images/icons/apps.png) . När du väljer den här ikonen kan du växla mellan olika Adobe-program som din organisation har tillgång till, till exempel Experience Platform, Analytics, Assets och andra.

### Hjälp

Till höger om programväljaren finns **hjälp- och supportmenyn** som representeras av ikonen ![frågetecken/hjälp](/help/images/icons/help.png) . När du väljer den här ikonen visas en snabbmeny med flera hjälp- och supportresurser. Fliken **[!UICONTROL Help]** visar en lista med relevant dokumentation för sidan som du för närvarande är på. På fliken **[!UICONTROL Support]** kan du skapa en supportanmälan med Adobe supportteam. På fliken **[!UICONTROL Feedback]** kan du skicka feedback om Platform till Adobe.

![](images/user-guide/homepage-help-clicked.png)

### Meddelanden och meddelanden

I **meddelandeavsnittet**, som representeras av ikonen ![bell/Notifications and Announcements](/help/images/icons/bell.png) . Fliken **[!UICONTROL Notifications]** visar viktig information om produkten och andra relevanta uppdateringar, medan fliken **[!UICONTROL Announcements]** visar information om serviceunderhåll.

### Användarprofil

Det sista objektet i det övre navigeringsfältet är **användarinställningarna**, som representeras av ikonen ![användarinställningar/användarprofil](images/user-guide/profile-icon.png) . Välj den här ikonen om du vill redigera dina inställningar eller logga ut.

Du kan växla mellan det ljusa och mörka temat för plattformsgränssnittet med växeln som finns precis nedanför ditt namn och din e-postadress. Välj det tema du föredrar.

![](images/theme.png)

### Sandlådor

Direkt nedanför det övre navigeringsfältet finns sandlådefältet. I det här fältet visas vilken sandlåda du använder för plattformen. Mer information om sandlådor finns i [översikten över sandlådor](../sandboxes/home.md).

## Vänster navigering {#left-nav}

Navigeringen till vänster på skärmen visar alla olika tjänster som stöds i plattformsgränssnittet.

Klicka på menyikonen för att visa eller dölja den vänstra navigeringspanelen.

![](images/user-guide/hidemenu.png)

Du kan låsa navigeringen i den öppna positionen genom att klicka igen när panelen har visats.

>[!IMPORTANT]
>
>I det vänstra navigeringsfältet visas bara de funktioner som du har tillgång till. I tidigare versioner av Adobe Experience Platform inaktiverades otillgängliga objekt. Kontakta systemadministratören om du anser att du bör ha åtkomst till ett avsnitt som inte visas.

![](images/user-guide/homepage-left.png)

I avsnittet **[!UICONTROL Home]** kan du gå tillbaka till startsidan för plattformsgränssnittet.

I avsnittet **[!UICONTROL Workflows]** visas en lista med arbetsflöden i flera steg för att utföra åtgärder inom plattformen. Mer information om arbetsflöden finns i [översikten över arbetsflöden](./workflows.md).

### [!UICONTROL Connections]

I avsnittet **[!UICONTROL Sources]** kan du skapa, uppdatera och ta bort källanslutningar så att du kan importera data från externa källor till plattformen. Du hittar mer information om källor i [Källöversikten](../sources/home.md).

I avsnittet **[!UICONTROL Destinations]** kan du skapa, uppdatera och ta bort mål, så att du kan exportera data från plattformen till många externa mål. Mer information om mål finns i [målöversikten](../destinations/home.md).

### [!UICONTROL Customer]

I avsnittet **[!UICONTROL Profiles]** kan du bläddra bland kundprofiler, visa profilmått, skapa och hantera sammanfogningsprinciper och visa fackliga scheman. Läs [[!DNL Profile] användarhandboken](../profile/ui/user-guide.md) om du vill veta mer om hur du använder avsnittet [!UICONTROL Profiles]. Mer information om kundprofilen i realtid finns i [Översikt över kundprofilen i realtid](../profile/home.md).

I avsnittet **[!UICONTROL Audiences]** kan du skapa och hantera segmentdefinitioner. Läs [användarhandboken för segmentering](../segmentation/ui/overview.md) om du vill veta mer om hur du använder avsnittet [!UICONTROL Audiences]. Mer information om segmenteringstjänsten finns i [Översikt över segmenteringstjänsten](../segmentation/home.md).

I avsnittet **[!UICONTROL Identities]** kan du skapa och hantera identitetsnamnutrymmen. Mer information om avsnittet [!UICONTROL Identities], inklusive information om identitetsnamnutrymmen och hur du använder identiteter i plattformsgränssnittet, finns i [översikten över identitetsnamnrymden](../identity-service/features/namespaces.md).

### [!UICONTROL Privacy]

I avsnittet **[!UICONTROL Policies]** kan du skapa och hantera dataanvändningsprinciper. Läs användarhandboken för [dataanvändningsprinciper](../data-governance/policies/user-guide.md) om du vill veta mer om hur du använder avsnittet Profiler. Mer information om dataanvändningsprinciper finns i [översikten över dataanvändningsprinciper](../data-governance/policies/overview.md).

I avsnittet **[!UICONTROL Requests]** kan du skapa och hantera sekretessförfrågningar. Observera att du måste vara tillåtslista för att få tillgång till Privacy Servicens användargränssnitt. Mer information om hur du använder avsnittet med förfrågningar finns i användarhandboken för [Privacy Servicen](../privacy-service/ui/user-guide.md). Mer information om Privacy Service finns i [Privacy Servicen overview](../privacy-service/home.md).

### [!UICONTROL Data Science]

Avsnittet **[!UICONTROL Notebooks]** ger åtkomst till JupyterLab, en interaktiv utvecklingsmiljö där du kan utforska, analysera och modellera data. Läs användarhandboken för [JupyterLab](../data-science-workspace/jupyterlab/overview.md) om du vill veta mer om hur du använder avsnittet Anteckningsböcker. Mer information om Data Science Workspace finns i [Översikt över Data Science Workspace](../data-science-workspace/home.md)

I avsnittet **[!UICONTROL Models]** kan du använda maskininlärning och artificiell intelligens för att skapa, utveckla, utbilda och trimma modeller för att göra prognoser. Du hittar mer information om modellavsnittet i självstudiekursen om [utbildning och utvärderar modellen](../data-science-workspace/models-recipes/train-evaluate-model-ui.md).

I avsnittet **[!UICONTROL Services]** kan du hantera dina publicerade modeller för schemalagd utbildning och poängsättning, eller använda Adobe Intelligent Services, en uppsättning AI-tjänster som levererar personaliserade kundupplevelser i realtid. Du hittar mer information om tjänstavsnittet i [Publicera en modell som en självstudiekurs](../data-science-workspace/models-recipes/publish-model-service-ui.md).

### [!UICONTROL Data management]

I avsnittet **[!UICONTROL Schemas]** kan du skapa och hantera XDM-scheman (Experience Data Model). Om du vill veta mer om scheman kan du läsa självstudiekursen om att [skapa ett schema](../xdm/tutorials/create-schema-ui.md). Mer information om XDM finns i [XDM-systemöversikt](../xdm/home.md).

I avsnittet **[!UICONTROL Datasets]** kan du skapa och hantera datauppsättningar. Mer information om datauppsättningar finns i användarhandboken för [datauppsättningar](../catalog/datasets/user-guide.md).

I avsnittet **[!UICONTROL Queries]** kan du skapa och hantera frågor, logga SQL-frågor som skapats av Adobe Experience Platform Query Service och visa dina [!DNL PostgreSQL]-autentiseringsuppgifter. Mer information om frågor finns i användarhandboken för [frågetjänsten](../query-service/ui/overview.md).

I avsnittet **[!UICONTROL Monitoring]** kan du övervaka inmatning av grupper och strömning. Mer information om övervakning finns i användarhandboken för [övervakning av datainhämtning](../ingestion/quality/monitor-data-ingestion.md).

### [!UICONTROL Federated data] (begränsad tillgänglighet)

I avsnittet **[!UICONTROL Models]** kan du utforma och skapa datamodeller och scheman som definierar datastrukturen, relationerna och begränsningarna. Mer information om datamodeller och scheman finns i användarhandboken [Federated Audience Composition](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/config/datamodel/schemas).

Avsnittet **[!UICONTROL Audit trail]** innehåller en detaljerad och kronologisk post för alla åtgärder och händelser som har utförts i din miljö i realtid. Du hittar mer information om granskningsspåret i användarhandboken för [Federated Audience Composition](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/audit-trail/audit-trail).


I avsnittet **[!UICONTROL Federated databases]** kan du ansluta Adobe Experience Platform till ditt företagsdatalager. Mer information om anslutning till federerade databaser finns i användarhandboken [Federated Audience Composition](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/config/federated-db).

>[!AVAILABILITY]
>
>Federated Audience Composition är för närvarande bara tillgängligt för en uppsättning organisationer (begränsad tillgänglighet). Kontakta din Adobe-representant om du vill veta mer.

### [!UICONTROL Decisioning]

Adobe Journey Optimizer är en programtjänst som är byggd ovanpå Experience Platform. Ni kan använda kraftfulla beslutstekniker för att leverera det bästa erbjudandet och upplevelsen till era kunder via alla kontaktytor vid rätt tidpunkt. Om du vill veta mer om Journey Optimizer, inklusive hur du arbetar med [!UICONTROL Offers] och [!UICONTROL Activities] kan du gå till [Journey Optimizer-dokumentationen](https://experienceleague.adobe.com/docs/journey-optimizer.html).

### [!UICONTROL Administration]

Användargränssnittet för plattformen (UI) är en kontrollpanel där du kan visa viktig information om din organisations licensanvändning, som den har hämtats under en ögonblicksbild. Gå till den här instrumentpanelen genom att välja **[!UICONTROL License usage]** i navigeringen. Mer information om kontrollpanelen för licensanvändning finns i handboken [för licensanvändning](./license-usage-and-guardrails/license-usage-dashboard.md).

>[!IMPORTANT]
>
>Kontrollpanelsfunktionen för licensanvändning är för närvarande alfabetisk och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

## Nästa steg

Genom att läsa den här guiden har du nu introducerats på startsidan och viktiga navigeringselement i användargränssnittet för plattformen. Mer detaljerad information om hur du arbetar i användargränssnittet finns i dokumentationen för respektive plattformstjänst. Länkar till den här dokumentationen finns i det [vänstra navigeringsavsnittet](#left-nav) som hittades tidigare i det här dokumentet.
