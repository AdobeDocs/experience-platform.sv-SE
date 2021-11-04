---
keywords: datastyrning rtcdp;rtcdp datastyrning;datastyrning i realtid för kunddataprofil
title: Datastyrning - översikt
seo-title: Data Governance in Real-time Customer Data Platform
description: 'Med datastyrning kan ni hantera kunddata och säkerställa att ni följer regler, begränsningar och policyer som gäller för dataanvändning. '
seo-description: Data Governance allows you to manage customer data and ensure compliance with regulations, restrictions, and policies applicable to data use.
exl-id: eb501d85-cabd-4667-a1cd-2210ec83fb71
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---

# Datastyrning i realtid CDP

[!DNL Real-time Customer Data Platform] (CDP i realtid) sammanför data från olika affärssystem så att marknadsförarna bättre kan identifiera, förstå och engagera sina kunder. Dessa data kan vara föremål för användarbegränsningar som fastställts av din organisation eller av juridiska bestämmelser. Därför är det viktigt att se till att CDP i realtid är kompatibelt med användningsprinciper när data hanteras.

Med Adobe Experience Platform Data Governance kan ni hantera kunddata och säkerställa att ni följer regler, begränsningar och policyer som gäller för dataanvändning. Det spelar en viktig roll inom CDP i realtid, så att ni kan definiera användarprofiler, kategorisera data baserat på dessa policyer och kontrollera om policyer har överträtts när ni utför vissa marknadsföringsåtgärder.

CDP i realtid är byggt på Adobe Experience Platform och därför omfattas merparten av datastyrningsfunktionerna i [!DNL Experience Platform] dokumentation. Detta dokument är avsett att komplettera [Datastyrning - översikt](../../data-governance/home.md) for [!DNL Experience Platform]och sammanfattar de styrningsfunktioner som finns i CDP i realtid. Följande ämnen behandlas:

* [Använd användningsetiketter på dina data](#labels)
* [Hantera dataanvändningsprinciper](#policies)
* [Klara regelefterlevnaden](#enforce)

## Använd användningsetiketter på dina data {#labels}

Med datastyrning kan du använda användningsetiketter på dina data, antingen på datamängdsnivå eller datamängdsfältnivå. Med etiketter för dataanvändning kan du kategorisera data enligt de användarprofiler som gäller för dessa data.

Mer information om hur du arbetar med dataanvändningsetiketter finns i [användarhandbok för dataanvändningsrubriker](../../data-governance/labels/overview.md) för Adobe Experience Platform.

## Konfigurera marknadsföringsåtgärder för mål {#destinations}

Du kan ange begränsningar för dataanvändning för ett mål genom att definiera marknadsföringsåtgärder (kallas även för användningsfall för marknadsföring) för det målet. En marknadsföringsåtgärd för ett mål anger avsikten med de data som ska exporteras till det målet.

>[!NOTE]
>
>Mer information om marknadsföringsåtgärder och hur de används i dataanvändningspolicyer finns i [dataanvändningsprinciper - översikt](../../data-governance/policies/overview.md) i [!DNL Experience Platform] dokumentation.

Genom att definiera marknadsföringsåtgärder för destinationer kan ni se till att profiler och segment som skickas till dessa destinationer följer dataanvändningsprinciperna. Ni bör därför lägga till lämpliga marknadsföringsåtgärder till era destinationer baserat på organisationens behov av att tillämpa policybegränsningar för aktivering.

Marknadsföringsåtgärder kan bara väljas när du ställer in ett mål för första gången. Beroende på vilken typ av mål du arbetar med visas möjligheten att konfigurera marknadsföringsåtgärder vid olika tillfällen i konfigurationsarbetsflödet. Se [destinationsdokumentation](../destinations/overview.md) för steg om hur du konfigurerar ditt särskilda mål.

## Hantera dataanvändningsprinciper {#policies}

För att dataanvändningsetiketter effektivt ska kunna stödja regelefterlevnad måste dataanvändningsprinciper definieras och aktiveras. Dataanvändningspolicyer är regler som beskriver den typ av marknadsföringsåtgärder som du tillåts eller begränsas från att utföra på data inom CDP i realtid. Se avsnittet &quot;Dataanvändningsprinciper&quot; i [!DNL Experience Platform] [Datastyrning - översikt](../../data-governance/home.md) för mer information.

Adobe Experience Platform har flera principer för vanliga kundupplevelsefall. Dessa profiler kan visas i användargränssnittet genom att gå till **[!UICONTROL Policies]** arbetsytan och välja **[!UICONTROL Browse]** -fliken. Se [användarhandbok](../../data-governance/policies/user-guide.md) i [!DNL Experience Platform] om du vill ha mer detaljerad information om hur du arbetar med profiler i användargränssnittet, inklusive hur du skapar egna anpassade profiler.

## Klara regelefterlevnaden {#enforce}

När data har märkts och användarprofiler har definierats kan ni se till att dataanvändningen följer reglerna. När målgruppssegment aktiveras till mål i realtid-CDP tillämpar Data Governance automatiskt användningspolicyer om det inträffar några överträdelser.

Visa dokumentet på [automatisk policytillämpning](../../data-governance/enforcement/auto-enforcement.md) för mer information.

## Nästa steg

Nu när du har introducerats till de viktigaste funktionerna för datastyrning i CDP i realtid och hur [!DNL Experience Platform] aktiverar dem, fortsätt [dokumentation för datastyrning för Adobe Experience Platform](../../data-governance/home.md). Dokumentationen innehåller översikter över viktiga datastyrningsbegrepp samt stegvisa arbetsflöden för hantering av etiketter och policyer för dataanvändning.

I följande video visas en översikt över datastyrning i CDP i realtid, inklusive användning av marknadsföringsfall på destinationer och exempelarbetsflöden för olika scenarier:

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)
