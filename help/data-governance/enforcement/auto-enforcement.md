---
keywords: Experience Platform;hem;populära ämnen;Politiska åtgärder;Automatisk tillsyn;API-baserad tillämpning;datastyrning
solution: Experience Platform
title: Automatisk policytillämpning
topic: guide
description: Det här dokumentet beskriver hur dataanvändningspolicyer tillämpas automatiskt när segment aktiveras för destinationer i Experience Platform.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 0%

---


# Automatisk policytillämpning

När data har märkts och användarprofiler har definierats kan ni se till att dataanvändningen följer reglerna. När målgruppssegment aktiveras för destinationer tillämpar Adobe Experience Platform automatiskt användarprofiler om något inträffar.

## Förutsättningar

Den här handboken kräver en fungerande förståelse av de plattformstjänster som används i automatisk tillämpning. Läs följande dokumentation om du vill veta mer innan du fortsätter med den här guiden:

* [Adobe Experience Platform datastyrning](../home.md): Det ramverk som Platform använder för att genomdriva efterlevnad av dataanvändning genom användning av etiketter och policyer.
* [Kundprofil](../../profile/home.md) i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [Adobe Experience Platform segmenteringstjänst](../../segmentation/home.md): Segmenteringsmotorn som  [!DNL Platform] används för att skapa målgruppssegment utifrån kundprofiler baserat på kundbeteenden och attribut.
* [Destinationer](../../destinations/home.md): Destinationer är färdiga integreringar med vanliga applikationer som möjliggör smidig aktivering av data från Platform för flerkanalskampanjer, e-postkampanjer, riktad annonsering och mycket mer.

## Tvingande flöde {#flow}

I följande diagram visas hur regelefterlevnad integreras i dataflödet för segmentaktivering:

![](../images/enforcement/enforcement-flow.png)

När ett segment aktiveras för första gången söker [!DNL Policy Service] efter policyöverträdelser baserat på följande faktorer:

* De dataanvändningsetiketter som används för fält och datauppsättningar i segmentet som ska aktiveras.
* Destinationens marknadsföringssyfte.

>[!NOTE]
>
>Om det finns dataanvändningsetiketter som bara har tillämpats på vissa fält i en datamängd (i stället för hela datamängden), tillämpas dessa fältetiketter endast under följande förhållanden:
>
>* Fälten används i segmentdefinitionen.
>* Fälten konfigureras som projicerade attribut för målmålet.


## Datalinje {#lineage}

Datalindelningen spelar en viktig roll när det gäller hur policyer tillämpas i plattformen. I allmänhet avser datalinjen ursprunget för en datauppsättning och vad som händer med den (eller där den flyttas) över tiden.

När det gäller [!DNL Data Governance] möjliggör raden att dataanvändningsetiketter kan spridas från datauppsättningar till underordnade tjänster som konsumerar deras data, som kundprofil i realtid och destinationer. Detta gör det möjligt att utvärdera och tillämpa principer vid flera viktiga punkter i dataöverföringen via Platform och ger kontext till datakonsumenterna om varför en policyöverträdelse inträffade.

I Experience Platform gäller den politiska kontrollen följande:

1. Data hämtas till plattformen och lagras i **datamängder**.
1. Kundprofiler identifieras och konstrueras utifrån dessa datauppsättningar genom att dataset slås samman i enlighet med **sammanfogningsprincipen**.
1. Grupper med profiler delas in i **segment** baserat på gemensamma attribut.
1. Segmenten aktiveras till **mål** nedströms.

Varje steg i ovanstående tidslinje representerar en enhet som kan bidra till att en policy överträds, vilket beskrivs i tabellen nedan:

