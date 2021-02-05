---
keywords: Experience Platform;hem;populära ämnen;api;API;XDM;XDM system;experience data model;Experience data model;experience data model;data model;data model;data model;schema register;schemaregister;
solution: Experience Platform
title: API-guide för schemaregister
description: Med API:t för schemaregister kan utvecklare programmässigt hantera alla scheman och relaterade XDM-resurser (Experience Data Model) inom Adobe Experience Platform. Följ den här vägledningen när du vill lära dig hur du utför nyckelåtgärder med API:t.
topic: developer guide
translation-type: tm+mt
source-git-commit: e649ab3da077cdd8e98562199b8bdece6108a572
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 0%

---


# [!DNL Schema Registry] API-guide

[!DNL Schema Registry] används för att komma åt schemabiblioteket i Adobe Experience Platform, med ett användargränssnitt och RESTful API från vilket alla tillgängliga biblioteksresurser är tillgängliga.

API:t för schemaregister innehåller flera slutpunkter som gör att du kan hantera alla scheman och relaterade XDM-resurser (Experience Data Model) som är tillgängliga inom plattformen. Detta omfattar de som definieras av Adobe, [!DNL Experience Platform] partners och leverantörer vars program du använder.

Dessa slutpunkter beskrivs nedan. Mer information finns i de enskilda slutpunktshandböckerna och i [komma igång-guiden](./getting-started.md) finns viktig information om obligatoriska huvuden, läsning av exempel-API-anrop med mera.

>[!IMPORTANT]
>
>XDM använder JSON-schemaformatering för att beskriva och validera strukturen för importerade kundupplevelsedata. Innan du börjar arbeta med API:t för schemaregister rekommenderar vi att du granskar [JSON Schema-dokumentationen](https://json-schema.org/) för att få en bättre förståelse för den underliggande tekniken.

Om du vill visa alla tillgängliga slutpunkter och CRUD-åtgärder går du till [API-referens för schemaregister](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

## Scheman

XDM-scheman representerar och validerar strukturen och formatet för data som hämtas till Platform. Ett schema består av en klass och noll eller flera mixiner. Du kan skapa, visa, redigera och ta bort scheman med `/schemas`-slutpunkten. Mer information om hur du använder den här slutpunkten finns i [schemas slutpunktshandbok](./schemas.md).

En steg-för-steg-guide om hur du skapar ett fullständigt schema i API:t för schemaregister, inklusive hur du skapar och lägger till mixiner och datatyper, finns i [självstudiekursen för att skapa API-schema](../tutorials/create-schema-api.md).

## Beteenden

Beteenden definierar den typ av data som ett schema beskriver. Varje XDM-klass måste referera till ett specifikt beteende, som alla scheman som använder den klassen ärver. Se [beteendeslutpunktshandboken](./behaviors.md) för att lära dig hur du visar tillgängliga beteenden i API:t.

## Klasser

En klass definierar den grundläggande strukturen för gemensamma egenskaper som alla scheman baserade på den klassen måste innehålla, och avgör vilka mixar som kan användas i dessa scheman. Alla klasser måste kopplas till ett befintligt beteende. Mer information om hur du arbetar med klasser i API finns i [klassernas slutpunktshandbok](./classes.md).

## Blandningar

Blandningar är återanvändbara komponenter som definierar ett eller flera fält som representerar ett visst koncept, till exempel en enskild person, en postadress eller en webbläsarmiljö. Blandningar är avsedda att ingå som en del av ett schema som implementerar en kompatibel klass, beroende på beteendet hos de data de representerar (post- eller tidsserie). Se [slutpunktshandboken för mixins](./mixins.md) för att lära dig hur du arbetar med mixiner i API:t.

## Datatyper

Datatyper används som referenstypfält i klasser eller blandningar på samma sätt som grundläggande litteralfält, med den största skillnaden är att datatyper kan definiera flera underfält. Även om de liknar blandningar i genom att de medger konsekvent användning av en struktur med flera fält, är datatyperna mer flexibla eftersom de kan inkluderas var som helst i schemastrukturen medan mixar bara kan läggas till på rotnivån. Mer information om hur du arbetar med datatyper i API finns i [slutpunktshandboken för datatyper](./data-types.md).

## Beskrivningar

Beskrivare är uppsättningar metadata som tilldelas till specifika fält i ett schema, och ger olika sammanhangsberoende detaljer, inklusive hur dessa fält (och själva schemat) är relaterade till andra scheman. Varje schema kan ha en eller flera beskrivningsentiteter tillämpade och det finns flera olika beskrivningstyper som kan användas i olika syften. Se [slutpunktshandboken för beskrivningar](./descriptors.md) för mer information om hur du arbetar med beskrivningar i API:t, och en översikt över de olika beskrivningstyperna och deras användningsfall.

## Unions

Med Platform kan du skapa scheman för särskilda användningsfall, men du kan också skapa en&quot;union&quot; av scheman som tillhör en viss klass. Ett unionsschema samlar fälten för alla scheman som delar samma klass i en enda representation. Genom att aktivera ett schema för användning med [Kundprofil för realtid](../../profile/home.md), inkluderas det schemat i unionen för den aktuella klassen. Det innebär att det inte går att redigera fackscheman direkt och att de bara kan påverkas om du inkluderar eller utesluter scheman för användning i profilen.

Mer information om hur du visar fackföreningar i API:t för schemaregister finns i [slutpunktshandboken för föreningar](./unions.md).

## Exportera/importera

Med API:t för schemaregister kan du överföra och dela XDM-resurser mellan sandlådor och IMS-organisationer. För alla scheman, mixin och datatyper kan du generera en exportnyttolast som innehåller resursstrukturen och alla beroende resurser. Denna nyttolast kan sedan användas för att importera resursen till en målsandlåda och IMS-organisation.

Mer information om hur du använder dessa slutpunkter finns i guiden [för export/import av slutpunkter](./export-import.md).

## Exempeldata

Du kan generera exempeldata för ett angivet schema i schemabiblioteket. Svarsobjektet som returneras kan sedan användas som källa för dataöverföring.

Mer information om hur du använder den här slutpunkten finns i [exempeldataguiden](./sample-data.md).

## Granskningslogg

Schemaregistret innehåller en logg över alla ändringar som har gjorts för en resurs (klass, mixin, datatyp eller schema) mellan olika uppdateringar. Du kan hämta loggen för en viss resurs genom att ange dess `$id` eller `meta:altId` i sökvägen för en GET-begäran till den här slutpunkten.

Mer information om hur du använder den här slutpunkten finns i [slutpunktshandboken för granskningsloggen](./audit-log.md).

## Nästa steg

Om du vill börja ringa anrop med API:t för schemaregistret läser du [Komma igång-guiden](./getting-started.md) och väljer sedan en av slutpunktshandböckerna för att lära dig hur du använder specifika slutpunkter.