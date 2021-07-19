---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;Schemas;emailAddress;xdm:emailAddress;email;email address;data type;data type;data type;
solution: Experience Platform
title: Datatyp för e-postadress
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över XDM-datatypen för e-postadress.
exl-id: 1364df42-f89f-4f48-bcda-5332f3828326
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# [!UICONTROL Email address] datatyp

[!UICONTROL Email address] är en standard-XDM-datatyp som beskriver informationen för en e-postadress.

<img src="../images/data-types/email-address.png" width="450" /><br />

| Egenskap | Beskrivning |
| --- | --- |
| `address` | Den tekniska adressen för e-postmeddelandet enligt den vanliga definitionen i RFC2822 och efterföljande standarder (till exempel `name@domain.com`). |
| `label` | Ytterligare visningsinformation som kan vara tillgänglig. Om ett e-postmeddelande till exempel har en Microsoft Outlook-adress som är `John Smith smithjr@company.uk`, placeras `John Smith` i det här fältet. |
| `primary` | Anger om det här är personens primära e-postadress. En profil kan bara ha en `primary`-e-postadress vid en given tidpunkt. |
| `status` | Anger om e-postadressen kan användas |
| `statusReason` | En beskrivning av aktuell `status`. |
| `type` | Det sätt som kontot relaterar till personen (till exempel `work` eller `personal`). |

{style=&quot;table-layout:auto&quot;}


Mer information om datatypen för e-postadresser finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.schema.json)
