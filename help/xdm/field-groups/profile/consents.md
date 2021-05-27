---
solution: Experience Platform
title: Fältgrupp för sekretess-/personaliserings-/marknadsföringsinställningar (samtycke)
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över schemafältgruppen Sekretess/personalisering/marknadsföring (samtycke).
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '2287'
ht-degree: 0%

---

# [!UICONTROL Privacy/Personalization/Marketing Preferences (Consents)] fältgrupp

[!UICONTROL Privacy/Personalization/Marketing Preferences (Consents)] (nedan kallad  [!DNL Privacy & Consents] fältgruppen) är en standardfältgrupp för  [[!DNL XDM Individual Profile] klassen](../../classes/individual-profile.md), som används för att samla in kundens samtycke och inställningsinformation.

>[!NOTE]
>
>Eftersom den här fältgruppen bara är kompatibel med [!DNL XDM Individual Profile], kan den inte användas för [!DNL XDM ExperienceEvent]-scheman. Om du vill inkludera samtycke- och inställningsdata i Experience Event-schemat lägger du till datatypen [[!UICONTROL Consent for Privacy, Personalization and Marketing Preferences]](../../data-types/consents.md) i schemat genom att använda en [anpassad fältgrupp](../../ui/resources/field-groups.md#create) i stället.

## Fältgruppstruktur {#structure}

>[!IMPORTANT]
>
>Fältgruppen [!DNL Consents & Preferences] är utformad för att omfatta en rad olika användningsfall för samtycke och preferenshantering. Det innebär att det här dokumentet beskriver hur fälten i fältgruppen används i allmänna termer och bara ger förslag på hur du ska tolka användningen av dessa fält. Kontakta ditt juridiska team för sekretess för att anpassa fältgruppens struktur till hur organisationen tolkar och presenterar dessa samtycke och preferenser för dina kunder.

Fältgruppen [!DNL Consents & Preferences] innehåller flera fält som används för att hämta **information om samtycke** och **inställning**.

Ett samtycke är ett alternativ som gör att kunden kan ange hur deras data får användas. De flesta samtycke har en juridisk aspekt, eftersom vissa jurisdiktioner kräver tillstånd innan data kan användas på ett visst sätt, eller kräver att kunden har möjlighet att stoppa användningen (avanmäl dig) om det inte krävs ett ja-medgivande.

En preferens är ett alternativ som gör det möjligt för kunden att specificera hur olika aspekter av upplevelsen av ett varumärke ska hanteras. Dessa infaller inom två kategorier:

* **Anpassningsinställningar**: Inställningar för hur varumärket ska personalisera upplevelser som levereras till en kund.
* **Marknadsföringsinställningar**: Inställningar för om ett varumärke får kontakta en kund via olika kanaler.

I följande skärmbild visas hur fältgruppens struktur visas i användargränssnittet för plattformen:

![](../../images/field-groups/consent.png)

>[!TIP]
>
>Se guiden [utforska XDM-resurser](../../ui/explore.md) för steg om hur du söker efter en XDM-resurs och inspekterar dess struktur i plattformens användargränssnitt.

I följande JSON visas ett exempel på den datatyp som fältgruppen [!DNL Consents & Preferences] kan bearbeta. Information om hur dessa fält används finns i de avsnitt som följer.

```json
{
  "consents": {
    "collect": {
      "val": "VI"
    },
    "share": {
      "val": "y"
    },
    "personalize": {
      "content": {
        "val": "y"
      }
    },
    "marketing": {
      "preferred": "email",
      "any": {
        "val": "y"
      },
      "email": {
        "val": "y"
      }
    },
    "idSpecific": {
      "ECID": {
        "37784337855396895622558625508046772577": {
          "adID": {
            "val": "n",
          },
          "share": {
            "val": "n"
          },
          "marketing": {
            "push": {
              "val": "n",
              "time": "2020-09-30T01:02:33+00:00",
              "reason": "not relevant"
            }
          }
        }
      },
      "email": {
        "john@xyz.com": {
          "marketing": {
            "email": {
              "val": "y"
            }
          }
        }
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
>* [Generera exempeldata i användargränssnittet](../../ui/sample.md)
* [Generera exempeldata i API](../../api/sample-data.md)


## Fältanvändningsfall

De avsedda användningsområdena för vart och ett av dessa fält anges i avsnitten nedan.

### `collect`

`collect` representerar kundens samtycke till att deras data samlas in.

```json
"collect" : {
  "val": "y"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `val` | Kunden har gett sitt medgivande för det här användningsärendet. Se [bilagan](#choice-values) för godkända värden och definitioner. |

{style=&quot;table-layout:auto&quot;}

### `share`

`share` representerar kundens samtycke för huruvida deras data kan delas med (eller säljas till) andra eller tredje part.

```json
"share" : {
  "val": "y"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `val` | Kunden har gett sitt medgivande för det här användningsärendet. Se [bilagan](#choice-values) för godkända värden och definitioner. |

{style=&quot;table-layout:auto&quot;}

### `personalize` {#personalize}

`personalize` Hämtar kundpreferenser för hur deras data kan användas för personalisering. Kunder kan välja bort specifika användningsfall för personalisering eller välja bort helt från personalisering.

>[!IMPORTANT]
`personalize` omfattar inte användningsfall för marknadsföring. Om en kund till exempel väljer bort personalisering för alla kanaler bör de inte sluta ta emot kommunikation via dessa kanaler. De meddelanden de får ska i stället vara generiska och inte baseras på deras profil.
Om en kund väljer bort direktmarknadsföring för alla kanaler (via `marketing`, vilket förklaras i [nästa avsnitt](#marketing)), ska kunden inte få några meddelanden, även om personalisering är tillåtet.

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
| `val` | Personalisering som kunden har tillhandahållit för det angivna användningsfallet. I de fall där kunden inte behöver uppmanas att ge sitt samtycke, ska värdet i detta fält ange grunden för personaliseringen. Se [bilagan](#choice-values) för godkända värden och definitioner. |

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
| `preferred` | Anger kundens föredragna kanal för att ta emot kommunikation. Se [bilagan](#preferred-values) för godkända värden. |
| `any` | Representerar kundens preferenser för direktmarknadsföring som helhet. Medgivandeinställningen i det här fältet anses vara standardinställning för alla marknadsföringskanaler, såvida den inte åsidosätts av ytterligare underfält som anges i `marketing`. Om du planerar att använda fler detaljerade alternativ för samtycke rekommenderar vi att du utelämnar det här fältet.<br><br>Om värdet är inställt på  `n`ska alla mer specifika personaliseringsinställningar ignoreras. Om värdet är `y` bör alla fininjektivkorniga anpassningsalternativ också behandlas som `y`, såvida de inte uttryckligen är inställda på `n`. Om värdet inte anges bör värdena för varje personaliseringsalternativ respekteras enligt vad som anges. |
| `email` | Anger om kunden går med på att ta emot e-postmeddelanden. Kunden kan också ange inställningar för enskilda prenumerationer i den här kanalen. Mer information finns i avsnittet [prenumerationer](#subscriptions) nedan. |
| `push` | Anger om kunden tillåter att push-meddelanden tas emot. Kunden kan också ange inställningar för enskilda prenumerationer i den här kanalen. Mer information finns i avsnittet [prenumerationer](#subscriptions) nedan. |
| `sms` | Anger om kunden accepterar att ta emot textmeddelanden. Kunden kan också ange inställningar för enskilda prenumerationer i den här kanalen. Mer information finns i avsnittet [prenumerationer](#subscriptions) nedan. |
| `val` | Inställningen som tillhandahålls av kunden för det angivna användningsfallet. I de fall där kunden inte behöver uppmanas att ge sitt samtycke ska värdet i detta fält ange grunden för användningen av marknadsföringen. Se [bilagan](#choice-values) för godkända värden och definitioner. |
| `time` | En ISO 8601-tidsstämpel för när marknadsföringsinställningen ändrades, om tillämpligt. Observera att om tidsstämpeln för en enskild inställning är densamma som den som anges under `metadata`, så behöver det här fältet inte anges för den inställningen. |
| `reason` | När en kund väljer bort från ett marknadsföringsärende representerar det här strängfältet anledningen till varför kunden valde bort. |

{style=&quot;table-layout:auto&quot;}

#### `subscriptions` {#subscriptions}

Egenskaperna `email`, `push` och `sms` för `marketing`-objektet kan representera kundprenumerationer för dessa enskilda kanaler. Detta uppnås genom att en `subscriptions`-egenskap läggs till i den aktuella marknadsföringskanalen.

```json
"marketing": {
  "email": {
    "val": "y",
    "subscriptions": {
      "daily-mail": {
        "val": "y",
        "type": "paid",
        "subscribers": {
          "john@xyz.com": {
            "time": "2019-01-01T15:52:25+00:00",
            "source": "website"
          }
        }
      },
      "shipped": {
        "val": "y",

        "subscribers": {
          "john@xyz.com": {
            "time": "2021-01-01T08:32:53+07:00",
            "source": "website"
          },
          "jane@xyz.com": {
            "time": "2020-02-03T07:54:21+07:00",
            "source": "call center",
          }
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

{style=&quot;table-layout:auto&quot;}

### `idSpecific`

`idSpecific` kan användas när ett visst samtycke eller en viss preferens inte gäller för en kund, utan är begränsad till en enda enhet eller ett enda ID. En kund kan till exempel välja att inte ta emot e-post till en adress, samtidigt som e-post kan tillåtas på en annan adress.

>[!IMPORTANT]
Medgivande och inställningar på kanalnivå (dvs. de som anges under `consents` utanför `idSpecific`) gäller för ID:n inom den kanalen. Därför påverkar allt innehåll och alla inställningar på kanalnivå direkt om motsvarande ID- eller enhetsspecifika inställningar uppfylls:
* Om kunden har valt att inte göra det på kanalnivå, ignoreras alla motsvarande samtycke eller inställningar i `idSpecific`.
* Om samtycke eller inställning på kanalnivå inte har angetts, eller om kunden har valt att göra det, respekteras motsvarande samtycke eller inställningar i `idSpecific`.


Varje nyckel i `idSpecific`-objektet representerar ett specifikt ID-namnområde som känns igen av Adobe Experience Platform Identity Service. Du kan definiera egna namnutrymmen för att kategorisera olika identifierare, men vi rekommenderar att du använder ett av de standardnamnutrymmen som ingår i identitetstjänsten för att minska lagringsstorlekarna för kundprofilen i realtid. Mer information om identitetsnamnutrymmen finns i [översikten över identitetsnamnrymden](../../../identity-service/namespaces.md) i dokumentationen för identitetstjänsten.

Nycklarna för varje namnområdesobjekt representerar de unika identitetsvärden som kunden har angett inställningar för. Varje identitetsvärde kan innehålla en komplett uppsättning innehåll och inställningar, formaterade på samma sätt som `consents`.

```json
"idSpecific": {
  "email": {
    "jdoe@example.com": {
      "marketing": {
        "email": {
          "val": "n"
        }
      }
    }
  },
  "ECID" : {
    "37784337855396895622558625508046772577": {
      "collect": {
        "val": "y"
      },
      "adID": {
        "val": "n"
      },
      "marketing": {
        "push": {
          "val": "n"
        }
      }
    }
  }
}
```

I `marketing`-objekt som anges i avsnittet `idSpecific` stöds inte fälten `any` och `preferred`. Dessa fält kan bara konfigureras på användarnivå. Dessutom stöder inte `idSpecific` marknadsföringsinställningarna för `email`, `sms` och `push` `subscriptions` fält.

Det finns också ett samtycke som bara kan ges i `idSpecific`-avsnittet: `adID`. Detta fält beskrivs i underavsnittet nedan.

#### `adID`

`adID`-medgivandet representerar kundens samtycke för huruvida ett annonser-ID (IDFA eller GAID) kan användas för att länka kunden mellan appar på den här enheten. Det här värdet kan bara konfigureras under `ECID`-identitetsnamnområdet i `idSpecific`-avsnittet och kan inte anges för andra namnutrymmen eller på användarnivå för den här fältgruppen.

```json
"idSpecific": {
  "ECID" : {
    "37784337855396895622558625508046772577": {
      "collect": {
        "val": "y"
      },
      "adID": {
        "val": "n"
      },
      "marketing": {
        "push": {
          "val": "n"
        }
      }
    }
  }
}
```

>[!NOTE]
Du förväntas inte ange det här värdet direkt eftersom Adobe Experience Platform Mobile SDK automatiskt anger det när det är lämpligt.

## Inmatning av data med fältgruppen {#ingest}

Om du vill använda fältgruppen [!DNL Consents & Preferences] för att importera medgivandedata från dina kunder måste du skapa en datauppsättning baserad på ett schema som innehåller den fältgruppen.

I självstudiekursen om att [skapa ett schema i användargränssnittet](http://www.adobe.com/go/xdm-schema-editor-tutorial-en) finns anvisningar om hur du tilldelar fältgrupper till fält. När du har skapat ett schema som innehåller ett fält med fältgruppen [!DNL Consents & Preferences], gå till avsnittet [skapa en datauppsättning](../../../catalog/datasets/user-guide.md#create) i användarhandboken för datauppsättningen och följ stegen för att skapa en datauppsättning med ett befintligt schema.

>[!IMPORTANT]
Om du vill skicka medgivandedata till [!DNL Real-time Customer Profile] måste du skapa ett [!DNL Profile]-aktiverat schema baserat på klassen [!DNL XDM Individual Profile] som innehåller fältgruppen [!DNL Consents & Preferences]. Den datauppsättning som du skapar baserat på det schemat måste också aktiveras för [!DNL Profile]. Se självstudiekurserna som är länkade ovan för specifika steg som rör [!DNL Real-time Customer Profile]-krav för scheman och datauppsättningar.
Dessutom måste du se till att dina sammanfogningsprinciper är konfigurerade för att prioritera de datauppsättningar som innehåller de senaste samtycke- och inställningsdata, så att kundprofilerna uppdateras korrekt. Mer information finns i översikten om [sammanfogningsprinciper](../../../rtcdp/profile/merge-policies.md).

## Hantera samtycke och ändringar av inställningar

När en kund ändrar sitt samtycke eller sina inställningar på webbplatsen bör dessa ändringar samlas in och tillämpas omedelbart med [Adobe Experience Platform Web SDK](../../../edge/consent/supporting-consent.md). Om en kund väljer bort från datainsamlingen måste all datainsamling omedelbart upphöra. Om en kund väljer bort personalisering bör det inte finnas någon personalisering på nästa sida de besöker.

## Bilaga {#appendix}

Avsnitten nedan innehåller ytterligare referensinformation om fältgruppen [!DNL Consents & Preferences].

### Godkända värden för `val` {#choice-values}

I följande tabell visas godkända värden för `val`:

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

### Fullständigt [!DNL Consents & Preferences]-schema {#full-schema}

Om du vill visa det fullständiga schemat för fältgruppen [!DNL Consents & Preferences], se [den officiella XDM-databasen](https://github.com/adobe/xdm/blob/master/components/datatypes/consent-preferences.schema.json).
