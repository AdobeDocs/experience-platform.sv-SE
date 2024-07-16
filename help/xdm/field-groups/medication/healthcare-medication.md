---
title: Fältgrupp för sjukvårdssystem
description: Läs mer om schemafältgruppen för sjukvårdsmedicin.
exl-id: 3423d067-fe8c-44e5-a6f9-ce0458d26ebc
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 0%

---

# Schemafältgruppen [!UICONTROL Healthcare medication]

[!UICONTROL Healthcare medication] är en standardschemafältgrupp för klassen [[!UICONTROL Medication] ](../../classes/medication.md). Det innehåller ett enskilt objekttypsfält `medication` som samlar in information som varumärkesnamn, partinummer och kvantitet.

![](../../images/field-groups/healthcare-medication.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `ingredients` | Array med objekt | Listar ingredienserna som finns i medicinen. Varje objekt innehåller följande egenskaper: <ul><li>`isActive`: (Boolean) Anger om den här ingrediensen fortfarande används aktivt i det här läkemedlet.</li><li>`name`: (String) Namnet på komponenten.</li><li>`quantity`: (String) Mängden ingrediens som finns i medicineringen.</li></ul> |
| `brandName` | Sträng | Läkemedlets varumärke. |
| `codes` | Array med strängar | En lista med koder som identifierar detta läkemedel. |
| `dosageUnitNumber` | Dubbel | Dosenhetsnumret för läkemedlet. |
| `dosageUnitOfMeasurement` | Sträng | Måttenheten för doseringsnumret. |
| `expiryDate` | DateTime | Utgångsdatum för läkemedlet. |
| `genericName` | Sträng | Det generiska namnet på läkemedlet. |
| `lotNumber` | Sträng | Unik identifierare för läkemedelsbatchen. |
| `manufacturerName` | Sträng | Läkemedlets namn. |
| `quantity` | Dubbel | Mängden läkemedel i förpackningen. |
| `status` | Sträng | En generell status som anger om läkemedlet eller läkemedlet är aktivt eller inte. |
| `volume` | Dubbel | Läkemedlets volym. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i [den offentliga XDM-databasen](https://github.com/adobe/xdm/blob/master/components/fieldgroups/medication/healthcare-medication.schema.json).
