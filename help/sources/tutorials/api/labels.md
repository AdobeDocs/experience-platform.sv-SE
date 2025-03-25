---
title: Använd åtkomstetiketter för att hantera användaråtkomst till källdata med API
description: Lär dig hur du använder API:t för Flow Service för att tillämpa åtkomstetiketter och hantera användaråtkomst till källdata.
hide: true
hidefromtoc: true
source-git-commit: 80fb60abdf33eb2a7ca691a9a48a811c632b34fc
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Använd åtkomstetiketter för att hantera användaråtkomst till källdata med API

Du kan använda funktionerna som tillhandahålls av [attributbaserad åtkomstkontroll](../../../access-control/abac/overview.md) i Real-Time CDP för att använda etiketter på källdata. Med den här funktionen kan du se till att bara en delmängd av användarna i organisationen får tillgång till specifika källdata.

När du lägger till en åtkomstetikett i ett visst dataflöde kan bara användare som har tillgång till en roll som är tilldelad den etiketten visa och redigera det dataflödet. Om ett källdataflöde inte är markerat med någon etikett, visas det för alla användare som tillhör din organisation. Om du till exempel använder etiketten C12 på ett dataflöde kommer användare som tilldelats en roll som inte har etiketten C12 inte att kunna visa och redigera dataflödet med etiketten C12.

Läs den här vägledningen om du vill ha information om hur du använder åtkomstetiketter i källdataflöden med [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Kom igång

Innan du arbetar med åtkomstkontrollsetiketter måste du först bekanta dig med funktionerna i attributbaserad åtkomstkontroll. Mer information finns i följande dokumentation:

* [Attributbaserad åtkomstkontroll - översikt](../../../access-control/abac/overview.md)
* [Attributbaserad åtkomstkontroll från början till slut](../../../access-control/abac/end-to-end-guide.md)
* [API-guide för attributbaserad åtkomstkontroll](../../../access-control/abac/api/overview.md)
* [Etikettordlista för dataanvändning](../../../data-governance/labels/reference.md)

## Tillämpa åtkomstetiketter på källdataflöden

>[!NOTE]
>
>* Du kan inte använda etiketter i en flödeskörning. Flödeskörningar ärver emellertid alla etiketter som du använder på det överordnade dataflödet.
>
>* Om du inte har åtkomst till ett dataflöde kan du inte heller visa dess motsvarande flödeskörningar.

Om du vill lägga till en etikett i ett dataflöde gör du en PATCH-begäran till slutpunkten `/flows` och anger ID:t för det dataflöde som du vill uppdatera.

**API-format**

```http
PATCH /flows/{FLOW_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{FLOW_ID}` | ID:t för det dataflöde som du vill uppdatera. |

**Begäran**

>[!TIP]
>
>Om du vill göra en PATCH-begäran anger du version/tagg för det dataflöde som du vill uppdatera som en `if-match`-huvudparameter.

Följande begäran lägger till C12-etiketten i dataflödet med ID: `84224def-1e2a-4d95-9ea2-132d697ed2aa`.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/flows/84224def-1e2a-4d95-9ea2-132d697ed2aa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'if-match: "c5002e0e-0000-0200-0000-67a3c3b70000"'
  -d '[
    {
        "op": "add",
        "path": "/labels",
        "value": ["core/C12"]
    }
]'
```

| Egenskap | Beskrivning |
| --- | --- |
| `op` | Åtgärdsanropet som används för att definiera den åtgärd som krävs för att uppdatera dataflödet. Åtgärderna omfattar: `add`, `replace` och `remove`. |
| `path` | Den del av dataflödet som ska uppdateras. |
| `value` | Det nya värdet som du vill uppdatera egenskapen med. |



**Svar**

Ett lyckat svar returnerar ditt flödes-ID och en uppdaterad tagg. Du kan verifiera uppdateringen genom att göra en GET-begäran till API:t [!DNL Flow Service] och samtidigt ange ditt flödes-ID.

```json
{
    "id": "84224def-1e2a-4d95-9ea2-132d697ed2aa",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

När du har konfigurerat åtkomstetiketter för ditt dataflöde kommer användare som inte har åtkomst till den etiketten inte längre att kunna hämta dataflödet. Om en användare som inte har etablerats med etiketten C12 gör en GET-begäran om att hämta dataflöde med ID: `84224def-1e2a-4d95-9ea2-132d697ed2aa` får de följande svar:

```json
{
    "type": "https://ns.adobe.com/aep/errors/FLOW-1439-404",
    "title": "Resource not found",
    "status": 404,
    "report": {
        "detailed-message": "The requested flows resource 84224def-1e2a-4d95-9ea2-132d697ed2aa is not found. Verify the resource ID before trying again.",
        "id": "84224def-1e2a-4d95-9ea2-132d697ed2aa",
        "request-id": "{REQUEST_ID}",
        "type": "flows"
    },
    "errorMessage": "The requested flows resource 84224def-1e2a-4d95-9ea2-132d697ed2aa is not found. Verify the resource ID before trying again.",
    "errorDetails": "The requested flows resource 84224def-1e2a-4d95-9ea2-132d697ed2aa is not found. Verify the resource ID before trying again."
}
```

Användare som inte har åtkomst till C12-etiketten kommer inte heller att kunna göra några PATCH- eller DELETE-begäranden mot det uppdaterade dataflödet och kommer att få följande svar:

```json
{
    "type": "https://ns.adobe.com/aep/errors/FLOW-2120-403",
    "title": "Forbidden",
    "status": 403,
    "report": {
        "detailed-message": "You do not have sufficient permissions to perform the operation. Please contact your administrator to resolve permissions and try again.",
        "request-id": "{REQUEST_ID}"
    },
    "errorMessage": "You do not have sufficient permissions to perform the operation. Please contact your administrator to resolve permissions and try again.",
    "errorDetails": "You do not have sufficient permissions to perform the operation. Please contact your administrator to resolve permissions and try again."
}
```

## Nästa steg

Du vet nu hur du använder åtkomstetiketter i källans dataflöden. Nu kan du se till att bara en viss grupp användare i organisationen har åtkomst till vissa källdata. Mer information finns i följande dokumentation:

* [Tillämpa åtkomstetiketter på källdataflöden i användargränssnittet](../ui/labels.md)
* [Översikt över åtkomstkontroll](../../../access-control/home.md)