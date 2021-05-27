---
solution: Experience Platform
title: Datatypen Allmänt fält för samtycke
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över XDM-datatypen för det allmänna innehållsfältet.
exl-id: f1f14eb7-21dd-45ca-8fb4-68f397cfa697
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 1%

---

# [!UICONTROL Generic Consent Field] datatyp

[!UICONTROL Generic Consent Field] är en standard-XDM-datatyp som beskriver en kunds val för en viss samtyckesinställning.

>[!NOTE]
>
>Den här datatypen är avsedd att användas för att anpassa strukturen för din organisations medgivandescheman med fältgruppen [[!UICONTROL Privacy/Personalization/Marketing Preferences (Consents)]](../field-groups/profile/consents.md) som baslinje.

![](../images/data-types/consent-field.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `val` | Sträng | Kunden har gett sitt medgivande för det här användningsärendet. I tabellen nedan finns godkända värden och definitioner. |

{style=&quot;table-layout:auto&quot;}

I följande tabell visas godkända värden för `val`:

| Värde | Titel | Beskrivning |
| --- | --- | --- |
| `y` | Ja | Kunden har valt att ge sitt samtycke. Med andra ord godkänner de **do** att deras uppgifter används, vilket framgår av det aktuella medgivandet. |
| `n` | Nej | Kunden har avböjt sitt medgivande. Med andra ord godkänner de **inte** att deras uppgifter används på det sätt som det aktuella medgivandet anger. |
| `p` | Väntande verifiering | Systemet har ännu inte fått något slutligt godkännandevärde. Detta används oftast som en del av ett samtycke som kräver tvåstegsverifiering. Om en kund till exempel väljer att ta emot e-postmeddelanden anges det medgivandet till `p` tills de väljer en länk i ett e-postmeddelande för att verifiera att de har angett rätt e-postadress, och då uppdateras medgivandet till `y`.<br><br>Om det här medgivandet inte använder en tvåstegsverifieringsprocess kan  `p` valet i stället användas för att ange att kunden ännu inte har svarat på bekräftelseuppmaningen. Du kan till exempel automatiskt ange värdet `p` på den första sidan på en webbplats, innan kunden har svarat på frågan om samtycke. I jurisdiktioner som inte kräver uttryckligt medgivande kan ni också använda det för att ange att kunden inte uttryckligen har avanmält sig (med andra ord antas medgivande). |
| `u` | Okänd | Kundens godkännandeinformation är okänd. |
| `LI` | Legitimalt intresse | Det legitima affärsintresset att samla in och behandla dessa uppgifter för det särskilda ändamålet uppväger den potentiella skada som de kan åsamka den enskilda personen. |
| `CT` | Kontrakt | Insamling av uppgifter för det angivna ändamålet krävs för att uppfylla avtalsförpliktelser med den enskilda personen. |
| `CP` | Efterlevnad av en juridisk skyldighet | Insamlingen av uppgifter för det angivna ändamålet krävs för att uppfylla företagets rättsliga skyldigheter. |
| `VI` | Enskilda personers vitala intressen | Insamling av uppgifter för det särskilda ändamålet krävs för att skydda den enskildes vitala intressen. |
| `PI` | Offentligt intresse | Insamling av uppgifter för det angivna ändamålet krävs för att utföra en uppgift i allmänhetens intresse eller vid utövandet av offentlig makt. |

{style=&quot;table-layout:auto&quot;}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-field.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-field.schema.json)
