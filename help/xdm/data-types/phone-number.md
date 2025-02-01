---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;Schemas;phoneNumber;xdm:phoneNumber;datatyp;datatyp;datatyp;data type;
solution: Experience Platform
title: Telefonnummerdatatyp
description: Läs mer om datatypen XDM för telefonnummer.
exl-id: b84e48f9-bbb4-4b8b-9476-4bc1c455ecfd
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# Datatypen [!UICONTROL Phone number]

[!UICONTROL Phone number] är en standard-XDM-datatyp som beskriver informationen för ett telefonnummer.

![](../images/data-types/phone-number.png){width=600}

| Egenskap | Beskrivning |
| --- | --- |
| `extension` | Det interna uppringningsnummer som används för anrop från en privat börs, operator eller instrumentpanel. |
| `number` | Telefonnumret. Observera att telefonnumret är en sträng och kan innehålla meningsfulla tecken som hakparenteser `()`, bindestreck `-` eller tecken för att indikera underordnade identifierare som tillägg `x`, till exempel `1-353(0)18391111` eller `+613 9403600x1234`. |
| `primary` | Ett booleskt värde som anger om det här är personens primära telefonnummer. Till skillnad från adress och e-postadress kan det finnas flera primära telefonnummer, ett per kommunikationskanal. Kommunikationskanalen definieras av typen (anges med namnet på den överordnade egenskapen): `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown` och `fax`. |
| `status` | Anger om telefonnumret kan användas. |
| `statusReason` | En beskrivning av aktuell status. |
| `validity` | Telefonnumrets tekniska korrekthet. |

{style="table-layout:auto"}

Mer information om datatypen för telefonnummer finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.schema.json)
