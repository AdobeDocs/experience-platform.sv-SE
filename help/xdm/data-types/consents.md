---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API;samtycke;samtycke;inställningar;Inställningar;sekretessOptOuts;marketingPreferences;optOutType;baseOfProcessing;medgivande;medgivande
title: Datatypen Innehåll och inställningar
description: Datatypen Privacy/Marketing Preferences (Consent) är avsedd att stödja insamling av kundbehörigheter och preferenser som genereras av CMP (Consent Management Platforms) och andra källor från era dataåtgärder.
topic: guide
translation-type: tm+mt
source-git-commit: 10ccccf72ff7a2fd726066332b9771dff1929af6
workflow-type: tm+mt
source-wordcount: '2040'
ht-degree: 0%

---


# [!DNL Consents & Preferences] datatyp

Datatypen [!DNL Privacy/Marketing Preferences (Consent)] (kallas nedan datatypen [!DNL Consents & Preferences]) är en [!DNL Experience Data Model]-datatyp (XDM) som är avsedd att stödja samlingen av kundbehörigheter och inställningar som genereras av CMP (Consent Management Platforms) och andra källor från dina dataåtgärder.

Det här dokumentet beskriver strukturen och den avsedda användningen av fälten som anges av datatypen [!DNL Consents & Preferences].

## Förutsättningar {#prerequisites}

Det här dokumentet kräver en fungerande förståelse av XDM och användning av scheman i [!DNL Experience Platform]. Läs följande dokumentation innan du fortsätter:

