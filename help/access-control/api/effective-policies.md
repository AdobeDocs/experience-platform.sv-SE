---
keywords: Experience Platform;hem;populära ämnen;effektiva profiler;åtkomstkontrolls-API
solution: Experience Platform
title: API-slutpunkt för gällande principer
topic: developer guide
description: Med åtkomstkontrollen i Adobe Experience Platform kan du hantera roller och behörigheter för olika plattformsfunktioner med Adobe Admin Console. Det här dokumentet är en guide till hur du visar effektiva profiler med hjälp av API:t för åtkomstkontroll för Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---


# Slutpunkt för gällande principer

Om du vill visa gällande principer för den aktuella POSTEN gör du en begäran till `/acl/effective-policies`-slutpunkten i [!DNL Access Control]-API:t. Behörigheterna och resurstyperna som du vill hämta måste anges i nyttolasten för begäran i form av en array. Detta visas i exemplet på API-anrop nedan.

**API-format**

```http
POST /acl/effective-policies
```

**Begäran**

Följande begäranden hämtar information om behörigheten [!UICONTROL Manage Datasets] och åtkomsten till resurstypen [!UICONTROL schemas] för den aktuella användaren.

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
>En fullständig lista över behörigheter och resurstyper som kan anges i nyttolastarrayen finns i bilagan om [godkända behörigheter och resurstyper](#accepted-permissions-and-resource-types).

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

I det här dokumentet beskrivs hur du anropar [!DNL Access Control]-API:t för att returnera information om aktiva behörigheter och relaterade principer för resurstyper. Mer information om åtkomstkontroll för [!DNL Experience Platform] finns i [åtkomstkontrollsöversikt](../home.md).

## Bilaga

I det här avsnittet finns ytterligare information om hur du använder API:t [!DNL Access Control].

### Godkända behörigheter och resurstyper

Nedan följer en lista över behörigheter och resurstyper som du kan inkludera i nyttolasten för en begäran om POST till `/acl/active-permissions`-slutpunkten.

**Behörigheter**

```plaintext
permissions/activate-destinations
permissions/evaluate-segments
permissions/execute-decisioning-activities
permissions/export-audience-for-segment
permissions/manage-datasets
permissions/manage-decisioning-activities
permissions/manage-decisioning-options
permissions/manage-destinations
permissions/manage-dsw
permissions/manage-dule-labels
permissions/manage-dule-policies
permissions/manage-identity-namespaces
permissions/manage-privacy-workflows
permissions/manage-profile-configs
permissions/manage-profiles
permissions/manage-queries
permissions/manage-schemas
permissions/manage-segments
permissions/manage-sources
permissions/reset-sandboxes
permissions/view-datasets
permissions/view-destinations
permissions/view-dule-labels
permissions/view-dule-policies
permissions/view-identity-namespaces
permissions/view-monitoring-dashboard
permissions/view-privacy-workflows
permissions/view-profile-configs
permissions/view-profiles
permissions/view-sandboxes
permissions/view-schemas
permissions/view-segments
permissions/view-sources
```

**Resurstyper**

```plaintext
resource-types/activation-associations
resource-types/activations
resource-types/activities
resource-types/analytics-source
resource-types/audience-manager-source
resource-types/bizible-source
resource-types/connection
resource-types/customer-attributes-source
resource-types/data-science-workspace
resource-types/dataset-preview
resource-types/datasets
resource-types/dule-label
resource-types/dule-policy
resource-types/enterprise-source
resource-types/identity-descriptor
resource-types/identity-namespaces
resource-types/launch-source
resource-types/marketing-action
resource-types/marketo-source
resource-types/monitoring
resource-types/offers
resource-types/placements
resource-types/privacy-consent
resource-types/privacy-content-delivery
resource-types/privacy-job
resource-types/profile-configs
resource-types/profile-datasets
resource-types/profiles
resource-types/query
resource-types/relationship-descriptor
resource-types/sandboxes
resource-types/schemas
resource-types/segment-jobs
resource-types/segments
resource-types/streaming-source
```
