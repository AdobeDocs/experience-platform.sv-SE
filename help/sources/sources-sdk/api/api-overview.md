---
keywords: Experience Platform;hem;populära ämnen;källor;kopplingar;källkopplingar;källor sdk;sdk;SDK
title: Självbetjänade källor (Batch SDK) API-guide
description: Det här dokumentet innehåller en översikt över processen att skapa en ny källa, inklusive steg för hur du hämtar, skriver och skickar en ny anslutningsspecifikation med API:t för Flow Service.
exl-id: 7e827989-207b-41e2-84d6-5ecb754bebb6
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 0%

---

# Självbetjänade källor (Batch SDK) API-guide

Det här dokumentet innehåller en översikt över processen att skapa en ny källa, inklusive steg för hur du skriver och skickar en ny anslutningsspecifikation med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

[!DNL Flow Service] används för att samla in och centralisera kunddata från olika källor inom plattformen. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som gör att du enkelt kan konfigurera källanslutningar till olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera dina tredjepartssystem, ange tider för att få tillgång till dem och hantera dataöverföringshastigheten.

API:t [!DNL Flow Service] innehåller flera slutpunkter som gör att du programmässigt kan hantera anslutnings- och flödesspecifikationerna för en ny källa som du integrerar via självbetjäningskällor (Batch SDK).

## Skapa en ny anslutningsspecifikation

Det första steget när du konfigurerar en ny källa är att skapa en ny anslutningsspecifikation.

Anslutningsspecifikationerna returnerar en källas kopplingsegenskaper. De innehåller autentiseringsspecifikationer som är relaterade till att skapa bas- och källanslutningar samt ett fast anslutnings-ID som tilldelats en viss källa. Anslutningsspecifikationerna är innehavar- och organisationsagnostiker. En typisk anslutningsspecifikation innehåller grundläggande information om en viss källa samt tre olika avsnitt: `authSpec`, `sourceSpec` och `exploreSpec`.

Detaljerade instruktioner finns i guiden om att [skapa en ny anslutningsspecifikation](./create.md). Information om egenskaper och värden som används för en anslutningsspecifikation, inklusive information om konfigurering av autentisering, källa och utforska specifikationer, finns i dokumentet [för konfigurationsalternativ](../config/config.md).

## Uppdatera flödesspecifikationer

När du har skapat en anslutningsspecifikation måste du lägga till flödesspecifikationen `RestStorageToAEP` för att göra det möjligt för källan att skapa ett dataflöde.

Flödesspecifikationer innehåller information som definierar ett flöde, inklusive käll- och målanslutnings-ID:n som stöds, transformeringsspecifikationer som behövs för att kunna tillämpas på data samt schemaläggningsparametrar som krävs för att generera ett flöde.

Detaljerade instruktioner finns i guiden om [uppdatering av flödesspecifikationer](./update-flow-specs.md).

## Uppdatera anslutningsspecifikationen

Du kan uppdatera din anslutningsspecifikation genom att göra en PUT-begäran till [!DNL Flow Service]-API:t. Mer information finns i guiden om [att uppdatera anslutningsspecifikationerna](./update-connection-specs.md).

## Skicka din källa

Om du vill skicka källan för integrering till Experience Platform måste du först slutföra hela [!DNL Flow Service] API-arbetsflödet för källor för att se till att källan fungerar som den ska. Om din källa fungerar som den ska kan du fortsätta och kontakta din Adobe-representant för att få en bekräftelse och en befordran. Mer information finns i guiden om att [testa och skicka källan](./submit.md)

## Nästa steg

Om du vill börja använda API:t [!DNL Flow Service] och skapa en ny källa via självbetjäningskällor (Batch SDK) läser du [ komma igång-guiden](./getting-started.md) och väljer sedan en av slutpunktshandböckerna för att lära dig hur du använder specifika slutpunkter.
