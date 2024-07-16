---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;scheman;person;datatyp;datatyp;datatyp;data type;
solution: Experience Platform
title: Persondatatyp
description: Läs mer om datatypen XDM (Person Experience Data Model).
exl-id: f28a52be-90c7-4ed0-a460-97165bb58046
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Datatypen [!UICONTROL Person]

[!UICONTROL Person] är en XDM-datatyp (Standard Experience Data Model) som beskriver en enskild person. Den här datatypen kan representera en person som agerar i olika roller, till exempel en kund, kontakt eller ägare.

<img src="../images/data-types/person.PNG" width="500" /><br />

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `name` | [[!UICONTROL Person name]](./person-name.md) | Beskriver information om personens fullständiga namn. |
| `birthDate` | Datum | Det fullständiga datumet en person föddes. Datumformatet (utan tid) ska följa standarden [RFC 3339, avsnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `birthDayAndMonth` | Sträng | Den dag och månad en person föddes, i formatet MM-DD. Detta fält ska användas när dagen och månaden för en persons födelse är känd, men inte året. Egenskapens format måste överensstämma med det reguljära uttrycket `[0-1][0-9]-[0-9][0-9]`. |
| `birthYear` | Heltal | Det år en person föddes, inklusive århundradet (till exempel `1983`). Detta fält ska användas när endast personens ålder är känd och inte det fullständiga födelsedatumet. Värdet måste vara mellan 1 och 32767. |
| `gender` | Sträng | Personens könsidentitet. Värdet för den här egenskapen måste vara lika med ett av följande kända enum-värden. <li> `female` </li> <li> `male` </li> <li> `not_specified` </li> <li> `non_specific` </li> Standardvärdet för det här värdet är `not_specified`. |
| `maritalStatus` | Sträng | Beskriver en persons relation med en viktig annan person. Värdet för den här egenskapen måste vara lika med ett av följande uppräkningsvärden. <li> `married` </li> <li> `single` </li> <li> `divorced` </li> <li> `widowed` </li> <li> `not_specified` </li> Standardvärdet för det här värdet är `not_specified`. |
| `nationality` | Sträng | Det rättsliga förhållandet mellan en person och deras stat representerat med ISO 3166-1 Alpha-2-koden. Egenskapens format måste överensstämma med det reguljära uttrycket `^[A-Z]{2}$`. |
| `taxId` | Sträng | Personens skatte- eller skatte-ID, t.ex. TIN (Taxpayer Identification Number) i USA eller Certificado de Identificación Fiscal (CIF/NIF) i Spanien. |

{style="table-layout:auto"}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.schema.json)
