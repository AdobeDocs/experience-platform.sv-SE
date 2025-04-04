---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API;medgivande;samtycke;inställningar;Inställningar;sekretessOptOuts;marketingPreferences;optOutType;baseOfProcessing;medgivande;medgivande
title: Datatypen Innehåll och inställningar
description: Datatypen Godkänn för sekretess, Personalization och marknadsföringsinställningar är avsedd att stödja insamling av kundbehörigheter och preferenser som genereras av CMP (Consent Management Platforms) och andra källor från era dataåtgärder.
exl-id: cdcc7b04-eeb9-40d3-b0b5-f736a5472621
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '2291'
ht-degree: 0%

---

# Datatypen [!UICONTROL Consents and Preferences]

Datatypen [!UICONTROL Consent for Privacy, Personalization and Marketing Preferences] (kallas nedan datatypen [!UICONTROL Consents and Preferences]) är en [!DNL Experience Data Model] (XDM) datatyp som har stöd för insamling av kundbehörigheter och inställningar som genereras av CMP (Consent Management Platforms) och andra källor från dina dataåtgärder.

Det här dokumentet beskriver strukturen och den avsedda användningen av fälten som anges av datatypen [!UICONTROL Consents and Preferences].

## Förhandskrav {#prerequisites}

Det här dokumentet kräver en fungerande förståelse av XDM och användning av scheman i [!DNL Experience Platform]. Läs följande dokumentation innan du fortsätter:

