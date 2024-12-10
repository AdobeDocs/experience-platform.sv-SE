---
title: Kodningsdatatyp
description: Läs mer om datatypen XDM (Coding Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 23b789da-1feb-4001-8268-f0d7e2e8563b
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 0%

---

# Datatypen [!UICONTROL Coding]

[!UICONTROL Coding] är en XDM-datatyp (Standard Experience Data Model) som beskriver en referens till en kod som definieras av ett terminologiskt system. Den här datatypen skapas enligt specifikationerna för HL7 FHIR version 5.

![Kodningsdatatypstruktur](../../../images/healthcare/data-types/coding.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | Sträng | Symbolen i syntaxen som definieras av systemet. |
| [!UICONTROL Display] | `display` | Sträng | Representationen som definieras av systemet. |
| [!UICONTROL System] | `system` | Sträng | Namnutrymmet för identifierarvärdet, representerat som en URI. |
| [!UICONTROL Is Selected By User] | `userSelected` | Boolean | En indikator på om den här kodningen har valts av användaren. Standardvärdet är false. |
| [!UICONTROL Version] | `version` | Sträng | Versionen av systemet. |

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/coding.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/coding.schema.json)
