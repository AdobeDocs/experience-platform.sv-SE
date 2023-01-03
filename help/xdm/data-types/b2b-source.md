---
title: Datatyp för B2B-källa
description: Det här dokumentet innehåller en översikt över datatypen B2B Source Experience Data Model (XDM).
exl-id: 01b7d41c-1ab6-4cbc-b9b3-77b6af69faf3
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 1%

---

# [!UICONTROL B2B Source] datatyp

[!UICONTROL B2B Source] är en XDM-datatyp (Standard Experience Data Model) som representerar en sammansatt identifierare för en B2B-enhet (till exempel en [konto](../classes/b2b/business-account.md), en [tillfälle](../classes/b2b/business-opportunity.md), eller en [kampanj](../classes/b2b/business-campaign.md)).

Om du endast använder strängbaserade identifierare kan det finnas överlappningar mellan ID:n i flera system (en möjlighet kan till exempel ges ett sträng-ID i ett CRM-system, men samma ID kan referera till en helt annan möjlighet). Detta kan leda till datakonflikter när data sammanfogas i [Kundprofil i realtid](../../profile/home.md).

The [!UICONTROL B2B Source] Med datatypen kan du använda ett enhets ursprungliga sträng-ID och kombinera det med källspecifik sammanhangsberoende information för att säkerställa att det förblir helt unikt i plattformssystemet oavsett varifrån det kommer.

![Källstruktur för B2B](../images/data-types/b2b-source.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `sourceID` | Sträng | Ett unikt ID för källposten. |
| `sourceInstanceID` | Sträng | Instans- eller organisations-ID för källdata. |
| `sourceKey` | Sträng | En unik identifierare som består av `sourceId`, `sourceInstanceId`och `sourceType` sammanfogade i följande format: `[sourceID]@$[sourceInstanceID].[sourceType]`.<br><br>Vissa källkopplingar som Marketo sammanfogar det här värdet automatiskt för vissa identifierare. Andra måste sammanfogas manuellt med [Dataprep `concat` function](../../data-prep/functions.md#string), till exempel: `concat(id,"@${ORG_ID}.Marketo")` |
| `sourceType` | Sträng | Namnet på plattformen som innehåller källdata. |

{style=&quot;table-layout:auto&quot;}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.schema.json)
