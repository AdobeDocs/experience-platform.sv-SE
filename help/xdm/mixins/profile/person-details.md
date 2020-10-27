---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;Schema design;mixin;mixin;person;person details;profile person details;person;
solution: Experience Platform
title: Blandning av demografiska detaljer
topic: overview
description: I det här dokumentet finns en översikt över blandningen av demografiska detaljer.
translation-type: tm+mt
source-git-commit: f9d8021643e72e3fbb5315b54a19815dcdaaa702
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 2%

---


# [!UICONTROL Demographic Details] blanda

>[!NOTE]
>
>Namnen på flera blandningar har ändrats. Mer information finns i dokumentet om uppdatering [av](../name-updates.md) blandade namn.

[!UICONTROL Demographic Details] är en standardblandning för [[!DNL XDM Individual Profile] klassen](../../classes/individual-profile.md). Mixin tillhandahåller ett objekt på rotnivå `person` vars underfält beskriver information om en enskild person.

<img src="../../images/mixins/profile-person-details.png" width="600" /><br />

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

Mer information om blandningen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.schema.json)å