* [XDM - systemöversikt](http://www.adobe.com/go/xdm-home-en)
* [Grunderna för schemakomposition](http://www.adobe.com/go/xdm-schema-best-practices-en)

## Datatypstruktur {#structure}

>[!IMPORTANT]
>
>Datatypen [!DNL Consents & Preferences] är utformad för att omfatta en rad olika användningsfall för samtycke och preferenshantering. Därför beskriver det här dokumentet användningen av datatypens fält i allmänna termer och ger bara förslag på hur du ska tolka användningen av dessa fält. Kontakta ditt juridiska team för sekretess för att anpassa datatypens struktur till hur din organisation tolkar och presenterar dessa samtycke och preferenser för dina kunder.

Datatypen [!DNL Consents & Preferences] innehåller flera fält som används för att hämta **information om samtycke** och **inställning**.

Ett samtycke är ett alternativ som gör att kunden kan ange hur deras data får användas. De flesta samtycke har en juridisk aspekt, eftersom vissa jurisdiktioner kräver tillstånd innan data kan användas på ett visst sätt, eller kräver att kunden har möjlighet att stoppa användningen (avanmäl dig) om det inte krävs ett ja-medgivande.

En preferens är ett alternativ som gör det möjligt för kunden att specificera hur olika aspekter av upplevelsen av ett varumärke ska hanteras. Dessa infaller inom två kategorier:

* **Anpassningsinställningar**: Inställningar för hur varumärket ska personalisera upplevelser som levereras till en kund.
* **Marknadsföringsinställningar**: Inställningar för om ett varumärke får kontakta en kund via olika kanaler.

I följande JSON visas ett exempel på den datatyp som kan bearbetas av datatypen [!DNL Consents & Preferences]. Information om hur dessa fält används finns i de avsnitt som följer.

```json
{
  "xdm:consents": {
    "xdm:collect": {
      "xdm:val": "y",
    },
    "xdm:adID": {
      "xdm:val": "VI"
    },
    "xdm:share": {
      "xdm:val": "y",
    },
    "xdm:personalize": {
      "xdm:content": {
        "xdm:val": "y"
      }
    },
    "xdm:marketing": {
      "xdm:preferred": "email",
      "xdm:any": {
        "xdm:val": "u"
      },
      "xdm:push": {
        "xdm:val": "n",
        "xdm:reason": "Too Frequent",
        "xdm:time": "2019-01-01T15:52:25+00:00"
      }
    },
    "xdm:idSpecific": {
      "email": {
        "jdoe@example.com": {
          "xdm:marketing": {
            "xdm:email": {
              "xdm:val": "n"
            }
          }
        }
      }
    }
  },
  "xdm:metadata": {
    "xdm:time": "2019-01-01T15:52:25+00:00"
  }
}
```

>[!NOTE]
>
>Exemplet ovan är avsett att illustrera strukturen för de data som skickas till [!DNL Platform] via datatypen [!DNL Consents & Preferences], för att ge kontext till resten av det här dokumentet som förklarar huvudfälten som datatypen tillhandahåller. Det fullständiga schemat för datatypens struktur finns i [bilagan](#full-schema) för referensändamål.

## xdm:consents {#choices}

`xdm:consents` innehåller flera fält som beskriver en kunds samtycke och önskemål. Dessa fält beskrivs närmare i underavsnitten nedan.

```json
"xdm:consents": {
  "xdm:collect": {
    "xdm:val": "y",
  },
  "xdm:adID": {
    "xdm:val": "VI"
  },
  "xdm:share": {
    "xdm:val": "y",
  },
  "xdm:personalize": {
    "xdm:content": {
      "xdm:val": "y"
    }
  },
  "xdm:marketing": {
    "xdm:preferred": "email",
    "xdm:any": {
      "xdm:val": "u"
    },
    "xdm:email": {
      "xdm:val": "n",
      "xdm:reason": "Too Frequent",
      "xdm:time": "2019-01-01T15:52:25+00:00"
    }
  }
}
```

### xdm:samla

`xdm:collect` representerar kundens samtycke till att deras data samlas in.

```json
"xdm:collect" : {
  "xdm:val": "y"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `xdm:val` | Kunden har gett sitt medgivande för det här användningsärendet. Se [bilagan](#choice-values) för godkända värden och definitioner. |

### xdm:adID

`xdm:adID` representerar kundens samtycke för om ett annonser-ID (IDFA eller GAID) kan användas för att länka kunden mellan appar på den här enheten.

```json
"xdm:adID" : {
  "xdm:val": "y"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `xdm:val` | Kunden har gett sitt medgivande för det här användningsärendet. Se [bilagan](#choice-values) för godkända värden och definitioner. |

### xdm:dela

`xdm:share` representerar kundens samtycke för huruvida deras data kan delas med (eller säljas till) andra eller tredje part.

```json
"xdm:share" : {
  "xdm:val": "y"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `xdm:val` | Kunden har gett sitt medgivande för det här användningsärendet. Se [bilagan](#choice-values) för godkända värden och definitioner. |

### xdm:anpassa {#personalize}

`xdm:personalize` Hämtar kundpreferenser för hur deras data kan användas för personalisering. Kunder kan välja bort specifika användningsfall för personalisering eller välja bort helt från personalisering.

>[!IMPORTANT]
>
>`xdm:personalize` omfattar inte användningsfall för marknadsföring. Om en kund till exempel väljer bort personalisering för alla kanaler bör de inte sluta ta emot kommunikation via dessa kanaler. De meddelanden de får ska i stället vara generiska och inte baseras på deras profil.
>
>Om en kund väljer bort direktmarknadsföring för alla kanaler (via `xdm:marketing`, vilket förklaras i [nästa avsnitt](#marketing)), ska kunden inte få några meddelanden, även om personalisering är tillåtet.

```json
"xdm:personalize": {
  "xdm:content": {
    "xdm:val": "y",
  }
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `xdm:content` | Representerar kundens önskemål om personaliserat innehåll på er webbplats eller i er tillämpning. |
| `xdm:val` | Personalisering som kunden har tillhandahållit för det angivna användningsfallet. I de fall där kunden inte behöver uppmanas att ge sitt samtycke, ska värdet i detta fält ange grunden för personaliseringen. Se [bilagan](#choice-values) för godkända värden och definitioner. |

### xdm:marknadsföring {#marketing}

`xdm:marketing` hämtar in kundpreferenser för vilka marknadsföringssyften deras data kan användas för. Kunderna kan välja bort specifika fall av marknadsföringsanvändning eller välja bort direkt marknadsföring helt och hållet.

```json
"xdm:marketing": {
  "xdm:preferred": "email",
  "xdm:any": {
    "xdm:val": "u"
  },
  "xdm:email": {
    "xdm:val": "n",
    "xdm:reason": "Too Frequent"
  },
  "xdm:push": {
    "xdm:val": "y"
  },
  "xdm:sms": {
    "xdm:val": "y"
  }
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `xdm:preferred` | Anger kundens föredragna kanal för att ta emot kommunikation. Se [bilagan](#preferred-values) för godkända värden. |
| `xdm:any` | Representerar kundens preferenser för direktmarknadsföring som helhet. Medgivandeinställningen i det här fältet anses vara standardinställning för alla marknadsföringskanaler, såvida den inte åsidosätts av ytterligare underfält som anges i `xdm:marketing`. Om du planerar att använda fler detaljerade alternativ för samtycke rekommenderar vi att du utelämnar det här fältet.<br><br>Om värdet är inställt på  `n`ska alla mer specifika personaliseringsinställningar ignoreras. Om värdet är `y` bör alla fininjektivkorniga anpassningsalternativ också behandlas som `y`, såvida de inte uttryckligen är inställda på `n`. Om värdet inte anges bör värdena för varje personaliseringsalternativ respekteras enligt vad som anges. |
| `xdm:email` | Anger om kunden går med på att ta emot e-postmeddelanden. |
| `xdm:push` | Anger om kunden tillåter att push-meddelanden tas emot. |
| `xdm:sms` | Anger om kunden accepterar att ta emot textmeddelanden. |
| `xdm:val` | Inställningen som tillhandahålls av kunden för det angivna användningsfallet. I de fall där kunden inte behöver uppmanas att ge sitt samtycke ska värdet i detta fält ange grunden för användningen av marknadsföringen. Se [bilagan](#choice-values) för godkända värden och definitioner. |
| `xdm:time` | En ISO 8601-tidsstämpel för när marknadsföringsinställningen ändrades, om tillämpligt. Observera att om tidsstämpeln för en enskild inställning är densamma som den som anges under `xdm:metadata`, så behöver det här fältet inte anges för den inställningen. |
| `xdm:reason` | När en kund väljer bort från ett marknadsföringsärende representerar det här strängfältet anledningen till varför kunden valde bort. |

### xdm:idSpecific

`xdm:idSpecific` kan användas när ett visst samtycke eller en viss preferens inte gäller för en kund, utan är begränsad till en enda enhet eller ett enda ID. En kund kan till exempel välja att inte ta emot e-post till en adress, samtidigt som e-post kan tillåtas på en annan adress.

>[!IMPORTANT]
>
>Medgivande och inställningar på kanalnivå (dvs. de som anges under `xdm:consents` utanför `xdm:idSpecific`) gäller för ID:n inom den kanalen. Därför påverkar allt innehåll och alla inställningar på kanalnivå direkt om motsvarande ID- eller enhetsspecifika inställningar uppfylls:
>
>* Om kunden har valt att inte göra det på kanalnivå, ignoreras alla motsvarande samtycke eller inställningar i `xdm:idSpecific`.
>* Om samtycke eller inställning på kanalnivå inte har angetts, eller om kunden har valt att göra det, respekteras motsvarande samtycke eller inställningar i `xdm:idSpecific`.


Varje nyckel i `xdm:idSpecific`-objektet representerar ett specifikt ID-namnområde som känns igen av Adobe Experience Platform Identity Service. Du kan definiera egna namnutrymmen för att kategorisera olika identifierare, men vi rekommenderar att du använder ett av de standardnamnutrymmen som ingår i identitetstjänsten för att minska lagringsstorlekarna för kundprofilen i realtid. Mer information om identitetsnamnutrymmen finns i [översikten över identitetsnamnrymden](../../identity-service/namespaces.md) i dokumentationen för identitetstjänsten.

Nycklarna för varje namnområdesobjekt representerar de unika identitetsvärden som kunden har angett inställningar för. Varje identitetsvärde kan innehålla en komplett uppsättning innehåll och inställningar, formaterade på samma sätt som `xdm:consents`.

```json
"xdm:idSpecific": {
  "email": {
    "jdoe@example.com": {
      "xdm:marketing": {
        "xdm:email": {
          "xdm:val": "n"
        }
      }
    }
  }
}
```

## xdm:metadata

`xdm:metadata` samlar in allmänna metadata om kundens samtycke och inställningar när de senast uppdaterades.

```json
"xdm:metadata": {
  "xdm:time": "2019-01-01T15:52:25+00:00",
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `xdm:time` | En tidsstämpel för senaste gången något av kundens samtycke och önskemål uppdaterades. Det här fältet kan användas i stället för att tidsstämplar tillämpas på enskilda inställningar för att minska inläsningen och komplexiteten. Om du anger ett `xdm:time`-värde under en enskild inställning åsidosätts tidsstämpeln `xdm:metadata` för den aktuella inställningen. |

## Inmatning av data med datatypen {#ingest}

Om du vill använda datatypen [!DNL Consents & Preferences] för att importera medgivandedata från dina kunder måste du skapa en datauppsättning baserad på ett schema som innehåller den datatypen.

I självstudiekursen om att [skapa ett schema i användargränssnittet](http://www.adobe.com/go/xdm-schema-editor-tutorial-en) finns anvisningar om hur du tilldelar datatyper till fält. När du har skapat ett schema som innehåller ett fält med datatypen [!DNL Consents & Preferences] kan du läsa avsnittet [skapa en datauppsättning](../../catalog/datasets/user-guide.md#create) i användarhandboken för datauppsättningen och följa stegen för att skapa en datauppsättning med ett befintligt schema.

>[!IMPORTANT]
>
>Om du vill skicka medgivandedata till [!DNL Real-time Customer Profile] måste du skapa ett [!DNL Profile]-aktiverat schema baserat på klassen [!DNL XDM Individual Profile] som innehåller datatypen [!DNL Consents & Preferences]. Den datauppsättning som du skapar baserat på det schemat måste också aktiveras för [!DNL Profile]. Se självstudiekurserna som är länkade ovan för specifika steg som rör [!DNL Real-time Customer Profile]-krav för scheman och datauppsättningar.
>
>Dessutom måste du se till att dina sammanfogningsprinciper är konfigurerade för att prioritera de datauppsättningar som innehåller de senaste samtycke- och inställningsdata, så att kundprofilerna uppdateras korrekt. Mer information finns i översikten om [sammanfogningsprinciper](../../rtcdp/profile/merge-policies.md).

## Hantera samtycke och ändringar av inställningar

När en kund ändrar sitt samtycke eller sina inställningar på webbplatsen bör dessa ändringar samlas in och tillämpas omedelbart med [Adobe Experience Platform Web SDK](../../edge/consent/supporting-consent.md). Om en kund väljer bort från datainsamlingen måste all datainsamling omedelbart upphöra. Om en kund väljer bort personalisering bör det inte finnas någon personalisering på nästa sida de besöker.

## Bilaga {#appendix}

Avsnitten nedan innehåller ytterligare referensinformation om datatypen [!DNL Consents & Preferences].

### Godkända värden för xdm:val {#choice-values}

I följande tabell visas godkända värden för `xdm:val`:

| Värde | Titel | Beskrivning |
| --- | --- | --- |
| `y` | Ja | Kunden har valt att ge sitt medgivande eller önskemål. De **godkänner med andra ord att deras uppgifter används enligt det aktuella medgivandet eller den aktuella preferensen.** |
| `n` | Nej | Kunden har valt bort samtycke eller önskemål. De **godkänner med andra ord inte** att deras uppgifter används på det sätt som anges i det aktuella medgivandet eller den aktuella preferensen. |
| `p` | Väntande verifiering | Systemet har ännu inte fått något slutligt godkännande eller inställningsvärde. Detta används oftast som en del av ett samtycke som kräver tvåstegsverifiering. Om en kund till exempel väljer att ta emot e-postmeddelanden anges det medgivandet till `p` tills de väljer en länk i ett e-postmeddelande för att verifiera att de har angett rätt e-postadress, och då uppdateras medgivandet till `y`.<br><br>Om detta samtycke eller denna inställning inte använder en tvåstegsverifieringsprocess kan  `p` valet i stället användas för att ange att kunden ännu inte har svarat på bekräftelseuppmaningen. Du kan till exempel automatiskt ange värdet `p` på den första sidan på en webbplats, innan kunden har svarat på frågan om samtycke. I jurisdiktioner som inte kräver uttryckligt medgivande kan ni också använda det för att ange att kunden inte uttryckligen har avanmält sig (med andra ord antas medgivande). |
| `u` | Okänd | Kundens samtycke eller inställningsinformation är okänd. |
| `LI` | Legitimalt intresse | Det legitima affärsintresset att samla in och behandla dessa uppgifter för det särskilda ändamålet uppväger den potentiella skada som de kan åsamka den enskilda personen. |
| `CT` | Kontrakt | Insamling av uppgifter för det angivna ändamålet krävs för att uppfylla avtalsförpliktelser med den enskilda personen. |
| `CP` | Efterlevnad av en juridisk skyldighet | Insamlingen av uppgifter för det angivna ändamålet krävs för att uppfylla företagets rättsliga skyldigheter. |
| `VI` | Enskilda personers vitala intressen | Insamling av uppgifter för det särskilda ändamålet krävs för att skydda den enskildes vitala intressen. |
| `PI` | Offentligt intresse | Insamling av uppgifter för det angivna ändamålet krävs för att utföra en uppgift i allmänhetens intresse eller vid utövandet av offentlig makt. |

### Godkända värden för xdm:preferred {#preferred-values}

I följande tabell visas godkända värden för `xdm:preferred`:

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

### Fullständigt [!DNL Consents & Preferences]-schema {#full-schema}

Mer information om det fullständiga schemat för datatypen [!DNL Consents & Preferences] finns i [den officiella XDM-databasen](https://github.com/adobe/xdm/blob/master/components/datatypes/consent-preferences.schema.json).
