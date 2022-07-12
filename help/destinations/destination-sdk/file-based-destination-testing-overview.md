---
description: Det filbaserade API:t för måltestning är en samling slutpunkter som du kan använda för att validera konfigurationen av de filbaserade mål som skapats genom Destinationen SDK.
title: Filbaserat API för måltestning
source-git-commit: 734d66cc881ab1b691c13ef446331d0c51851cf9
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---


# Filbaserat API för måltestning

## Översikt {#overview}

Det filbaserade API:t för måltestning är en uppsättning slutpunkter som du kan använda för att validera konfigurationen av de filbaserade mål som skapats genom Destinationen SDK.

Vi rekommenderar att du använder dessa verktyg för att validera konfigurationen innan [skicka](submit-destination.md) till Adobe för granskning.

För bästa testresultat rekommenderar vi att du använder denna API baserat på flödesdiagrammet nedan.

![Diagram som visar det rekommenderade testflödet för destinationen](assets/file-based-testing-flow.png)

I avsnitten nedan finns en kort översikt över vad varje slutpunkt kan göra.

## Generera exempelprofiler {#generate-sample-profiles}

Använd `/sample-profiles` API-slutpunkt för att generera exempelprofiler baserat på ditt befintliga källschema.

Exempelprofiler kan hjälpa dig att förstå JSON-strukturen för en profil. Dessutom får du ett standardvärde som du kan anpassa med dina egna profildata för ytterligare destinationstestning.

Se [dedikerad dokumentation](file-based-sample-profile-generation-api.md) om du vill lära dig hur du genererar exempelprofiler.

## Testa målkonfiguration {#test-destination-configuration}

Använd `/testing/destinationInstance` API-slutpunkt för att testa om ditt filbaserade mål är korrekt konfigurerat och för att verifiera dataflödenas integritet till det konfigurerade målet.

Du kan göra förfrågningar till testslutpunkten med eller utan att lägga till [exempelprofiler](file-based-sample-profile-generation-api.md) till samtalet. Om du inte skickar några profiler på begäran genererar API:t en exempelprofil automatiskt och lägger till den i begäran.

Se [dedikerad dokumentation](file-based-destination-testing-api.md) om du vill lära dig hur du testar målkonfigurationen med exempelprofiler.

## Visa detaljerade aktiveringsresultat {#view-detailed-activation-results}

Använd `/testing/destinationInstance` API-slutpunkten som du kan använda för att visa fullständig information om filbaserade testresultat för mål.

API-slutpunkten returnerar samma resultat som när du använder [API för flödestjänst](../api/update-destination-dataflows.md) för att övervaka dataflöden.

Se [dedikerad dokumentation](file-based-destination-results-api.md) om du vill lära dig mer om hur du får detaljerade aktiveringsresultat.

## Återge kunddatafält {#render-customer-data-fields}

Använd `/authoring/testing/template/render` API-slutpunkt för att visualisera hur mallen [kunddatafält](file-based-destination-configuration.md#customer-data-fields) som definierats i målkonfigurationen skulle se ut så här.

API-slutpunkten genererar slumpmässiga värden för kunddatafälten och returnerar dem i svaret. Detta hjälper dig att validera den semantiska strukturen i kunddatafält som t.ex. bucketnamn eller mappsökvägar.

Se [dedikerad dokumentation](file-based-render-template-api.md) om du vill lära dig hur ni genererar och visualiserar värden för era kunddatafält.