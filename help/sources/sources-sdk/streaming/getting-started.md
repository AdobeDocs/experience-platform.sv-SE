---
title: Komma igång med självbetjäningskällor (Streaming SDK)
description: Det här dokumentet innehåller en introduktion till den information som krävs för att du ska kunna skapa en ny källa med självbetjäningskällor (Streaming SDK).
exl-id: 6cc13279-ce0b-45bc-ad25-e2e6aafc2af0
badge: Beta
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---

# Komma igång med självbetjäningskällor (Streaming SDK)

>[!NOTE]
>
>Självbetjäning Källströmning SDK är en betaversion. Läs [källöversikten](../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade källor.

Med självbetjäningskällor (Streaming SDK) kan ni integrera er egen källa för att skicka strömmande data till Adobe Experience Platform. Det här dokumentet innehåller en introduktion till de centrala koncept som du behöver känna till innan du försöker anropa [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Högnivåprocess

Hur du konfigurerar källan i Experience Platform steg för steg beskrivs nedan:

### Integrering

* [Skapa en ny anslutningsspecifikation för direktuppspelning av SDK](create.md).
* [Uppdatera specifikationen för direktuppspelningsflödet med ditt nya anslutningsspecifikation-ID ](update-flow-specs.md).
* [Testa och skicka strömningskällan](submit.md).

### Dokumentation

* Om du vill börja dokumentera källan läser du [översikten om att skapa dokumentation för självbetjäningskällor](../documentation/doc-overview.md).
* Läs guiden på [med GitHub-webbgränssnittet](../documentation/github.md) för steg om hur du skapar dokumentation med GitHub.
* Läs guiden på [med en textredigerare](../documentation/text-editor.md) för steg om hur du skapar dokumentation med din lokala dator.
* [Använd dokumentationsmallen för direktuppspelande SDK API för att dokumentera källan i API:t](streaming-template-api.md).
* [Använd dokumentationsmallen för direktuppspelande SDK-gränssnitt för att dokumentera källan i användargränssnittet](streaming-template-ui.md).

Du kan även hämta dokumentationsmallarna nedan:

* [API-dokumentationsmall](../assets/streaming/streaming-template-api.zip)
* [Dokumentationsmall för användargränssnitt](../assets/streaming/streaming-template-ui.zip)

## Förhandskrav

>[!IMPORTANT]
>
>Källan som du integrerar med Experience Platform måste ha stöd för en webbkrok som en slutpunkt kan prenumereras på för att kunna skicka uppdateringar.

Om du vill använda självbetjäningskällor (Streaming SDK) måste du se till att du har tillgång till en sandlådeorganisation som har etablerats med Adobe Experience Platform Sources.

Handboken kräver även en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster.
* [Sandlådor](../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Experience Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

## Läser exempel-API-anrop

I API-dokumentationen för självbetjäningskällor (Streaming SDK) och [!DNL Flow Service] finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [Så här läser du exempel-API-anrop](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

## Samla in värden för obligatoriska rubriker

För att kunna anropa Experience Platform API:er måste du först slutföra [autentiseringssjälvstudiekursen](https://www.adobe.com/go/platform-api-authentication-en). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alla resurser i Experience Platform, inklusive de som tillhör [!DNL Flow Service], är isolerade till specifika virtuella sandlådor. Alla förfrågningar till Experience Platform API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i Experience Platform finns i [sandlådedokumentationen](../../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare ett huvud:

* `Content-Type: application/json`

## Nästa steg

Om du vill börja skapa en ny källa med självbetjäningskällor (direktuppspelande SDK) ska du titta i självstudiekursen [Skapa en ny källa](./create.md).
