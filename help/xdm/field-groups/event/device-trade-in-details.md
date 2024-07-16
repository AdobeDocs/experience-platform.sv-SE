---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;ExperienceEvent;fields;schemas;Schema design;field group;field group;device;trade in;trade in;trade in;
solution: Experience Platform
title: Schemafältgrupp för detaljer för enhetshandel
description: Läs mer om schemafältgruppen Device Trade-In Details.
exl-id: 744557be-0297-453f-9134-9d0f4ef2df4d
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# Schemafältgruppen [!UICONTROL Device Trade-In Details]

>[!NOTE]
>
>Namnen på flera schemafältgrupper har ändrats. Mer information finns i dokumentet om [uppdatering av fältgruppnamn](../name-updates.md).

[!UICONTROL Device Trade-In Details] är en standardschemafältgrupp för [[!DNL XDM ExperienceEvent] klassen](../../classes/experienceevent.md). Det innehåller ett enskilt fält (`deviceTradeInDetails`) som beskriver en enhets inbytestransaktion, inklusive inbytesvärde, ursprungligt enhets-ID och nytt enhets-ID.

![Struktur för detaljer om inbyte av enheter](../../images/field-groups/device-trade-in-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `tradeInValue` | [Valuta](../../data-types/currency.md) | Värdet på enheten som handlas. |
| `newDeviceID` | Sträng | ID:t för den nya enheten som handlas för. |
| `originalDeviceID` | Sträng | ID för enheten som handlas. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.schema.json)
