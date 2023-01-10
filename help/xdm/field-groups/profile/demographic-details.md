---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;Individuell profil;fält;scheman;scheman;schemadesign;fältgrupp;fältgrupp;person;personinformation;profilpersoninformation;person;
solution: Experience Platform
title: Fältgrupp för schema för demografiska detaljer
description: Det här dokumentet innehåller en översikt över schemafältgruppen för demografiska detaljer.
exl-id: 588c044c-b80d-4cb9-9f97-92f040d54bb4
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 2%

---


# [!UICONTROL Demographic Details] schemafältgrupp

>[!NOTE]
>
>Namnen på flera schemafältgrupper har ändrats. Visa dokumentet på [uppdaterar fältgruppnamn](../name-updates.md) för mer information.

[!UICONTROL Demographic Details] är en standardgrupp för schemafält för [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md). Fältgruppen har en rotnivå `person` objekt, vars underfält beskriver information om en enskild person.

![](../../images/field-groups/demographic-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `person.name` | [Personnamn](../../data-types/person-name.md) | Ett objekt vars underfält beskriver olika element i en persons namn. |
| `person.birthDate` | Datum | Det fullständiga datum som en person föddes på, i form av en ISO 8601-tidsstämpel. |
| `person.birthDayAndMonth` | Sträng | Den dag och månad en person föddes, i formatet MM-DD. Detta fält ska användas när dagen och månaden för en persons födelse är känd, men inte året. |
| `person.birthYear` | Heltal | Det år en person föddes, inklusive 1989. Detta fält ska användas när endast personens ålder är känd, inte det fullständiga födelsedatumet. |
| `person.gender` | Sträng | Personens könsidentitet. |
| `person.martialStatus` | Sträng | Beskriver en persons relation med en viktig annan person. |
| `person.nationality` | Sträng | Det rättsliga förhållandet mellan en person och deras stat representerat med ISO 3166-1 Alpha-2-koden. |
| `person.taxId` | Sträng | Personens skatte-/skatte-ID, t.ex. TIN i USA eller CIF/NIF i Spanien. |

{style=&quot;table-layout:auto&quot;}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.schema.json)