---
keywords: Experience Platform; säkerhet; ip-åtkomst; validering; API-guide; frågetjänst; IP-verifiering
title: IP-valideringsslutpunkt
description: Lär dig hur du validerar IP-åtkomst för sandlådor i Query Service med hjälp av API-slutpunkten för IP-validering.
role: Developer
source-git-commit: ad1b6d8449a2a3ca9c8422e70769d12e33d8e255
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# IP-valideringsslutpunkt

Använd API-slutpunkten för IP-validering för att kontrollera om en angiven IP-adress har åtkomst till en angiven sandlåda i Query Service. Den här kontrollen bekräftar om åtkomstbegränsningar gäller eller om en IP-adress tillåts få åtkomst till data i en sandlåda.

## Validera IP för sandlådeåtkomst {#validate-ip-for-sandbox-access}

Använd slutpunkten för IP-validering för att kontrollera om en given IP-adress har åtkomst till data för den angivna sandlådan. Om inga IP-begränsningar har konfigurerats för sandlådan tillåts alla IP-adresser som standard. Om det finns befintliga IP- eller CIDR-begränsningar verifierar detta API om den angivna IP-adressen matchar eventuella konfigurerade intervall.

>[!NOTE]
>
>Du kan komma åt den här slutpunkten med antingen **användartokens** eller **tjänsttoken**. Inga specifika rollkrav behövs.

**API-format**

```http
POST /security/validate/ip-access
```

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/security/validate/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
       "ipAddress": "197.2.0.2"
     }'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med ett booleskt värde som anger om IP-adressen är tillåten.

>[!NOTE]
>
>Fältet `isAllowed` i svaret returnerar `true` om den angivna IP-adressen har behörighet att komma åt sandlådan och `false` i annat fall. Detta API har stöd för dynamisk validering av åtkomst och säkerställande av säkerhetsefterlevnad för sandlådemiljöer.

```json
{
"isAllowed": true
}
```
