---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API;samtycke;samtycke;inställningar;Inställningar;sekretessOptOuts;marketingPreferences;optOutType;baseOfProcessing;medgivande;medgivande
title: Datatypen Innehåll och inställningar
description: Datatypen Godkännande av sekretess, personalisering och marknadsföringsinställningar är avsedd att stödja insamling av kundbehörigheter och preferenser som genereras av CMP (Consent Management Platforms) och andra källor från era dataåtgärder.
topic-legacy: guide
exl-id: cdcc7b04-eeb9-40d3-b0b5-f736a5472621
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2015'
ht-degree: 0%

---

# [!UICONTROL Consents and Preferences] datatyp

The [!UICONTROL Consent for Privacy, Personalization and Marketing Preferences] datatyp (nedan kallad[!UICONTROL Consents and Preferences] datatypen&quot;) är en [!DNL Experience Data Model] (XDM) datatyp som är avsedd att stödja insamling av kundbehörigheter och preferenser som genereras av CMP (Consent Management Platforms) och andra källor från dataåtgärderna.

Detta dokument omfattar strukturen och den avsedda användningen av de fält som tillhandahålls av [!UICONTROL Consents and Preferences] datatyp.

## Förutsättningar {#prerequisites}

Det här dokumentet kräver en fungerande förståelse av XDM och användning av scheman i [!DNL Experience Platform]. Läs följande dokumentation innan du fortsätter:

