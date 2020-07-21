---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Visa gällande policyer
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 1%

---


# Visa gällande policyer

Om du vill visa gällande principer för den aktuella användaren gör du en POST-begäran till `/acl/effective-policies` slutpunkten i [!DNL Access Control] API:t. Behörigheterna och resurstyperna som du vill hämta måste anges i nyttolasten för begäran i form av en array. Detta visas i exemplet på API-anrop nedan.

**API-format**

```http
POST /acl/effective-policies
```

**Begäran**

Följande förfrågningar hämtar information om behörigheten &quot;[!UICONTROL Manage Datasets]&quot; och åtkomsten till resurstypen &quot;[!UICONTROL schemas]&quot; för den aktuella användaren.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/acl/effective-policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    "/permissions/manage-datasets",
    "/resource-types/schemas"
  ]'
```

>[!NOTE]
>
>En fullständig lista över behörigheter och resurstyper som kan anges i nyttolastarrayen finns i avsnittet i bilagan om [godkända behörigheter och resurstyper](#accepted-permissions-and-resource-types).

**Svar**

Ett godkänt svar returnerar information om behörigheter och resurstyper som anges i begäran. Svaret innehåller de aktiva behörigheter som den aktuella användaren har för de resurstyper som anges i begäran. Om någon behörighet som ingår i nyttolasten för begäran är aktiv för den aktuella användaren, returnerar API behörigheten med en asterisk (`*`) för att ange att behörigheten är aktiv. Alla behörigheter som anges i begäran och som inte är aktiva för användaren utelämnas från svarsnyttolasten.

```json
{
    "policies": {
        "/resource-types/schemas": [
            "read",
            "write",
            "delete"
        ],
        "/permissions/manage-datasets": [
            "*"
        ]
    }
}
```

## Nästa steg

I det här dokumentet beskrivs hur du anropar API:t för att returnera information om aktiva behörigheter och relaterade principer för resurstyper. [!DNL Access Control] Mer information om åtkomstkontroll för [!DNL Experience Platform]finns i [åtkomstkontrollen - översikt](../home.md).

## Bilaga

I det här avsnittet finns ytterligare information om hur du använder [!DNL Access Control] API.

### Godkända behörigheter och resurstyper

Nedan följer en lista över behörigheter och resurstyper som du kan inkludera i nyttolasten för en POST-begäran till `/acl/active-permissions` slutpunkten.

**Behörigheter**

```plaintext
"permissions/activate-destinations"
"permissions/export-audience-for-segments"
"permissions/manage-datasets"
"permissions/manage-destinations"
"permissions/manage-identity-namespaces"
"permissions/manage-profiles"
"permissions/manage-sandboxes"
"permissions/manage-schemas"
"permissions/reset-sandboxes"
"permissions/view-datasets"
"permissions/view-destinations"
"permissions/view-identity-namespaces"
"permissions/view-monitoring-dashboard"
"permissions/view-profiles"
"permissions/view-sandboxes"
"permissions/view-schemas"
```

**Resurstyper**

```plaintext
"resource-types/classes"
"resource-types/connections"
"resource-types/data-types"
"resource-types/dataset-data"
"resource-types/datasets"
"resource-types/destinations"
"resource-types/dule-labels"
"resource-types/identity-descriptors"
"resource-types/identity-namespaces"
"resource-types/mixins"
"resource-types/monitoring"
"resource-types/profile-configs
"resource-types/profile-datasets"
"resource-types/profiles"
"resource-types/relationship-descriptors"
"resource-types/reset-sandboxes"
"resource-types/sandboxes"
"resource-types/schemas"
"resource-types/segment-jobs"
"resource-types/segments"
```
