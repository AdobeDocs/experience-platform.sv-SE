---
keywords: Experience Platform;hem;populära ämnen;källor;kopplingar;källkopplingar;källor sdk;sdk;SDK
solution: Experience Platform
title: Självbetjänade källor (batch-SDK) - översikt
description: Adobe Experience Platform Self-Serve Sources (Batch SDK) är en uppsättning konfigurations-API:er som gör att du kan integrera en REST API-baserad källa med API:t för Flow Service för att överföra data till Experience Platform.
exl-id: 5d5449ad-a1ba-402b-a281-0b2d8b704f32
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---

# Självbetjänade källor (Batch SDK) - översikt

Adobe Experience Platform Self-Serve Sources (Batch SDK) är ett ramverk som gör att du kan integrera en REST API-baserad källa till källkatalogen i Experience Platform med hjälp av [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Självbetjäningskällor (Batch SDK) innehåller en uppsättning konfigurations-API:er för att skapa en egen källa och överföra batchdata till Experience Platform.

Med självbetjäningskällor (batch-SDK) kan du:

* Konfigurera och integrera en ny källa till Experience Platform-katalogen med [!DNL Flow Service] API.
* Definiera specifikationer för källan, inklusive information om vilka autentiseringstyper som stöds och hur resursdata hämtas.
* Skapa användarinriktad dokumentation för den nya källan.

Dokumentationen för självbetjäningskällor innehåller anvisningar om hur du konfigurerar, testar och släpper en REST API-baserad källintegration med Experience Platform, och hur du gör att källan blir en del av den ständigt växande källkatalogen.

![katalog](./assets/catalog.png)

## Om källor

Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av Experience Platform-tjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Mer information om källor och en lista över olika källor som för närvarande stöds på Experience Platform finns i [källöversikt](../home.md).

## Skapa en källa

Genom självbetjäningskällor kan ni integrera er egen REST API-baserade källa och överföra data till Experience Platform med [!DNL Flow Service]. Du kan integrera en källa i Experience Platform-källkatalogen genom att skapa, konfigurera och skicka en ny anslutningsspecifikation via [!DNL Flow Service] API.

Se guiden [skapa en ny anslutningsspecifikation](./api/api-overview.md) om du vill ha information om hur du integrerar en ny källa för Experience Platform.

## Dokumentera källan

När du har skapat källan kan du se [handbok](./documentation/doc-overview.md) för instruktioner om hur du dokumenterar källan via [!DNL GitHub] webbgränssnitt eller via din egen textredigerare.

## Högnivåprocess

Hur du konfigurerar källan i Experience Platform beskrivs nedan:

* Läs [Självbetjänade källor (Batch SDK) API-guide](./api/api-overview.md).
   * Läs [komma igång-guide](./api/getting-started.md).
   * Följ självstudiekursen på [skapa en ny anslutningsspecifikation](./api/create.md).
   * Följ självstudiekursen på [uppdatera anslutningsspecifikationen](./api/update-connection-specs.md).
   * Följ självstudiekursen på [lägga till ditt nya anslutningsspecifikation-ID i en flödesspecifikation](./api/update-flow-specs.md)
   * [Skicka din nya källa](./api/submit.md).
* Om du vill få en bättre förståelse för strukturen och egenskaperna i en anslutningsspecifikation kan du läsa guiden på [konfigurationsalternativ för självbetjäningskällor (batch-SDK)](./config/config.md).
   * Läs guiden på [konfigurera dina autentiseringsspecifikationer](./config/authspec.md) för att få en bättre förståelse för de olika autentiseringstyper som du kan använda för källan.
   * Läs guiden på [konfigurera dina källspecifikationer](./config/sourcespec.md) om du vill ha information om olika sidnumreringstyper, schemaläggningsformat och anpassade scheman som kan konfigureras för källan.
   * Läs guiden på [konfigurera dina specifikationer](./config/explorespec.md) om du vill ha information om hur du definierar de parametrar som krävs för att utforska och inspektera objekt som finns i källan.
* Om du vill börja dokumentera källan läser du [översikt över hur du skapar dokumentation för självbetjäningskällor](./documentation/doc-overview.md)
   * Du kan använda den här [dokumentationsmall för käll-API](./documentation/template.md) för att strukturera API-dokumentationen.
   * Du kan använda den här [dokumentationsmall för källanvändargränssnitt](./documentation/ui-template.md) för att strukturera användargränssnittets dokumentation.
   * Se guiden [med GitHub-webbgränssnittet](./documentation/github.md) för steg om hur du skapar dokumentation med GitHub.
   * Se guiden [använda en textredigerare](./documentation/text-editor.md) för steg om hur du skapar dokumentation med din lokala dator.