| Datalindelningsfas | Roll vid policytillämpning |
| --- | --- |
| Datauppsättning | Datauppsättningar innehåller dataanvändningsetiketter (som används på datauppsättnings- eller fältnivå) som definierar vilka användningsfall som hela datauppsättningen eller specifika fält kan användas för. Policyöverträdelser inträffar om en datauppsättning eller ett fält som innehåller vissa etiketter används i ett syfte som en princip begränsar. |
| Kopplingsprincip | Sammanslagningsprinciper är de regler som används i Platform för att avgöra hur data ska prioriteras när fragment från flera datauppsättningar sammanfogas. Principöverträdelser inträffar om sammanfogningsprinciperna har konfigurerats så att datauppsättningar med begränsade etiketter aktiveras till ett mål. Mer information finns i guiden [sammanfogningsprinciper](../../profile/ui/merge-policies.md). |
| Segment | Segmentregler definierar vilka attribut som ska inkluderas från kundprofiler. Beroende på vilka fält en segmentdefinition innehåller ärver segmentet användningsetiketter som används för dessa fält. Policyöverträdelser inträffar om du aktiverar ett segment vars ärvda etiketter begränsas av måldestinationens tillämpliga policyer, baserat på dess användningsfall för marknadsföring. |
| Destination | När man skapar en destination kan man definiera en marknadsföringsåtgärd (kallas ibland för ett marknadsföringsfall). Det här användningsexemplet korrelerar till en marknadsföringsåtgärd enligt definitionen i en dataanvändningspolicy. Med andra ord avgör vilket marknadsföringsfall du definierar för ett mål vilka dataanvändningsprinciper som gäller för det målet. Policyöverträdelser inträffar om du aktiverar ett segment vars användningsetiketter begränsas av målmålets tillämpliga profiler. |

När policyöverträdelser inträffar ger de resulterande meddelandena som visas i användargränssnittet användbara verktyg för att utforska det datalinje som bidrar till att lösa problemet. Mer information finns i nästa avsnitt.

## Policyfelmeddelanden {#enforcement}

Om en principöverträdelse inträffar när ett försök görs att aktivera ett segment (eller [göra ändringar i ett redan aktiverat segment](#policy-enforcement-for-activated-segments)), förhindras åtgärden och en pover visas som anger att en eller flera profiler har överträtts. När en överträdelse har utlösts är knappen **[!UICONTROL Save]** inaktiverad för entiteten som du ändrar tills rätt komponenter uppdateras för att uppfylla dataanvändningsprinciperna.

Välj en principöverträdelse i poverarens vänstra kolumn för att visa information om den överträdelsen.

![](../images/enforcement/violation-policy-select.png)

Överträdelsemeddelandet innehåller en sammanfattning av den princip som överträtts, inklusive villkoren som principen är konfigurerad att kontrollera, den specifika åtgärd som utlöste överträdelsen och en lista med möjliga lösningar på problemet.

![](../images/enforcement/violation-summary.png)

Ett datalinjediagram visas under sammanfattningen av överträdelser, vilket gör att du kan se vilka datauppsättningar, sammanfogningsprinciper, segment och mål som berördes av överträdelsen. Enheten som du håller på att ändra markeras i diagrammet, vilket anger vilken punkt i flödet som orsakar att överträdelsen inträffar. Du kan välja ett enhetsnamn i diagrammet för att öppna informationssidan för den aktuella entiteten.

![](../images/enforcement/data-lineage.png)

Du kan också använda ikonen **[!UICONTROL Filter]** (![](../images/enforcement/filter.png)) för att filtrera de visade enheterna efter kategori. Minst två kategorier måste väljas för att data ska kunna visas.

![](../images/enforcement/lineage-filter.png)

Välj **[!UICONTROL List view]** om du vill visa datalinjen som en lista. Om du vill växla tillbaka till det visuella diagrammet väljer du **[!UICONTROL Path view]**.

![](../images/enforcement/list-view.png)

## Principanvändning för aktiverade segment {#policy-enforcement-for-activated-segments}

Regelefterlevnad gäller fortfarande för segment efter att de har aktiverats och begränsar eventuella ändringar av ett segment eller dess mål som skulle leda till en policyöverträdelse. På grund av hur [datalinje](#lineage) fungerar vid policytillämpning kan någon av följande åtgärder utlösa en överträdelse:

* Uppdaterar dataanvändningsetiketter
* Ändra datauppsättningar för ett segment
* Ändra segmentpredikat
* Ändra målkonfigurationer

Om någon av ovanstående åtgärder utlöser en överträdelse förhindras åtgärden från att sparas och ett meddelande om policyöverträdelse visas, vilket säkerställer att de aktiverade segmenten fortsätter att följa dataanvändningsprinciperna när de ändras.

## Nästa steg

Det här dokumentet beskriver hur automatisk tillämpning av regler fungerar i Experience Platform. Anvisningar om hur du programmässigt integrerar policytillämpning i dina program med API-anrop finns i handboken om [API-baserad tvingande](./api-enforcement.md).