* [Översikt över XDM-systemet](https://www.adobe.com/go/xdm-home-en)
* [Grundläggande om schemakomposition](https://www.adobe.com/go/xdm-schema-best-practices-en)

## Datatypstruktur {#structure}

>[!IMPORTANT]
>
>Datatypen [!UICONTROL Consents and Preferences] är utformad för att omfatta en rad olika användningsfall för samtycke och preferenshantering. Därför beskriver det här dokumentet användningen av datatypens fält i allmänna termer och ger bara förslag på hur du ska tolka användningen av dessa fält. Kontakta ditt juridiska team för sekretess för att anpassa datatypens struktur till hur din organisation tolkar och presenterar dessa samtycke och preferenser för dina kunder.

Datatypen [!UICONTROL Consents and Preferences] innehåller flera fält som används för att hämta information om **medgivande** och **inställning**.

Ett samtycke är ett alternativ som gör att kunden kan ange hur deras data får användas. De flesta samtycke har en juridisk aspekt, eftersom vissa jurisdiktioner kräver tillstånd innan data kan användas på ett visst sätt, eller kräver att kunden har möjlighet att stoppa användningen (avanmäl dig) om det inte krävs ett godkännande.

En preferens är ett alternativ som gör det möjligt för kunden att specificera hur olika aspekter av upplevelsen av ett varumärke ska hanteras. De kan delas in i två kategorier:

* **Personalization-inställningar**: Inställningar för hur varumärket ska personalisera upplevelser som levereras till en kund.
* **Marknadsföringsinställningar**: Inställningar för om ett varumärke får kontakta en kund via olika kanaler eller inte.

I följande skärmbild visas hur datatypens struktur visas i användargränssnittet i Experience Platform:

![](../images/data-types/consents.png)

>[!TIP]
>
>I guiden om [att utforska XDM-resurser](../ui/explore.md) finns anvisningar om hur du söker efter en XDM-resurs och inspekterar dess struktur i Experience Platform användargränssnitt.

I följande JSON visas ett exempel på vilken typ av data som datatypen [!UICONTROL Consents and Preferences] kan bearbeta. Information om hur dessa fält används finns i de avsnitt som följer.

```json
{
  "consents": {
    "collect": {
      "val": "VI",
    },
    "adID": {
      "idType": "IDFA",
      "val": "y"
    },
    "share": {
      "val": "y",
    },
    "personalize": {
      "content": {
        "val": "y"
      }
    },
    "marketing": {
      "preferred": "email",
      "any": {
        "val": "u"
      },
      "push": {
        "val": "n",
        "reason": "Too Frequent",
        "time": "2019-01-01T15:52:25+00:00"
      }
    },
    "metadata": {
      "time": "2019-01-01T15:52:25+00:00"
    }
  }
}
```

>[!TIP]
>
>Du kan generera exempel på JSON-data för alla XDM-scheman som du definierar i Experience Platform för att visualisera hur kundens samtycke och inställningsdata ska mappas. Mer information finns i följande dokumentation:
>
>* [Generera exempeldata i användargränssnittet](../ui/sample.md)
>* [Generera exempeldata i API](../api/sample-data.md)

## `consents` {#choices}

`consents` innehåller flera fält som beskriver en kunds samtycke och inställningar. Dessa fält beskrivs närmare i underavsnitten nedan.

```json
"consents": {
  "collect": {
    "val": "VI",
  },
  "adID": {
    "idType": "IDFA",
    "val": "y"
  },
  "share": {
    "val": "y",
  },
  "personalize": {
    "content": {
      "val": "y"
    }
  },
  "marketing": {
    "preferred": "email",
    "any": {
      "val": "u"
    },
    "email": {
      "val": "n",
      "reason": "Too Frequent",
      "time": "2019-01-01T15:52:25+00:00"
    }
  }
}
```

### `collect`

`collect` representerar kundens samtycke till att deras data samlas in.

```json
"collect": {
  "val": "y"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `val` | Kunden har gett sitt medgivande för det här användningsärendet. I [bilagan](#choice-values) finns godkända värden och definitioner. |

{style="table-layout:auto"}

### `adID`

`adID` representerar kundens samtycke för om ett annonser-ID kan användas för att länka kunden mellan appar på den här enheten.

```json
"adID": {
  "idType": "IDFA",
  "val": "y"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `idType` | Typen av annons-ID, antingen `IDFA` för Apple-ID för annonsörer eller `GAID` för Google Advertiser-ID, även känt som Android Advertiser-ID (AAID). |
| `val` | Kunden har gett sitt medgivande för det här användningsärendet. I [bilagan](#choice-values) finns godkända värden och definitioner. |

{style="table-layout:auto"}

### `share`

`share` representerar kundens samtycke för huruvida deras data kan delas med (eller säljas till) andra eller tredje part.

```json
"share": {
  "val": "y"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `val` | Kunden har gett sitt medgivande för det här användningsärendet. I [bilagan](#choice-values) finns godkända värden och definitioner. |

{style="table-layout:auto"}

### `personalize` {#personalize}

`personalize` samlar in kundpreferenser om vilka sätt deras data kan användas för personalisering. Kunder kan välja bort specifika användningsfall för personalisering eller välja bort helt från personalisering.

>[!IMPORTANT]
>
>`personalize` omfattar inte användningsfall för marknadsföring. Om en kund till exempel väljer bort personalisering för alla kanaler bör de inte sluta ta emot kommunikation via dessa kanaler. De meddelanden de får ska i stället vara generiska och inte baseras på deras profil.
>
>Om en kund väljer bort direktmarknadsföring för alla kanaler (via `marketing`, vilket förklaras i [nästa avsnitt](#marketing)) bör kunden inte få några meddelanden, även om personalisering är tillåtet.

```json
"personalize": {
  "content": {
    "val": "y",
  }
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `content` | Representerar kundens önskemål om personaliserat innehåll på er webbplats eller i er tillämpning. |
| `val` | Personalisering som kunden har tillhandahållit för det angivna användningsfallet. I de fall där kunden inte behöver uppmanas att ge sitt samtycke, ska värdet i detta fält ange grunden för personaliseringen. I [bilagan](#choice-values) finns godkända värden och definitioner. |

{style="table-layout:auto"}

### `marketing` {#marketing}

`marketing` fångar upp kundpreferenser vad gäller vilka marknadsföringssyften deras data kan användas för. Kunderna kan välja bort specifika fall av marknadsföringsanvändning eller välja bort direkt marknadsföring helt och hållet.

```json
"marketing": {
  "preferred": "email",
  "any": {
    "val": "u"
  },
  "email": {
    "val": "n",
    "reason": "Too Frequent"
  },
  "push": {
    "val": "y"
  },
  "sms": {
    "val": "y"
  }
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `preferred` | Anger kundens föredragna kanal för att ta emot kommunikation. Godkända värden finns i [bilagan](#preferred-values). |
| `any` | Representerar kundens preferenser för direktmarknadsföring som helhet. Medgivandeinställningen som anges i det här fältet betraktas som standardinställningen för alla marknadsföringskanaler, såvida den inte åsidosätts av ytterligare underfält som anges under `marketing`. Om du planerar att använda fler detaljerade alternativ för samtycke rekommenderar vi att du utelämnar det här fältet.<br><br>Om värdet är `n` ska alla mer specifika personaliseringsinställningar ignoreras. Om värdet är `y` ska alla fininniga anpassningsalternativ också behandlas som `y`, såvida de inte uttryckligen är inställda på `n`. Om värdet inte anges bör värdena för varje personaliseringsalternativ respekteras enligt vad som anges. |
| `email` | Anger om kunden går med på att ta emot e-postmeddelanden. |
| `push` | Anger om kunden tillåter att push-meddelanden tas emot. |
| `sms` | Anger om kunden går med på att ta emot textmeddelanden. |
| `val` | Inställningen som tillhandahålls av kunden för det angivna användningsfallet. I de fall där kunden inte behöver uppmanas att ge sitt samtycke, ska värdet i detta fält ange grunden för användningen av marknadsföringen. I [bilagan](#choice-values) finns godkända värden och definitioner. |
| `time` | En ISO 8601-tidsstämpel för när marknadsföringsinställningen ändrades, om tillämpligt. Observera, att om tidsstämpeln för en enskild inställning är densamma som den som anges under `metadata`, kommer det här fältet inte att anges för den inställningen. |
| `reason` | När en kund väljer bort från ett marknadsföringsärende representerar det här strängfältet anledningen till varför kunden valde bort. |

{style="table-layout:auto"}

### `metadata`

`metadata` samlar in allmänna metadata om kundens samtycke och inställningar när de senast uppdaterades.

```json
"metadata": {
  "time": "2019-01-01T15:52:25+00:00",
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `time` | En ISO 8601-tidsstämpel för senaste gången som något av kundens samtycke och inställningar uppdaterades. Det här fältet kan användas i stället för att tidsstämplar tillämpas på enskilda inställningar för att minska inläsningen och komplexiteten. Om du anger ett `time`-värde under en enskild inställning åsidosätts tidsstämpeln `metadata` för den aktuella inställningen. |

{style="table-layout:auto"}

## Inhämta data med datatypen {#ingest}

Om du vill använda datatypen [!UICONTROL Consents and Preferences] för att importera medgivandedata från dina kunder måste du skapa en datauppsättning som baseras på ett schema som innehåller den datatypen.

I självstudiekursen [Skapa ett schema i användargränssnittet](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) finns anvisningar om hur du tilldelar datatyper till fält. När du har skapat ett schema som innehåller ett fält med datatypen [!UICONTROL Consents and Preferences] kan du läsa avsnittet om att [skapa en datamängd](../../catalog/datasets/user-guide.md#create) i användarhandboken för datauppsättningen och följa stegen för att skapa en datamängd med ett befintligt schema.

>[!IMPORTANT]
>
>Om du vill skicka medgivandedata till [!DNL Real-Time Customer Profile] måste du skapa ett [!DNL Profile]-aktiverat schema baserat på klassen [!DNL XDM Individual Profile] som innehåller datatypen [!UICONTROL Consents and Preferences]. Den datauppsättning som du skapar baserat på det schemat måste också aktiveras för [!DNL Profile]. Se självstudiekurserna som är länkade ovan för specifika steg som rör [!DNL Real-Time Customer Profile]-krav för scheman och datauppsättningar.
>
>Dessutom måste du se till att dina sammanfogningsprinciper är konfigurerade för att prioritera de datauppsättningar som innehåller de senaste samtycke- och inställningsdata, så att kundprofilerna uppdateras korrekt. Mer information finns i översikten om [sammanfogningsprinciper](../../rtcdp/profile/merge-policies.md).

## Hantera samtycke och ändringar av inställningar

När en kund ändrar sitt samtycke eller sina inställningar på webbplatsen bör dessa ändringar samlas in och tillämpas omedelbart med [Adobe Experience Platform Web SDK](../../web-sdk/commands/setconsent.md). Om en kund väljer bort från datainsamlingen måste all datainsamling omedelbart upphöra. Om en kund väljer bort personalisering bör det inte finnas någon personalisering på nästa sida de besöker.

## Bilaga {#appendix}

Avsnitten nedan innehåller ytterligare referensinformation om datatypen [!UICONTROL Consents and Preferences].

### Godkända värden för `val` {#choice-values}

I följande tabell visas godkända värden för `val`:

| Värde | Titel | Beskrivning |
| --- | --- | --- |
| `y` | Ja (anmälan) | Kunden har valt att ge sitt medgivande eller önskemål. Med andra ord **do** samtycker de till att deras data används, vilket anges i det aktuella medgivandet eller den aktuella preferensen. |
| `n` | Nej (avanmälan) | Kunden har valt bort samtycke eller önskemål. Med andra ord **godkänner de inte** att deras data används enligt det aktuella medgivandet eller den aktuella preferensen. |
| `p` | Väntande verifiering | Systemet har ännu inte fått något slutligt godkännande eller inställningsvärde. Detta används oftast som en del av ett samtycke som kräver tvåstegsverifiering. Om en kund till exempel väljer att ta emot e-postmeddelanden anges det medgivandet till `p` tills de väljer en länk i ett e-postmeddelande för att verifiera att de har angett rätt e-postadress, och då uppdateras medgivandet till `y`.<br><br>Om detta samtycke eller denna inställning inte använder en tvåmängdsverifieringsprocess kan valet `p` i stället användas för att ange att kunden ännu inte har svarat på bekräftelseuppmaningen. Du kan till exempel automatiskt ställa in värdet på `p` på den första sidan på en webbplats innan kunden har svarat på frågan om samtycke. I jurisdiktioner som inte kräver uttryckligt medgivande kan ni också använda det för att ange att kunden inte uttryckligen har avanmält sig (med andra ord antas medgivande).<br><br> Det här värdet kan importeras i [!DNL Profile] med andra mekanismer, till exempel direktuppspelning, men det stöds **inte** för datainsamling eller medgivande från [!DNL Edge Network]. Även om värdet `p` inte kan skickas explicit hanteras händelsekön fortfarande av [[!DNL Web SDK]](../../landing/governance-privacy-security/consent/sdk.md) och händelsen skickas till [!DNL Edge Network] när slutanvändarens samtycke är explicit `in`. |
| `u` | Okänd | Kundens samtycke eller inställningsinformation är okänd. |
| `dy` | Standard för Ja (anmälan) | Kunden har inte lämnat in något medgivande i sig och behandlas som en anmälan (&quot;Ja&quot;) som standard. Med andra ord antas samtycke tills kunden anger något annat.<br><br>Observera att om lagar eller ändringar i företagets sekretesspolicy leder till ändringar i standardvärdena för vissa eller alla användare, måste du uppdatera alla profiler som innehåller standardvärden manuellt. |
| `dn` | Standard för Nej (avanmälan) | Kunden har inte lämnat in något medgivande och behandlas som standard som avanmälan (&quot;Nej&quot;). Med andra ord antas kunden ha vägrat samtycke tills de anger något annat.<br><br>Observera att om lagar eller ändringar i företagets sekretesspolicy leder till ändringar i standardvärdena för vissa eller alla användare, måste du uppdatera alla profiler som innehåller standardvärden manuellt. |
| `LI` | Legitimalt intresse | Det legitima affärsintresset att samla in och behandla dessa uppgifter för det särskilda ändamålet uppväger den potentiella skada som de kan åsamka den enskilda personen. |
| `CT` | Kontrakt | Insamling av uppgifter för det angivna ändamålet krävs för att uppfylla avtalsförpliktelser med den enskilda personen. |
| `CP` | Efterlevnad av en juridisk skyldighet | Insamlingen av uppgifter för det angivna ändamålet krävs för att uppfylla företagets rättsliga skyldigheter. |
| `VI` | Enskilda personers vitala intressen | Insamling av uppgifter för det särskilda ändamålet krävs för att skydda den enskildes vitala intressen. |
| `PI` | Offentligt intresse | Insamling av uppgifter för det angivna ändamålet krävs för att utföra en uppgift i allmänhetens intresse eller vid utövandet av offentlig makt. |

{style="table-layout:auto"}

### Godkända värden för `preferred` {#preferred-values}

Följande tabell visar de godkända värdena för `preferred`. `preferred`-värdena anger kundens föredragna kanal för att ta emot kommunikation som informerar dem om datainsamling, sekretesspolicyer och personaliseringsalternativ.

| Värde | Beskrivning |
| --- | --- |
| `email` | Den här inställningen anger kundens samtycke till att ta emot meddelanden via e-post. |
| `push` | Den här inställningen anger kundens samtycke till att ta emot push-meddelanden. Det här är meddelanden eller aviseringar som skickas direkt till enheten, ofta ett mobilprogram. |
| `inApp` | Den här inställningen anger kundens samtycke till att ta emot meddelanden i appen. Dessa meddelanden levereras inom ett mobil- eller webbprogram och ger information medan användaren är aktiv i appen. |
| `sms` | Den här inställningen anger kundens samtycke till att ta emot meddelanden via SMS (Short Message Service). Det här är textmeddelanden som skickas till mobiltelefonen. |
| `phone` | Den här inställningen anger att kunden samtycker till att ta emot kommunikation via telefonsamtal. |
| `phyMail` | Den här inställningen anger kundens samtycke till att ta emot material via fysisk post. |
| `inVehicle` | Den här inställningen anger att kunden samtycker till att ta emot meddelanden när kunden är i fordonet. Dessa meddelanden kan levereras via fordonsinfogningssystem eller andra kommunikationskanaler i fordonet. |
| `inHome` | Den här inställningen anger kundens samtycke till att ta emot meddelanden hemma. Dessa meddelanden kan levereras via smarta hemenheter eller andra hembaserade kommunikationskanaler. |
| `iot` | Den här inställningen anger att kunden samtycker till att ta emot meddelanden som rör sakernas internet. Dessa meddelanden kan levereras via anslutna enheter och system i deras miljö. |
| `social` | Den här inställningen anger att kunden samtycker till att ta emot kommunikation via plattformar för sociala medier. |
| `other` | Den här inställningen omfattar kanaler som inte passar in i standardkategorier. Det representerar alternativa eller specialiserade kommunikationskanaler som kan vara specifika för ett visst företag eller en viss bransch. |
| `none` | Den här inställningen anger att kunden inte har någon föredragen kommunikationskanal. |
| `unknown` | Den här inställningen innebär att kundens önskade kommunikationskanal inte är känd eller inte har angetts. Detta kan inträffa om kunden inte har lämnat något uttryckligt medgivande eller någon särskild information om önskemål. |

{style="table-layout:auto"}

### Fullständigt [!UICONTROL Consents and Preferences]-schema {#full-schema}

Mer information om det fullständiga schemat för datatypen [!UICONTROL Consents and Preferences] finns i den [officiella XDM-databasen](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-preferences.schema.json).
