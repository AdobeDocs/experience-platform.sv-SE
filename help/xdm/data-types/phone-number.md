---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;Schemas;phoneNumber;xdm:phoneNumber;datatyp;datatyp;datatyp;data type;
solution: Experience Platform
title: Telefonnummerdatatyp
topic: overview
description: Det här dokumentet innehåller en översikt över datatypen XDM för telefonnummer.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---


# [!UICONTROL Phone number] datatyp

[!UICONTROL Phone number] är en standard-XDM-datatyp som beskriver informationen för ett telefonnummer.

<img src="../images/data-types/phone-number.png" width="600" /><br />

| Egenskap | Beskrivning |
| --- | --- |
| `extension` | Det interna uppringningsnummer som används för anrop från en privat börs, operator eller instrumentpanel. |
| `number` | Telefonnumret. Observera att telefonnumret är en sträng och kan innehålla meningsfulla tecken, t.ex. hakparenteser `()`, bindestreck `-` eller tecken som anger underordnade identifierare, t.ex. tillägg `x` eller `+613 9403600x1234`.`1-353(0)18391111` |
| `primary` | Ett booleskt värde som anger om det här är personens primära telefonnummer. Till skillnad från adress och e-postadress kan det finnas flera primära telefonnummer. en per kommunikationskanal. Kommunikationskanalen definieras av typen (anges med namnet på den överordnade egenskapen): `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown` och `fax`. |
| `status` | Anger om telefonnumret kan användas. |
| `statusReason` | En beskrivning av aktuell status. |
| `validity` | Telefonnumrets tekniska korrekthet. |

Mer information om datatypen för telefonnummer finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/phonenumber.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/phonenumber.schema.json)