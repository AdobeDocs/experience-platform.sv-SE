---
title: Skapa målgrupps-API-slutpunkt
description: Lär dig hur du skapar metadata för en extern målgrupp med API:t.
hide: true
hidefromtoc: true
source-git-commit: 74fa66e78ac36c8007eb89e8c271d989845c96f0
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 2%

---


# Skapa målgruppsslutpunkt

POST `/audiences`-slutpunkten kan användas för att skapa metadata för en extern målgrupp. Du bör använda den här slutpunkten om målgruppsinmatningen hanteras i en separat tjänst, som batchförbrukning.

## Komma igång

>[!IMPORTANT]
>
>Slutpunkterna i den här guiden har prefixet `/core/ais` i motsats till `/core/ups`.

För att du ska kunna använda Experience Platform API:er måste du ha slutfört [autentiseringssjälvstudiekursen](https://www.adobe.com/go/platform-api-authentication-en). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i Experience Platform API-anrop, vilket visas nedan:

- Behörighet: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Alla begäranden till [!DNL Experience Platform] API:er kräver ett huvud som anger namnet på den sandlåda där åtgärden ska utföras:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om hur du arbetar med sandlådor i [!DNL Experience Platform] finns i [översiktsdokumentationen för sandlådor](../../sandboxes/home.md).

**API-format**

>[!IMPORTANT]
>
>Du **måste** inkludera frågeparametern `createAudienceMetaOnly=true` som en del av begäran.

```http
POST /audiences?createAudienceMetaOnly=true
```

**Begäran**

>[!IMPORTANT]
>
>Du **måste** inkludera rubriken `Accept: application/vnd.adobe.external.audiences+json; version=2` som en del av API-begäran.

```shell
curl -X POST https://platform.adobe.io/core/ais/audiences?createAudienceMetaOnly=true \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'\
 -H 'Accept: application/vnd.adobe.external.audiences+json; version=2'
 -d '{
    "name": "Sample audience name",
    "description" "A sample description for the audience.",
    "namespace": "agora",
    "originName": "Agora_Collaboration"
 }'
```

| Egenskap | Typ | Beskrivning |
| -------- | ---- | ----------- |
| `name` | Sträng | Namnet på publiken. |
| `description` | Sträng | En valfri beskrivning för målgruppen. |
| `namespace` | Sträng | Namnutrymmet för målgruppen. |
| `originName` | Sträng | Namnet på målgruppens ursprung. |

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om den nya målgruppen.

```json
{
    "name": "Sample audience name",
    "audienceId": "4a815904-f2f9-4237-82fb-55605bcc2ad7"
}
```

| Egenskap | Typ | Beskrivning |
| -------- | ---- | ----------- |
| `name` | Sträng | Namnet på den målgrupp du skapade. |
| `audienceId` | Sträng | ID:t för den målgrupp du skapade. |
