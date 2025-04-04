---
keywords: Experience Platform;home;populära topics;identity xid;XID
solution: Experience Platform
title: Hämta det inbyggda ID:t för en identitet
description: Identitetsdata anges vanligtvis som ett ID-strängvärde och identitetsnamnområde i inmatade XDM-data och när en identitet anges för användning i ett API-anrop. När identiteter bevaras i identitetstjänsten genereras och tilldelas ett ID till den identiteten, som kallas ursprungligt XID. Experience Platform-API:er som kräver stöd för identitetsdata med detta mer kompakta formulär för aggregerat ID och namnutrymme. XID är en base64-kodad sträng.
role: Developer
exl-id: e734f5d8-e00b-43fa-b06c-97c73e1f7c71
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# Hämta det inbyggda ID:t för en identitet

Identitetsdata anges vanligtvis som ett ID-strängvärde och identitetsnamnområde i inmatade XDM-data och när en identitet anges för användning i ett API-anrop. När identiteter bevaras i [!DNL Identity Service] genereras och tilldelas ett ID till den identiteten, som kallas ursprungligt XID. [!DNL Experience Platform] API:er som kräver stöd för identitetsdata med det här mer kompakta formuläret för aggregerat ID och namnområde. XID är en base64-kodad sträng.

>[!NOTE]
>
>Formatet är huvudsakligen avsett för intern Adobe-användning. Inbyggt XID som ett enskilt värde är mer utrymmeseffektivt och används internt i [!DNL Experience Platform]-lösningar för lagring och serialisering. Det är dock inte läsbart för människor, det är ogenomskinligt och kräver ett separat anrop för att få det att användas.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

```json
{
    "xid":"BVrqzwVuzbXrLfmnaG3rXrLf3KJg"
}
```
