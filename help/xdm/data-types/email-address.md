---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;emailAddress;xdm:emailAddress;email;email address;datatype;data-type;data type;
solution: Experience Platform
title: Datatyp för e-postadress
topic: overview
description: Det här dokumentet innehåller en översikt över XDM-datatypen för e-postadress.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---


# [!UICONTROL Email address] datatyp

[!UICONTROL Email address] är en standard-XDM-datatyp som beskriver informationen för en e-postadress.

<img src="../images/data-types/email-address.png" width="450" /><br />

| Egenskap | Beskrivning |
| --- | --- |
| `address` | Den tekniska adressen för e-postmeddelandet enligt den vanliga definitionen i RFC2822 och efterföljande standarder (till exempel `name@domain.com`). |
| `label` | Ytterligare visningsinformation som kan vara tillgänglig. Om ett e-postmeddelande t.ex. har en Microsoft Outlook-adress som `John Smith smithjr@company.uk`visas, `John Smith` placeras det här fältet. |
| `primary` | Anger om det här är personens primära e-postadress. En profil kan bara ha en `primary` e-postadress vid en viss tidpunkt. |
| `status` | Anger om e-postadressen kan användas |
| `statusReason` | En beskrivning av aktuell `status`. |
| `type` | Kontots förhållande till personen (till exempel `work` eller `personal`). |


Mer information om datatypen för e-postadresser finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.schema.json)