---
keywords: Experience Platform; säkerhet; ip-åtkomst; QS-Auth; API guide; frågetjänst; IP-intervall
title: IP-åtkomstslutpunkt
description: Lär dig hur du hanterar IP-intervall för sandlådeåtkomst i Query Service med API-slutpunkten för IP Access.
role: Developer
exl-id: fc15ab50-c125-4f00-a311-81fd41697c7d
source-git-commit: bf696c8836407a2fea82e9078201cb1f5004bcf8
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 1%

---

# IP-åtkomstslutpunkt

>[!AVAILABILITY]
>
>Den här funktionaliteten är tillgänglig för kunder som har köpt Data Distiller-tillägget. Kontakta din Adobe-representant om du vill veta mer.

Använd IP Access-slutpunkten för att hantera tillåtna IP-intervall om du vill skydda dataåtkomsten i en angiven frågetjänstsandlåda. Du kan använda detta API för att hämta, konfigurera eller ta bort IP-intervall som är kopplade till organisationens ID.

Du kan utföra följande åtgärder med IP Access-API:t:

- **Hämta alla IP-intervall**
- **Ange nya IP-intervall**
- **Ta bort befintliga IP-intervall**

Det här dokumentet täcker förfrågningar och svar som du kan göra och ta emot från slutpunkten `/security/ip-access`.

>[!NOTE]
>
>Du måste ha en användartoken för att kunna anropa denna API. Information om hur du hämtar obligatoriska värden för varje rubrik finns i [Komma igång-guiden](./getting-started.md) .

## Hämta alla IP-intervall {#fetch-all-ip-ranges}

Hämta en lista över alla IP-intervall som har konfigurerats för din sandlåda. Om inga IP-intervall anges tillåts alla IP-adresser som standard, och svaret returnerar en tom lista i `allowedIpRanges`.

**API-format**

```http
GET /security/ip-access
```

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/security/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med en lista över sandlådans tillåtna IP-intervall.

```json
{
  "imsOrg": "{ORG_ID}",
  "sandboxName": "prod",
  "channel": "data_distiller",
  "allowedIpRanges": [
    {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
    {"ipRange": "101.10.1.1"}
  ]
}
```

Följande tabell innehåller en beskrivning och ett exempel på egenskaperna för svarsschemat:

| Egenskap | Beskrivning | Exempel |
|------------------|---------------------------------------------|-----------------------------------------------------------------------------------------------|
| `imsOrg` | Organisations-ID för sandlådan. | `{ORG_ID}` |
| `sandboxName` | Namn på sandlådan där IP-begränsningar gäller. | `prod` |
| `channel` | Åtkomstläget för IP-begränsningar. Det enda godkända värdet är `data_distiller`. Det här värdet anger att IP-begränsningar tillämpas på PSQL- eller JDBC-anslutningar. | `data_distiller` |
| `allowedIpRanges` | Lista över tillåtna IP-adresser i CIDR- eller fast IP-format. Varje post kan innehålla en valfri beskrivning. | `[{"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"}]` |

>[!NOTE]
>
>Fältet `allowedIpRanges` kan innehålla två typer av IP-specifikationer:<br><ul><li>**CIDR**: CIDR-standardnotation (till exempel `"136.23.110.0/23"`) för att definiera IP-intervall.</li><li>**Fast IP**: En IP-adress för individuella åtkomstbehörigheter (till exempel `"101.10.1.1"`).</li></ul>

## Ange nya IP-intervall

Skriv över befintliga IP-intervall genom att ange en ny lista för sandlådan. Den här åtgärden kräver en fullständig lista över IP-intervall, inklusive alla som inte ändras.

**API-format**

```http
PUT /security/ip-access
```

**Begäran**

```shell
curl -X PUT https://platform.adobe.io/data/foundation/query/security/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "ipRanges": [
       {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
       {"ipRange": "17.102.17.0/23", "description": "VPN-2 gateway IPs"},
       {"ipRange": "101.10.1.1"},
       {"ipRange": "163.77.30.9", "description": "Test server IP"}
     ]
   }'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om de nyligen konfigurerade IP-intervallen.

```json
{
  "imsOrg": "{ORG_ID}",
  "sandboxName": "prod",
  "channel": "data_distiller",
  "allowedIpRanges": [
    {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
    {"ipRange": "17.102.17.0/23", "description": "VPN-2 gateway IPs"},
    {"ipRange": "101.10.1.1"},
    {"ipRange": "163.77.30.9", "description": "Test server IP"}
  ]
}
```

## Ta bort IP-intervall {#delete-ip-ranges}

Ta bort alla konfigurerade IP-intervall för sandlådan. Den här åtgärden tar bort IP-intervallen och returnerar den borttagna IP-listan.

>[!NOTE]
>
>Borttagningsåtgärden gäller för organisations-ID:t (`imsOrg`) och påverkar alla IP-intervall som har konfigurerats för sandlådan.

**API-format**

```http
DELETE /security/ip-access
```

**Begäran**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/security/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om de borttagna IP-intervallen.

```json
{
  "imsOrg": "{ORG_ID}",
  "sandboxName": "prod",
  "channel": "data_distiller",
  "deletedIpRanges": [
    {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
    {"ipRange": "17.102.17.0/23", "description": "VPN-2 gateway IPs"},
    {"ipRange": "101.10.1.1"},
    {"ipRange": "163.77.30.9", "description": "Test server IP"}
  ]
}
```
