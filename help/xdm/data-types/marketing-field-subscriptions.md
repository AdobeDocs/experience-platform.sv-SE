---
solution: Experience Platform
title: Allmänt fält för marknadsföringsinställningar med prenumerationsdatatyp
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över det allmänna inställningsfältet för marknadsföring med datatypen Subscriptions XDM.
exl-id: 170ea6ca-77fc-4b0a-87f9-6d4b6f32d953
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 1%

---

# [!UICONTROL Generic Marketing Preference Field with Subscriptions] datatyp

[!UICONTROL Generic Marketing Preference Field with Subscriptions] är en standard-XDM-datatyp som beskriver en kunds val för en viss marknadsinställning.

>[!NOTE]
>
>Den här datatypen är avsedd att användas för att anpassa strukturen för din organisations medgivandescheman med fältgruppen [[!UICONTROL Privacy/Personalization/Marketing Preferences (Consents)]](../field-groups/profile/consents.md) som baslinje.
>
>Om du inte behöver en `subscriptions`-karta för ett visst marknadsföringsinställningsfält kan du använda datatypen [för grundläggande marknadsföringsfält](./marketing-field.md) i stället.

![](../images/data-types/marketing-field-subscriptions.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `reason` | Sträng | När en kund väljer bort från ett marknadsföringsärende representerar det här strängfältet anledningen till varför kunden valde bort. |
| `subscriptions` | Mappa | En karta över kundernas marknadsföringsönskemål för specifika prenumerationer. Mer information finns i avsnittet [prenumerationer](#subscriptions). |
| `time` | DateTime | En ISO 8601-tidsstämpel för när marknadsföringsinställningen ändrades, om tillämpligt. |
| `val` | Sträng | Kundens val av preferens för detta marknadsföringsärende. I [nästa avsnitt](#val) finns godkända värden och definitioner. |

{style=&quot;table-layout:auto&quot;}

## `val` {#val}

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

{style=&quot;table-layout:auto&quot;}

## `subscriptions` {#subscriptions}

Vissa företag tillåter kunder att välja mellan olika prenumerationer som är kopplade till en viss marknadsföringskanal. Ett bankföretag kan t.ex. tillåta kunder att abonnera på telefonaviseringar för överutnyttjade konton eller ta emot försäljningssamtal för erbjudanden om lojalitetsprogram.

Följande JSON representerar ett exempel på ett marknadsföringsfält för en marknadsföringskanal för telefonsamtal som innehåller en `subscriptions`-karta. Varje nyckel i `subscriptions`-objektet representerar en enskild prenumeration för marknadsföringskanalen. Varje prenumeration innehåller i sin tur ett anmälningsvärde (`val`).

```json
"phone-marketing-field": {
  "val": "y",
  "time": "2019-01-01T15:52:25+00:00",
  "subscriptions": {
    "loyalty-offers": {
      "val": "y",
      "type": "sales",
      "subscribers": {
        "123-555-0928": {
          "time": "2019-01-01T15:52:25+00:00",
          "source": "website"
        }
      }
    },
    "overdrawn-account": {
      "val": "y",
      "type": "issues",
      "subscribers": {
        "123-555-0928": {
          "time": "2021-01-01T08:32:53+07:00",
          "source": "website"
        },
        "301-555-1527": {
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
| `type` | Prenumerationstypen. Detta kan vara vilken beskrivande sträng som helst, förutsatt att den är högst 15 tecken. |
| `subscribers` | Ett valfritt mappningsfält som representerar en uppsättning identifierare (t.ex. e-postadresser eller telefonnummer) som har prenumererat på en viss prenumeration. Varje nyckel i det här objektet representerar den aktuella identifieraren och innehåller två underegenskaper: <ul><li>`time`: En ISO 8601-tidsstämpel som anger när identiteten prenumererade, om tillämpligt.</li><li>`source`: Källan som prenumeranten kommer från. Detta kan vara vilken beskrivande sträng som helst, förutsatt att den är högst 15 tecken.</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Ytterligare resurser

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)
