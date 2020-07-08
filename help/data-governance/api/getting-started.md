---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Utvecklarhandbok för DULE Policy Service API
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 0%

---


# Utvecklarhandbok för DULE [!DNL Policy Service] API

Varumärkning och verkställighet av dataanvändning (DULE) är kärnmekanismen i Adobe Experience Platform datastyrning. DULE Policy Service tillhandahåller ett RESTful-API som gör att du kan skapa och hantera dataanvändningsprinciper för att avgöra vilka marknadsföringsåtgärder som kan vidtas mot data som har märkts med vissa dataanvändningsetiketter.

Det här dokumentet innehåller anvisningar för hur du utför nyckelåtgärder som är tillgängliga i principtjänstens API. Om du ännu inte har gjort det börjar du med att läsa igenom [datastyrningsöversikten](../home.md) för att bekanta dig med DULE-ramverket. Stegvisa instruktioner för att skapa och verkställa DULE-regler finns i självstudiekursen om [DULE-principer](../policies/create.md).

Det här dokumentet innehåller en introduktion till de centrala koncept som du behöver känna till innan du försöker anropa API:t för principtjänsten.

## Komma igång med DULE [!DNL Policy Service]

Innan du börjar arbeta med [!DNL Policy Service]måste data på [!DNL Experience Platform] ha rätt DULE-etiketter. Fullständiga stegvisa instruktioner för att använda dataanvändningsetiketter på datauppsättningar och fält finns i användarhandboken för [DULE-etiketter](../labels/user-guide.md).

## Förutsättningar

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Datastyrning](../home.md): Ramverket som [!DNL Experience Platform] genomdriver efterlevnad av dataanvändning.
   * [DULE-etiketter](../labels/overview.md): Dataanvändningsetiketter används i XDM-datafält (Experience Data Model), vilket anger begränsningar för hur data kan nås.
* [Experience Data Model (XDM) System](../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata.
* [Kundprofil](../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [Sandlådor](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda Platform-instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

## Läser exempel-API-anrop

Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguiden.

## Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till API: [!DNL Platform] er måste du först slutföra [autentiseringssjälvstudiekursen](../../tutorials/authentication.md). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

* Behörighet: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i [!DNL Experience Platform], inklusive de som tillhör [!DNL Data Governance], isoleras till specifika virtuella sandlådor. Alla förfrågningar till API: [!DNL Platform] er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Platform]finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

* Innehållstyp: application/json

## Kärna eller anpassade resurser

I API:t [!DNL Policy Service] kallas alla policyer och marknadsföringsåtgärder antingen `core` eller `custom` resurser.

Resurserna är sådana som definieras och underhålls av Adobe, medan `core` `custom` resurser skapas och underhålls av enskilda kunder och därför är unika och synliga enbart för den IMS-organisation som skapade dem. Därför är listnings- och uppslagsåtgärder (`GET`) de enda åtgärder som tillåts för `core` resurser, medan listnings-, uppslags- och uppdateringsåtgärder (`POST`, `PUT`, `PATCH`och `DELETE`) är tillgängliga för `custom` resurser.

## Policystatus

Dataanvändningsprinciper kan ha en av tre möjliga statusvärden: `DRAFT`, `ENABLED`eller `DISABLED`.

Som standard deltar endast ENABLED-principer i policyutvärderingen.

Du kan också ta hänsyn till UTKAST-principer i principutvärderingen, men bara genom att ställa in frågeparametern `?includeDraft=true`. Mer information om policyutvärdering finns i dokumentet om [policytillämpning](../enforcement/overview.md) i slutet av det här dokumentet.

## Namn på marknadsföringsåtgärder {#marketing-actions}

Marknadsföringsåtgärdsnamn är unika identifierare för marknadsföringsåtgärder. Varje `core` marknadsföringsåtgärd har ett unikt namn som gäller för alla IMS-organisationer. Dessa namn definieras och underhålls av Adobe. Samtidigt är alla kunddefinierade marknadsföringsåtgärder (`custom` resurser) unika inom din enskilda organisation och är inte synliga eller delade med andra IMS-organisationer.

Steg för att arbeta med marknadsföringsåtgärder i API:t beskrivs senare i avsnittet [!DNL Policy Service] Marknadsföringsåtgärder [](#marketing-actions) i det här dokumentet.

## Nästa steg

Nu när du har de nödvändiga kunskaperna och autentiseringsuppgifterna kan du fortsätta att läsa de exempel-API-anrop som finns i den här utvecklarhandboken:

* [Marknadsföringsåtgärder](marketing-actions.md)
* [Profiler](policies.md)