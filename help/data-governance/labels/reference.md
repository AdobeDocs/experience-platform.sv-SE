---
keywords: Experience Platform;home;popular topics;data governance;data usage label api;policy service api;supported data usage labels;contract labels;identity labels;sensitive labels
solution: Experience Platform
title: Etiketter för grundläggande dataanvändning
topic: labels
description: I det här dokumentet finns en översikt över alla dataanvändningsetiketter som för närvarande stöds av Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: cddc559dfb65ada888bb367d6265863091a9b2a1
workflow-type: tm+mt
source-wordcount: '1882'
ht-degree: 1%

---


# Etiketter för grundläggande dataanvändning

Med etiketter för dataanvändning kan du kategorisera datauppsättningar och fält enligt de användarprofiler som gäller för dessa data. Adobe Experience Platform Data Governance innehåller flera färdiga etiketter för dataanvändning som du kan använda för att kategorisera dina data.

I det här dokumentet finns en beskrivning av de etiketter för användning av kärndata som för närvarande tillhandahålls av [!DNL Experience Platform]. Mer information om [!DNL Data Governance] datastyrning finns i översikten över [](../home.md)datastyrning.

## Kontraktsetiketter

Kontraktets&quot;C&quot;-etiketter används för att kategorisera data som har avtalsmässiga skyldigheter eller som är relaterade till organisationens policyer för datastyrning.

