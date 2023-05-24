---
title: Impression, datatyp
description: Det här dokumentet innehåller en översikt över datatypen Impressions XDM.
exl-id: 1e758043-a41e-45f7-ae8b-514990d0649e
source-git-commit: afdac5ce2ed967b4688d456a586c946bc2cf4179
workflow-type: tm+mt
source-wordcount: '136'
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

{style="table-layout:auto"}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.schema.json)
