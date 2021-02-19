---
keywords: datastyrning rtcdp;rtcdp datastyrning;datastyrning i realtid för kunddataprofil
title: Datastyrning - översikt
seo-title: Datastyrning i kunddataplattformen i realtid
description: 'Med datastyrning kan ni hantera kunddata och säkerställa att ni följer regler, begränsningar och policyer som gäller för dataanvändning. '
seo-description: 'Med datastyrning kan ni hantera kunddata och säkerställa att ni följer regler, begränsningar och policyer som gäller för dataanvändning. '
translation-type: tm+mt
source-git-commit: 5435661d750c4138ea6a2d40619a48236b7b1e4f
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 0%

---


# [!DNL Data Governance] i realtid CDP

[!DNL Real-time Customer Data Platform] (CDP i realtid) sammanför data från olika affärssystem så att marknadsförarna bättre kan identifiera, förstå och engagera sina kunder. Dessa data kan vara föremål för användarbegränsningar som fastställts av din organisation eller av juridiska bestämmelser. Därför är det viktigt att se till att CDP i realtid är kompatibelt med användningsprinciper när data hanteras.

Med Adobe Experience Platform [!DNL Data Governance] kan ni hantera kunddata och säkerställa efterlevnad av regler, begränsningar och policyer som gäller för dataanvändning. Det spelar en viktig roll inom CDP i realtid, så att ni kan definiera användarprofiler, kategorisera data baserat på dessa policyer och kontrollera om policyer har överträtts när ni utför vissa marknadsföringsåtgärder.

CDP för realtid är byggt på Adobe Experience Platform och därför beskrivs merparten av [!DNL Data Governance]-funktionerna i [!DNL Experience Platform]-dokumentationen. Det här dokumentet är avsett att komplettera [datastyrningsöversikten](../../data-governance/home.md) för [!DNL Experience Platform] och visar de styrningsfunktioner som finns i CDP i realtid. Följande ämnen behandlas:

* [Använd användningsetiketter på dina data](#labels)
* [Hantera dataanvändningsprinciper](#policies)
* [Klara regelefterlevnaden](#enforce)

## Använd användningsetiketter på dina data {#labels}

[!DNL Data Governance] gör att du kan använda användningsetiketter på dina data, antingen på datauppsättnings- eller datamängdsfältnivå. Med etiketter för dataanvändning kan du kategorisera data enligt de användarprofiler som gäller för dessa data.

Mer information om hur du arbetar med dataanvändningsetiketter finns i användarhandboken [för dataanvändningsetiketter](../../data-governance/labels/overview.md) för Adobe Experience Platform.

## Konfigurera marknadsföringsåtgärder för mål {#destinations}

Du kan ange begränsningar för dataanvändning för ett mål genom att definiera marknadsföringsåtgärder (kallas även för användningsfall för marknadsföring) för det målet. En marknadsföringsåtgärd för ett mål anger avsikten med de data som ska exporteras till det målet.

>[!NOTE]
>
>Mer information om marknadsföringsåtgärder och hur de används i dataanvändningsprinciper finns i [översikten över dataanvändningsprinciper](../../data-governance/policies/overview.md) i [!DNL Experience Platform]-dokumentationen.

Genom att definiera marknadsföringsåtgärder för destinationer kan ni se till att profiler och segment som skickas till dessa destinationer följer dataanvändningsprinciperna. Ni bör därför lägga till lämpliga marknadsföringsåtgärder till era destinationer baserat på organisationens behov av att tillämpa policybegränsningar för aktivering.

Marknadsföringsåtgärder kan bara väljas när du ställer in ett mål för första gången. Beroende på vilken typ av mål du arbetar med visas möjligheten att konfigurera marknadsföringsåtgärder vid olika tillfällen i konfigurationsarbetsflödet. Se [måldokumentationen](../destinations/overview.md) för steg om hur du konfigurerar ditt särskilda mål.

## Hantera dataanvändningsprinciper {#policies}

För att dataanvändningsetiketter effektivt ska kunna stödja regelefterlevnad måste dataanvändningsprinciper definieras och aktiveras. Dataanvändningspolicyer är regler som beskriver den typ av marknadsföringsåtgärder som du tillåts eller begränsas från att utföra på data inom CDP i realtid. Mer information finns i avsnittet &quot;Dataanvändningsprinciper&quot; i [!DNL Experience Platform] [Datastyrningsöversikt](../../data-governance/home.md).

Adobe Experience Platform har flera principer för vanliga kundupplevelsefall. Du kan visa dessa profiler i användargränssnittet genom att gå till arbetsytan **[!UICONTROL Policies]** och välja fliken **[!UICONTROL Browse]**. I [användarhandboken för profiler](../../data-governance/policies/user-guide.md) i [!DNL Experience Platform]-dokumentationen finns mer detaljerad information om hur du arbetar med principer i användargränssnittet, inklusive hur du skapar egna principer.

## Genomför regelefterlevnad för dataanvändning {#enforce}

När data har märkts och användarprofiler har definierats kan ni se till att dataanvändningen följer reglerna. När målgruppssegment aktiveras till mål i realtid-CDP, tillämpar [!DNL Data Governance] automatiskt användarprofiler om överträdelser inträffar.

Mer information finns i dokumentet om [automatisk policytillämpning](../../data-governance/enforcement/auto-enforcement.md).

## Nästa steg

Nu när du har introducerats till nyckelfunktionerna [!DNL Data Governance] för CDP i realtid och hur [!DNL Experience Platform] aktiverar dem kan du fortsätta med [dokumentationen för datastyrning på Adobe Experience Platform](../../data-governance/home.md). Dokumentationen innehåller översikter av viktiga [!DNL Data Governance]-koncept samt stegvisa arbetsflöden för att hantera etiketter och policyer för dataanvändning.

I följande video visas en översikt över [!DNL Data Governance] i CDP i realtid, inklusive användningen av användningsfall för marknadsföring på destinationer och exempelarbetsflöden för olika scenarier:

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)