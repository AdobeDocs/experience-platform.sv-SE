---
title: Datatyp för postadress
description: Läs mer om datatypen XDM (Postal Address Experience Data Model).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# [!UICONTROL Postal Address] datatyp

[!UICONTROL Postal Address] är en XDM-datatyp (Standard Experience Data Model) som ger adressinformation.

![Ett diagram över [!UICONTROL Postal Address] datatyp.](../images/data-types/postal-address.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
|------------------------------------|------------------|-----------|-----------------------------------------------------------------------------------------------|
| [!UICONTROL Primary] | `primary` | boolesk | Indikator för primär adress. En profil kan bara ha en `primary` adress vid en viss tidpunkt. |
| [!UICONTROL Label] | `label` | string | Adressens namn i fritt format. |
| [!UICONTROL Street 1] | `street1` | string | Primär information om gatuminivå, lägenhetsnummer, gatunummer och gatunamn. |
| [!UICONTROL Street 2] | `street2` | string | Ytterligare gatuinformation, andra raden. |
| [!UICONTROL Street 3] | `street3` | string | Ytterligare gatuinformation, tredje linje. |
| [!UICONTROL Street 4] | `street4` | string | Ytterligare gatuinformation, fjärde raden. |
| [!UICONTROL Region] | `region` | string | Region, region eller distrikt. |
| [!UICONTROL Post office box] | `postOfficeBox` | string | Adressens box. |
| [!UICONTROL Country] | `country` | string | Namnet på det statligt administrerade territoriet. Annan än ``countryCode``är det ett friformsfält som kan ha landsnamnet på vilket språk som helst. |
| [!UICONTROL State] | `state` | string | Statens namn. Det här är ett frihandsfält. |
| [!UICONTROL Status] | `status` | string | En indikation om möjligheten att använda adressen. |
| [!UICONTROL Status reason] | `statusReason` | string | En beskrivning av aktuell status. |
| [!UICONTROL Last verified date] | `lastVerifiedDate` | string | Det datum då adressen senast verifierades som fortfarande associerad med personen. |

{style="table-layout:auto"}

Mer information om datatypen finns i [fullständigt schema](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/address.schema.json) på den offentliga XDM-databasen:
