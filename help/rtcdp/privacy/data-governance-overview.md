---
title: Datastyrning - översikt
seo-title: Datastyrning i realtid med kunddata i Platform
description: 'Med datastyrning kan ni hantera kunddata och säkerställa att ni följer regler, begränsningar och policyer som gäller för dataanvändning. '
seo-description: 'Med datastyrning kan ni hantera kunddata och säkerställa att ni följer regler, begränsningar och policyer som gäller för dataanvändning. '
translation-type: tm+mt
source-git-commit: c4e5e8ccac1af976c890adb1c9f0ff7f7b5ed9b4
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 0%

---


# Datastyrning i realtid CDP

Kunddata i realtid Platform (CDP i realtid) samlar data från olika affärssystem, vilket gör det möjligt för marknadsförarna att bättre identifiera, förstå och engagera sina kunder. Dessa data kan vara föremål för användarbegränsningar som fastställts av din organisation eller av juridiska bestämmelser. Därför är det viktigt att se till att CDP i realtid är kompatibelt med användningsprinciper när data hanteras.

Med Adobe Experience Platform Data Governance kan ni hantera kunddata och se till att ni följer regler, begränsningar och policyer som gäller för dataanvändning. Det spelar en viktig roll inom CDP i realtid, så att ni kan definiera användarprofiler, kategorisera data baserat på dessa policyer och kontrollera om policyer har överträtts när ni utför vissa marknadsföringsåtgärder.

CDP i realtid är byggt på Adobe Experience Platform och därför beskrivs merparten av datastyrningsfunktionerna i dokumentationen för Experience Platform. Detta dokument är avsett att komplettera [datastyrningsöversikten](../../data-governance/home.md) för Experience Platform och sammanfattar de styrningsfunktioner som finns i CDP i realtid. Följande ämnen behandlas:

* [Använd användningsetiketter på dina data](#labels)
* [Hantera dataanvändningsprinciper](#policies)
* [Klara regelefterlevnaden](#enforce-data-usage-compliance)

## Använd användningsetiketter på dina data {#labels}

Med datastyrning kan du använda användningsetiketter på dina data, antingen på datamängdsnivå eller datamängdsfältnivå. Med etiketter för dataanvändning kan du kategorisera data enligt de användarprofiler som gäller för dessa data.

Mer information om hur du arbetar med dataanvändningsetiketter finns i användarhandboken [för](../../data-governance/labels/overview.md) dataanvändningsetiketter för Adobe Experience Platform.

## Konfigurera användningsfall för marknadsföring för destinationer {#destinations}

Du kan ange begränsningar för dataanvändning för ett mål genom att definiera användningsfall för marknadsföring (kallas även marknadsföringsåtgärder) för det målet. Ett användningsfall för marknadsföring för en destination anger avsikten med de data som ska exporteras till den destinationen.

>[!NOTE] Mer information om marknadsföringsåtgärder och hur de används i dataanvändningspolicyer finns i översikten över [dataanvändningspolicyn](../../data-governance/policies/overview.md) i Experience Platform-dokumentationen.

Genom att definiera användningsfall för marknadsföring på destinationer kan ni se till att profiler och segment som skickas till dessa destinationer följer dataanvändningsprinciperna. Ni bör därför lägga till lämpliga användningsfall för marknadsföring till era destinationer baserat på organisationens behov av att tillämpa policybegränsningar för aktivering.

Marknadsföringsfall kan bara väljas när du ställer in ett mål för första gången. Beroende på vilken typ av mål du arbetar med visas möjligheten att konfigurera användningsfall för marknadsföring vid olika tillfällen i konfigurationsarbetsflödet. Anvisningar om hur du konfigurerar ett visst mål finns i [måldokumentationen](../destinations/destinations-overview.md) .


## Hantera dataanvändningsprinciper {#policies}

För att dataanvändningsetiketter effektivt ska kunna stödja regelefterlevnad måste dataanvändningsprinciper definieras och aktiveras. Dataanvändningspolicyer är regler som beskriver den typ av marknadsföringsåtgärder som du tillåts eller begränsas från att utföra på data inom CDP i realtid. Mer information finns i avsnittet&quot;Dataanvändningspolicyer&quot; i Experience Platform [datastyrningsöversikten](../../data-governance/home.md) .

Adobe Experience Platform har flera **huvudprinciper** för vanliga kundupplevelsefall. Du kan visa dessa profiler i användargränssnittet genom att gå till **[!UICONTROL Policies]** arbetsytan och välja **[!UICONTROL Browse]** fliken. I användarhandboken för [profiler](../../data-governance/policies/user-guide.md) i dokumentationen för Experience Platform finns mer detaljerad information om hur du arbetar med policyer i användargränssnittet, inklusive hur du skapar egna policyer.

## (Beta) Tillämpa regelefterlevnad för dataanvändning {#enforce-data-usage-compliance}

>[!IMPORTANT]
>Den här funktionen är för närvarande i betaversion och är inte tillgänglig för alla användare. Den kan aktiveras på begäran. Dokumentationen och funktionaliteten kan komma att ändras.

När data har märkts och användarprofiler har definierats kan ni se till att dataanvändningen följer reglerna. När målgruppssegment aktiveras till mål i realtid-CDP tillämpar Data Governance automatiskt användningspolicyer om det inträffar några överträdelser.

I följande diagram visas hur regelefterlevnad integreras i dataflödet för segmentaktivering:

![](assets/enforcement-flow.png)

När ett segment aktiveras för första gången kontrollerar DULE Policy Service om det finns policyöverträdelser baserade på följande faktorer:

* De dataanvändningsetiketter som används för fält och datauppsättningar i segmentet som ska aktiveras.
* Destinationens marknadsföringssyfte.

>[!NOTE] Om det finns dataanvändningsetiketter som bara har tillämpats på vissa fält i en datamängd (i stället för hela datamängden), tillämpas dessa fältetiketter endast under följande förhållanden:
>* Fälten används i segmentdefinitionen.
>* Fälten konfigureras som projicerade attribut för målmålet.


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

Nu när du har introducerats till de viktigaste datastyrningsfunktionerna för CDP i realtid och hur Experience Platform möjliggör dem kan du fortsätta med [dokumentationen för datastyrning på Adobe Experience Platform](../../data-governance/home.md). Dokumentationen innehåller översikter över viktiga datastyrningsbegrepp samt stegvisa arbetsflöden för hantering av etiketter och policyer för dataanvändning.

I följande video visas en översikt över datastyrning i CDP i realtid, inklusive användning av marknadsföringsfall på destinationer och exempelarbetsflöden för olika scenarier:

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)