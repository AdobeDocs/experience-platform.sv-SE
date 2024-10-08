---
title: Principklass
description: Läs mer om klassen Policy i Experience Data Model (XDM).
exl-id: 56cc8c69-84a0-493e-85c5-e0cd994e4bee
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 0%

---

# klassen [!UICONTROL Policy]

I Experience Data Model (XDM) hämtar klassen [!UICONTROL Policy] den minsta uppsättningen egenskaper som definierar en försäkringsprofil.

![](../images/classes/policy.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `assignedBeneficiary` | Matris med [[!UICONTROL Person]](../data-types/person.md) datatyper | Fångar den eller de mottagare som tilldelats policyn. |
| `benefitAmount` | [[!UICONTROL Currency]](../data-types/currency.md) | Det belopp som ska betalas enligt policyvillkoren. |
| `location` | [[!UICONTROL Postal address]](../data-types/postal-address.md) | Den plats där försäkringsbrevet utfärdas. |
| `owner` | [!UICONTROL Object] | Hämtar profilinnehavarens profilinformation. |
| `owner.faxPhone` | [[!UICONTROL Phone number]](../data-types/phone-number.md) | Ägarens faxnummer. |
| `owner.homeAddress` | [[!UICONTROL Postal address]](../data-types/postal-address.md) | Ägarens hemadress. |
| `owner.homePhone` | [[!UICONTROL Phone number]](../data-types/phone-number.md) | Ägarens hemtelefonnummer. |
| `owner.mobilePhone` | [[!UICONTROL Phone number]](../data-types/phone-number.md) | Ägarens mobiltelefonnummer. |
| `owner.personalEmail` | [[!UICONTROL Email address]](../data-types/email-address.md) | Ägarens personliga e-postadress. |
| `ID` | [!UICONTROL String] | En identifierare för försäkringsskyddet. |
| `_id` | [!UICONTROL String] | En unik systemgenererad strängidentifierare för posten. Det här fältet används för att spåra en enskild posts unika karaktär, förhindra dubblering av data och för att söka efter posten i underordnade tjänster.<br><br>Eftersom det här fältet är systemgenererat anges inget explicit värde vid datainmatning. Du kan dock välja att ange egna unika ID-värden om du vill. |
| `endDate` | [!UICONTROL DateTime] | Det datum då försäkringsskyddet upphör (eller upphör). |
| `hasAssignedBeneficiary` | [!UICONTROL Boolean] | Anger om policyn har tilldelats en mottagare. |
| `name` | [!UICONTROL String] | Namnet på försäkringsavtalet. |
| `startDate` | [!UICONTROL DateTime] | Det datum då försäkringsskyddet börjar (eller börjar). |
| `type` | [!UICONTROL String] | Typ av försäkring, t.ex. hemförsäkring, bilförsäkring, uthyrning eller båt. |

{style="table-layout:auto"}
