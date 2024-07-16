---
title: API-guide för reaktor
description: Med Reactor API kan utvecklare programmässigt hantera alla resurser för taggar i Adobe Experience Platform. Följ den här användarhandboken om du vill lära dig hur du utför viktiga åtgärder med API:t.
exl-id: 153eab11-db08-499e-80d1-c56f254372ce
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1079'
ht-degree: 2%

---

# API-guide för [!DNL Reactor]

Reaktors-API:t innehåller flera slutpunkter som gör att du kan hantera alla resurser för taggar i Adobe Experience Platform programmatiskt.

Dessa slutpunkter beskrivs nedan. Besök de enskilda slutpunktshandböckerna för mer information och se [kom-igång-guiden](./getting-started.md) för viktig information om hur du autentiserar till API:t.

Om du vill visa alla tillgängliga slutpunkter och CRUD-åtgärder går du till [API-referens för reaktor](https://www.adobe.io/experience-platform-apis/references/reactor/).

## Företag

Ett företag representerar organisationen för en tagg-användare, vanligtvis ett företag. De här företagen matchar 1:1 med organisations-ID:n. API-användare kan bara se vilka företag de har åtkomst till.

Se [företagens slutpunktsguide](./endpoints/companies.md) för att lära dig hur du visar tillgängliga företag i API:t.

## Egenskaper

En egenskap är en behållare som innehåller de flesta andra resurser som är tillgängliga i Reactor API. De enda resurser som inte ägs av en egenskap är granskningshändelser, företag, tilläggspaket och profiler. En egenskap tillhör exakt ett företag och ett företag kan ha många egenskaper.

Se [egenskapens slutpunktshandbok](./endpoints/properties.md) om du vill veta mer om hur du hanterar egenskaper i API:t.

## Dataelement

Ett dataelement fungerar som en variabel som pekar på en viktig datadel i programmet. Dataelement används i regler och tilläggskonfigurationer. När regeln aktiveras vid körning i en webbläsare eller ett program tolkas dataelementets värde och används i regeln.

Se [dataelementets slutpunktshandbok](./endpoints/data-elements.md) om du vill veta mer om hur du hanterar dataelement i API:t.

## Regler

Regler styr beteendet för resurserna i ett distribuerat bibliotek. En regel är en grupp med en eller flera regelkomponenter och finns för att knyta ihop regelkomponenterna på ett logiskt sätt.

Läs [regelslutpunktshandboken](./endpoints/rules.md) om du vill veta mer om hur du hanterar regler i API:t.

## Regelkomponenter

Regelkomponenter är de enskilda objekt som utgör en regel. Regelkomponenter har tre grundläggande typer:

* **Händelser**: Vad utlöser en regel
* **Villkor**: Det som regeln kontrollerar för att avgöra en åtgärd
* **Åtgärder**: Vad regeln körs beroende på om villkoret är uppfyllt

Läs [regelslutpunktshandboken](./endpoints/rules.md) om du vill veta mer om hur du hanterar regler i API:t.

## Tilläggspaket

Ett tilläggspaket representerar en gruppering av enskilda funktioner som kan göras tillgängliga för en tagganvändare. De flesta vanliga funktionerna är regelkomponenter och dataelement, men kan även innehålla huvudmoduler och delade moduler. De funktioner som ingår i ett tilläggspaket installeras som ett tillägg när det ingår i ett bibliotek.

Läs slutpunktshandboken för [tilläggspaket](./endpoints/extension-packages.md) om du vill veta mer om hur du hanterar tilläggspaket i API:t.

## Tillägg

Ett tillägg representerar den installerade instansen av ett tilläggspaket. Ett tillägg gör de funktioner som definieras av ett tilläggspaket tillgängliga för en egenskap. De här funktionerna används när du skapar dataelement och regelkomponenter.

Läs [tilläggsslutpunktshandboken](./endpoints/extensions.md) om du vill veta mer om hur du hanterar tillägg i API:t.

## Bibliotek

Ett bibliotek är en samling resurser (tillägg, regler och dataelement) som representerar önskat beteende för en egenskap. Bibliotek kompileras till byggen, och dessa byggen tilldelas olika miljöer när de går ned i publiceringsflödet från testning till produktion.

Läs [bibliotekets slutpunktshandbok](./endpoints/libraries.md) om du vill veta mer om hur du hanterar bibliotek i API:t.

## Bygger

Ett taggbibliotek kompileras till ett bygge för att det ska kunna tilldelas till en miljö för testning och distribution. Innehållet i ett bygge varierar beroende på vilka resurser som ingår i biblioteket, konfigurationen av miljön som bygget tilldelas till och plattformen för egenskapen som bygget tillhör.

Se [guiden för byggslutpunkter](./endpoints/builds.md) om du vill veta mer om hur du hanterar byggen i API:t.

## Miljöer

En miljö anger den specifika värd där en bygge kan distribueras och om den ska distribueras som en uppsättning filer eller komprimeras i ett arkivformat. I Reaktors-API:t är miljöer åtskilda från värdarna själva, som hanteras av slutpunkten `/hosts`.

Se [guiden för byggslutpunkter](./endpoints/builds.md) om du vill veta mer om hur du hanterar byggen i API:t.

## Värdar

En värd representerar ett värdbaserat mål där ett biblioteksbygge kan levereras och slutligen distribueras. Värdar kan vara antingen Akamai- eller SFTP-servrar.

Läs [värdslutpunktshandboken](./endpoints/hosts.md) om du vill veta mer om hur du hanterar värdar i API:t.

## Appkonfigurationer

Appkonfigurationer tillåter att autentiseringsuppgifter lagras och hämtas för senare bruk. Läs slutpunktshandboken för [appkonfigurationer](./endpoints/app-configurations.md) om du vill veta mer om hur du hanterar appkonfigurationer i API:t.

## Granskningshändelser

En granskningshändelse är en post med en specifik ändring av en annan taggresurs som genereras när ändringen görs. Detta är systemhändelser som du kan prenumerera på med hjälp av en callback-funktion.

I [slutpunktshandboken för granskningshändelser](./endpoints/audit-events.md) finns mer information om hur du hanterar granskningshändelser i API:t.

## Återanrop

Ett återanrop är ett meddelande som Platform skickar till en URL-värd när en ny granskningshändelse genereras. Se [slutpunktshandboken för återanrop](./endpoints/callbacks.md) om du vill veta mer om hur du hanterar återanrop i API:t.

## Anteckningar

Anteckningar är textanteckningar som du kan lägga till i vissa taggresurser, till exempel dataelement, tillägg, bibliotek, egenskaper, regler och regelkomponenter. Läs slutpunktshandboken för [anteckningar](./endpoints/notes.md) om du vill veta mer om hur du hanterar anteckningar i API:t.

## Profil

En profil innehåller all information om den inloggade användaren, inklusive alla Adobe-organisationer som de tillhör, produktprofiler som de tillhör inom varje organisation och de rättigheter som de har från varje produktprofil.

Se [profilslutpunktshandboken](./endpoints/profile.md) om du vill veta hur du visar den här informationen i API:t.

## Sök

Med slutpunkten `/search` kan du hitta resurser som matchar ett önskat villkor, uttryckt som en fråga. Alla frågor omfattar ditt aktuella företag och tillgängliga egenskaper. Läs [guiden för sökslutpunkter](./endpoints/search.md) om du vill veta hur du använder den här funktionen.

## Hemligheter

En hemlighet innehåller autentiseringsuppgifter som gör att händelsevidarebefordran kan autentiseras till ett annat system för säkert datautbyte. I [hemlighetsguiden](./guides/secrets.md) finns en översikt över hur hemligheter fungerar vid vidarebefordran av händelser och i [slutpunktshandboken för hemligheter](./endpoints/secrets.md) finns information om hur du hanterar dem i Reaktors-API:t.

## Nästa steg

Om du vill börja ringa anrop med API:t för schemaregister läser du [kom igång-guiden](./getting-started.md) och väljer sedan en av slutpunktshandböckerna för att lära dig hur du använder specifika slutpunkter.
