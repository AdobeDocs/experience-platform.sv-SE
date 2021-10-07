---
title: Impression, datatyp
description: Det här dokumentet innehåller en översikt över datatypen Impressions XDM.
source-git-commit: 7fc16546176d196582a3cdfcee51f799eeef9788
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 2%

---

# [!UICONTROL Impressions] datatyp

[!UICONTROL Impressions] är en standard-XDM-datatyp som beskriver ett marknadsföringsintryck, som är ett mått som används för att kvantifiera antalet digitala vyer eller engagemang för en del av innehåll som en annons, ett digitalt inlägg eller en webbsida.

![](../images/data-types/impressions.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `ID` | Sträng | Ett unikt ID för intrycket. |
| `displays` | Heltal | Antalet gånger som visningsobjektet har visats för en kund. |
| `selected` | Heltal | Antalet gånger som intryckningsobjektet har markerats eller klickats. |
| `type` | Sträng | Typ av intryck. |

{style=&quot;table-layout:auto&quot;}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.schema.json)
