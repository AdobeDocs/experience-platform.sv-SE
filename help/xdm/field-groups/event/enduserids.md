---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;ExperienceEvent;fields;schemas;Schema design;field group;field group;enduserids;end user;ids;
solution: Experience Platform
title: Schemafältgrupp för detaljer för slutanvändar-ID
description: Läs mer om schemafältgruppen för information om slutanvändar-ID.
exl-id: ff5b74f4-7700-4d10-821e-b50f80ea8c05
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---


# Schemafältgruppen [!UICONTROL End User ID Details]

>[!NOTE]
>
>Namnen på flera schemafältgrupper har ändrats. Mer information finns i dokumentet om [uppdatering av fältgruppnamn](../name-updates.md).

[!UICONTROL End User ID Details] är en standardschemafältgrupp för [[!DNL XDM ExperienceEvent] klassen](../../classes/experienceevent.md) som används för att beskriva en persons identitetsinformation i flera Adobe-program. Fältgruppen tillhandahåller ett `endUserIDs`-objekt på rotnivå, som i sin tur innehåller ett skrivskyddat `_experience`-fält vars värden uppdateras automatiskt när data hämtas.

![](../../images/field-groups/enduserids.png){width=700}

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `aacustomid` | [Identitet](../../data-types/identity.md) | Anpassade användar-ID för Adobe Analytics Cloud. |
| `aaid` | [Identitet](../../data-types/identity.md) | Slutanvändar-ID för Adobe Analytics Cloud. |
| `acid` | [Identitet](../../data-types/identity.md) | Slutanvändar-ID för Adobe Campaign. |
| `adcloud` | [Identitet](../../data-types/identity.md) | Slutanvändar-ID för Adobe Advertising Cloud. |
| `emailid` | [Identitet](../../data-types/identity.md) | E-postadress-ID. |
| `mcid` | [Identitet](../../data-types/identity.md) | Adobe Marketing Cloud ID (MCID). MCID kallas nu Experience Cloud-ID (ECID). |
| `phonenumberid` | [Identitet](../../data-types/identity.md) | Telefonnummer-ID. |
| `tntid` | [Identitet](../../data-types/identity.md) | Slutanvändar-ID för Adobe Target. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.schema.json)
