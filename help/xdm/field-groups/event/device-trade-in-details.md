---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;ExperienceEvent;fields;schemas;Schema design;field group;field group;device;trade in;trade in;trade in;
solution: Experience Platform
title: Schemafältgrupp för detaljer för enhetshandel
description: Det här dokumentet innehåller en översikt över schemafältgruppen Device Trade-In Details.
exl-id: 744557be-0297-453f-9134-9d0f4ef2df4d
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 1%

---

# [!UICONTROL Device Trade-In Details] schemafältgrupp

>[!NOTE]
>
>Namnen på flera schemafältgrupper har ändrats. Visa dokumentet på [uppdaterar fältgruppnamn](../name-updates.md) för mer information.

[!UICONTROL Device Trade-In Details] är en standardgrupp för schemafält för [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Det innehåller ett enda fält (`deviceTradeInDetails`) som beskriver en enhets inbytestransaktion, inklusive inbytesvärde, ursprungligt enhets-ID och nytt enhets-ID.

![Struktur för detaljer för enhetshandel](../../images/field-groups/device-trade-in-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `tradeInValue` | [Valuta](../../data-types/currency.md) | Värdet på enheten som handlas. |
| `newDeviceID` | Sträng | ID:t för den nya enheten som handlas för. |
| `originalDeviceID` | Sträng | ID för enheten som handlas. |

{style=&quot;table-layout:auto&quot;}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.schema.json)
