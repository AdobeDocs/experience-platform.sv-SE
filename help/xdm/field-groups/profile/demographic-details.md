---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;Individuell profil;fält;scheman;scheman;schemadesign;fältgrupp;fältgrupp;person;personinformation;profilpersoninformation;person;
solution: Experience Platform
title: Fältgrupp för schemainformation för demografiska detaljer
description: Läs mer om schemafältgruppen för demografiska detaljer.
exl-id: 588c044c-b80d-4cb9-9f97-92f040d54bb4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---


# Schemafältgruppen [!UICONTROL Demographic Details]

>[!NOTE]
>
>Namnen på flera schemafältgrupper har ändrats. Mer information finns i dokumentet om [uppdatering av fältgruppnamn](../name-updates.md).

[!UICONTROL Demographic Details] är en standardschemafältgrupp för [[!DNL XDM Individual Profile] klassen](../../classes/individual-profile.md). Fältgruppen tillhandahåller ett `person`-objekt på rotnivå, vars underfält beskriver information om en enskild person.

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

{style="table-layout:auto"}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.schema.json)