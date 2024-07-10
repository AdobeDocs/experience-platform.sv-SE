---
keywords: Experience Platform;hem;populära ämnen;Adobe Experience Platform;användarhandbok;användarhandbok;användarhandbok för plattformen;introduktion till plattformen;instrumentpanel;
solution: Experience Platform
title: Experience Platform - översikt
description: Adobe Experience Platform
exl-id: 47f9a3fb-731d-4ade-8069-faaa18f224dc
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1735'
ht-degree: 0%

---

# Adobe Experience Platform UI Guide

Den här guiden är en introduktion till hur du använder Adobe Experience Platform användargränssnitt, förklarar vad de olika komponenterna används för och ger länkar till ytterligare dokumentation för mer information.

Läs mer om Adobe Experience Platform i [Experience Platform - översikt](home.md).

## Hemskärm

När du har loggat in på Adobe Experience Platform finns du på [!UICONTROL Home] som består av [instrumentpanel för mätvärden](#metrics), [senaste data](#recent-data)och [rekommenderad utbildning](#recommended-learning) -avsnitt.

![](images/user-guide/homepage.png)

### Mätvärden

Kontrollpanelen för mätvärden innehåller kort som ger dig information om datauppsättningar, profiler, segment och mål inom organisationen.

![](images/user-guide/homepage-dashboard.png)

The **[!UICONTROL Datasets]** -avsnittet visar antalet datauppsättningar inom organisationen. Numret uppdateras när en ny datauppsättning skapas. Mer information om datauppsättningar finns i [datauppsättningar, översikt](../catalog/datasets/overview.md).

The **[!UICONTROL Profiles]** visar det totala antalet personer med profiler inom organisationen, exklusive profilfragment. Det totala antalet personer representerar den totala adresserbara publiken och uppdateras en gång var 24:e timme. Mer information om profiler finns i [Översikt över kundprofiler i realtid](../profile/home.md).

The **[!UICONTROL Segments]** visar det totala antalet segment som har skapats i organisationen. Numret uppdateras när ett nytt segment skapas. Mer information om segment finns i [Översikt över segmenteringstjänsten](../segmentation/home.md).

The **[!UICONTROL Destinations]** visar det totala antalet destinationer som skapats för organisationen. Numret uppdateras när ett nytt mål skapas. Mer information om destinationer finns i [destinationer, översikt](../destinations/home.md).

### Senaste data

Den senaste datapanelen innehåller information om nyligen skapade datauppsättningar, källor, segment och mål.

![](images/user-guide/homepage-recent.png)

The **[!UICONTROL Recent datasets]** i listas de fem senast skapade datauppsättningarna i din organisation. Den här listan uppdateras varje gång en ny datauppsättning skapas. Du kan välja en datauppsättning i listan om du vill visa mer information om den angivna datauppsättningen eller välja **[!UICONTROL View all]** om du vill se en lista över alla skapade datauppsättningar. Mer information om datauppsättningar finns i [datauppsättningar, översikt](../catalog/datasets/overview.md).

The **[!UICONTROL Recent sources]** i listas de fem senast skapade källanslutningarna i din organisation. Listan uppdateras varje gång en ny källkoppling skapas. Du kan välja en källanslutning i listan om du vill visa mer information om den angivna kopplingen eller välja **[!UICONTROL View all]** om du vill se en lista över alla skapade källanslutningar. Mer information om källor finns i [källöversikt](../sources/home.md).

The **[!UICONTROL Recent segments]** i listas de fem senast skapade segmentdefinitionerna i din organisation. Listan uppdateras varje gång en ny segmentdefinition skapas. Du kan välja en segmentdefinition i listan om du vill visa mer information om den angivna segmentdefinitionen eller välja **[!UICONTROL View all]** om du vill se en lista över alla segmentdefinitioner som har skapats. Mer information om segment finns i [Översikt över segmenteringstjänsten](../segmentation/home.md).

The **[!UICONTROL Recent destinations]** i listas de fem senast skapade destinationerna inom din organisation. Listan uppdateras varje gång ett nytt mål skapas. Du kan välja ett mål i listan om du vill visa mer information om det angivna målet eller välja **[!UICONTROL View all]** om du vill se en lista över alla destinationer som skapats. Mer information om destinationer finns i [destinationer, översikt](../destinations/home.md).

### Rekommenderad utbildning

The **[!UICONTROL Recommended learning]** innehåller länkar till användbar dokumentation för att komma igång med Adobe Experience Platform.

![](images/user-guide/homepage-recommended.png)

## Övre navigeringsfältet

I det övre navigeringsfältet i plattformsgränssnittet visas den organisation som du är inloggad på och det finns flera viktiga kontroller.

Till vänster i navigeringsfältet finns Adobe Experience Platform logotyp. När du väljer den här logotypen kommer du tillbaka till startskärmen för användargränssnittet för plattformen.

![](./images/user-guide/homepage-top-nav-bar.png)

### Organisationsväljare

Det första objektet till höger i det övre navigeringsfältet är **Organisationsväljare**.

![](./images/user-guide/homepage-ims-org-switcher.png)

När du väljer väljaren öppnas en listruta med organisationer som du har tillgång till, om det finns några. Om du vill byta till en annan organisation väljer du ett alternativ i listan.

### Byt program

Nästa objekt till höger om den översta navigeringen är **programväljare**, som representeras av ![programväljare](./images/user-guide/app-switcher-icon.png) -ikon. När du väljer den här ikonen kan du växla mellan olika Adobe-program som din organisation har tillgång till, till exempel Experience Platform, Analytics, Assets och andra.

### Hjälp

Till höger om programväljaren finns **hjälp- och supportmeny**, som representeras av ![frågetecken/hjälp](./images/user-guide/help-icon.png) -ikon. När du väljer den här ikonen visas en snabbmeny med flera hjälp- och supportresurser. The **[!UICONTROL Help]** -fliken visar en lista med relevant dokumentation för sidan som du är på. The **[!UICONTROL Support]** kan du skapa en supportanmälan med Adobe supportteam. The **[!UICONTROL Feedback]** kan du skicka feedback om Platform till Adobe.

![](images/user-guide/homepage-help-clicked.png)

### Meddelanden och meddelanden

I **meddelandesektion**, som representeras av ![klockor/meddelanden och meddelanden](images/user-guide/notification-icon.png) -ikon. The **[!UICONTROL Notifications]** -fliken visar viktig information om produkten och andra relevanta uppdateringar, medan **[!UICONTROL Announcements]** -fliken visar information om serviceunderhåll.

### Användarprofil

Det sista objektet i navigeringsfältet är **användarinställningar**, som representeras av ![användarinställningar/användarprofil](images/user-guide/profile-icon.png) -ikon. Välj den här ikonen om du vill redigera dina inställningar eller logga ut.

Du kan växla mellan det ljusa och mörka temat för plattformsgränssnittet med växeln som finns precis nedanför ditt namn och din e-postadress. Välj det tema du föredrar.

![](images/theme.png)

### Sandlådor

Direkt nedanför det övre navigeringsfältet finns sandlådefältet. I det här fältet visas vilken sandlåda du använder för plattformen. Mer information om sandlådor finns i [översikt över sandlådor](../sandboxes/home.md).

## Vänster navigering {#left-nav}

Navigeringen till vänster på skärmen visar alla olika tjänster som stöds i plattformsgränssnittet.

Klicka på menyikonen för att visa eller dölja den vänstra navigeringspanelen.

![](images/user-guide/hidemenu.png)

Du kan låsa navigeringen i den öppna positionen genom att klicka igen när panelen har visats.

>[!IMPORTANT]
>
>I det vänstra navigeringsfältet visas bara de funktioner som du har tillgång till. I tidigare versioner av Adobe Experience Platform inaktiverades otillgängliga objekt. Kontakta systemadministratören om du anser att du bör ha åtkomst till ett avsnitt som inte visas.

![](images/user-guide/homepage-left.png)

The **[!UICONTROL Home]** kan du gå tillbaka till startsidan för användargränssnittet för plattformen.

The **[!UICONTROL Workflows]** I visas en lista med arbetsflöden i flera steg för att utföra åtgärder inom plattformen. Mer information om arbetsflöden finns i [arbetsflöden översikt](./workflows.md).

### [!UICONTROL Connections]

The **[!UICONTROL Sources]** kan du skapa, uppdatera och ta bort källanslutningar, så att du kan importera data från externa källor till Platform. Mer information om källor finns i [källöversikt](../sources/home.md).

The **[!UICONTROL Destinations]** kan du skapa, uppdatera och ta bort mål, så att du kan exportera data från Platform till många externa mål. Mer information om destinationer finns i [destinationer, översikt](../destinations/home.md).

### [!UICONTROL Customer]

The **[!UICONTROL Profiles]** kan du bläddra bland kundprofiler, visa profilvärden, skapa och hantera sammanfogningspolicyer och visa unionens scheman. Mer information om hur du använder [!UICONTROL Profiles] läs [[!DNL Profile] användarhandbok](../profile/ui/user-guide.md). Mer information om kundprofilen i realtid finns i [Översikt över kundprofiler i realtid](../profile/home.md).

The **[!UICONTROL Audiences]** kan du skapa och hantera segmentdefinitioner. Mer information om hur du använder [!UICONTROL Audiences] läs [segmenteringsanvändarhandbok](../segmentation/ui/overview.md). Mer information om segmenteringstjänsten finns i [Översikt över segmenteringstjänsten](../segmentation/home.md).

The **[!UICONTROL Identities]** I kan du skapa och hantera identitetsnamnutrymmen. Mer information om [!UICONTROL Identities] och information om identitetsnamnutrymmen och hur du använder identiteter i plattformsgränssnittet finns i [Översikt över namnutrymmet identity](../identity-service/features/namespaces.md).

### [!UICONTROL Privacy]

The **[!UICONTROL Policies]** kan du skapa och hantera dataanvändningsprinciper. Mer information om hur du använder avsnittet Profiler finns i [användarhandbok för dataanvändningsprinciper](../data-governance/policies/user-guide.md). Mer information om dataanvändningsprinciper finns i [dataanvändningsprinciper - översikt](../data-governance/policies/overview.md).

The **[!UICONTROL Requests]** kan du skapa och hantera sekretessförfrågningar. Observera att du måste vara tillåtslista för att få tillgång till Privacy Servicens användargränssnitt. Läs mer om hur du använder avsnittet med förfrågningar i [Användarhandbok för Privacy Service](../privacy-service/ui/user-guide.md). Mer information om Privacy Service finns i [Översikt över Privacy Servicen](../privacy-service/home.md).

### [!UICONTROL Data Science]

The **[!UICONTROL Notebooks]** -avsnittet ger åtkomst till JupyterLab, en interaktiv utvecklingsmiljö där du kan utforska, analysera och modellera data. Mer information om hur du använder anteckningsböcker finns i [Användarhandbok för JupyterLab](../data-science-workspace/jupyterlab/overview.md). Mer information om Data Science Workspace finns i [Data Science Workspace - översikt](../data-science-workspace/home.md)

The **[!UICONTROL Models]** kan du använda maskininlärning och artificiell intelligens för att skapa, utveckla, utbilda och trimma modeller för att göra prognoser. Mer information om modellavsnittet finns i självstudiekursen om [utbilda och utvärdera en modell](../data-science-workspace/models-recipes/train-evaluate-model-ui.md).

The **[!UICONTROL Services]** kan ni hantera era publicerade modeller för schemalagd utbildning och poängsättning, eller använda Adobe Intelligent Services, en uppsättning AI-tjänster som levererar personaliserade kundupplevelser i realtid. Mer information om tjänstavsnittet finns i [Publicera en modell som en självstudiekurs om tjänster](../data-science-workspace/models-recipes/publish-model-service-ui.md).

### [!UICONTROL Data management]

The **[!UICONTROL Schemas]** kan du skapa och hantera XDM-scheman (Experience Data Model). Läs självstudiekursen om du vill veta mer om scheman [skapa ett schema](../xdm/tutorials/create-schema-ui.md). Mer information om XDM finns i [XDM - systemöversikt](../xdm/home.md).

The **[!UICONTROL Datasets]** kan du skapa och hantera datauppsättningar. Mer information om datauppsättningar finns i [användarhandbok för datauppsättningar](../catalog/datasets/user-guide.md).

The **[!UICONTROL Queries]** kan du skapa och hantera frågor, logga SQL-frågor som har gjorts av Adobe Experience Platform Query Service och visa [!DNL PostgreSQL] autentiseringsuppgifter. Mer information om frågor finns i [Användarhandbok för frågetjänsten](../query-service/ui/overview.md).

The **[!UICONTROL Monitoring]** kan du övervaka inmatning av grupper och direktuppspelning. Mer information om övervakning finns i [användarhandbok för övervakning av dataöverföring](../ingestion/quality/monitor-data-ingestion.md).

### [!UICONTROL Decisioning]

Adobe Journey Optimizer är en programtjänst som är byggd ovanpå Experience Platform. Ni kan använda kraftfulla beslutstekniker för att leverera det bästa erbjudandet och upplevelsen till era kunder via alla kontaktytor vid rätt tidpunkt. Läs mer om Journey Optimizer, inklusive att arbeta med [!UICONTROL Offers] och [!UICONTROL Activities] gå till [Journey Optimizer-dokumentation](https://experienceleague.adobe.com/docs/journey-optimizer.html).

### [!UICONTROL Administration]

Användargränssnittet för plattformen (UI) är en kontrollpanel där du kan visa viktig information om din organisations licensanvändning, som den har hämtats under en ögonblicksbild. Gå till den här instrumentpanelen genom att välja **[!UICONTROL License usage]** i navigeringen. Mer information om kontrollpanelen för licensanvändning finns på [kontrollpanel för licensanvändning](./license-usage-and-guardrails/license-usage-dashboard.md).

>[!IMPORTANT]
>
>Kontrollpanelsfunktionen för licensanvändning är för närvarande alfabetisk och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

## Nästa steg

Genom att läsa den här guiden har du nu introducerats på startsidan och viktiga navigeringselement i användargränssnittet för plattformen. Mer detaljerad information om hur du arbetar i användargränssnittet finns i dokumentationen för respektive plattformstjänst. Länkar till denna dokumentation finns i [vänster navigering](#left-nav) tidigare i det här dokumentet.
