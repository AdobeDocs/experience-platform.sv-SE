---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Hämta det inbyggda ID:t för en identitet
topic: API guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# Hämta XID för en identitet

Identitetsdata anges vanligtvis som ett ID-strängvärde och identitetsnamnområde i inmatade XDM-data och när en identitet anges för användning i ett API-anrop. När identiteter bevaras i identitetstjänsten genereras och tilldelas ett ID till den identiteten, som kallas ursprungligt XID. Plattforms-API:er som kräver stöd för identitetsdata med detta mer kompakta formulär för aggregerat ID och namnutrymme. XID är en base64-kodad sträng.

>[!NOTE] Formatet är huvudsakligen avsett för intern Adobe-användning. Inbyggt XID som ett enskilt värde är mer utrymmeseffektivt och används internt i plattformslösningar för lagring och serialisering. Det är dock inte läsbart för människor, det är ogenomskinligt och kräver ett separat anrop för att få det att användas.

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