* [XDM - systemöversikt](https://www.adobe.com/go/xdm-home-en)
* [Grunderna för schemakomposition](https://www.adobe.com/go/xdm-schema-best-practices-en)

## Datatypstruktur {#structure}

>[!IMPORTANT]
>
>The [!UICONTROL Consents and Preferences] datatypen är avsedd att omfatta en rad olika användningsområden för samtycke och preferenshantering. Därför beskriver det här dokumentet användningen av datatypens fält i allmänna termer och ger bara förslag på hur du ska tolka användningen av dessa fält. Kontakta ditt juridiska team för sekretess för att anpassa datatypens struktur till hur din organisation tolkar och presenterar dessa samtycke och preferenser för dina kunder.

The [!UICONTROL Consents and Preferences] datatypen innehåller flera fält som används för att hämta **samtycke** och **inställning** information.

Ett samtycke är ett alternativ som gör att kunden kan ange hur deras data får användas. De flesta samtycke har en juridisk aspekt, eftersom vissa jurisdiktioner kräver tillstånd innan data kan användas på ett visst sätt, eller kräver att kunden har möjlighet att stoppa användningen (avanmäl dig) om det inte krävs ett ja-medgivande.

En preferens är ett alternativ som gör det möjligt för kunden att specificera hur olika aspekter av upplevelsen av ett varumärke ska hanteras. De kan delas in i två kategorier:

* **Personaliseringsinställningar**: Inställningar för hur varumärket ska personalisera upplevelser som levereras till en kund.
* **Marknadsföringsinställningar**: Inställningar för om ett varumärke får kontakta en kund via olika kanaler.

I följande skärmbild visas hur strukturen för datatypen visas i användargränssnittet för plattformen:

![](../images/data-types/consents.png)

>[!TIP]
>
>Se guiden [utforska XDM-resurser](../ui/explore.md) om du vill ha steg om hur du söker upp en XDM-resurs och inspekterar dess struktur i plattformens användargränssnitt.

I följande JSON visas ett exempel på den datatyp som [!UICONTROL Consents and Preferences] kan bearbeta datatypen. Information om hur dessa fält används finns i de avsnitt som följer.

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
>Du kan generera JSON-exempeldata för alla XDM-scheman som du definierar i Experience Platform för att visualisera hur kundens samtycke och inställningsdata ska mappas. Mer information finns i följande dokumentation:
>
>* [Generera exempeldata i användargränssnittet](../ui/sample.md)
>* [Generera exempeldata i API](../api/sample-data.md)


## `consents` {#choices}

`consents` innehåller flera fält som beskriver en kunds samtycke och önskemål. Dessa fält beskrivs närmare i underavsnitten nedan.

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
| `val` | Kunden har gett sitt medgivande för det här användningsärendet. Se [appendix](#choice-values) för godkända värden och definitioner. |

{style=&quot;table-layout:auto&quot;}

### `adID`

`adID` representerar kundens samtycke för huruvida ett annonser-ID kan användas för att länka kunden mellan appar på den här enheten.

```json
"adID": {
  "idType": "IDFA",
  "val": "y"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `idType` | Typ av annons-ID, antingen `IDFA` för Apple ID för annonsörer eller `GAID` för Google Advertiser ID, även känt som Android Advertiser ID (AAID). |
| `val` | Kunden har gett sitt medgivande för det här användningsärendet. Se [appendix](#choice-values) för godkända värden och definitioner. |

{style=&quot;table-layout:auto&quot;}

### `share`

`share` representerar kundens samtycke för huruvida deras data kan delas med (eller säljas till) andra eller tredje part.

```json
"share": {
  "val": "y"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `val` | Kunden har gett sitt medgivande för det här användningsärendet. Se [appendix](#choice-values) för godkända värden och definitioner. |

{style=&quot;table-layout:auto&quot;}

### `personalize` {#personalize}

`personalize` Hämtar kundpreferenser för hur deras data kan användas för personalisering. Kunder kan välja bort specifika användningsfall för personalisering eller välja bort helt från personalisering.

>[!IMPORTANT]
>
>`personalize` omfattar inte användningsfall för marknadsföring. Om en kund till exempel väljer bort personalisering för alla kanaler bör de inte sluta ta emot kommunikation via dessa kanaler. De meddelanden de får ska i stället vara generiska och inte baseras på deras profil.
>
>I samma exempel väljer en kund att inte använda direktmarknadsföring för alla kanaler (via `marketing`, som förklaras i [nästa avsnitt](#marketing)) ska kunden inte få något meddelande, även om personalisering är tillåten.

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
| `val` | Personalisering som kunden har tillhandahållit för det angivna användningsfallet. I de fall där kunden inte behöver uppmanas att ge sitt samtycke, ska värdet i detta fält ange grunden för personaliseringen. Se [appendix](#choice-values) för godkända värden och definitioner. |

{style=&quot;table-layout:auto&quot;}

### `marketing` {#marketing}

`marketing` hämtar in kundpreferenser för vilka marknadsföringssyften deras data kan användas för. Kunderna kan välja bort specifika fall av marknadsföringsanvändning eller välja bort direkt marknadsföring helt och hållet.

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
| `preferred` | Anger kundens föredragna kanal för att ta emot kommunikation. Se [appendix](#preferred-values) för godkända värden. |
| `any` | Representerar kundens preferenser för direktmarknadsföring som helhet. Den medgivandeinställning som anges i detta fält anses vara standardinställning för alla marknadsföringskanaler, såvida den inte åsidosätts av ytterligare delfält som anges i `marketing`. Om du planerar att använda fler detaljerade alternativ för samtycke rekommenderar vi att du utelämnar det här fältet.<br><br>Om värdet är inställt på `n`ska alla mer specifika personaliseringsinställningar ignoreras. Om värdet är inställt på `y`så bör alla fininniga personaliseringsalternativ också behandlas som `y`, såvida inte explicit inställt på `n`. Om värdet inte anges bör värdena för varje personaliseringsalternativ respekteras enligt vad som anges. |
| `email` | Anger om kunden går med på att ta emot e-postmeddelanden. |
| `push` | Anger om kunden tillåter att push-meddelanden tas emot. |
| `sms` | Anger om kunden accepterar att ta emot textmeddelanden. |
| `val` | Inställningen som tillhandahålls av kunden för det angivna användningsfallet. I de fall där kunden inte behöver uppmanas att ge sitt samtycke ska värdet i detta fält ange grunden för användningen av marknadsföringen. Se [appendix](#choice-values) för godkända värden och definitioner. |
| `time` | En ISO 8601-tidsstämpel för när marknadsföringsinställningen ändrades, om tillämpligt. Observera att om tidsstämpeln för en enskild inställning är densamma som den som anges under `metadata`, ska det här fältet inte ställas in för den inställningen. |
| `reason` | När en kund väljer bort från ett marknadsföringsärende representerar det här strängfältet anledningen till varför kunden valde bort. |

{style=&quot;table-layout:auto&quot;}

### `metadata`

`metadata` samlar in allmänna metadata om kundens samtycke och inställningar när de senast uppdaterades.

```json
"metadata": {
  "time": "2019-01-01T15:52:25+00:00",
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `time` | En ISO 8601-tidsstämpel för senaste gången som något av kundens samtycke och inställningar uppdaterades. Det här fältet kan användas i stället för att tidsstämplar tillämpas på enskilda inställningar för att minska inläsningen och komplexiteten. Tillhandahåller en `time` värdet under en enskild inställning åsidosätter `metadata` tidsstämpel för den aktuella inställningen. |

{style=&quot;table-layout:auto&quot;}

## Inhämta data med datatypen {#ingest}

För att kunna använda [!UICONTROL Consents and Preferences] datatyp för att kunna importera medgivandedata från dina kunder måste du skapa en datauppsättning som baseras på ett schema som innehåller den datatypen.

Se självstudiekursen om [skapa ett schema i användargränssnittet](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) för steg om hur du tilldelar datatyper till fält. När du har skapat ett schema som innehåller ett fält med [!UICONTROL Consents and Preferences] datatypen, se avsnittet om [skapa en datauppsättning](../../catalog/datasets/user-guide.md#create) i användarhandboken för datauppsättningen följer du stegen för att skapa en datauppsättning med ett befintligt schema.

>[!IMPORTANT]
>
>Om du vill skicka medgivandedata till [!DNL Real-Time Customer Profile]måste du skapa en [!DNL Profile]-aktiverat schema baserat på [!DNL XDM Individual Profile] klassen som innehåller [!UICONTROL Consents and Preferences] datatyp. Den datauppsättning som du skapar baserat på det schemat måste också aktiveras för [!DNL Profile]. Se självstudiekurserna som är länkade ovan för specifika steg som rör [!DNL Real-Time Customer Profile] krav för scheman och datauppsättningar.
>
>Dessutom måste du se till att dina sammanfogningsprinciper är konfigurerade för att prioritera de datauppsättningar som innehåller de senaste samtycke- och inställningsdata, så att kundprofilerna uppdateras korrekt. Se översikten på [sammanfogningsprinciper](../../rtcdp/profile/merge-policies.md) för mer information.

## Hantera samtycke och ändringar av inställningar

När en kund ändrar sitt samtycke eller sina inställningar på webbplatsen bör dessa ändringar samlas in och tillämpas omedelbart med hjälp av [Adobe Experience Platform Web SDK](../../edge/consent/supporting-consent.md). Om en kund väljer bort från datainsamlingen måste all datainsamling omedelbart upphöra. Om en kund väljer bort personalisering bör det inte finnas någon personalisering på nästa sida de besöker.

## Bilaga {#appendix}

Avsnitten nedan innehåller ytterligare referensinformation om [!UICONTROL Consents and Preferences] datatyp.

### Godkända värden för `val` {#choice-values}

I följande tabell visas godkända värden för `val`:

| Värde | Titel | Beskrivning |
| --- | --- | --- |
| `y` | Ja (anmälan) | Kunden har valt att ge sitt medgivande eller önskemål. Med andra ord: **do** samtycke till att deras uppgifter används i enlighet med det aktuella medgivandet eller den berörda förmånsbehandlingen. |
| `n` | Nej (avanmäl dig) | Kunden har valt bort samtycke eller önskemål. Med andra ord: **inte** samtycke till att deras uppgifter används i enlighet med det aktuella medgivandet eller den berörda förmånsbehandlingen. |
| `p` | Väntande verifiering | Systemet har ännu inte fått något slutligt godkännande eller inställningsvärde. Detta används oftast som en del av ett samtycke som kräver tvåstegsverifiering. Om en kund till exempel väljer att ta emot e-postmeddelanden ställs detta medgivande in på `p` tills de väljer en länk i ett e-postmeddelande för att verifiera att de har angett rätt e-postadress, och då uppdateras medgivandet till `y`.<br><br>Om detta samtycke eller denna inställning inte använder en tvåstegsverifieringsprocess ska `p` kan i stället användas för att ange att kunden ännu inte har svarat på frågan om samtycke. Du kan till exempel ställa in värdet automatiskt på `p` på första sidan av en webbplats, innan kunden har svarat på frågan om samtycke. I jurisdiktioner som inte kräver uttryckligt medgivande kan ni också använda det för att ange att kunden inte uttryckligen har avanmält sig (med andra ord antas medgivande). |
| `u` | Okänd | Kundens samtycke eller inställningsinformation är okänd. |
| `dy` | Standard för Ja (anmälan) | Kunden har inte lämnat in något medgivande i sig och behandlas som en anmälan (&quot;Ja&quot;) som standard. Med andra ord antas samtycke tills kunden anger något annat.<br><br>Observera att om lagar eller ändringar i företagets sekretesspolicy leder till ändringar av standardvärdena för vissa eller alla användare, måste du uppdatera alla profiler som innehåller standardvärden manuellt. |
| `dn` | Standard för Nej (avanmälan) | Kunden har inte lämnat in något medgivande och behandlas som standard som avanmälan (&quot;Nej&quot;). Med andra ord antas kunden ha vägrat samtycke tills de anger något annat.<br><br>Observera att om lagar eller ändringar i företagets sekretesspolicy leder till ändringar av standardvärdena för vissa eller alla användare, måste du uppdatera alla profiler som innehåller standardvärden manuellt. |
| `LI` | Legitimalt intresse | Det legitima affärsintresset att samla in och behandla dessa uppgifter för det särskilda ändamålet uppväger den potentiella skada som de kan åsamka den enskilda personen. |
| `CT` | Kontrakt | Insamling av uppgifter för det angivna ändamålet krävs för att uppfylla avtalsförpliktelser med den enskilda personen. |
| `CP` | Efterlevnad av en juridisk skyldighet | Insamlingen av uppgifter för det angivna ändamålet krävs för att uppfylla företagets rättsliga skyldigheter. |
| `VI` | Enskilda personers vitala intressen | Insamling av uppgifter för det särskilda ändamålet krävs för att skydda den enskildes vitala intressen. |
| `PI` | Offentligt intresse | Insamling av uppgifter för det angivna ändamålet krävs för att utföra en uppgift i allmänhetens intresse eller vid utövandet av offentlig makt. |

{style=&quot;table-layout:auto&quot;}

### Godkända värden för `preferred` {#preferred-values}

I följande tabell visas godkända värden för `preferred`:

| Värde | Beskrivning |
| --- | --- |
| `email` | E-postmeddelanden. |
| `push` | Push-meddelanden. |
| `inApp` | Meddelanden i appen. |
| `sms` | SMS-meddelanden. |
| `phone` | Telefonsamtalsinteraktioner. |
| `phyMail` | Fysisk post. |
| `inVehicle` | Meddelanden i fordon. |
| `inHome` | Hemmeddelanden. |
| `iot` | Internet of things (IoT) messages. |
| `social` | Innehåll i sociala medier. |
| `other` | En kanal som inte passar in i en standardkategori. |
| `none` | Ingen föredragen kanal. |
| `unknown` | Den önskade kanalen är okänd. |

{style=&quot;table-layout:auto&quot;}

### Fullständig [!UICONTROL Consents and Preferences] schema {#full-schema}

Så här visar du det fullständiga schemat för [!UICONTROL Consents and Preferences] datatyp, se [officiell XDM-databas](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-preferences.schema.json).
