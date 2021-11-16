---
keywords: Experience Platform;hem;populära ämnen;källor;kopplingar;källkopplingar;källor sdk;sdk;SDK
title: Sources SDK API Guide (beta)
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över processen att skapa en ny källa, inklusive steg för hur du hämtar, skriver och skickar en ny anslutningsspecifikation med API:t för Flow Service.
hide: true
hidefromtoc: true
source-git-commit: bfe6be73ed05b494a4a3eb1153e53ee8b9864ecf
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---

# Sources SDK API Guide (beta)

>[!IMPORTANT]
>
>SDK:n för källor är för närvarande i betaversion och din organisation har kanske inte åtkomst till den än. Funktionerna som beskrivs i den här dokumentationen kan komma att ändras.

I det här dokumentet finns en översikt över processen att skapa en ny källa, inklusive steg för hur du skriver och skickar en ny anslutningsspecifikation med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

[!DNL Flow Service] används för att samla in och centralisera kunddata från olika källor inom plattformen. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som gör att du enkelt kan konfigurera källanslutningar till olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera dina tredjepartssystem, ange tider för att få tillgång till dem och hantera dataöverföringshastigheten.

The [!DNL Flow Service] API har flera slutpunkter som gör att du kan hantera anslutnings- och flödesspecifikationerna programmatiskt för en ny källa som du integrerar via Sources SDK.

## Skapa en ny anslutningsspecifikation

Det första steget när du konfigurerar en ny källa är att skapa en ny anslutningsspecifikation.

Anslutningsspecifikationerna returnerar en källas kopplingsegenskaper. De innehåller autentiseringsspecifikationer som relaterar till att skapa bas- och källanslutningar och ett fast anslutningsspecifikations-ID som tilldelats en viss källa. Anslutningsspecifikationerna är innehavar- och IMS-organisationstjänster. En typisk anslutningsspecifikation innehåller grundläggande information om en viss källa samt tre olika avsnitt: `authSpec`, `sourceSpec`och `exploreSpec`.

Detaljerade anvisningar finns i handboken på [skapa en ny anslutningsspecifikation](./create.md). Information om egenskaper och värden som används för en anslutningsspecifikation, inklusive information om konfigurering av autentisering, källa och utforska specifikationer, finns i [konfigurationsalternativdokument](../config/config.md).

## Uppdatera flödesspecifikationer

När du har skapat en anslutningsspecifikation måste du lägga till `RestStorageToAEP` flödesspecifikation som gör att källan kan skapa ett dataflöde.

Flödesspecifikationer innehåller information som definierar ett flöde, inklusive käll- och målanslutnings-ID:n som stöds, transformeringsspecifikationer som behövs för att kunna tillämpas på data samt schemaläggningsparametrar som krävs för att generera ett flöde.

Detaljerade anvisningar finns i handboken på [uppdatera flödesspecifikationer](./update-flow-specs.md).

## Uppdatera anslutningsspecifikationen

Du kan uppdatera din anslutningsspecifikation genom att göra en PUT-förfrågan till [!DNL Flow Service] API. Se guiden [uppdatera dina anslutningsspecifikationer](./update-connection-specs.md) för mer information.

## Skicka din källa

Om du vill skicka in källan för integrering till Experience Platform måste du först slutföra hela [!DNL Flow Service] API-arbetsflöde för källor för att säkerställa att källan fungerar som den ska. Om din källa fungerar som den ska kan du fortsätta och kontakta din Adobe-representant för att få en bekräftelse och en befordran. Se guiden [testar och skickar källan](./submit.md) för mer information

## Nästa steg

Börja använda [!DNL Flow Service] API och skapa en ny källa via Sources SDK, läs [komma igång-guide](./getting-started.md) Välj sedan en av slutpunktsstödlinjerna och lär dig hur du använder specifika slutpunkter.