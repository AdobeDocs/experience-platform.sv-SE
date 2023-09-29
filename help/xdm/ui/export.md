---
solution: Experience Platform
title: Exportera XDM-scheman i användargränssnittet
description: Lär dig hur du exporterar ett befintligt schema till en annan sandlåda eller organisation i Adobe Experience Platform användargränssnitt.
type: Tutorial
exl-id: c467666d-55bc-4134-b8f4-7758d49c4786
source-git-commit: d25042e80ca5f655a50deac6a65ce9168225d6e6
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# Exportera XDM-scheman i användargränssnittet

Alla resurser i schemabiblioteket finns i en specifik sandlåda i en organisation. I vissa fall kanske du vill dela XDM-resurser (Experience Data Model) mellan sandlådor och organisationer.

För att tillgodose detta behov [!UICONTROL Schemas] Med arbetsytan i Adobe Experience Platform UI kan du generera en exportnyttolast för alla scheman i schemabiblioteket. Denna nyttolast kan sedan användas i ett anrop till API:t för schemaregister för att importera schemat (och alla beroende resurser) till en målsandlåda och en målorganisation.

>[!NOTE]
>
>Du kan också använda API:t för schemafält för att exportera andra resurser utöver scheman, inklusive klasser, schemafältgrupper och datatyper. Se [slutpunktsguide för export](../api/export.md) för mer information.

## Förutsättningar

Med plattformsgränssnittet kan du exportera XDM-resurser, men du måste använda API:t för schemaregister för att importera dessa resurser till andra sandlådor eller organisationer för att slutföra arbetsflödet. Se vägledningen på [komma igång med API:t för schemaregister](../api/getting-started.md) om du vill ha viktig information om obligatoriska autentiseringshuvuden innan du följer den här handboken.

## Generera en exportnyttolast {#generate-export-payload}

Du kan generera exportnyttolaster i plattformsgränssnittet från informationspanelen på panelen [!UICONTROL Browse] eller direkt från arbetsytan i schemat i Schemaredigeraren.

Om du vill generera en exportnyttolast väljer du **[!UICONTROL Schemas]** i den vänstra navigeringen. I [!UICONTROL Schemas] på arbetsytan väljer du raden för det schema som du vill exportera för att visa schemainformation i den högra sidofältet.

>[!TIP]
>
>Se guiden på [utforska XDM-resurser](./explore.md) om du vill ha mer information om hur du hittar den XDM-resurs du söker.

Nästa steg är att välja **[!UICONTROL Copy JSON]** ikon (![Kopiera ikon](../images/ui/export/icon.png)) bland de tillgängliga alternativen.

![Arbetsytan Scheman med en schemarad och [!UICONTROL Copy to JSON] markerad.](../images/ui/export/copy-json.png)

Detta kopierar en JSON-nyttolast till Urklipp, som genereras baserat på schemastrukturen. För &quot;[!DNL Loyalty Members]&quot; som visas ovan genereras följande JSON:

