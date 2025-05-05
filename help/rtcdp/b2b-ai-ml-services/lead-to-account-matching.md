---
title: Lead till kontomatchning i Real-Time CDP B2B
type: Documentation
description: En översikt och mer information om funktionen för att matcha lead-till-konto i Experience Platform CDP B2B.
feature: Get Started, Profiles, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/se/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 2f853599-6bca-4ba6-bbba-131a49d8854e
source-git-commit: 4ba609e777716b1b38f5b143587e5476d851e344
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# Lead till kontomatchning i Real-Time CDP B2B

## Översikt {#overview}

Kontobaserad marknadsföring är en allt viktigare strategi för B2B-marknadsföring. Kontobaserad marknadsföring ger följande viktiga fördelar när det gäller att värva specifika värdefulla kunder:

- Rensa avkastningen
- Försäljning och marknadsföring
- Ett personaliserat tillvägagångssätt
- Färre resurser som går förlorade
- En kortare säljcykel

Kontobaserad marknadsföring ger möjlighet att länka kända kunder till försäljningskonton. På så sätt kan marknadsföringsteamen interagera med potentiella leads från målkontona tidigt under kundresan för att öka sina chanser till konvertering. En känd personpost innehåller vanligtvis delar av eller all följande information:

- Personnamn
- E-postadress
- Kontaktnummer
- Företag
- Företagets webbplats
- Befattning
- Plats

## Så fungerar det {#how-it-works}

Dagliga jobb använder både deterministiska och sannolikhetsfaktorer för att matcha kända lead-profiler utan befintliga kontoassociationer. Kända lead-profiler har något av följande attribut:

- b2b.companyName
- b2b.companyWebsite
- workEmail

>[!NOTE]
>
> Attributet b2b.personKey.sourceKey måste finnas.

Attributen b2b.companyName, b2b.companyWebsite och b2b.personKey.sourceKey finns i fältgruppen b2b i B2B-personschemat.

![Personschema B2B visar attribut](/help/rtcdp/accounts/images/b2b-person-schema.png)

Attributet workEmail finns på den översta fältgruppen i B2B-personschemat.

![Personschema B2B visar workEmail](/help/rtcdp/accounts/images/b2b-person-workemail.png)

Profiler matchas bäst endast om matchningspoängen överstiger ett internt förtroendetröskelvärde. Resultaten sparas i en ny systemdatauppsättning för den befintliga kontopersonens XDM-relation.

Tjänsten lead to account matching körs när en ögonblicksbild av en ny personprofil blir tillgänglig, vilket är en gång var 24:e timme. Mer information om [konfigurationen av lead-till-konto-matchning](/help/rtcdp/accounts/account-profile-ui-guide.md) finns i dokumentationen.

## Så här visar du lead-to-account matching-utdata {#how-to-view}

Efter jobbkörningen sparas resultaten i en ny datamängd för den befintliga kontopersonens relation-XDM.

Om du vill förhandsgranska datauppsättningen väljer du **[!UICONTROL Preview dataset]** i det övre högra hörnet.

![Ny datauppsättning](/help/rtcdp/accounts/images/b2b-dataset-output.png)

Datauppsättningen innehåller den matchande kontoinformationen samt matchningspoängen för den valda datauppsättningen. Fältet **[!UICONTROL Relationship Source]** anger om det kom från lead-till-kontomatchningsprocessen.

![Förhandsgranska datauppsättningens konfidensgrad och utdata](/help/rtcdp/accounts/images/b2b-dataset-preview.png)

## Övervaka lead till kontomatchningsjobb {#monitoring-jobs}

Du kan övervaka jobbstatus och associerade mått för alla lead-till-kontomatchningsjobb via kontrollpanelen.

Mer information om [övervakningsjobben för kontomatchning](/help/dataflows/ui/b2b/monitor-profile-enrichment.md) finns i dokumentationen.
