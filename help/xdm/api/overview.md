---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;
solution: Experience Platform
title: Utvecklarhandbok för API för schematabell
description: 'Med API:t för schemaregister kan du programmässigt hantera alla scheman och tillhörande XDM-resurser som är tillgängliga i Experience Platform. '
topic: developer guide
translation-type: tm+mt
source-git-commit: 33f9ee45e8dd649d23f9b3b4f03ecf00d8e18fd2
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 0%

---


# [!DNL Schema Registry] Utvecklarhandbok för API

Den [!DNL Schema Registry] används för att komma åt schemabiblioteket i Adobe Experience Platform, med ett användargränssnitt och RESTful API som alla tillgängliga biblioteksresurser kan nås från.

API:t för schemaregister innehåller flera slutpunkter som gör att du kan hantera alla scheman och relaterade XDM-resurser (Experience Data Model) som är tillgängliga inom plattformen. Detta gäller även de som definieras av Adobe, [!DNL Experience Platform] partners och leverantörer vars program du använder.

Dessa slutpunkter beskrivs nedan. Besök de enskilda slutpunktshandböckerna för mer information och se [komma igång-guiden](./getting-started.md) för viktig information om obligatoriska huvuden, läsning av exempel-API-anrop med mera.

>[!IMPORTANT]
>
>XDM använder JSON-schemaformatering för att beskriva och validera strukturen för importerade kundupplevelsedata. Innan du börjar arbeta med API:t för schemaregister bör du läsa den [officiella JSON-schemadokumentationen](https://json-schema.org/) för att få en bättre förståelse för den underliggande tekniken.

Om du vill visa alla tillgängliga slutpunkter och CRUD-åtgärder går du till API-referensen [för](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)schemaregister.

## Scheman

XDM-scheman representerar och validerar strukturen och formatet för data som hämtas till Platform. Ett schema består av en klass och noll eller flera mixiner. Du kan skapa, visa, redigera och ta bort scheman med hjälp av `/schemas` slutpunkten. Mer information om hur du använder den här slutpunkten finns i [schemas slutpunktshandbok](./schemas.md).

En steg-för-steg-guide om hur du skapar ett fullständigt schema i API:t för schemaregister, inklusive hur du skapar och lägger till blandningar och datatyper, finns i självstudiekursen [för att skapa](../tutorials/create-schema-api.md)API-schema.

## Beteenden

Beteenden definierar den typ av data som ett schema beskriver. Varje XDM-klass måste referera till ett specifikt beteende, som alla scheman som använder den klassen ärver. Se [beteendeslutpunktshandboken](./behaviors.md) för att lära dig hur du visar tillgängliga beteenden i API:t.

## Klasser

En klass definierar den grundläggande strukturen för gemensamma egenskaper som alla scheman baserade på den klassen måste innehålla, och avgör vilka mixar som kan användas i dessa scheman. Alla klasser måste kopplas till ett befintligt beteende. Mer information om hur du arbetar med klasser i API finns i [klassernas slutpunktshandbok](./classes.md) .

## Blandningar

Blandningar är återanvändbara komponenter som definierar ett eller flera fält som representerar ett visst koncept, till exempel en enskild person, en postadress eller en webbläsarmiljö. Blandningar är avsedda att ingå som en del av ett schema som implementerar en kompatibel klass, beroende på beteendet hos de data de representerar (post- eller tidsserie). Läs slutpunktshandboken för [mixins](./mixins.md) om du vill lära dig hur du arbetar med blandningar i API:t.

## Datatyper

Datatyper används som referenstypfält i klasser eller blandningar på samma sätt som grundläggande litteralfält, med den största skillnaden är att datatyper kan definiera flera underfält. Även om de liknar blandningar i genom att de medger konsekvent användning av en struktur med flera fält, är datatyperna mer flexibla eftersom de kan inkluderas var som helst i schemastrukturen medan mixar bara kan läggas till på rotnivån. Mer information om hur du arbetar med datatyper i API finns i guiden [för](./data-types.md) datatyper.

## Beskrivningar

Beskrivare är uppsättningar metadata som tilldelas till specifika fält i ett schema, och ger olika sammanhangsberoende detaljer, inklusive hur dessa fält (och själva schemat) är relaterade till andra scheman. Varje schema kan ha en eller flera beskrivningsentiteter tillämpade och det finns flera olika beskrivningstyper som kan användas i olika syften. Mer information om hur du arbetar med beskrivningar i API:t finns i [beskrivningens slutpunktshandbok](./descriptors.md) , samt en översikt över de olika beskrivningstyperna och deras användningsfall.

## Unions

Med Platform kan du skapa scheman för särskilda användningsfall, men du kan också skapa en&quot;union&quot; av scheman som tillhör en viss klass. Ett unionsschema samlar fälten för alla scheman som delar samma klass i en enda representation. Genom att aktivera ett schema för användning med kundprofilen [i](../../profile/home.md)realtid, inkluderas det schemat i unionen för sin särskilda klass. Det innebär att det inte går att redigera fackscheman direkt och att de bara kan påverkas om du inkluderar eller utesluter scheman för användning i profilen.

Om du vill lära dig hur du visar föreningar i API:t för schematabellen läser du i [slutpunktshandboken](./unions.md)för föreningar.

## Exportera/importera

Med API:t för schemaregister kan du överföra och dela XDM-resurser mellan sandlådor och IMS-organisationer. För alla scheman, mixin och datatyper kan du generera en exportnyttolast som innehåller resursstrukturen och alla beroende resurser. Denna nyttolast kan sedan användas för att importera resursen till en målsandlåda och IMS-organisation.

Mer information om hur du använder den här slutpunkten finns i API-referensen [för](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) schemaregistret.

## Exempeldata

Du kan generera exempeldata för ett angivet schema i schemabiblioteket. Svarsobjektet som returneras kan sedan användas som källa för dataöverföring.

Mer information om hur du använder den här slutpunkten finns i API-referensen [för](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) schemaregistret.

## Granskningslogg

Schemaregistret innehåller en logg över alla ändringar som har gjorts för en resurs (klass, mixin, datatyp eller schema) mellan olika uppdateringar. Du kan hämta loggen för en viss resurs genom att ange dess `$id` eller `meta:altId` i sökvägen för en GET-begäran till den här slutpunkten.

Mer information om hur du använder den här slutpunkten finns i API-referensen [för](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) schemaregistret.

## Nästa steg

Om du vill börja ringa anrop med API:t för schemaregistret läser du [Komma igång-guiden](./getting-started.md) och väljer sedan en av slutpunktshandböckerna för att lära dig hur du använder specifika slutpunkter.