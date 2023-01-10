---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fält;scheman;scheman;scheman;adress;xdm:address;datatyp;datatyp;datatyp;data type;
solution: Experience Platform
title: Datatyp för postadress
description: Det här dokumentet innehåller en översikt över datatypen XDM för postadress.
exl-id: 94457fe5-80bc-4822-9f6c-48f77d56c89b
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---

# [!UICONTROL Postal address] datatyp

[!UICONTROL Postal address] är en standard-XDM-datatyp som beskriver informationen för en postadress.

<img src="../images/data-types/postal-address.png" width="450" /><br />

| Egenskap | Beskrivning |
| --- | --- |
| `city` | Namnet på staden. |
| `country` | Namnet på det statligt administrerade territoriet. Det här är ett friformsfält som kan ha landsnamnet på vilket språk som helst. |
| `countryCode` | De två tecknen <a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a> landskoden. |
| `createdByBatchID` | ID för den inkapslade batchfilen som skapade adressposten. |
| `dmaID` | Nielsens medieforskning har utsett ett marknadsområde. |
| `label` | Ett friformsnamn för adressen. |
| `lastVerifiedDate` | Datumet då adressen senast verifierades som fortfarande kopplad till personen. |
| `modifiedByBatchID` | ID för den inkapslade batchfilen som senast ändrade posten. |
| `msaID` | Det statistiska storstadsområdet i Förenta staterna där observationen gjordes. |
| `postOfficeBox` | Adressens box. |
| `postalCode` | Postnumret för platsen. Postnummer är inte tillgängliga för alla länder. I vissa länder innehåller detta endast en del av postnumret. |
| `primary` | Ett booleskt värde som anger om det här är personens primära adress. En profil kan bara ha en `primary` adress vid en viss tidpunkt. |
| `region` | Regionen, distriktet eller distriktet i adressen. |
| `repositoryCreatedBy` | ID för den användare som skapade posten. |
| `repositoryLastModifiedBy` | ID för den användare som senast ändrade posten. |
| `stateProvince` | Delstaten eller provinsdelen av observationen. Formatet följer [ISO 3166-2 (land och delområde)](https://www.unece.org/cefact/locode/subdivisions.html) standard. |
| `status` | Anger om adressen kan användas just nu. |
| `statusReason` | En beskrivning av den aktuella `status`. |
| `street1` - `street4` | Dessa fyra fält är avsedda att innehålla information om gatuminivå, lägenhetsnummer, gatunummer och gatunamn. `street2` till `street4` är valfria. |

{style=&quot;table-layout:auto&quot;}

Mer information om datatypen för postadresser finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.schema.json)