```json
[
  {
    "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
    "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.mixins.9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
    "meta:resourceType": "mixins",
    "version": "1.0",
    "title": "Loyalty details",
    "type": "object",
    "description": "",
    "definitions": {
      "customFields": {
        "type": "object",
        "properties": {
          "_<XDM_TENANTID_PLACEHOLDER>": {
            "type": "object",
            "properties": {
              "loyalty": {
                "title": "Loyalty",
                "description": "",
                "type": "object",
                "isRequired": false,
                "required": [
                  
                ],
                "properties": {
                  "loyaltyId": {
                    "title": "Loyalty ID",
                    "description": "",
                    "type": "string",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "meta:xdmType": "string"
                  },
                  "memberSince": {
                    "title": "Member Since",
                    "description": "",
                    "type": "string",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "format": "date",
                    "meta:xdmType": "date"
                  },
                  "points": {
                    "title": "Points",
                    "description": "",
                    "type": "integer",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "meta:xdmType": "int"
                  },
                  "loyaltyLevel": {
                    "title": "Loyalty Level",
                    "description": "",
                    "type": "string",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "enum": [
                      "platinum",
                      "gold",
                      "silver",
                      "bronze"
                    ],
                    "meta:enum": {
                      "platinum": "Platinum",
                      "gold": "Gold",
                      "silver": "Silver",
                      "bronze": "Bronze"
                    },
                    "meta:xdmType": "string"
                  }
                },
                "meta:xdmType": "object"
              }
            },
            "meta:xdmType": "object"
          }
        },
        "meta:xdmType": "object"
      }
    },
    "allOf": [
      {
        "$ref": "#/definitions/customFields",
        "type": "object",
        "meta:xdmType": "object"
      }
    ],
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:intendedToExtend": [
      
    ],
    "meta:xdmType": "object",
    "meta:sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
    "meta:sandboxType": "production"
  },
  {
    "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/schemas/1e5a739ded8fd1d766a0e06e881a38031874dddd1c7020ad",
    "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.schemas.1e5a739ded8fd1d766a0e06e881a38031874dddd1c7020ad",
    "meta:resourceType": "schemas",
    "version": "1.4",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Describes customers who are members of a loyalty program.",
    "allOf": [
      {
        "$ref": "https://ns.adobe.com/xdm/context/profile",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/xdm/mixins/profile-consents",
        "type": "object",
        "meta:xdmType": "object"
      }
    ],
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
      "https://ns.adobe.com/xdm/context/profile-person-details",
      "https://ns.adobe.com/xdm/context/profile-personal-details",
      "https://ns.adobe.com/xdm/common/auditable",
      "https://ns.adobe.com/xdm/data/record",
      "https://ns.adobe.com/xdm/context/profile",
      "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
      "https://ns.adobe.com/xdm/mixins/profile-consents"
    ],
    "meta:xdmType": "object",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
    "meta:sandboxType": "production",
    "meta:immutableTags": [
      
    ]
  }
]
```

Nyttolasten kan också kopieras genom att välja [!UICONTROL More] i det övre högra hörnet i Schemaredigeraren. Det finns två alternativ i en listruta: [!UICONTROL Copy JSON structure] och [!UICONTROL Delete schema].

>[!NOTE]
>
>Ett schema kan inte tas bort när det är aktiverat för profilen eller har associerade datauppsättningar.

![Schemaredigeraren med [!UICONTROL More] och [!UICONTROL Copy to JSON] markerad.](../images/ui/export/schema-editor-copy-json.png)

Nyttolasten består av en array där varje arrayobjekt är ett objekt som representerar en anpassad XDM-resurs som ska exporteras. I exemplet ovan är &quot;[!DNL Loyalty details]&quot; egen fältgrupp och &quot;[!DNL Loyalty Members]schemat ingår. Alla huvudresurser som används av schemat inkluderas inte i exporten eftersom dessa resurser är tillgängliga i alla sandlådor och organisationer.

Observera att varje instans av organisationens klientorganisations-ID visas som `<XDM_TENANTID_PLACEHOLDER>` i nyttolasten. Dessa platshållare ersätts automatiskt med rätt innehavar-ID-värde beroende på var du importerar schemat i nästa steg.

## Importera resursen med API:t

När du har kopierat export-JSON för schemat kan du använda det som nyttolast för en POST-förfrågan till `/rpc/import` slutpunkt i API:t för schemaregistret. Se [importera slutpunktsguide](../api/import.md) om du vill ha information om hur du konfigurerar anropet för att skicka schemat till önskad organisation och sandlåda.

## Nästa steg

Genom att följa den här guiden har du exporterat ett XDM-schema till en annan organisation eller sandlåda. Mer information om funktionerna i [!UICONTROL Schemas] Gränssnittet, se [[!UICONTROL Schemas] Översikt över användargränssnittet](./overview.md).
