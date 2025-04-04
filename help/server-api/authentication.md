---
title: Autentisering
description: Lär dig hur du konfigurerar autentisering för Adobe Experience Platform Edge Network Server API.
exl-id: 73c7a186-9b85-43fe-a586-4c6260b6fa8c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 1%

---

# Autentisering {#authentication}

## Översikt

[!DNL Edge Network Server API] hanterar både autentiserad och oautentiserad datainsamling, beroende på händelsekällan och API-samlingsdomänen.

För varje begäran verifierar [!DNL Server API] datastream [!DNL access type]-inställningen. Med den här inställningen kan kunderna konfigurera en datastam för att acceptera antingen autentiserade data eller både autentiserade och oautentiserade data. Som standard accepteras båda datatyperna.

Mer information om hur du konfigurerar åtkomsttypen för datastream finns i dokumentationen om hur du [skapar och konfigurerar ett datastream](../datastreams/overview.md#create).

Nedan visas en sammanfattning av beteendet, baserat på datastream [!DNL Access Type]-konfigurationen och slutpunkten som begäran tas emot på.

| [!DNL Access Type] | edge.adobedc.net | server.adobedc.net |
|-----------------|-------------------------------|-----------------------|
| blandad (standard) | Autentiserar inte begäran | Autentiserar begäran |
| autentiserad | Autentiserar begäran | Autentiserar begäran |

API-anrop från en privat server på `server.adobedc.net` ska alltid autentiseras.

## Förhandskrav {#prerequisites}

Innan du kan ringa samtal till [!DNL Server API] måste du kontrollera att du uppfyller följande krav:

* Du har ett organisationskonto med tillgång till Adobe Experience Platform.
* Ditt Experience Platform-konto har rollerna `developer` och `user` aktiverade för Adobe Experience Platform API-produktprofilen. Kontakta din [Admin Console](../access-control/home.md)-administratör om du vill aktivera de här rollerna för ditt konto.
* Du har en Adobe ID. Om du inte har någon Adobe ID går du till [Adobe Developer Console](https://developer.adobe.com/console) och skapar ett nytt konto.

## Samla in inloggningsuppgifter {#credentials}

För att kunna anropa Experience Platform API:er måste du först slutföra [autentiseringssjälvstudiekursen](../landing/api-authentication.md). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla Experience Platform API-anrop, vilket visas nedan:

* Behörighet: Bärare `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Resurser i Experience Platform kan isoleras till specifika virtuella sandlådor. I förfrågningar till Experience Platform API:er kan du ange namn och ID för sandlådan som åtgärden ska utföras i. Dessa är valfria parametrar.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i Experience Platform finns i översiktsdokumentationen för [sandlådan](../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver en extra medietypsrubrik:

* Innehållstyp: `application/json`

## Konfigurera skrivbehörigheter för datauppsättning {#dataset-write-permissions}

Om du vill konfigurera skrivbehörigheter för datauppsättningar går du till [Admin Console](https://adminconsole.adobe.com), letar reda på produktprofilen som är kopplad till din API-nyckel och anger följande behörigheter:

* I avsnittet [!UICONTROL Sandboxes] markerar du datastream-sandlådan.
* Välj behörigheten **[!UICONTROL Manage Datasets]** i avsnittet [!UICONTROL Data Management].

## Felsöka auktoriseringsfel {#troubleshooting-authorization}

| Felkod | Felmeddelande | Beskrivning |
| --- | --- | --- |
| `EXEG-0500-401` | Ogiltig auktoriseringstoken | Det här felmeddelandet visas i följande situationer:  <ul><li>Rubrikvärdet `authorization` saknas.</li><li>Rubrikvärdet `authorization` innehåller inte den nödvändiga `Bearer`-token.</li><li>Angiven auktoriseringstoken har ett ogiltigt format.</li><li>Datastream kräver autentisering, men begäran saknar obligatoriska huvuden.</li></ul> |
| `EXEG-0501-401` | Ogiltig token för användarauktorisering | Det här felmeddelandet visas i följande situationer: <ul><li>API-anropet saknar det obligatoriska `x-user-token`-huvudet.</li><li>Angiven användartoken har ett ogiltigt format.</li></ul> |
| `EXEG-0502-401` | Ogiltig auktoriseringstoken | Det här felmeddelandet visas när den angivna auktoriseringstoken har ett giltigt format (JWT), men signaturen är ogiltig. Gå till självstudiekursen [för autentisering](../landing/api-authentication.md) och lär dig hur du hämtar en giltig JWT-token. |
| `EXEG-0503-401` | Ogiltig auktoriseringstoken | Det här felmeddelandet visas när den angivna auktoriseringstoken har upphört att gälla. Gå igenom självstudiekursen [för autentisering](../landing/api-authentication.md) och generera en ny token. |
| `EXEG-0504-401` | Den obligatoriska produktkontexten saknas | Det här felmeddelandet visas i följande situationer:  <ul><li>Utvecklarkontot har inte åtkomst till Adobe Experience Platform produktkontext.</li><li>Företaget har ännu inte rätt till Adobe Experience Experience Platform.</li></ul> |
| `EXEG-0505-401` | Obligatoriskt auktoriseringstokenomfång saknas | Detta fel gäller endast autentisering av tjänstkonto. Felmeddelandet visas när tjänstauktoriseringstoken som ingår i anropet tillhör ett tjänstkonto som inte har åtkomst till IMS-scopet `acp.foundation`. |
| `EXEG-0506-401` | Sandlådan är inte tillgänglig för skrivning | Det här felmeddelandet visas när utvecklarkontot inte har `WRITE`-åtkomst till Experience Platform-sandlådan där datastream definieras. |
