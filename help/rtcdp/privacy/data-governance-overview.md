---
title: Datastyrning - översikt
seo-title: Datastyrning i kunddataplattformen i realtid
description: 'Med datastyrning kan ni hantera kunddata och säkerställa att ni följer regler, begränsningar och policyer som gäller för dataanvändning. '
seo-description: 'Med datastyrning kan ni hantera kunddata och säkerställa att ni följer regler, begränsningar och policyer som gäller för dataanvändning. '
translation-type: tm+mt
source-git-commit: af7fa6048fa60392a98975fe6fc36e8302355a05
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 0%

---


# Datastyrning i realtid CDP

Kunddataplattformen (CDP) i realtid samlar data från flera företagssystem, vilket gör det möjligt för marknadsförarna att bättre identifiera, förstå och engagera sina kunder. Dessa data kan vara föremål för användarbegränsningar som fastställts av din organisation eller av juridiska bestämmelser. Därför är det viktigt att se till att CDP i realtid är kompatibelt med användningsprinciper när data hanteras.

Med Adobe Experience Platform Data Governance kan ni hantera kunddata och säkerställa efterlevnad av regler, begränsningar och policyer som gäller för dataanvändning. Det spelar en viktig roll inom CDP i realtid, så att ni kan definiera användarprofiler, kategorisera data baserat på dessa policyer och kontrollera om policyer har överträtts när ni utför vissa marknadsföringsåtgärder.

CDP i realtid är byggt på Adobe Experience Platform och därför ingår de flesta datastyrningsfunktionerna i dokumentationen för Experience Platform. Detta dokument är avsett att komplettera [datastyrningsöversikten](../../data-governance/home.md) för Experience Platform och sammanfattar de styrningsfunktioner som finns i CDP i realtid. Följande ämnen behandlas:

* [Använd användningsetiketter på dina data](#labels)
* [Hantera dataanvändningsprinciper](#policies)
* [Klara regelefterlevnaden](#enforcement)

## Använd användningsetiketter på dina data {#labels}

Med datastyrning kan du använda användningsetiketter på dina data, antingen på datamängdsnivå eller datamängdsfältnivå. Med etiketter för dataanvändning kan du kategorisera data enligt de användarprofiler som gäller för dessa data.

Mer information om hur du arbetar med dataanvändningsetiketter finns i användarhandboken [för](../../data-governance/labels/overview.md) dataanvändningsetiketter för Adobe Experience Platform.

## Ange begränsningar för destinationer

Du kan ange begränsningar för dataanvändning för ett mål genom att definiera användningsfall för marknadsföring för det målet. Genom att definiera användningsfall för destinationer kan du kontrollera om det finns några överträdelser av användarprofiler och se till att profiler eller segment som skickas till destinationen är kompatibla med datastyrningsreglerna.

Marknadsföringsanvändningsfall kan definieras under _konfigurationsfasen_ för arbetsflödet _Redigera mål_ . Mer information finns i måldokumentationen.


## Hantera dataanvändningsprinciper {#policies}

För att dataanvändningsetiketter effektivt ska kunna stödja regelefterlevnad måste dataanvändningsprinciper definieras och aktiveras. Dataanvändningspolicyer är regler som beskriver den typ av marknadsföringsåtgärder som du tillåts eller begränsas från att utföra på data inom CDP i realtid. Mer information finns i avsnittet Dataanvändningsprinciper i Experience Platform [Data Governance-översikten](../../data-governance/home.md) .

Adobe Experience Platform har flera **huvudprinciper** för vanliga kundupplevelsefall. Dessa profiler kan visas genom att en begäran görs till API:t för [DULE Policy Service](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml), vilket visas i avsnittet&quot;List all policies&quot; i utvecklarhandboken [för](../../data-governance/policies/overview.md)Policy Service. Du kan också skapa egna **anpassade profiler** för att modellera anpassade användningsbegränsningar, vilket visas i avsnittet&quot;Skapa en princip&quot; i utvecklarhandboken.

## (Beta) Tillämpa regelefterlevnad för dataanvändning {#enforce-data-usage-compliance}

>[!IMPORTANT]
>Den här funktionen är för närvarande i betaversion och är inte tillgänglig för alla användare. Den kan aktiveras på begäran. Dokumentationen och funktionaliteten kan komma att ändras.

När data har märkts och användarprofiler har definierats kan ni se till att dataanvändningen följer reglerna. När målgruppssegment aktiveras till mål i realtid-CDP tillämpar Data Governance automatiskt användningspolicyer om det inträffar några överträdelser.

I följande diagram visas hur regelefterlevnad integreras i dataflödet för segmentaktivering:

![](assets/enforcement-flow.png)

När ett segment aktiveras för första gången kontrollerar DULE Policy Service om det finns policyöverträdelser baserade på följande faktorer:

* De dataanvändningsetiketter som används för fält och datauppsättningar i segmentet som ska aktiveras.
* Destinationens marknadsföringssyfte.

### Policyfelsmeddelanden {#enforcement}

Om en principöverträdelse inträffar från försök att aktivera ett segment (eller [göra ändringar i ett redan aktiverat segment](#policy-enforcement-for-activated-segments)) förhindras åtgärden och en pover visas som anger att en eller flera profiler har överträtts. Välj en principöverträdelse i poverarens vänstra kolumn för att visa information om den överträdelsen.

![](assets/violation-popover.png)

Fliken *Information* om drivrutinen anger vilken åtgärd som utlöste överträdelsen och varför överträdelsen inträffade, och ger förslag på hur problemet kan lösas.

Klicka på **Datalinje** för att spåra mål, segment, sammanfogningsprinciper eller datauppsättningar vars dataetiketter utlöste överträdelsen.

![](assets/data-lineage.png)

När en överträdelse har utlösts inaktiveras knappen **Spara** för aktiveringen tills rätt komponenter har uppdaterats enligt dataanvändningsprinciperna.

### Tillämpning av policyer för aktiverade segment {#policy-enforcement-for-activated-segments}

Regelefterlevnad gäller fortfarande för segment efter att de har aktiverats och begränsar eventuella ändringar av ett segment eller dess mål som skulle leda till en policyöverträdelse. På grund av de många komponenter som används för att aktivera segment till mål kan någon av följande åtgärder utlösa en överträdelse:

* Uppdaterar dataanvändningsetiketter
* Ändra datauppsättningar för ett segment
* Ändra segmentpredikat
* Ändra målkonfigurationer

Om någon av ovanstående åtgärder utlöser en överträdelse förhindras åtgärden från att sparas och ett meddelande om policyöverträdelse visas, vilket säkerställer att de aktiverade segmenten fortsätter att följa dataanvändningsprinciperna när de ändras.

## Nästa steg

Nu när ni har introducerats till de viktigaste funktionerna för datastyrning i CDP i realtid och hur Experience Platform gör det möjligt för dem kan ni fortsätta med [dokumentationen för datastyrning på Adobe Experience Platform](../../data-governance/home.md). Dokumentationen innehåller översikter över viktiga datastyrningsbegrepp samt stegvisa arbetsflöden för hantering av etiketter och policyer för dataanvändning.

I följande video visas en översikt över datastyrning i CDP i realtid, inklusive användning av marknadsföringsfall på destinationer och exempelarbetsflöden för olika scenarier:

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)