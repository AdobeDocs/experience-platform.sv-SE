---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;phoneNumber;xdm:phoneNumber;datatype;data-type;data type;
solution: Experience Platform
title: Datatyp för telefonnummer
topic: overview
description: Det här dokumentet innehåller en översikt över datatypen XDM för telefonnummer.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# [!UICONTROL Phone number] datatyp

[!UICONTROL Phone number] är en standard-XDM-datatyp som beskriver informationen för ett telefonnummer.

<img src="../images/data-types/phone-number.png" width="600" /><br />

| Egenskap | Beskrivning |
| --- | --- |
| `extension` | Det interna uppringningsnummer som används för anrop från en privat börs, operator eller instrumentpanel. |
| `number` | Telefonnumret. Observera att telefonnumret är en sträng och kan innehålla meningsfulla tecken som hakparenteser `()`, bindestreck `-`eller tecken för att indikera underordnade identifierare som tillägg `x` till exempel `1-353(0)18391111` eller `+613 9403600x1234`. |
| `primary` | Ett booleskt värde som anger om det här är personens primära telefonnummer. Till skillnad från adress och e-postadress kan det finnas flera primära telefonnummer. en per kommunikationskanal. Kommunikationskanalen definieras av typen (anges med namnet på den överordnade egenskapen): `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown`och `fax`. |
| `status` | Anger om telefonnumret kan användas. |
| `statusReason` | En beskrivning av aktuell status. |
| `validity` | Telefonnumrets tekniska korrekthet. |

Mer information om datatypen för telefonnummer finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/phonenumber.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/phonenumber.schema.json)