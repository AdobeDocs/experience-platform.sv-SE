---
solution: Experience Platform
title: Exportera XDM-scheman i användargränssnittet
description: Lär dig hur du exporterar ett befintligt schema till en annan sandlåda eller organisation i Adobe Experience Platform användargränssnitt.
type: Tutorial
exl-id: c467666d-55bc-4134-b8f4-7758d49c4786
source-git-commit: 0f0842c1d14ce42453b09bf97e1f3690448f6e9a
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---

# Exportera XDM-scheman i användargränssnittet {#export-xdm-schemas-in-the-UI}

>[!CONTEXTUALHELP]
>id="platform_xdm_copyjsonstructure"
>title="Kopiera JSON-struktur"
>abstract="Generera en exportnyttolast för det valda schemat genom att kopiera JSON-strukturen till Urklipp. Använd den här funktionen för att exportera information om scheman i schemabiblioteket. Denna exporterade JSON kan sedan användas för att importera schemat och alla relaterade resurser till en annan sandlåda eller organisation. Detta gör det enkelt och effektivt att dela och återanvända scheman mellan olika miljöer."

Alla resurser i schemabiblioteket finns i en specifik sandlåda i en organisation. I vissa fall kanske du vill dela XDM-resurser (Experience Data Model) mellan sandlådor och organisationer.

För att tillgodose detta behov kan du med arbetsytan [!UICONTROL Schemas] i Adobe Experience Platform UI generera en exportnyttolast för vilket schema som helst i schemabiblioteket. Denna nyttolast kan sedan användas i ett anrop till API:t för schemaregister för att importera schemat (och alla beroende resurser) till en målsandlåda och en målorganisation.

>[!NOTE]
>
>Du kan också använda API:t för schemafält för att exportera andra resurser utöver scheman, inklusive klasser, schemafältgrupper och datatyper. Mer information finns i [exportslutpunktshandboken](../api/export.md).

## Förhandskrav

Med plattformsgränssnittet kan du exportera XDM-resurser, men du måste använda API:t för schemaregister för att importera dessa resurser till andra sandlådor eller organisationer för att slutföra arbetsflödet. Se guiden [Komma igång med API:t för schemaregister](../api/getting-started.md) för viktig information om obligatoriska autentiseringshuvuden innan du följer den här guiden.

## Generera en exportnyttolast {#generate-export-payload}

Du kan generera exportnyttolaster i plattformsgränssnittet från informationspanelen på fliken [!UICONTROL Browse] eller direkt från arbetsytan för schemat i schemaläggaren.

Om du vill generera en exportnyttolast väljer du **[!UICONTROL Schemas]** i den vänstra navigeringen. I arbetsytan [!UICONTROL Schemas] väljer du raden för det schema som du vill exportera för att visa schemainformation i den högra sidofältet.

>[!TIP]
>
>Mer information om hur du söker efter XDM-resursen finns i guiden [Utforska XDM-resurser](./explore.md).

Välj sedan ikonen **[!UICONTROL Copy JSON]** (![Kopiera ikon](../images/ui/export/icon.png)) bland de tillgängliga alternativen.

![Arbetsytan Scheman med en schemarad och [!UICONTROL Copy to JSON] markerad.](../images/ui/export/copy-json.png)

Detta kopierar en JSON-nyttolast till Urklipp, som genereras baserat på schemastrukturen. För schemat [!DNL Loyalty Members] som visas ovan genereras följande JSON:

+++Välj för att expandera en exempelnyttolast för JSON

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

+++

Nyttolasten kan också kopieras genom att välja [!UICONTROL More] i det övre högra hörnet i Schemaredigeraren. En nedrullningsbar meny innehåller två alternativ, [!UICONTROL Copy JSON structure] och [!UICONTROL Delete schema].

>[!NOTE]
>
>Ett schema kan inte tas bort när det är aktiverat för profilen eller har associerade datauppsättningar.

![Schemaredigeraren med [!UICONTROL More] och [!UICONTROL Copy to JSON] markerat.](../images/ui/export/schema-editor-copy-json.png)

Nyttolasten består av en array där varje arrayobjekt är ett objekt som representerar en anpassad XDM-resurs som ska exporteras. I exemplet ovan ingår den anpassade fältgruppen [!DNL Loyalty details] och schemat [!DNL Loyalty Members]. Alla huvudresurser som används av schemat inkluderas inte i exporten eftersom dessa resurser är tillgängliga i alla sandlådor och organisationer.

Observera att varje instans av organisationens klient-ID visas som `<XDM_TENANTID_PLACEHOLDER>` i nyttolasten. Dessa platshållare ersätts automatiskt med rätt innehavar-ID-värde beroende på var du importerar schemat i nästa steg.

## Importera resursen med API:t {#import-resource-with-api}

När du har kopierat export-JSON för schemat kan du använda det som nyttolast för en POST-begäran till `/rpc/import`-slutpunkten i API:t för schemaregistret. Mer information om hur du konfigurerar anropet för att skicka schemat till önskad organisation och sandlåda finns i [importguiden](../api/import.md).

## Nästa steg

Genom att följa den här guiden har du exporterat ett XDM-schema till en annan organisation eller sandlåda. Mer information om funktionerna i användargränssnittet för [!UICONTROL Schemas] finns i [[!UICONTROL Schemas] användargränssnittsöversikt ](./overview.md).
