---
solution: Experience Platform
title: Allmän datatyp för inställningsfält för anpassning
description: Läs mer om datatypen XDM för det allmänna inställningsfältet för personalisering.
exl-id: 3f6a3c31-19f3-4bad-921e-9ad33c6b9ac9
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# [!UICONTROL Generic Personalization Preference Field] datatyp

[!UICONTROL Generic Personalization Preference Field] är en standard-XDM-datatyp som beskriver en kunds val för en viss personaliseringsinställning.

>[!NOTE]
>
>Den här datatypen är avsedd att användas för att anpassa strukturen för organisationens medgivandescheman med hjälp av [[!UICONTROL Consents and Preferences] fältgrupp](../field-groups/profile/consents.md) som en baslinje.

![](../images/data-types/personalization-field.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `val` | Sträng | Det föredragna valet för den här typen av personalisering som kunden tillhandahållit. I tabellen nedan finns godkända värden och definitioner. |

{style="table-layout:auto"}

I följande tabell visas godkända värden för `val`:

| Värde | Titel | Beskrivning |
| --- | --- | --- |
| `y` | Ja (anmälan) | Kunden har valt att göra detta. Med andra ord: **do** samtycke till att deras uppgifter används på det sätt som anges i föremålet i fråga. |
| `n` | Nej (avanmälan) | Kunden har valt att inte göra det. Med andra ord: **inte** samtycke till att deras uppgifter används på det sätt som anges i föremålet i fråga. |
| `p` | Väntande verifiering | Systemet har ännu inte fått något slutligt inställningsvärde. Detta används oftast som en del av ett samtycke som kräver tvåstegsverifiering. Om en kund till exempel väljer att ta emot e-postmeddelanden ställs detta medgivande in på `p` tills de väljer en länk i ett e-postmeddelande för att verifiera att de har angett rätt e-postadress, och då uppdateras medgivandet till `y`.<br><br>Om den här inställningen inte använder en verifieringsprocess i två uppsättningar `p` kan i stället användas för att ange att kunden ännu inte har svarat på frågan om samtycke. Du kan till exempel ställa in värdet automatiskt på `p` på första sidan av en webbplats, innan kunden har svarat på frågan om samtycke. I jurisdiktioner som inte kräver uttryckligt medgivande kan ni också använda det för att ange att kunden inte uttryckligen har avanmält sig (med andra ord antas medgivande). |
| `u` | Okänd | Kundens inställningsinformation är okänd. |
| `dy` | Standard för Ja (anmälan) | Kunden har inte lämnat in något medgivande i sig och behandlas som en anmälan (&quot;Ja&quot;) som standard. Med andra ord antas samtycke tills kunden anger något annat.<br><br>Observera att om lagar eller ändringar i företagets sekretesspolicy leder till ändringar av standardvärdena för vissa eller alla användare, måste du uppdatera alla profiler som innehåller standardvärden manuellt. |
| `dn` | Standard för Nej (avanmälan) | Kunden har inte lämnat in något medgivande och behandlas som standard som avanmälan (&quot;Nej&quot;). Med andra ord antas kunden ha vägrat samtycke tills de anger något annat.<br><br>Observera att om lagar eller ändringar i företagets sekretesspolicy leder till ändringar av standardvärdena för vissa eller alla användare, måste du uppdatera alla profiler som innehåller standardvärden manuellt. |
| `LI` | Legitimalt intresse | Det legitima affärsintresset att samla in och behandla dessa uppgifter för det särskilda ändamålet uppväger den potentiella skada som de kan åsamka den enskilda personen. |
| `CT` | Kontrakt | Insamling av uppgifter för det angivna ändamålet krävs för att uppfylla avtalsförpliktelser med den enskilda personen. |
| `CP` | Efterlevnad av en juridisk skyldighet | Insamlingen av uppgifter för det angivna ändamålet krävs för att uppfylla företagets rättsliga skyldigheter. |
| `VI` | Enskilda personers vitala intressen | Insamling av uppgifter för det särskilda ändamålet krävs för att skydda den enskildes vitala intressen. |
| `PI` | Offentligt intresse | Insamling av uppgifter för det angivna ändamålet krävs för att utföra en uppgift i allmänhetens intresse eller vid utövandet av offentlig makt. |

{style="table-layout:auto"}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/personalization-field.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/personalization-field.schema.json)
