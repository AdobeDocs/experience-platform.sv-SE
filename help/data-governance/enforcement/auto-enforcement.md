---
keywords: Experience Platform;hem;populära ämnen;Politiska åtgärder;Automatisk tillsyn;API-baserad tillämpning;datastyrning
solution: Experience Platform
title: Automatisk policytillämpning
description: Det här dokumentet beskriver hur dataanvändningspolicyer tillämpas automatiskt när segment aktiveras för destinationer i Experience Platform.
exl-id: c6695285-77df-48c3-9b4c-ccd226bc3f16
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1713'
ht-degree: 0%

---

# Automatisk policytillämpning

>[!IMPORTANT]
>
>Automatisk policystyrning är bara tillgängligt för organisationer som har köpt **Adobe Healthcare Shield** eller **Adobe Privacy &amp; Security Shield**.

När data har märkts och dataanvändningsprinciper har definierats, kan ni se till att dataanvändningsprinciperna följs. När målgruppssegment aktiveras för destinationer tillämpar Adobe Experience Platform automatiskt användarprofiler om något inträffar.

>[!NOTE]
>
>I det här dokumentet fokuseras på att genomföra regler för datastyrning och samtycke. Mer information om åtkomstkontrollprinciper finns i dokumentationen om [attributbaserad åtkomstkontroll](../../access-control/abac/overview.md).

## Förutsättningar

Den här handboken kräver en fungerande förståelse av de plattformstjänster som används i automatisk tillämpning. Läs följande dokumentation om du vill veta mer innan du fortsätter med den här guiden:

