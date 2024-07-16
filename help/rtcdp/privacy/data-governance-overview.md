---
keywords: datastyrning rtcdp;rtcdp datastyrning;datastyrning i realtid för kunddataprofil
title: Datastyrning - översikt
description: Med datastyrning kan ni hantera kunddata och säkerställa att ni följer regler, begränsningar och policyer som gäller för dataanvändning.
feature: Get Started, Data Governance
exl-id: eb501d85-cabd-4667-a1cd-2210ec83fb71
source-git-commit: 82535ec3ac2dd27e685bb591fdf661d3ab5dd2c9
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 0%

---

# Datastyrning i Real-Time CDP

[!DNL Adobe Real-Time Customer Data Platform] (Real-Time CDP) samlar data från flera företagssystem, vilket gör det möjligt för marknadsförarna att bättre identifiera, förstå och engagera sina kunder. Dessa data kan vara föremål för användarbegränsningar som fastställts av din organisation eller av juridiska bestämmelser. Därför är det viktigt att se till att Real-Time CDP följer användarreglerna när data hanteras.

Med Adobe Experience Platform Data Governance kan ni hantera kunddata och säkerställa att ni följer regler, begränsningar och policyer som gäller för dataanvändning. Den har en nyckelroll inom Real-Time CDP och gör det möjligt att definiera användarprofiler, kategorisera data baserat på dessa policyer och söka efter policyöverträdelser när ni utför vissa marknadsföringsåtgärder.

Real-Time CDP är byggt ovanpå Adobe Experience Platform och därför beskrivs de flesta datastyrningsfunktionerna i [!DNL Experience Platform]-dokumentationen. Det här dokumentet är avsett att komplettera [datastyrningsöversikten](../../data-governance/home.md) för [!DNL Experience Platform] och innehåller en översikt över de styrningsfunktioner som är tillgängliga i Real-Time CDP. Följande ämnen behandlas:

* [Använd användningsetiketter på dina data](#labels)
* [Hantera dataanvändningspolicyer](#policies)
* [Klara regelefterlevnaden](#enforce)

## Använd användningsetiketter på dina data {#labels}

Med datastyrning kan du använda användningsetiketter på dina data, antingen på datamängdsnivå eller datamängdsfältnivå. Med etiketter för dataanvändning kan du kategorisera data enligt de användarprofiler som gäller för dessa data.

Mer information om hur du arbetar med dataanvändningsetiketter finns i användarhandboken för [dataanvändningsetiketter](../../data-governance/labels/overview.md) för Adobe Experience Platform.

## Konfigurera marknadsföringsåtgärder för mål {#destinations}

Du kan ange begränsningar för dataanvändning för ett mål genom att definiera marknadsföringsåtgärder (kallas även för användningsfall för marknadsföring) för det målet. En marknadsföringsåtgärd för ett mål anger avsikten med de data som ska exporteras till det målet.

>[!NOTE]
>
>Mer information om marknadsföringsåtgärder och hur de används i dataanvändningsprinciper finns i [översikten över dataanvändningsprinciper](../../data-governance/policies/overview.md) i [!DNL Experience Platform]-dokumentationen.

Genom att definiera marknadsföringsåtgärder för destinationer kan ni se till att profiler och målgrupper som skickas till dessa destinationer följer dataanvändningsprinciperna. Ni bör därför lägga till lämpliga marknadsföringsåtgärder till era destinationer baserat på organisationens behov av att tillämpa policybegränsningar för aktivering.

Marknadsföringsåtgärder kan bara väljas när du ställer in ett mål för första gången. Beroende på vilken typ av mål du arbetar med visas möjligheten att konfigurera marknadsföringsåtgärder vid olika tillfällen i konfigurationsarbetsflödet. I [måldokumentationen](../destinations/overview.md) finns anvisningar om hur du konfigurerar ditt mål.

## Hantera dataanvändningspolicyer {#policies}

För att dataanvändningsetiketter effektivt ska kunna stödja regelefterlevnad måste dataanvändningsprinciper definieras och aktiveras. Dataanvändningspolicyer är regler som beskriver den typ av marknadsföringsåtgärder som du tillåts eller begränsas från att utföra på data inom Real-Time CDP. Mer information finns i avsnittet Dataanvändningsprinciper i [!DNL Experience Platform] [Översikt över datastyrning](../../data-governance/home.md) .

Adobe Experience Platform har flera principer för vanliga kundupplevelsefall. Du kan visa dessa profiler i användargränssnittet genom att gå till arbetsytan **[!UICONTROL Policies]** och välja fliken **[!UICONTROL Browse]**. I användarhandboken för [profiler](../../data-governance/policies/user-guide.md) i [!DNL Experience Platform]-dokumentationen finns mer detaljerad information om hur du arbetar med profiler i användargränssnittet, inklusive hur du skapar egna anpassade profiler.

## Klara regelefterlevnaden {#enforce}

När data har märkts och användarprofiler har definierats kan ni se till att dataanvändningen följer reglerna. När målgrupper aktiveras till destinationer i Real-Time CDP tillämpar Data Governance automatiskt användarprofiler om överträdelser inträffar.

Mer information finns i dokumentet om [automatisk policytillämpning](../../data-governance/enforcement/auto-enforcement.md).

## Nästa steg

Nu när du har introducerats till de viktigaste datastyrningsfunktionerna i Real-Time CDP och hur [!DNL Experience Platform] aktiverar dem kan du fortsätta med [dokumentationen för datastyrning i Adobe Experience Platform](../../data-governance/home.md). Dokumentationen innehåller översikter över viktiga datastyrningsbegrepp samt stegvisa arbetsflöden för hantering av etiketter och policyer för dataanvändning.

I följande video visas en översikt över datastyrning i Real-Time CDP, inklusive användning av marknadsföringsfall på destinationer och exempelarbetsflöden för olika scenarier:

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)
