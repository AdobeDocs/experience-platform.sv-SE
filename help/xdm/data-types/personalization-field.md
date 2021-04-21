---
solution: Experience Platform
title: Allmän datatyp för inställningsfält för personalisering
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över datatypen XDM för det allmänna inställningsfältet för personalisering.
exl-id: 3f6a3c31-19f3-4bad-921e-9ad33c6b9ac9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 1%

---

# [!UICONTROL Generic Personalization Preference Field] datatyp

[!UICONTROL Generic Personalization Preference Field] är en standard-XDM-datatyp som beskriver en kunds val för en viss personaliseringsinställning.

>[!NOTE]
>
>Den här datatypen är avsedd att användas för att anpassa strukturen för organisationens medgivandescheman med hjälp av [[!UICONTROL Privacy/Personalization/Marketing Preferences (Consents)]-mixin](../mixins/profile/consents.md) som baslinje.

![](../images/data-types/personalization-field.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `val` | Sträng | Det föredragna valet för den här typen av personalisering som kunden tillhandahållit. I tabellen nedan finns godkända värden och definitioner. |

I följande tabell visas godkända värden för `val`:

| Värde | Titel | Beskrivning |
| --- | --- | --- |
| `y` | Ja | Kunden har valt att göra detta. De **do** samtycker med andra ord till att deras data används, vilket den aktuella inställningen anger. |
| `n` | Nej | Kunden har valt att inte göra det. De **godkänner med andra ord inte** att deras data används på det sätt som inställningen i fråga anger. |
| `p` | Väntande verifiering | Systemet har ännu inte fått något slutligt inställningsvärde. Detta används oftast som en del av ett samtycke som kräver tvåstegsverifiering. Om en kund till exempel väljer att ta emot e-postmeddelanden anges det medgivandet till `p` tills de väljer en länk i ett e-postmeddelande för att verifiera att de har angett rätt e-postadress, och då uppdateras medgivandet till `y`.<br><br>Om den här inställningen inte använder en tvåstegsverifieringsprocess kan  `p` valet i stället användas för att ange att kunden ännu inte har svarat på bekräftelseuppmaningen. Du kan till exempel automatiskt ange värdet `p` på den första sidan på en webbplats, innan kunden har svarat på frågan om samtycke. I jurisdiktioner som inte kräver uttryckligt medgivande kan ni också använda det för att ange att kunden inte uttryckligen har avanmält sig (med andra ord antas medgivande). |
| `u` | Okänd | Kundens inställningsinformation är okänd. |
| `LI` | Legitimalt intresse | Det legitima affärsintresset att samla in och behandla dessa uppgifter för det särskilda ändamålet uppväger den potentiella skada som de kan åsamka den enskilda personen. |
| `CT` | Kontrakt | Insamling av uppgifter för det angivna ändamålet krävs för att uppfylla avtalsförpliktelser med den enskilda personen. |
| `CP` | Efterlevnad av en juridisk skyldighet | Insamlingen av uppgifter för det angivna ändamålet krävs för att uppfylla företagets rättsliga skyldigheter. |
| `VI` | Enskilda personers vitala intressen | Insamling av uppgifter för det särskilda ändamålet krävs för att skydda den enskildes vitala intressen. |
| `PI` | Offentligt intresse | Insamling av uppgifter för det angivna ändamålet krävs för att utföra en uppgift i allmänhetens intresse eller vid utövandet av offentlig makt. |

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/personalization-field.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/personalization-field.schema.json)
