---
title: Komma igång med självbetjäningskällor (Streaming SDK)
description: Det här dokumentet innehåller en introduktion till den information som krävs för att du ska kunna skapa en ny källa med hjälp av självbetjäningskällor (Streaming SDK).
hide: true
hidefromtoc: true
source-git-commit: 7744fef9751212a40f8f20df52812d38130c42fc
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# Komma igång med självbetjäningskällor (Streaming SDK)

Med självbetjäningskällor (Streaming SDK) kan du integrera din egen källa för att skicka strömmande data till Adobe Experience Platform. Det här dokumentet innehåller en introduktion till de centrala koncept du behöver känna innan du försöker ringa till [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Högnivåprocess

Hur du konfigurerar källan i Experience Platform beskrivs nedan:

### Integrering

* [Skapa en ny anslutningsspecifikation för Streaming SDK](create.md).
* [Uppdatera specifikationen för strömningsflödet med ditt nya anslutningsspecifikation-ID](update-flow-specs.md).
* [Testa och skicka strömningskällan](submit.md).

### Dokumentation

* Om du vill börja dokumentera källan läser du [översikt över hur du skapar dokumentation för självbetjäningskällor](../documentation/doc-overview.md).
* Läs guiden på [med GitHub-webbgränssnittet](../documentation/github.md) för steg om hur du skapar dokumentation med GitHub.
* Läs guiden på [använda en textredigerare](../documentation/text-editor.md) för steg om hur du skapar dokumentation med din lokala dator.
* [Använd dokumentationsmallen för Streaming SDK API för att dokumentera källan i API:t](streaming-template-api.md).
* [Använd dokumentationsmallen för användargränssnittet för direktuppspelning av SDK för att dokumentera källan i användargränssnittet](streaming-template-ui.md).

Du kan även hämta dokumentationsmallarna nedan:

* [API-dokumentationsmall](../assets/streaming/streaming-template-api.zip)
* [Dokumentationsmall för användargränssnitt](../assets/streaming/streaming-template-ui.zip)

## Förutsättningar

>[!IMPORTANT]
>
>Källan som du integrerar med Experience Platform måste ha stöd för en webkrok som en slutpunkt kan prenumereras på för att kunna skicka uppdateringar.

Om du vill använda självbetjäningskällor (Streaming SDK) måste du se till att du har tillgång till en sandlådeorganisation som har etablerats med Adobe Experience Platform Sources.

Handboken kräver även en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

## Läser exempel-API-anrop

Självbetjäningskällor (Streaming SDK) och [!DNL Flow Service] API-dokumentationen innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om konventionerna som används i dokumentationen för exempel-API-anrop finns i avsnittet om [läsa exempel-API-anrop](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

## Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till plattforms-API:er måste du först slutföra [självstudiekurs om autentisering](https://www.adobe.com/go/platform-api-authentication-en). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop enligt nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alla resurser i Platform, inklusive de som tillhör [!DNL Flow Service], isoleras till specifika virtuella sandlådor. Alla begäranden till Platform API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i plattformen finns i [sandlådedokumentation](../../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

* `Content-Type: application/json`

## Nästa steg

Om du vill börja skapa en ny källa med självbetjäningskällor (Streaming SDK) ska du titta i självstudiekursen om [skapa en ny källa](./create.md).
