---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;Schemas;emailAddress;xdm:emailAddress;email;email address;data type;data type;data type;
solution: Experience Platform
title: Datatyp för e-postadress
description: Det här dokumentet innehåller en översikt över XDM-datatypen för e-postadress.
exl-id: 1364df42-f89f-4f48-bcda-5332f3828326
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# [!UICONTROL Email address] datatyp

[!UICONTROL Email address] är en XDM-datatyp (Experience Data Model) som beskriver informationen för en e-postadress.

<img src="../images/data-types/email-address.png" width="450" /><br />

| Egenskap | Beskrivning |
| --- | --- |
| `address` | Den tekniska adressen för e-postmeddelandet enligt den vanliga definitionen i RFC2822 och efterföljande standarder (till exempel `name@domain.com`).<br><br>I XDM måste e-postadresser innehålla en giltig toppnivådomän för att kunna validera. Se följande [dokument](https://data.iana.org/TLD/tlds-alpha-by-domain.txt) om du vill ha en fullständig lista över giltiga toppnivådomäner enligt definitionen av IANA (Internet Assigned Numbers Authority). |
| `label` | Ytterligare visningsinformation som kan vara tillgänglig. Om ett e-postmeddelande t.ex. har en omfattande adressvisning i Microsoft Outlook på `John Smith smithjr@company.uk`, `John Smith` placeras i det här fältet. |
| `primary` | Anger om det här är personens primära e-postadress. En profil kan bara ha en `primary` e-postadress vid en viss tidpunkt. |
| `status` | Anger om e-postadressen kan användas |
| `statusReason` | En beskrivning av den aktuella `status`. |
| `type` | Hur kontot är kopplat till personen (t.ex. `work` eller `personal`). |

{style="table-layout:auto"}


Mer information om datatypen för e-postadresser finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.schema.json)
