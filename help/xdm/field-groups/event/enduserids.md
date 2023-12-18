---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;ExperienceEvent;fields;schemas;Schema design;field group;field group;enduserids;end user;ids;
solution: Experience Platform
title: Schemafältgrupp för detaljer för slutanvändar-ID
description: Läs mer om schemafältgruppen för information om slutanvändar-ID.
exl-id: ff5b74f4-7700-4d10-821e-b50f80ea8c05
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 0%

---


# [!UICONTROL End User ID Details] schemafältgrupp

>[!NOTE]
>
>Namnen på flera schemafältgrupper har ändrats. Visa dokumentet på [uppdaterar fältgruppnamn](../name-updates.md) för mer information.

[!UICONTROL End User ID Details] är en standardgrupp för schemafält för [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md), används för att beskriva en persons identitetsinformation i flera olika Adobe-program. Fältgruppen har en rotnivå `endUserIDs` objekt, som i sin tur innehåller ett skrivskyddat `_experience` fält vars värden uppdateras automatiskt när data hämtas.

<img src="../../images/field-groups/enduserids.png" width="700" /><br />

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
