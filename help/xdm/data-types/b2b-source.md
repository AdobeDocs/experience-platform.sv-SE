---
title: Datatyp för B2B-källa
description: Det här dokumentet innehåller en översikt över datatypen B2B Source Experience Data Model (XDM).
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 1%

---

# [!UICONTROL B2B Source] datatyp

>[!NOTE]
>
>Den här datatypen är endast tillgänglig för organisationer som har tillgång till B2B-utgåvan av kunddataplattformen i realtid.

[!UICONTROL B2B Source] är en XDM-datatyp (Standard Experience Data Model) som representerar en sammansatt identifierare för en B2B-enhet (till exempel ett  [konto](../classes/b2b/business-account.md), en  [affärsmöjlighet](../classes/b2b/business-opportunity.md) eller en  [kampanj](../classes/b2b/business-campaign.md)).

Om du endast använder strängbaserade identifierare kan det finnas överlappningar mellan ID:n i flera system (en möjlighet kan till exempel ges ett sträng-ID i ett CRM-system, men samma ID kan referera till en helt annan möjlighet). Detta kan orsaka datakonflikter när data sammanfogas i [Kundprofil i realtid](../../profile/home.md).

Med datatypen [!UICONTROL B2B Source] kan du använda det ursprungliga sträng-ID:t för en entitet och kombinera det med källspecifik sammanhangsberoende information för att säkerställa att den förblir helt unik i plattformssystemet oavsett vilken källa den kommer från.

![Källstruktur för B2B](../images/data-types/b2b-source.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `sourceID` | Sträng | Ett unikt ID för källposten. |
| `sourceInstanceID` | Sträng | Instans- eller organisations-ID för källdata. |
| `sourceKey` | Sträng | En unik identifierare som består av `sourceId`, `sourceInstanceId` och `sourceType` sammanfogade i följande format: `[sourceID]@$[sourceInstanceID].[sourceType]`.<br><br>Vissa källkopplingar som Marketo sammanfogar det här värdet automatiskt för vissa identifierare. Andra måste sammanfogas manuellt med funktionen [Dataprep `concat`](../../data-prep/functions.md#string), till exempel: `concat(id,"@${ORG_ID}.Marketo")` |
| `sourceType` | Sträng | Namnet på plattformen som innehåller källdata. |

{style=&quot;table-layout:auto&quot;}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.schema.json)
