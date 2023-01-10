---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;Schemas;phoneNumber;xdm:phoneNumber;datatyp;datatyp;datatyp;data type;
solution: Experience Platform
title: Telefonnummerdatatyp
description: Det här dokumentet innehåller en översikt över datatypen XDM för telefonnummer.
exl-id: b84e48f9-bbb4-4b8b-9476-4bc1c455ecfd
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# [!UICONTROL Phone number] datatyp

[!UICONTROL Phone number] är en standard-XDM-datatyp som beskriver informationen för ett telefonnummer.

<img src="../images/data-types/phone-number.png" width="600" /><br />

| Egenskap | Beskrivning |
| --- | --- |
| `extension` | Det interna uppringningsnummer som används för anrop från en privat börs, operator eller instrumentpanel. |
| `number` | Telefonnumret. Observera att telefonnumret är en sträng och kan innehålla meningsfulla tecken som hakparenteser `()`, bindestreck `-`, eller tecken som anger underuppringningsidentifierare som tillägg `x` till exempel `1-353(0)18391111` eller `+613 9403600x1234`. |
| `primary` | Ett booleskt värde som anger om det här är personens primära telefonnummer. Till skillnad från adress och e-postadress kan det finnas flera primära telefonnummer. en per kommunikationskanal. Kommunikationskanalen definieras av typen (anges med namnet på den överordnade egenskapen): `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown`och `fax`. |
| `status` | Anger om telefonnumret kan användas. |
| `statusReason` | En beskrivning av aktuell status. |
| `validity` | Telefonnumrets tekniska korrekthet. |

{style=&quot;table-layout:auto&quot;}

Mer information om datatypen för telefonnummer finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.schema.json)
