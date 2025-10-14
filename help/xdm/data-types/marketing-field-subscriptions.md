---
solution: Experience Platform
title: Allmänt fält för marknadsföringsinställningar med prenumerationsdatatyp
description: Läs mer om det allmänna fältet för marknadsföringsinställningar med XDM-datatypen Subscriptions.
exl-id: 170ea6ca-77fc-4b0a-87f9-6d4b6f32d953
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 0%

---

# Datatypen [!UICONTROL Generic Marketing Preference Field with Subscriptions]

[!UICONTROL Generic Marketing Preference Field with Subscriptions] är en standard-XDM-datatyp som beskriver en kunds val för en viss marknadsföringsinställning.

>[!NOTE]
>
>Den här datatypen är avsedd att användas för att anpassa strukturen för organisationens medgivandescheman med hjälp av fältgruppen [[!UICONTROL Consents and Preferences] &#x200B;](../field-groups/profile/consents.md) som baslinje.
>
>Om du inte behöver en `subscriptions`-karta för ett visst marknadsföringsinställningsfält kan du använda datatypen [basic marketing field](./marketing-field.md) i stället.

![](../images/data-types/marketing-field-subscriptions.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `reason` | Sträng | När en kund väljer bort från ett marknadsföringsärende representerar det här strängfältet anledningen till varför kunden valde bort. |
| `subscriptions` | Karta | En karta över kundernas marknadsföringsönskemål för specifika prenumerationer. Mer information finns i avsnittet om [prenumerationer](#subscriptions). |
| `time` | DateTime | En ISO 8601-tidsstämpel för när marknadsföringsinställningen ändrades, om tillämpligt. |
| `val` | Sträng | Kundens val av preferens för detta marknadsföringsärende. I [nästa avsnitt](#val) finns godkända värden och definitioner. |

{style="table-layout:auto"}

## `val` {#val}

I följande tabell visas godkända värden för `val`:

| Värde | Titel | Beskrivning |
| --- | --- | --- |
| `y` | Ja (anmälan) | Kunden har valt att göra detta. Med andra ord **do** samtycker de till att deras data används, vilket anges av den aktuella inställningen. |
| `n` | Nej (avanmälan) | Kunden har valt att inte göra det. Med andra ord **godkänner de inte** att deras data används, vilket den aktuella inställningen anger. |
| `p` | Väntande verifiering | Systemet har ännu inte fått något slutligt inställningsvärde. Detta används oftast som en del av ett samtycke som kräver tvåstegsverifiering. Om en kund till exempel väljer att ta emot e-postmeddelanden anges det medgivandet till `p` tills de väljer en länk i ett e-postmeddelande för att verifiera att de har angett rätt e-postadress, och då uppdateras medgivandet till `y`.<br><br>Om den här inställningen inte använder en tvåmängdsverifieringsprocess kan valet `p` i stället användas för att ange att kunden ännu inte har svarat på bekräftelseuppmaningen. Du kan till exempel automatiskt ställa in värdet på `p` på den första sidan på en webbplats innan kunden har svarat på frågan om samtycke. I jurisdiktioner som inte kräver uttryckligt medgivande kan ni också använda det för att ange att kunden inte uttryckligen har avanmält sig (med andra ord antas medgivande). |
| `u` | Okänd | Kundens inställningsinformation är okänd. |
| `dy` | Standard för Ja (anmälan) | Kunden har inte lämnat in något medgivande i sig och behandlas som en anmälan (&quot;Ja&quot;) som standard. Med andra ord antas samtycke tills kunden anger något annat.<br><br>Observera att om lagar eller ändringar i företagets sekretesspolicy leder till ändringar i standardvärdena för vissa eller alla användare, måste du uppdatera alla profiler som innehåller standardvärden manuellt. |
| `dn` | Standard för Nej (avanmälan) | Kunden har inte lämnat in något medgivande och behandlas som standard som avanmälan (&quot;Nej&quot;). Med andra ord antas kunden ha vägrat samtycke tills de anger något annat.<br><br>Observera att om lagar eller ändringar i företagets sekretesspolicy leder till ändringar i standardvärdena för vissa eller alla användare, måste du uppdatera alla profiler som innehåller standardvärden manuellt. |
| `LI` | Legitimalt intresse | Det legitima affärsintresset att samla in och behandla dessa uppgifter för det särskilda ändamålet uppväger den potentiella skada som de kan åsamka den enskilda personen. |
| `CT` | Kontrakt | Insamling av uppgifter för det angivna ändamålet krävs för att uppfylla avtalsförpliktelser med den enskilda personen. |
| `CP` | Efterlevnad av en juridisk skyldighet | Insamlingen av uppgifter för det angivna ändamålet krävs för att uppfylla företagets rättsliga skyldigheter. |
| `VI` | Enskilda personers vitala intressen | Insamling av uppgifter för det särskilda ändamålet krävs för att skydda den enskildes vitala intressen. |
| `PI` | Offentligt intresse | Insamling av uppgifter för det angivna ändamålet krävs för att utföra en uppgift i allmänhetens intresse eller vid utövandet av offentlig makt. |

{style="table-layout:auto"}

## `subscriptions` {#subscriptions}

Vissa företag tillåter kunder att välja mellan olika prenumerationer som är kopplade till en viss marknadsföringskanal. Ett bankföretag kan t.ex. tillåta kunder att abonnera på telefonaviseringar för överutnyttjade konton eller ta emot försäljningssamtal för erbjudanden om lojalitetsprogram.

Följande JSON representerar ett exempel på ett marknadsföringsfält för en marknadsföringskanal för telefonsamtal som innehåller en `subscriptions`-karta. Varje nyckel i objektet `subscriptions` representerar en enskild prenumeration för marknadsföringskanalen. Varje prenumeration innehåller i sin tur ett anmälningsvärde (`val`).

```json
"email-marketing-field": {
  "val": "y",
  "time": "2019-01-01T15:52:25+00:00",
  "subscriptions": {
    "loyalty-offers": {
      "val": "y",
      "type": "sales",
      "topics": ["discounts", "early-access"],
      "subscribers": {
        "jdoe@example.com": {
          "time": "2019-01-01T15:52:25+00:00",
          "source": "website"
        }
      }
    },
    "newsletters": {
      "val": "y",
      "type": "advertising",
      "topics": ["hardware"],
      "subscribers": {
        "jdoe@example.com": {
          "time": "2021-01-01T08:32:53+07:00",
          "source": "website"
        },
        "tparan@example.com": {
          "time": "2020-02-03T07:54:21+07:00",
          "source": "call center"
        }
      }
    }
  }
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `val` | [värdet &#x200B;](#val) för medgivande för prenumerationen. |
| `type` | Prenumerationstypen. Detta kan vara vilken beskrivande sträng som helst, förutsatt att den är högst 15 tecken. |
| `topics` | En array med strängar som representerar intressanta områden som en kund prenumererar på, som kan användas för att skicka relevant innehåll till dem. |
| `subscribers` | Ett valfritt mappningsfält som representerar en uppsättning identifierare (t.ex. e-postadresser eller telefonnummer) som har prenumererat på en viss prenumeration. Varje nyckel i det här objektet representerar den aktuella identifieraren och innehåller två underegenskaper: <ul><li>`time`: En ISO 8601-tidsstämpel för när identiteten prenumererade, om tillämpligt.</li><li>`source`: Källan som prenumeranten kommer från. Detta kan vara vilken beskrivande sträng som helst, förutsatt att den är högst 15 tecken.</li></ul> |

{style="table-layout:auto"}

## Ytterligare resurser

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)
