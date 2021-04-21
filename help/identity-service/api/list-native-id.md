---
keywords: Experience Platform;hem;populära ämnen;identitet xid;XID
solution: Experience Platform
title: Hämta det inbyggda ID:t för en identitet
topic-legacy: API guide
description: Identitetsdata anges vanligtvis som ett ID-strängvärde och identitetsnamnområde i inmatade XDM-data och när en identitet anges för användning i ett API-anrop. När identiteter bevaras i identitetstjänsten genereras och tilldelas ett ID till den identiteten, som kallas ursprungligt XID. Plattforms-API:er som kräver stöd för identitetsdata med detta mer kompakta formulär för aggregerat ID och namnutrymme. XID är en base64-kodad sträng.
exl-id: e734f5d8-e00b-43fa-b06c-97c73e1f7c71
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# Hämta det inbyggda ID:t för en identitet

Identitetsdata anges vanligtvis som ett ID-strängvärde och identitetsnamnområde i inmatade XDM-data och när en identitet anges för användning i ett API-anrop. När identiteter bevaras i [!DNL Identity Service] genereras och tilldelas ett ID till den identiteten, som kallas ursprungligt XID. [!DNL Platform] API:er som kräver stöd för identitetsdata med detta mer kompakta formulär för aggregerat ID och namnutrymme. XID är en base64-kodad sträng.

>[!NOTE]
>
>Formatet är huvudsakligen avsett för intern Adobe. Inbyggt XID som ett enskilt värde är mer utrymmeseffektivt och används internt i [!DNL Platform]-lösningar för lagring och serialisering. Det är dock inte läsbart för människor, det är ogenomskinligt och kräver ett separat anrop för att få det att användas.

Hämta XID för ett givet ID-värde och namnutrymme med den tjänst som beskrivs i det här avsnittet.

**API-format**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/identity?namespace={NAMESPACE}&id={ID_VALUE}
```

**Begäran**

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/identity?namespace=email&id=test@adobetest.com' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

```json
{
    "xid":"BVrqzwVuzbXrLfmnaG3rXrLf3KJg"
}
```
