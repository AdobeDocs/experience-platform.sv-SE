---
title: Principklass
description: Det här dokumentet innehåller en översikt över klassen Policy i Experience Data Model (XDM).
exl-id: 56cc8c69-84a0-493e-85c5-e0cd994e4bee
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# [!UICONTROL Policy] class

I Experience Data Model (XDM) är [!UICONTROL Policy] klassen hämtar den minsta uppsättning egenskaper som definierar en försäkringsprofil.

![](../images/classes/policy.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `assignedBeneficiary` | Array med [[!UICONTROL Person]](../data-types/person.md) datatyper | Fångar den eller de mottagare som tilldelats policyn. |
| `benefitAmount` | [[!UICONTROL Currency]](../data-types/currency.md) | Det belopp som ska betalas enligt policyvillkoren. |
| `location` | [[!UICONTROL Postal address]](../data-types/postal-address.md) | Den plats där försäkringsbrevet utfärdas. |
| `owner` | [!UICONTROL Object] | Hämtar profilinnehavarens profilinformation. |
| `owner.faxPhone` | [[!UICONTROL Phone number]](../data-types/phone-number.md) | Ägarens faxnummer. |
| `owner.homeAddress` | [[!UICONTROL Postal address]](../data-types/postal-address.md) | Ägarens hemadress. |
| `owner.homePhone` | [[!UICONTROL Phone number]](../data-types/phone-number.md) | Ägarens hemtelefonnummer. |
| `owner.mobilePhone` | [[!UICONTROL Phone number]](../data-types/phone-number.md) | Ägarens mobiltelefonnummer. |
| `owner.personalEmail` | [[!UICONTROL Email address]](../data-types/email-address.md) | Ägarens personliga e-postadress. |
| `ID` | [!UICONTROL String] | En identifierare för försäkringsskyddet. |
| `_id` | [!UICONTROL String] | En unik systemgenererad strängidentifierare för posten. Det här fältet används för att spåra en enskild posts unika karaktär, förhindra dubblering av data och för att söka efter posten i underordnade tjänster.<br><br>Eftersom det här fältet genereras av systemet, anges inget explicit värde vid datainmatning. Du kan dock välja att ange egna unika ID-värden om du vill. |
| `endDate` | [!UICONTROL DateTime] | Det datum då försäkringsskyddet upphör (eller upphör). |
| `hasAssignedBeneficiary` | [!UICONTROL Boolean] | Anger om policyn har tilldelats en mottagare. |
| `name` | [!UICONTROL String] | Namnet på försäkringsavtalet. |
| `startDate` | [!UICONTROL DateTime] | Det datum då försäkringsskyddet börjar (eller börjar). |
| `type` | [!UICONTROL String] | Typ av försäkring, t.ex. hemförsäkring, bilförsäkring, uthyrning eller båt. |

{style="table-layout:auto"}
