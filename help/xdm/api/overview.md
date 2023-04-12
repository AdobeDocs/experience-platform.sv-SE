---
keywords: Experience Platform;hem;populära ämnen;api;API;XDM;XDM system;experience data model;Experience data model;experience data model;data model;data model;data model;schema register;schemaregister;
solution: Experience Platform
title: API-guide för schemaregister
description: Med API:t för schemaregister kan utvecklare programmässigt hantera alla scheman och relaterade XDM-resurser (Experience Data Model) inom Adobe Experience Platform. Följ den här användarhandboken om du vill lära dig hur du utför viktiga åtgärder med API:t.
exl-id: 9e693d29-303e-462a-a1e2-93c0d517b8e3
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 1%

---

# [!DNL Schema Registry] API-guide

The [!DNL Schema Registry] används för att få åtkomst till schemabiblioteket i Adobe Experience Platform, med ett användargränssnitt och RESTful API från vilket alla tillgängliga biblioteksresurser är tillgängliga.

API:t för schemaregister innehåller flera slutpunkter som gör att du kan hantera alla scheman och relaterade XDM-resurser (Experience Data Model) som är tillgängliga inom plattformen. Detta omfattar de som definieras av Adobe, [!DNL Experience Platform] partners och leverantörer vars program ni använder.

Dessa slutpunkter beskrivs nedan. Mer information finns i de enskilda slutpunktshandböckerna och i [komma igång-guide](./getting-started.md) om du vill ha viktig information om obligatoriska rubriker, läsa exempel-API-anrop med mera.

