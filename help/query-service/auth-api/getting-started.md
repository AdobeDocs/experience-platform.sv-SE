---
keywords: Experience Platform; frågetjänst; IP-åtkomstkontroll; auktorisering; API; komma igång
title: API-guide för auktorisering av frågetjänst
description: Lär dig hur du kommer igång med auktorisering och IP-intervallbegränsningar för säker dataåtkomst i Adobe Experience Platform Query Service.
role: Developer
source-git-commit: eb6558c2cc3faebb2cb14f49f7517227d57f7162
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# API-guide för auktorisering av frågetjänst

Med API:t för frågetjänstens auktorisering får organisationer bättre kontroll över dataåtkomsten via SQL-gränssnittet i Adobe Experience Platform. Du kan använda detta API för att definiera IP-begränsningar, begränsa dataåtkomst till angivna nätverk och förbättra säkerhetsövervakningen.

I den här handboken beskrivs hur du ställer in autentiseringsuppgifter och behörigheter som krävs för att anropa API:t för frågetjänstens auktorisering.

## Komma igång {#getting-started}

I följande avsnitt finns information om hur du förbereder nödvändiga auktoriseringsvärden och gör dina första förfrågningar till API:t för auktorisering av frågetjänst.

### Nödvändiga behörigheter {#required-permissions}

Om du vill aktivera säkra dataåtkomstbegränsningar i frågetjänsten måste du ha behörigheten **[!UICONTROL Manage Allowed List]**. Med den här behörigheten kan organisationer definiera specifika IP-intervall (i IPv4- eller IPv6-format) som har behörighet att komma åt data i plattformen via SQL-gränssnittet. Åtkomst hanteras på sandlådenivå, där användare kan konfigurera en lista över godkända IP-adresser eller CIDR-block som begränsar åtkomsten endast till tillåtna nätverk.

>[!NOTE]
>
>Systemadministratörer kan konfigurera användarbehörigheter från Adobe [Admin Console](https://adminconsole.adobe.com/). Mer information finns i användarhandboken för [Admin Console](https://helpx.adobe.com/se/enterprise/using/admin-console.html).

Följande funktioner är tillgängliga med behörigheten **[!UICONTROL Manage Allowed List]**:

- **Definiera tillåtna IP-intervall**: Endast IP-adresser eller CIDR-block från dessa definierade intervall kan komma åt data i plattformen med SQL via frågetjänsten.
- **Använd kontroller för IP-intervall**: Anslutningar från IP-adresser utanför tillåtna intervall nekas.
- **Gransknings- och aviseringsfunktioner**: Alla åtkomstförsök, inklusive nekade anslutningar, loggas som granskningshändelser. Dessa händelser är tillgängliga i [Adobe Experience Platform granskningsloggar](../../landing/governance-privacy-security/audit-logs/overview.md), vilket möjliggör övervakning av potentiella säkerhetsöverträdelser.

### Samla in värden för obligatoriska rubriker {#gather-values-for-required-headers}

Om du vill anropa API:t för frågetjänstens auktorisering måste du slutföra självstudiekursen [Platform API authentication](../../landing/api-authentication.md), som innehåller värden för obligatoriska huvuden i API-anrop. Inkludera följande rubriker i varje begäran:

- **Behörighet**: `Bearer {ACCESS_TOKEN}`
- **x-api-key**: `{API_KEY}`
- **x-gw-ims-org-id**: `{ORG_ID}`
- **x-sandbox-name**: `{SANDBOX_NAME}`

>[!NOTE]
>
> Mer information om sandlådor finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver också följande rubrik:

- **Innehållstyp**: `application/json`

### Nästa steg

När de nödvändiga behörigheterna och rubrikvärdena har samlats in är du redo att börja konfigurera IP-begränsningar för frågetjänsten. Fortsätt till slutpunktsdokumentationen för detaljerade exempel på CRUD-åtgärder, som omfattar:

- API-format och exempel på par för begäran/svar.
- Huvuden, nyttolaster och svarskoder för varje åtgärd.

Varje API-anropsexempel visar hur du formaterar begäranden och tolkar svar, vilket hjälper dig att få säker åtkomst till dina data i Query Service.

Mer information om hur du konfigurerar och validerar IP-begränsningar finns i dokumentationen för [IP Access-slutpunkten](./ip-access.md) och i dokumentationen för [IP-valideringsslutpunkten](./validate.md).
