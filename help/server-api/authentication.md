---
title: Autentisering
description: Lär dig hur du konfigurerar autentisering för Adobe Experience Platform Edge Network Server API.
exl-id: 73c7a186-9b85-43fe-a586-4c6260b6fa8c
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 1%

---

# Autentisering {#authentication}

## Översikt

The [!DNL Edge Network Server API] hanterar både autentiserad och oautentiserad datainsamling, beroende på händelsekällan och API-samlingsdomänen.

För varje begäran [!DNL Server API] verifierar datastream [!DNL access type] inställning. Med den här inställningen kan kunderna konfigurera en datastam för att acceptera antingen autentiserade data eller både autentiserade och oautentiserade data. Som standard accepteras båda datatyperna.

Mer information om hur du konfigurerar åtkomsttypen för datastream finns i dokumentationen om hur du [skapa och konfigurera ett datastream](../edge/datastreams/overview.md#create).

Nedan visas en sammanfattning av beteendet utifrån datastream [!DNL Access Type] konfiguration och slutpunkten som begäran tas emot på.

| [!DNL Access Type] | edge.adobedc.net | server.adobedc.net |
|-----------------|-------------------------------|-----------------------|
| blandad (standard) | Autentiserar inte begäran | Autentiserar begäran |
| autentiserad | Autentiserar begäran | Autentiserar begäran |

API-anrop från en privat server på `server.adobedc.net` ska alltid vara autentiserade.

## Förutsättningar {#prerequisites}

Innan du kan ringa samtal till [!DNL Server API]kontrollerar du att följande krav uppfylls:

* Du har ett organisationskonto med tillgång till Adobe Experience Platform.
* Ditt Experience Platform-konto har `developer` och `user` roller har aktiverats för Adobe Experience Platform API-produktprofilen. Kontakta [Admin Console](../access-control/home.md) administratör för att aktivera de här rollerna för ditt konto.
* Du har en Adobe ID. Om du inte har någon Adobe ID går du till [Adobe Developer Console](https://developer.adobe.com/console) och skapa ett nytt konto.

## Samla in inloggningsuppgifter {#credentials}

För att kunna ringa anrop till plattforms-API:er måste du först slutföra [självstudiekurs om autentisering](../landing/api-authentication.md). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, vilket visas nedan:

* Behörighet: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Resurser i Experience Platform kan isoleras till specifika virtuella sandlådor. I förfrågningar till plattforms-API:er kan du ange namnet och ID:t för sandlådan som åtgärden ska utföras i. Dessa är valfria parametrar.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i Experience Platform finns i [översiktsdokumentation för sandlåda](../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

* Innehållstyp: `application/json`

## Konfigurera skrivbehörigheter för datauppsättning {#dataset-write-permissions}

Om du vill konfigurera skrivbehörigheter för datauppsättningar går du till [Admin Console](https://adminconsole.adobe.com), leta reda på produktprofilen som är kopplad till din API-nyckel och ange följande behörigheter:

* I [!UICONTROL Sandboxes] markerar du datastream-sandlådan.
* I [!UICONTROL Data Management] väljer du **[!UICONTROL Manage Datasets]** behörighet.

## Felsöka auktoriseringsfel {#troubleshooting-authorization}

| Felkod | Felmeddelande | Beskrivning |
| --- | --- | --- |
| `EXEG-0500-401` | Ogiltig auktoriseringstoken | Det här felmeddelandet visas i följande situationer:  <ul><li>The `authorization` rubrikvärde saknas.</li><li>The `authorization` rubrikvärdet innehåller inte det obligatoriska `Bearer` token.</li><li>Angiven auktoriseringstoken har ett ogiltigt format.</li><li>Datastream kräver autentisering, men begäran saknar obligatoriska huvuden.</li></ul> |
| `EXEG-0501-401` | Ogiltig token för användarauktorisering | Det här felmeddelandet visas i följande situationer: <ul><li>API-anropet saknar det nödvändiga `x-user-token` header.</li><li>Angiven användartoken har ett ogiltigt format.</li></ul> |
| `EXEG-0502-401` | Ogiltig auktoriseringstoken | Det här felmeddelandet visas när den angivna auktoriseringstoken har ett giltigt format (JWT), men signaturen är ogiltig. Kontrollera [självstudiekurs om autentisering](../landing/api-authentication.md) om du vill lära dig hur du får en giltig JWT-token. |
| `EXEG-0503-401` | Ogiltig auktoriseringstoken | Det här felmeddelandet visas när den angivna auktoriseringstoken har upphört att gälla. Gå igenom [självstudiekurs om autentisering](../landing/api-authentication.md) för att generera en ny token. |
| `EXEG-0504-401` | Nödvändig produktkontext saknas | Det här felmeddelandet visas i följande situationer:  <ul><li>Utvecklarkontot har inte åtkomst till Adobe Experience Platform produktkontext.</li><li>Företagskontot har ännu inte rätt till Adobe Experience Platform.</li></ul> |
| `EXEG-0505-401` | Obligatoriskt auktoriseringstokenomfång saknas | Detta fel gäller endast autentisering av tjänstkonto. Felmeddelandet visas när tjänstauktoriseringstoken som ingår i anropet tillhör ett tjänstkonto som inte har åtkomst till `acp.foundation` IMS-omfång. |
| `EXEG-0506-401` | Sandlådan är inte tillgänglig för skrivning | Det här felmeddelandet visas när utvecklarkontot inte har `WRITE` åtkomst till sandlådan Experience Platform där datastream definieras. |