>[!IMPORTANT]
>
>XDM använder JSON-schemaformatering för att beskriva och validera strukturen för importerade kundupplevelsedata. Innan du börjar arbeta med API:t för schemaregistret rekommenderar vi att du granskar [officiell dokumentation för JSON-schema](https://json-schema.org/) för en bättre förståelse av denna underliggande teknik.

Om du vill visa alla tillgängliga slutpunkter och CRUD-åtgärder går du till [API-referens för schemaregister](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

## Scheman

XDM-scheman representerar och validerar strukturen och formatet för data som hämtas till Platform. Ett schema består av en klass och noll eller flera schemafältgrupper. Du kan skapa, visa, redigera och ta bort scheman med `/schemas` slutpunkt. Om du vill lära dig hur du använder den här slutpunkten kan du läsa [slutpunktshandbok för scheman](./schemas.md).

En steg-för-steg-guide om hur du skapar ett fullständigt schema i API:t för schemaregister, inklusive hur du skapar och lägger till fältgrupper och datatyper, finns i [Skapa API-schema, genomgång](../tutorials/create-schema-api.md).

Om du importerar CSV-data, se avsnittet om [CSV till schemakonvertering](#csv-to-schema).

## Beteenden

Beteenden definierar den typ av data som ett schema beskriver. Varje XDM-klass måste referera till ett specifikt beteende, som alla scheman som använder den klassen ärver. Se [beteendeslutpunktsguide](./behaviors.md) om du vill lära dig hur du visar tillgängliga beteenden i API:t.

## Klasser

En klass definierar den grundläggande strukturen för gemensamma egenskaper som alla scheman baserade på den klassen måste innehålla, och fastställer vilka fältgrupper som kan användas i dessa scheman. Alla klasser måste kopplas till ett befintligt beteende. Se [klassers slutpunktshandbok](./classes.md) om du vill ha mer information om hur du arbetar med klasser i API:t.

## Fältgrupper

Fältgrupper är återanvändbara komponenter som definierar ett eller flera fält som representerar ett visst koncept, till exempel en enskild person, en postadress eller en webbläsarmiljö. Fältgrupper är avsedda att ingå som en del av ett schema som implementerar en kompatibel klass, beroende på beteendet för de data de representerar (post- eller tidsserie). Se [slutpunktsguide för fältgrupper](./field-groups.md) om du vill lära dig hur du arbetar med fältgrupper i API:t.

## Datatyper

Datatyper används som referenstypfält i klasser eller fältgrupper på samma sätt som grundläggande litteralfält, med den största skillnaden är att datatyper kan definiera flera underfält. Även om datatyperna liknar fältgrupper på så sätt att de medger konsekvent användning av en struktur med flera fält, är datatyperna mer flexibla eftersom de kan inkluderas var som helst i schemastrukturen medan fältgrupper bara kan läggas till på rotnivån. Se [slutpunktsguide för datatyper](./data-types.md) om du vill ha mer information om hur du arbetar med datatyper i API:t.

## Beskrivningar

Beskrivare är uppsättningar metadata som tilldelas till specifika fält i ett schema, och ger olika sammanhangsberoende detaljer, inklusive hur dessa fält (och själva schemat) är relaterade till andra scheman. Varje schema kan ha en eller flera beskrivningsentiteter tillämpade och det finns flera olika beskrivningstyper som kan användas i olika syften. Se [slutpunktshandbok för beskrivningar](./descriptors.md) om du vill ha mer information om hur du arbetar med beskrivningar i API:t, och en översikt över de olika beskrivningstyperna och deras användningsfall.

## Unions

Med Platform kan du skapa scheman för särskilda användningsfall, men du kan också skapa en&quot;union&quot; av scheman som tillhör en viss klass. Ett unionsschema samlar fälten för alla scheman som delar samma klass i en enda representation. Genom att aktivera ett schema för användning med [Kundprofil i realtid](../../profile/home.md)blir det schemat inkluderat i unionen för sin särskilda klass. Det innebär att det inte går att redigera fackscheman direkt och att de bara kan påverkas om du inkluderar eller utesluter scheman för användning i profilen.

Mer information om hur du visar föreningar i API:t för schematabellen finns i [slutpunktshandbok för föreningar](./unions.md).

## CSV till schemakonvertering {#csv-to-schema}

Du kan automatiskt generera ett XDM-schema med en CSV-fil som mall, vilket gör att du kan skapa mallar för att importera schemafält gruppvis och skära ned på manuellt API- eller gränssnittsarbete.

Se [Slutpunktshandbok för CSV-konvertering till schema](./export.md) för mer information.

>[!NOTE]
>
>Du kan också använda användargränssnittet för att [mappa en CSV-fil till ett schema med hjälp av AI-genererade rekommendationer](../../ingestion/tutorials/map-csv/recommendations.md) (för närvarande i betaversion).

## Exportera {#export}

Med API:t för schemaregister kan du överföra och dela XDM-resurser mellan sandlådor och organisationer. För alla scheman, fältgrupper och datatyper kan du generera en exportnyttolast som innehåller resursstrukturen och eventuella beroende resurser. Denna nyttolast kan sedan användas för att importera resursen till en målsandlåda och en målorganisation.

Se [slutpunktsguide för export](./export.md) om du vill ha mer information om hur du skapar en exportnyttolast för en befintlig XDM-resurs.

## Import

Om du använder [export](#export) eller [CSV till schemakonvertering](./import.md) slutpunkter för att skapa en exportnyttolast kan du skicka den nyttolasten till en målorganisation och sandlåda för att importera de angivna resurserna.

Se [importera slutpunktsguide](./export.md) om du vill ha mer information om hur du genererar XDM-resurser från exportnyttolaster.

## Exempeldata

Du kan generera exempeldata för ett angivet schema i schemabiblioteket. Svarsobjektet som returneras kan sedan användas som källa för dataöverföring.

Se [exempeldatas slutpunktsguide](./sample-data.md) om du vill ha mer information om användningen av den här slutpunkten.

## Granskningslogg

Schemaregistret innehåller en logg över alla ändringar som har gjorts för en resurs (klass, fältgrupp, datatyp eller schema) mellan olika uppdateringar. Du kan hämta loggen för en viss resurs genom att ange dess `$id` eller `meta:altId` i sökvägen för en GET-begäran till den här slutpunkten.

Se [slutpunktshandbok för granskningslogg](./audit-log.md) om du vill ha mer information om användningen av den här slutpunkten.

## Nästa steg

Om du vill börja ringa anrop med API:t för schemaregister läser du [komma igång-guide](./getting-started.md) Välj sedan en av slutpunktsstödlinjerna och lär dig hur du använder specifika slutpunkter.
