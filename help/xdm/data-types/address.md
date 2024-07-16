---
title: Datatyp för postadress
description: Läs mer om datatypen XDM (Postal Address Experience Data Model).
exl-id: 92385cd8-60c8-4360-a8e7-e6224e85e4d4
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# Datatypen [!UICONTROL Postal Address]

[!UICONTROL Postal Address] är en XDM-datatyp (Standard Experience Data Model) som tillhandahåller adressinformation.

![Ett diagram över datatypen [!UICONTROL Postal Address].](../images/data-types/postal-address.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
|------------------------------------|------------------|-----------|-----------------------------------------------------------------------------------------------|
| [!UICONTROL Primary] | `primary` | boolesk | Indikator för primär adress. En profil kan bara ha en `primary`-adress vid en given tidpunkt. |
| [!UICONTROL Label] | `label` | string | Adressens namn i fritt format. |
| [!UICONTROL Street 1] | `street1` | string | Primär information om gatuminivå, lägenhetsnummer, gatunummer och gatunamn. |
| [!UICONTROL Street 2] | `street2` | string | Ytterligare gatuinformation, andra raden. |
| [!UICONTROL Street 3] | `street3` | string | Ytterligare gatuinformation, tredje linje. |
| [!UICONTROL Street 4] | `street4` | string | Ytterligare gatuinformation, fjärde raden. |
| [!UICONTROL Region] | `region` | string | Region, region eller distrikt. |
| [!UICONTROL Post office box] | `postOfficeBox` | string | Post box of the address. |
| [!UICONTROL Country] | `country` | string | Namnet på det statligt administrerade territoriet. Förutom ``countryCode`` är det här ett friformsfält som kan ha landsnamnet på vilket språk som helst. |
| [!UICONTROL State] | `state` | string | Statens namn. Det här är ett frihandsfält. |
| [!UICONTROL Status] | `status` | string | En indikation om möjligheten att använda adressen. |
| [!UICONTROL Status reason] | `statusReason` | string | En beskrivning av aktuell status. |
| [!UICONTROL Last verified date] | `lastVerifiedDate` | string | Det datum då adressen senast verifierades som fortfarande associerad med personen. |

{style="table-layout:auto"}

Mer information om datatypen finns i det [fullständiga schemat](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/address.schema.json) i den offentliga XDM-databasen:
