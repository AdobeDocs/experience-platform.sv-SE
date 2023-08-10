---
title: Lead till kontomatchning i Real-Time CDP B2B
type: Documentation
description: En översikt och mer information om funktionen för att matcha lead-till-konto i Experience Platform CDP B2B.
exl-id: 2f853599-6bca-4ba6-bbba-131a49d8854e
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 3%

---

# Lead till kontomatchning i Real-Time CDP B2B

## Översikt {#overview}

Kontobaserad marknadsföring är en allt viktigare strategi för B2B-marknadsföring. Kontobaserad marknadsföring ger följande viktiga fördelar när det gäller att värva specifika värdefulla kunder:

- Rensa avkastningen
- Försäljning och marknadsföring
- Ett personaliserat tillvägagångssätt
- Färre resurser som går förlorade
- En kortare säljcykel

Kontobaserad marknadsföring ger möjlighet att länka kända personer och anonyma webbbesökare till försäljningskonton. På så sätt kan marknadsföringsteamen interagera med potentiella leads från målkontona tidigt under kundresan för att öka sina chanser till konvertering. En känd personpost innehåller vanligtvis delar av eller all följande information:

- Personnamn
- E-postadress
- Kontaktnummer
- Företagsnamn
- Företagets webbplats
- Befattning
- Plats

Lead till kontomatchning gör att du kan gå med i kända personprofiler till kontoprofiler. Sedan kan ni segmentera och rikta in data i ett B2B-sammanhang som konton, affärsmöjligheter och så vidare. Personprofilerna kan delas in i följande tre kategorier:

- **Kontopersonprofil:** Personprofilen är redan associerad med minst en kontoprofil via relationen från en datakälla. Det innebär att det finns minst ett kontaktfragment.

>[!NOTE]
>
> Kontopersonsprofiler matchas inte när lead körs för kontomatchningsjobb.

- **Känd personprofil:** Personprofilen är INTE associerad med någon kontoprofil och minst ett av följande personprofilattribut har ett värde:

   - E-postadress
   - Företagsnamn
   - Företagets webbplats

- **Anonym personprofil:** Personprofilen är INTE associerad med någon kontoprofil och inget av följande attribut för personprofiler har ett värde:

   - E-postadress
   - Företagsnamn
   - Företagets webbplats

>[!NOTE]
>
> En personprofil kan vara relaterad till flera kontoprofiler. Processen för att matcha lead-till-konto kommer dock endast att matcha den bästa matchningen. Om en större uppsättning matchningar krävs, kopplar du leadet till kontomatchningen med funktionen för relaterade konton.

## Så fungerar det {#how-it-works}

Dagliga jobb använder både deterministiska och sannolikhetsfaktorer för att matcha kända lead-profiler utan befintliga kontoassociationer. Kända lead-profiler har något av följande attribut:

- b2b.companyName
- b2b.companyWebsite
- workEmail

>[!NOTE]
>
> Attributet b2b.personKey.sourceKey måste finnas.

Attributen b2b.companyName, b2b.companyWebsite och b2b.personKey.sourceKey finns i fältgruppen b2b i B2B-personschemat.

![Personschema som visar attribut](/help/rtcdp/accounts/images/b2b-person-schema.png)

Attributet workEmail finns på den översta fältgruppen i B2B-personschemat.

![Schema för B2B-person som visar arbeteE-post](/help/rtcdp/accounts/images/b2b-person-workemail.png)

Profiler matchas bäst endast om matchningspoängen överstiger ett internt förtroendetröskelvärde. Resultaten sparas i en ny systemdatauppsättning för den befintliga kontopersonens XDM-relation.

Tjänsten lead to account matching körs när en ögonblicksbild av en ny personprofil blir tillgänglig, vilket är en gång var 24:e timme. Mer information om [konfiguration av lead till kontomatchning](/help/rtcdp/accounts/account-profile-ui-guide.md).

## Så här visar du lead-to-account matching-utdata {#how-to-view}

Efter jobbkörningen sparas resultaten i en ny datamängd för den befintliga kontopersonens relation-XDM.

Om du vill förhandsgranska datauppsättningen väljer du **[!UICONTROL Preview dataset]** längst upp till höger.

![Ny datauppsättning](/help/rtcdp/accounts/images/b2b-dataset-output.png)

Datauppsättningen innehåller den matchande kontoinformationen samt matchningspoängen för den valda datauppsättningen. The **[!UICONTROL Relationship Source]** anger om det kom från matchningsprocessen mellan lead och konto.

![Förhandsgranska datauppsättningens konfidensgrad och resultat](/help/rtcdp/accounts/images/b2b-dataset-preview.png)

## Övervaka lead till kontomatchningsjobb {#monitoring-jobs}

Du kan övervaka jobbstatus och associerade mått för alla lead-till-kontomatchningsjobb via kontrollpanelen.

Mer information om [övervaka jobb för lead-kontomatchning](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).
