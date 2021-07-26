---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;ExperienceEvent;fields;schemas;Schema design;field group;field group;device;trade in;trade in;trade in;
solution: Experience Platform
title: Schemafältgrupp för detaljer för enhetshandel
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över schemafältgruppen Device Trade-In Details.
source-git-commit: 2592d4f494d4d3dcfba63eb539498416fbdf6707
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 1%

---

# [!UICONTROL Device Trade-In Details] schemafältgrupp

>[!NOTE]
>
>Namnen på flera schemafältgrupper har ändrats. Mer information finns i dokumentet om [uppdatering av fältgruppnamn](../name-updates.md).

[!UICONTROL Device Trade-In Details] är en standardgrupp för schemafält för  [[!DNL XDM ExperienceEvent] klassen](../../classes/experienceevent.md). Det innehåller ett enda fält (`deviceTradeInDetails`) som beskriver en enhets inbytestransaktion, inklusive inbytesvärde, ursprungligt enhets-ID och nytt enhets-ID.

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
