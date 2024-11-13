---
keywords: Experience Platform; säkerhet; ip-åtkomst; validering; API-guide; frågetjänst; IP-verifiering
title: IP-valideringsslutpunkt
description: Lär dig hur du validerar IP-åtkomst för sandlådor i Query Service med hjälp av API-slutpunkten för IP-validering.
role: Developer
exl-id: 4ce9ab1c-e333-4ed5-a430-43ffec36a46d
source-git-commit: bf696c8836407a2fea82e9078201cb1f5004bcf8
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 3%

---

# IP-valideringsslutpunkt

>[!AVAILABILITY]
>
>Den här funktionaliteten är tillgänglig för kunder som har köpt Data Distiller-tillägget. Kontakta din Adobe-representant om du vill veta mer.

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
