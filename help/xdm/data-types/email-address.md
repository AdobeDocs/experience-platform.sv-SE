---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;Schemas;emailAddress;xdm:emailAddress;email;email address;data type;data type;data type;
solution: Experience Platform
title: Datatyp för e-postadress
description: Läs mer om XDM-datatypen för e-postadresser.
exl-id: 1364df42-f89f-4f48-bcda-5332f3828326
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---

# Datatypen [!UICONTROL Email address]

[!UICONTROL Email address] är en XDM-datatyp (Standard Experience Data Model) som beskriver informationen för en e-postadress.

![](../images/data-types/email-address.png){width=450}

| Egenskap | Beskrivning |
| --- | --- |
| `address` | Den tekniska adressen för e-postmeddelandet enligt den vanliga definitionen i RFC2822 och efterföljande standarder (till exempel `name@domain.com`).<br><br>I XDM måste e-postadresser innehålla en giltig toppnivådomän för att kunna validera. I följande [dokument](https://data.iana.org/TLD/tlds-alpha-by-domain.txt) finns en fullständig lista över giltiga toppnivådomäner som definierats av IANA (Internet Assigned Numbers Authority). |
| `label` | Ytterligare visningsinformation som kan vara tillgänglig. Om ett e-postmeddelande till exempel har en avancerad adressvisning i Microsoft Outlook på `John Smith smithjr@company.uk`, placeras `John Smith` i det här fältet. |
| `primary` | Anger om det här är personens primära e-postadress. En profil kan bara ha en `primary`-e-postadress vid en viss tidpunkt. |
| `status` | Anger om e-postadressen kan användas |
| `statusReason` | En beskrivning av aktuell `status`. |
| `type` | Det sätt som kontot relaterar till personen (till exempel `work` eller `personal`). |

{style="table-layout:auto"}


Mer information om datatypen för e-postadresser finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.schema.json)
