---
title: Datatyp för kontoinformation
description: Det här dokumentet innehåller en översikt över datatypen XDM (Account Details Experience Data Model).
exl-id: 17254393-263e-4000-9bd2-815a9e842533
source-git-commit: 55f86fdd4fd36d21dcbd575d6da83df18abb631d
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 4%

---

# [!UICONTROL Account Details] datatyp

[!UICONTROL Account Details] är en XDM-datatyp (Standard Experience Data Model) som beskriver information som rör en affärsorganisation.

![Datatypstruktur](../images/data-types/account-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `annualRevenue` | [[!UICONTROL Currency]](./currency.md) | Organisationens beräknade årsomsättning. |
| `DUNSNumber` | Sträng | Organisationens Dun &amp; Bradstreet D-U-N-S-nummer. Detta är ett icke-indikativt niosiffrigt nummer som tilldelas varje affärsplats i Dun &amp; Bradstreet-databasen med en unik, separat och distinkt åtgärd och som underhålls endast av Dun &amp; Bradstreet. |
| `NAICSCode` | Sträng | Organisationens klassificering i det nordamerikanska branschklassificeringssystemet. |
| `NAICSDescription` | Sträng | En kort beskrivning av en organisations verksamhetsområde utifrån dess NAICS-kod. |
| `SICCode` | Sträng | Organisationens kod för standardnäringsgrensindelning (SIC). Detta är en fyrsiffrig kod som kategoriserar den bransch som företagen tillhör baserat på deras affärsverksamhet. |
| `SICDescription` | Sträng | En kort beskrivning av en organisations verksamhetsområde utifrån dess SIC-kod. |
| `companyProductAndServices` | Sträng | De produkter och tjänster som organisationen hanterar eller gör affärer med. |
| `facebookPageUrl` | Sträng | En webbplatslänk till organisationens Facebook-konto. |
| `industry` | Sträng | Branschen som den här organisationen är en del av. Det här är ett frihandsfält och du bör använda ett strukturerat värde för frågor eller för att använda `xdm:classifier` -egenskap. |
| `jigsaw` | Sträng | Data.com för organisationen. |
| `linkedinPageUrl` | Sträng | En webbplatslänk till organisationens LinkedIn-konto. |
| `logoUrl` | Sträng | En sökväg som ska kombineras med URL:en för en Salesforce-instans (till exempel `https://yourInstance.salesforce.com/`) för att generera en URL för att begära den profilbild för sociala nätverk som är kopplad till organisationen. Den genererade URL:en returnerar en HTTP-omdirigering (kod 302) till profilbilden för det sociala nätverket för organisationen. |
| `marketSegment` | Sträng | Den namngivna målgrupp som organisationen deltar i. Det här är ett frihandsfält och du bör använda ett strukturerat värde för frågor eller för att använda `xdm:identifier` -egenskap. |
| `numberOfEmployees` | Heltal | Antalet anställda i organisationen. |
| `organizationType` | Sträng | En etikett som beskriver typen av organisation. |
| `primaryEmailDomain` | Sträng | Den primära e-postdomänen som organisationen använder för sin personal. |
| `rating` | Dubbel | Det beräknade poängtalet eller stjärngraderingen för den här organisationen. `1` anger högsta möjliga klassificering, och `0` är det minsta möjliga omdömet. |
| `tickerSymbol` | Sträng | Börssymbolen för detta konto. Högst 20 tecken. |
| `twitterHandleUrl` | Sträng | En webbplatslänk till organisationens twitter handle. |
| `website` | Sträng | URL till organisationens webbplats. |

{style="table-layout:auto"}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/account-organization.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/account-organization.schema.json)
