---
title: Fältgrupp för platsschema
description: Läs mer om fältgruppen Plats.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 99831093-89da-4329-be29-c130c1d48f63
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# Schemafältgruppen [!UICONTROL Location]

[!UICONTROL Location] är en standardschemafältgrupp för [[!DNL Location] klassen](../classes/location.md). Det tillhandahåller ett enskilt objekttypsfält `healthcareLocation` som samlar in information och positionsinformation för en plats.

![Fältgruppsstruktur](../../../images/healthcare/field-groups/location.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Address] | `address` | [[!UICONTROL Address]](../data-types/address.md) | Den fysiska platsens adress. |
| [!UICONTROL Characteristic] | `characteristic` | Array med [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | En samling av platsens egenskaper. |
| [!UICONTROL Contact] | `contact` | Array med [[!UICONTROL Extended Contact Details]](../data-types/extended-contact-detail.md) | Kontaktinformationen för platsen. |
| [!UICONTROL Endpoint] | `endpoint` | Array med [[!UICONTROL Reference]](../data-types/reference.md) | De tekniska slutpunkterna som ger åtkomst till driftstjänster för platsen. |
| [!UICONTROL Form] | `form` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Platsens fysiska form. |
| [!UICONTROL Hours of Operation] | `hoursOfOperation` | Array med [[!UICONTROL Availability]](../data-types/availability.md) | Vilka dagar och tider den här platsen vanligtvis är öppen (inklusive undantag). |
| [!UICONTROL Identifier] | `identifier` | Array med [[!UICONTROL Identifier]](../data-types/identifier.md) | Den unika koden eller numret som identifierar platsen. |
| [!UICONTROL Managing Organization] | `managingOrganization` | [[!UICONTROL Reference]](../data-types/reference.md) | Organisationen som ansvarar för etablering och underhåll. |
| [!UICONTROL Operational Status] | `operationalStatus` | [[!UICONTROL Coding]](../data-types/coding.md) | Driftstatus för platsen. |
| [!UICONTROL Part Of Location] | `partOf` | [[!UICONTROL Reference]](../data-types/reference.md) | Platsen som den här platsen är en del av. |
| [!UICONTROL Position] | `position` | Objekt | Den absoluta geografiska platsen. Innehåller tre egenskaper i Double-format: <li>`longitude`: Longitud med WGS84-datum</li> <li>`latitude`: Latitude med WGS84-datum.</li> <li>`altitude`: Höjd med WGS84-datum.</li> |
| [!UICONTROL Type] | `type` | Array med [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Den typ av funktion som utförs på platsen. |
| [!UICONTROL Virtual Service] | `virtualService` | Array med [[!UICONTROL Virtual Service Detail]](../data-types/virtual-service-detail.md) | Anslutningsinformationen för en virtuell tjänst. |
| [!UICONTROL Alias] | `alias` | Array med strängar | En lista med alternativa namn som platsen är eller var känd som. |
| [!UICONTROL Description] | `description` | Sträng | Ytterligare information för att identifiera platsen efter dess namn. |
| [!UICONTROL Mode] | `mode` | Sträng | Platsens läge. Värdet för den här egenskapen måste vara lika med ett av följande kända enum-värden. <li> `instance` </li> <li> `kind` </li> |
| [!UICONTROL Name] | `name` | Sträng | Namnet på platsen. |
| [!UICONTROL Status] | `status` | Sträng | Platsens status. Värdet för den här egenskapen måste vara lika med ett av följande kända enum-värden. <li> `active` </li> <li> `inactive` </li> <li> `suspended` </li> |

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/location.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/location.schema.json)
