---
title: B2B Source datatyp
description: Läs mer om datatypen B2B Source Experience Data Model (XDM).
exl-id: 01b7d41c-1ab6-4cbc-b9b3-77b6af69faf3
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---

# Datatypen [!UICONTROL B2B Source]

[!UICONTROL B2B Source] är en XDM-datatyp (Standard Experience Data Model) som representerar en sammansatt identifierare för en B2B-entitet (till exempel ett [konto](../classes/b2b/business-account.md), en [möjlighet](../classes/b2b/business-opportunity.md) eller en [kampanj](../classes/b2b/business-campaign.md)).

Om du endast använder strängbaserade identifierare kan det finnas överlappningar mellan ID:n i flera system (en möjlighet kan till exempel ges ett sträng-ID i ett CRM-system, men samma ID kan referera till en helt annan möjlighet). Detta kan orsaka datakonflikter när data sammanfogas i [Kundprofil i realtid](../../profile/home.md).

Datatypen [!UICONTROL B2B Source] gör att du kan använda det ursprungliga sträng-ID:t för en entitet och kombinera det med källspecifik sammanhangsberoende information för att se till att den förblir helt unik i plattformssystemet oavsett vilken källa den kommer från.

![B2B Source-struktur](../images/data-types/b2b-source.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `sourceID` | Sträng | Ett unikt ID för källposten. |
| `sourceInstanceID` | Sträng | Instans- eller organisations-ID för källdata. |
| `sourceKey` | Sträng | En unik identifierare som består av `sourceId`, `sourceInstanceId` och `sourceType` sammanfogade i följande format: `[sourceID]@[sourceInstanceID].[sourceType]`.<br><br>Vissa källanslutningar som Marketo sammanfogar det här värdet automatiskt för vissa identifierare. Andra måste sammanfogas manuellt med funktionen [Dataprep `concat`](../../data-prep/functions.md#string), till exempel: `concat(id,"@${ORG_ID}.Marketo")` |
| `sourceType` | Sträng | Namnet på plattformen som innehåller källdata. |

{style="table-layout:auto"}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.schema.json)