* [Adobe Experience Platform datastyrning](../home.md): Det ramverk som Platform använder för att genomdriva efterlevnad av dataanvändning genom användning av etiketter och policyer.
* [Kundprofil i realtid](../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [Adobe Experience Platform segmenteringstjänst](../../segmentation/home.md): Segmenteringsmotorn i [!DNL Platform] används för att skapa målgruppssegment utifrån era kundprofiler utifrån kundbeteenden och attribut.
* [Destinationer](../../destinations/home.md): Destinationer är färdiga integreringar med vanliga applikationer som möjliggör smidig aktivering av data från Platform för flerkanalskampanjer, e-postkampanjer, riktad reklam med mera.

## Tvingande flöde {#flow}

I följande diagram visas hur regelefterlevnad integreras i dataflödet för segmentaktivering:

![](../images/enforcement/enforcement-flow.png)

När ett segment aktiveras första gången [!DNL Policy Service] kontroller av tillämpliga policyer grundade på följande faktorer:

* De dataanvändningsetiketter som används för fält och datauppsättningar i segmentet som ska aktiveras.
* Destinationens marknadsföringssyfte.
* De profiler som har samtyckt till att inkluderas i segmentaktiveringen, baserat på dina konfigurerade medgivandeprinciper.

>[!NOTE]
>
>Om det finns dataanvändningsetiketter som bara har tillämpats på vissa fält i en datamängd (i stället för hela datamängden), tillämpas dessa fältetiketter endast under följande förhållanden:
>
>* Fälten används i segmentdefinitionen.
>* Fälten konfigureras som projicerade attribut för målmålet.


## Datalinje {#lineage}

Datalindelningen spelar en viktig roll när det gäller hur policyer tillämpas i plattformen. I allmänhet avser datalinjen ursprunget för en datauppsättning och vad som händer med den (eller där den flyttas) över tiden.

När det gäller datastyrning gör länkning det möjligt för dataanvändningsetiketter att sprida data från datauppsättningar till tjänster i senare led som konsumerar deras data, som kundprofil i realtid och destinationer. Detta gör det möjligt att utvärdera och tillämpa principer vid flera viktiga punkter i dataöverföringen via Platform och ger kontext till datakonsumenterna om varför en policyöverträdelse inträffade.

I Experience Platform gäller den politiska kontrollen följande:

1. Data hämtas till plattformen och lagras i **datauppsättningar**.
1. Kundprofiler identifieras och konstrueras utifrån dessa datauppsättningar genom att sammanfoga datafragment enligt **sammanfogningsprincip**.
1. Profilgrupper delas in i **segment** baserat på gemensamma attribut.
1. Segmenten aktiveras nedåt **mål**.

Varje steg i ovanstående tidslinje representerar en enhet som kan bidra till policytillämpning, enligt tabellen nedan:

| Datalindelningsfas | Roll vid policytillämpning |
| --- | --- |
| Datauppsättning | Datauppsättningar innehåller dataanvändningsetiketter (som används på datauppsättnings- eller fältnivå) som definierar vilka användningsfall som hela datauppsättningen eller specifika fält kan användas för. Policyöverträdelser inträffar om en datauppsättning eller ett fält som innehåller vissa etiketter används i ett syfte som en princip begränsar.<br><br>Alla medgivandeattribut som samlas in från dina kunder lagras också i datauppsättningar. Om du har tillgång till profiler för samtycke, kommer profiler som inte uppfyller kraven för attributet för samtycke i dina profiler att exkluderas från segment som aktiveras för en destination. |
| Kopplingsprincip | Sammanslagningsprinciper är de regler som används i Platform för att avgöra hur data ska prioriteras när fragment från flera datauppsättningar sammanfogas. Principöverträdelser inträffar om sammanfogningsprinciperna har konfigurerats så att datauppsättningar med begränsade etiketter aktiveras till ett mål. Se [sammanfogningsprinciper - översikt](../../profile/merge-policies/overview.md) för mer information. |
| Segment | Segmentregler definierar vilka attribut som ska inkluderas från kundprofiler. Beroende på vilka fält en segmentdefinition innehåller ärver segmentet användningsetiketter som används för dessa fält. Policyöverträdelser inträffar om du aktiverar ett segment vars ärvda etiketter begränsas av måldestinationens tillämpliga policyer, baserat på dess användningsfall för marknadsföring. |
| Destination | När man skapar en destination kan man definiera en marknadsföringsåtgärd (kallas ibland för ett marknadsföringsfall). Det här användningsexemplet korrelerar till en marknadsföringsåtgärd enligt definitionen i en policy. Det innebär att den marknadsföringsåtgärd som du definierar för ett mål avgör vilka dataanvändningsprinciper och profiler för samtycke som gäller för det målet.<br><br>Policyöverträdelser för dataanvändning inträffar om du aktiverar ett segment vars användningsetiketter är begränsade för målmålets marknadsföringsåtgärd.<br><br>(Beta) När ett segment aktiveras exkluderas alla profiler som inte innehåller de obligatoriska medgivandeattributen för marknadsföringsåtgärden (som definieras i er medgivandepolicy) från den aktiverade målgruppen. |

>[!IMPORTANT]
>
>En del dataanvändningsprinciper kan ange två eller flera etiketter med en AND-relation. En policy kan till exempel begränsa en marknadsföringsåtgärd om etiketter `C1` OCH `C2` finns båda, men begränsar inte samma åtgärd om bara en av etiketterna finns.
>
>När det gäller automatisk verkställighet anser datastyrningsramverket inte att aktivering av separata segment till en destination är en kombination av data. Därför är exemplet `C1 AND C2` principen är **NOT** framtvingas om dessa etiketter ingår i separata segment. I stället tillämpas den här principen bara när båda etiketterna finns i samma segment vid aktivering.

När policyöverträdelser inträffar ger de resulterande meddelandena som visas i användargränssnittet användbara verktyg för att utforska det datalinje som bidrar till att lösa problemet. Mer information finns i nästa avsnitt.

## Policytvingande meddelanden {#enforcement}

Avsnitten nedan beskriver olika policyefterlevnadsmeddelanden som visas i plattformsgränssnittet:

* [Policyöverträdelse för dataanvändning](#data-usage-violation)
* [Principutvärdering av samtycke](#consent-policy-evaluation)

### Policyöverträdelse för dataanvändning {#data-usage-violation}

Om en principöverträdelse inträffar vid försök att aktivera ett segment (eller [redigera ett redan aktiverat segment](#policy-enforcement-for-activated-segments)) förhindras åtgärden och en pover visas som indikerar att en eller flera profiler har överträtts. När en överträdelse har utlösts **[!UICONTROL Save]** knappen är inaktiverad för den entitet som du ändrar tills rätt komponenter uppdateras för att uppfylla dataanvändningsprinciperna.

Välj en principöverträdelse i poverarens vänstra kolumn för att visa information om den överträdelsen.

![](../images/enforcement/violation-policy-select.png)

Överträdelsemeddelandet innehåller en sammanfattning av den princip som överträtts, inklusive villkoren som principen är konfigurerad att kontrollera, den specifika åtgärd som utlöste överträdelsen och en lista med möjliga lösningar på problemet.

![](../images/enforcement/violation-summary.png)

Ett datalinjediagram visas nedanför sammanfattningen av överträdelser, vilket gör att du kan se vilka datauppsättningar, sammanfogningsprinciper, segment och mål som berördes av principöverträdelsen. Enheten som du håller på att ändra markeras i diagrammet, vilket anger vilken punkt i flödet som orsakar att överträdelsen inträffar. Du kan välja ett enhetsnamn i diagrammet för att öppna informationssidan för den aktuella entiteten.

![](../images/enforcement/data-lineage.png)

Du kan också använda **[!UICONTROL Filter]** ikon (![](../images/enforcement/filter.png)) för att filtrera de visade enheterna efter kategori. Minst två kategorier måste väljas för att data ska kunna visas.

![](../images/enforcement/lineage-filter.png)

Välj **[!UICONTROL List view]** för att visa datalinjen som en lista. Om du vill växla tillbaka till det visuella diagrammet väljer du **[!UICONTROL Path view]**.

![](../images/enforcement/list-view.png)

### Principutvärdering av samtycke {#consent-policy-evaluation}

Om du har [policyer för skapat samtycke](../policies/user-guide.md#consent-policy) och som aktiverar ett segment till en destination kan du se hur dina medgivandeprinciper påverkar procentandelen profiler som ingår i aktiveringen.

#### Utvärdering före aktivering

När du har nått **[!UICONTROL Review]** steg när [aktivera ett mål](../../destinations/ui/activation-overview.md), markera **[!UICONTROL View applied policies]**.

![Visa knapp för tillämpade profiler i arbetsflödet för aktivering av mål](../images/enforcement/view-applied-policies.png)

En dialogruta för policykontroll visas som visar en förhandsgranskning av hur dina medgivandeprinciper påverkar den godkända publiken för de aktiverade segmenten.

![Dialogrutan Kontroll av sambandsprincip i plattformsgränssnittet](../images/enforcement/consent-policy-check.png)

Dialogrutan visar den godkända publiken för ett segment i taget. Om du vill visa principutvärderingen för ett annat segment använder du listrutan ovanför diagrammet och väljer ett segment i listan.

![Segmentväljare i dialogrutan för principkontroll](../images/enforcement/segment-switcher.png)

Använd den vänstra listen för att växla mellan tillämpliga medgivandeprinciper för det valda segmentet. Profiler som inte är markerade visas i[!UICONTROL Other policies]i diagrammet.

![Principväljaren i dialogrutan för principkontroll](../images/enforcement/policy-switcher.png)

I diagrammet visas överlappningen mellan tre profilgrupper:

1. Profiler som är kvalificerade för det valda segmentet
1. Profiler som är kvalificerade för den valda medgivandeprincipen
1. Profiler som uppfyller villkoren för andra tillämpliga medgivandepolicyer för segmentet (kallas&quot;[!UICONTROL Other policies]&quot; i diagrammet)

De profiler som är kvalificerade för alla tre av de ovanstående grupperna representerar den godkända målgruppen för det valda segmentet, som sammanfattas i den högra listen.

![Sammanfattningsavsnitt i dialogrutan för principkontroll](../images/enforcement/summary.png)

Håll pekaren över en av målgrupperna i diagrammet för att visa antalet profiler som det innehåller.

![Markera ett diagramavsnitt i dialogrutan för principkontroll](../images/enforcement/highlight-segment.png)

Den godkända publiken representeras av den centrala överlappningen i diagrammet och kan markeras som i andra avsnitt.

![Markera den godkända målgruppen i diagrammet](../images/enforcement/consented-audience.png)

#### Flödeskörning

När data aktiveras till ett mål visar flödeskörningsinformationen antalet identiteter som har uteslutits på grund av aktiva medgivandeprinciper.

![Exkluderade identitetsvärden för ett dataflöde](../images/enforcement/dataflow-run-enforcement.png)

## Tillämpning av policyer för aktiverade segment {#policy-enforcement-for-activated-segments}

Regelefterlevnad gäller fortfarande för segment efter att de har aktiverats och begränsar eventuella ändringar av ett segment eller dess mål som skulle leda till en policyöverträdelse. På grund av hur [datalinje](#lineage) fungerar i policytillämpning, kan någon av följande åtgärder utlösa en överträdelse:

* Uppdaterar dataanvändningsetiketter
* Ändra datauppsättningar för ett segment
* Ändra segmentpredikat
* Ändra målkonfigurationer

Om någon av ovanstående åtgärder utlöser en överträdelse förhindras åtgärden från att sparas och ett meddelande om policyöverträdelse visas, vilket säkerställer att de aktiverade segmenten fortsätter att följa dataanvändningsprinciperna när de ändras.

## Nästa steg

Det här dokumentet beskriver hur automatisk tillämpning av regler fungerar i Experience Platform. Anvisningar om hur du programmässigt integrerar policytillämpning i dina program med API-anrop finns i handboken [API-baserad tillämpning](./api-enforcement.md).