| Etikett | Definition |
|---|---|
| **C1** | Data kan bara exporteras från Adobe Experience Cloud i en aggregerad form utan att inkludera enskilda identifierare eller enhetsidentifierare. [Mer information...](#c1) |
| **C2** | Data kan inte exporteras till tredje part. [Mer information...](#c2) |
| **C3** | Data kan inte kombineras eller på annat sätt användas med direkt identifierbar information. [Mer information...](#c3) |
| **C4** | Data kan inte användas för annonser eller innehåll som riktar sig till webbplatser eller webbplatser. [Mer information...](#c4) |
| **C5** | Data kan inte användas för intressebaserad, övergripande målinriktning av innehåll eller annonser. [Mer information...](#c5) |
| **C6** | Data kan inte användas för annonsanpassning på plats. [Mer information...](#c6) |
| **C7** | Data kan inte användas för målanpassning av innehåll på plats. [Mer information...](#c7) |
| **C8** | Data kan inte användas för att mäta organisationens webbplatser eller appar. [Mer information...](#c8) |
| **C9** | Data kan inte användas i arbetsflöden för datavetenskap. [Mer information...](#c9) |
| **C10** | Data kan inte användas för aktivering av sammanfogad identitet. [Mer information...](#c10) |

## Identitetsetiketter

Identitet&quot;I&quot;-etiketter används för att kategorisera data som kan identifiera eller kontakta en viss person.

| Etikett | Definition |
|---|---|
| **I1** | Direkt identifierbara data som kan identifiera eller kontakta en viss person, i stället för en enhet. |
| **I2** | Indirekt identifierbara data som kan användas i kombination med andra data för att identifiera eller kontakta en viss person. |

## Känsliga etiketter

Känsliga S-etiketter används för att kategorisera data som du, och din organisation, anser vara känsliga.

En typ av data som du anser vara känsliga kan vara olika typer av geografiska data; Denna kategori är dock inte begränsad till geografiska data.

| Etikett | Definition |
|---|---|
| **S1** | Data som anger latitud och longitud som kan användas för att fastställa en enhets exakta placering. |
| **S2** | Data som kan användas för att fastställa ett brett definierat geofence-område. |

## Bilaga

Avsnitten nedan innehåller ytterligare information om tillgängliga etiketter för dataanvändning.

### Information om kontraktsetikett

I följande avsnitt ges detaljerad information om genomförandet av särskilda avtalsetiketter C.

#### C1 {#c1}

Vissa data kan bara exporteras från Adobe Experience Cloud i en aggregerad form utan att innehålla identifierare för enskilda enheter eller enheter. Till exempel data som kommer från sociala nätverk.

#### C2 {#c2}

Vissa dataleverantörer har villkor i sina kontrakt som förbjuder export av data som de ursprungligen samlades in från. Kontrakt för sociala nätverk begränsar till exempel ofta överföringen av data som du får från dem. C2-etiketten är mer restriktiv än [C1](#c1), som endast kräver aggregation och anonyma data.

#### C3 {#c3}

Vissa dataleverantörer har villkor i sina kontrakt som förbjuder kombinationen eller användningen av dessa data med direkt identifierbar information. Till exempel innehåller kontrakt för data som hämtas från annonsnätverk, annonsservrar och tredjepartsleverantörer av data ofta specifika avtalsförbud för användning av sådana data med direkt identifierbara data.

#### C4 {#c4}

C4 är den mest restriktiva etiketten - den omfattar etiketterna [C5](#c5), [C6](#c6)och [C7](#c7).

#### C5 {#c5}

Intressebaserad målinriktning, eller personalisering, uppstår om följande tre villkor uppfylls: De data som samlas in på webbplatsen (1) används för att dra slutsatser om en användares intressen, (2) används i ett annat sammanhang, t.ex. på en annan webbplats eller i en app (utanför webbplatsen) OCH (3) används för att välja vilket innehåll eller vilka annonser som ska hanteras baserat på dessa slutsatser.

En kombination av data från flera platser, inklusive en kombination av data på plats och data utanför platsen eller en kombination av data från flera källor utanför platsen, kallas data mellan olika platser. Olika webbplatser representerar olika kontexter så att användningen av data mellan webbplatser i olika sammanhang skiljer sig från originalet. Data från olika webbplatser samlas vanligtvis in och behandlas för att man ska kunna dra slutsatser om användarnas intressen. Därför kan användningen av data för olika webbplatser för att rikta annonser eller innehåll normalt betraktas som intressebaserad målinriktning, oavsett om annonsen eller innehållet visas på plats eller utanför webbplatsen. Om data på plats till exempel användes i kombination med externa data för att välja vilken annons som ska visas för en användare på en organisations egen webbplats, skulle den användningen kvalificera sig som intressebaserad målinriktning. Ett annat exempel är att återmarknadsföring av annonser till användare utanför webbplatsen sannolikt även skulle kvalificera som intressebaserad målinriktning.

Användning av data utanför webbplatsen som enda målgruppsanpassning skulle troligtvis också kvalificera som intressebaserad målgruppsanpassning, eftersom data utanför webbplatsen vanligtvis samlas in och behandlas för att skapa slutsatser om användarnas intressen.

Men målgruppsanpassning av innehåll eller annonser som bara använder webbplatsdata skulle vanligtvis inte kvalificera som intressebaserad målinriktning. Målinriktning på plats som annars inte kan betecknas som räntebaserad målinriktning behandlas som två distinkta etiketter. Etikett C6 tar upp målgruppsanpassning och rapportering på plats och talar specifikt om urval, leverans och rapportering av annonser, och etiketten C7 tar upp val, leverans och rapportering av innehåll på plats (anpassning av innehåll på webbplatsen).

I slutändan är det upp till er att tolka etiketten och hur användningen av data med den etiketten upprätthålls. Som referens ges ramverken IAB och DAA nedan:

IAB: Personalisering. Samling och bearbetning av information om din användning av den här tjänsten för att därefter personalisera annonser och/eller innehåll för dig i andra sammanhang, till exempel på andra webbplatser eller appar, över tid. Vanligtvis används innehållet på webbplatsen eller appen för att dra slutsatser om dina intressen, som utgör grunden för det framtida urvalet av annonser och/eller innehåll.

DAA: Onlinebeteendeannonsering. Samla in data från en viss dator eller enhet om webbvisningsbeteenden över tid och på icke-anslutna webbplatser i syfte att förutse användarnas preferenser eller intressen för att leverera annonser till den datorn eller enheten baserat på preferenser eller intressen som följer av sådana webbvisningsbeteenden.

#### C6 {#c6}

Annonser är meddelanden eller meddelanden, inklusive text och bilder, som visas på en webbplats eller i en app som främst är avsedda att marknadsföra försäljning av varor eller tjänster. Det är upp till dig att fastställa syftet med sådana meddelanden eller meddelanden. Annonserna är åtskilda från webbplatsinnehållet, som täcks av etiketten [C7](#c7). Data med en C6-etikett kan inte användas för annonsanpassning på plats, inklusive val och leverans av annonser på organisationens webbplatser eller appar, eller för att mäta leveransen och effektiviteten av sådana annonser. Detta inkluderar att använda tidigare insamlade data på plats om användarnas intressen för att välja annonser, bearbeta data om vilka annonser som visades, när och var de visades och om användarna vidtagit några åtgärder som rör annonsen, som att klicka på en annons eller göra ett köp. Vanligtvis kan det inte anses vara intressebaserad målinriktning (även kallad personalisering) att dra slutsatser om en användares preferenser baserat på den användarens aktiviteter på webbplatsen och sedan använda dessa preferenser i annonsinriktning på webbplatsen, eftersom den inte uppfyller alla tre kraven för intressebaserad målinriktning. _[Se etikett C5 för dessa krav.](#c5)_

I slutändan är det upp till er att tolka etiketten och hur användningen av data med den etiketten upprätthålls. Som referens ges ramverken IAB och DAA nedan:

IAB: 3. Val av annonser, leverans, rapportering: Insamling av information, och kombination med tidigare insamlad information, för att välja ut och leverera annonser för er och för att mäta hur effektiva dessa annonser är och hur de levereras. Detta inkluderar att använda tidigare insamlad information om era intressen för att välja annonser, bearbeta data om vilka annonser som visades, hur ofta de visades, när och var de visades och om ni vidtagit några åtgärder som rör annonsen, till exempel klicka på en annons eller göra ett köp. Detta inkluderar inte personalisering, som är insamling och bearbetning av information om din användning av den här tjänsten för att senare personalisera annonser och/eller innehåll för dig i andra sammanhang, som webbplatser eller appar, över tid.

DAA: Onlineannonsering omfattar inte aktiviteter som utförs av första part, annonsleverans eller annonsrapportering eller sammanhangsbaserad annonsering (dvs. annonsering som baseras på innehållet på den webbsida som besöks, en kunds aktuella besök på en webbsida eller en sökfråga).

#### C7 {#c7}

Webbplatsinnehåll är text och bilder som är utformade för att informera, utbilda eller underhålla och som inte är skapade för att främja försäljningen av varor eller tjänster. Det är upp till er att fastställa syftet med innehållet, inklusive huruvida innehållet skulle kunna kvalificeras som ursprunglig reklam. C7-etiketten är inte avsedd att omfatta annonser på plats, som omfattas av etiketten [C6](#c6). Data med en C7-etikett kan inte användas för att målinrikta innehåll på plats, inklusive val och leverans av innehåll på organisationens webbplatser eller appar, eller för att mäta leveransen och effektiviteten av sådant innehåll. Detta inkluderar tidigare insamlad information om användarnas intressen i utvalda innehåll, bearbetning av data om vilket innehåll som visades, hur ofta eller hur länge det visades, när och var det visades, och om användarna vidtagit några åtgärder som rör innehållet, t.ex. att klicka på innehållet. Vanligtvis kan det inte anses vara intressebaserad målinriktning (även kallad personalisering) att dra slutsatser om en användares preferenser baserat på den användarens aktiviteter på webbplatsen och sedan använda dessa preferenser i målgruppsinriktning på webbplatsen, eftersom den inte uppfyller alla tre kraven för intressebaserad målinriktning. _[Se etikett C5 för dessa krav.](#c5)_

I slutändan är det upp till er att tolka etiketten och hur användningen av data med den etiketten upprätthålls. Som referens ges ramverken IAB och DAA nedan:

IAB: 4. Val, leverans, rapportering: Insamling av information, och kombination med tidigare insamlad information, för att välja ut och leverera innehåll åt er och för att mäta hur effektivt sådant innehåll levereras. Detta inkluderar att använda tidigare insamlad information om dina intressen för att välja innehåll, bearbeta data om vilket innehåll som visades, hur ofta eller hur länge det visades, när och var det visades, och om du vidtagit några åtgärder som rör innehållet, till exempel klicka på innehållet. Detta inkluderar inte personalisering, som är insamling och bearbetning av information om din användning av den här tjänsten för att senare anpassa innehåll och/eller annonsering för dig i andra sammanhang, som webbplatser eller appar, över tid.

DAA: Onlineannonsering omfattar inte aktiviteter som utförs av första part, annonsleverans eller annonsrapportering eller sammanhangsbaserad annonsering (dvs. annonsering som baseras på innehållet på den webbsida som ska besökas, en kunds aktuella besök på en webbsida eller en sökfråga).

#### C8 {#c8}

Data kan inte användas för att mäta, förstå och rapportera om hur användare använder organisationens webbplatser eller appar. Detta inkluderar inte intressebaserad målinriktning (målinriktning över flera webbplatser), som är en samling information om din användning av den här tjänsten för att sedan personalisera innehåll och/eller annonsering för dig i andra sammanhang, dvs. på andra tjänster, som webbplatser eller appar, över tid.

#### C9 {#c9}

I vissa avtal ingår uttryckliga förbud mot dataanvändning för datavetenskap. Ibland formuleras dessa i termer som förbjuder användning av data för artificiell intelligens (AI), maskininlärning (ML) eller modellering.

#### C10 {#c10}

Vissa dataanvändningsprinciper begränsar användningen av sammanfogade identitetsdata för personalisering. C10-etiketten används automatiskt på segment om deras sammanfogningsprinciper använder alternativet &quot;privat diagram&quot;.
