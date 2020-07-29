---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Översikt över mixning av sekretess
topic: guide
translation-type: tm+mt
source-git-commit: 02014c503dc9d4597e1129cafe3ba86f4abe37e9
workflow-type: tm+mt
source-wordcount: '1778'
ht-degree: 0%

---


# [!DNL Privacy Consent] mixin översikt

Den [!DNL Privacy/Marketing Preferences (Consent)] mixin (nedan kallad&quot;[!DNL Privacy Consent] mixin&quot;) är en [!DNL Experience Data Model] (XDM)-blandning som är avsedd att stödja samlingen av användarbehörigheter och -inställningar som genereras av CMP och andra källor från kunder. Detta dokument omfattar strukturen och den avsedda användningen av de olika fält som anges i blandningen.

## Förutsättningar {#prerequisites}

Det här dokumentet kräver en fungerande förståelse av [!DNL Experience Data Model] (XDM) och användning av scheman i [!DNL Experience Platform]. Läs följande dokumentation innan du fortsätter:

* [XDM - systemöversikt](http://www.adobe.com/go/xdm-home-en)
* [Grunderna för schemakomposition](http://www.adobe.com/go/xdm-schema-best-practices-en)

## Exempel på schema {#schema}

>[!NOTE]
>
>Exemplet nedan är avsett att illustrera strukturen för de data som skickas till [!DNL Platform] via [!DNL Privacy Consent] mixin, för att ge kontext till nästa avsnitt i det här dokumentet som förklarar de viktigaste fälten i mixen. Ett fullständigt exempel på schemats struktur finns i [bilagan](#full-schema) för referens.

I följande JSON visas ett exempel på vilken typ av data som kan bearbetas med [!DNL Privacy Consent] mixin. I nästa avsnitt finns information om hur vart och ett av dessa fält används.

```json
{
  "xdm:privacyOptOuts": [
     {
        "xdm:optOutType": "general_opt_out",
        "xdm:optOutValue": "in",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "legitimate_interest"
     },
     {
        "xdm:optOutType": "device_linking",
        "xdm:optOutValue": "not_provided",
        "xdm:basisOfProcessing": "vital_interest"
     },
     {
        "xdm:optOutType": "anonymous_analysis",
        "xdm:optOutValue": "out"
     }
  ],
  "xdm:personalizationPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "consent"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in"
        },
        {
           "xdm:type": "push_notifications",
           "xdm:choice": "out",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00"
        }
     ]
  },
  "xdm:marketingPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in",
           "xdm:subscriptions": {
              "weekly_mailer": {
                 "xdm:choice": "out",
                 "xdm:timestamp": "2019-02-03T15:52:25+00:00"
              },
              "daily_newsletter": {
                 "xdm:choice": "pending"
              }
           }
        },
        {
           "xdm:type": "iot",
           "xdm:choice": "out",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:subscriptions": {
              "out_of_milk": {
                 "xdm:choice": "in"
              }
           }
        }
     ]
  },
  "xdm:version": "1.0.0",
  "xdm:timestamp": "2019-01-01T15:52:25+00:00",
  "xdm:userLocale": "UK",
  "xdm:localeSource": "ip"
}
```

## Fält {#fields}

Avsnitten nedan beskriver hur vart och ett av de större fälten som finns i [!DNL Privacy Consent] blandningen används och hur delfälten ska struktureras.

### xdm:privacyOptOuts {#privacyOptOuts}

`xdm:privacyOptOuts` är en matris som representerar allmänna inställningar för avanmälan som valts av kunden. Flera objekt kan inkluderas i den här arrayen, där var och en representerar en specifik avanmälningstyp och de inställningar kunden har valt för den typen.

```json
"xdm:privacyOptOuts": [
     {
        "xdm:optOutType": "general_opt_out",
        "xdm:optOutValue": "in",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "legitimate_interest"
     },
     {
        "xdm:optOutType": "device_linking",
        "xdm:optOutValue": "not_provided",
        "xdm:basisOfProcessing": "vital_interest"
     },
     {
        "xdm:optOutType": "anonymous_analysis",
        "xdm:optOutValue": "out"
     }
  ]
```

| Egenskap | Beskrivning |
| --- | --- |
| `xdm:optOutType` | Typ av avanmälan. I [bilagan](#optOutType-values) finns godkända värden och definitioner. |
| `xdm:optOutValue` | Den valda inställningen som kunden har valt för just den här avanmälningstypen. I [bilagan](#choice-optOutValue-values) finns godkända värden och definitioner. |
| `xdm:timestamp` | En ISO 8601-tidsstämpel för när inställningen för avanmälan ändrades, om tillämpligt. |
| `xdm:basisOfProcessing` | Anger den sekretessrelaterade bas som data ska samlas in och behandlas utifrån. Som standard är det här fältet inställt på `consent`, vilket anger att data endast ska behandlas om användaren har gett sitt samtycke (vilket återspeglas i `xdm:optOutValue`).<br><br>I vissa fall behöver kunderna inte uppmanas att ge sitt samtycke till databehandling. `xdm:basisOfProcessing` i dessa fall måste ingå i avanmälningsobjektet, vilket anger varför en uppmaning om medgivande inte har lämnats. I [bilagan](#basisOfProcessing-values) finns godkända värden och definitioner. |

### xdm:personalizationPreferences {#personalizationPreferences}

`xdm:personalizationPreferences` Hämtar kundpreferenser för hur deras data kan användas för personalisering. Användare kan välja bort specifika användningsfall för personalisering eller välja bort helt från personalisering.

>[!IMPORTANT]
>
>`xdm:personalizationPreferences` omfattar inte användningsfall för marknadsföring. Om en kund t.ex. väljer bort personalisering för e-postmeddelanden får de inte längre e-postmeddelanden. De e-postmeddelanden de får är snarare generiska och baseras inte på deras profil.
>
>Om en kund väljer bort från e-postmarknadsföring (via `xdm:marketingPreferences`, vilket förklaras i [nästa avsnitt](#marketingPreferences)) får kunden inga e-postmeddelanden, även om e-postpersonalisering är tillåten.

```json
"xdm:personalizationPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "consent"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in"
        },
        {
           "xdm:type": "push_notifications",
           "xdm:choice": "out",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00"
        }
     ]
  }
```

| Egenskap | Beskrivning |
| --- | --- |
| `xdm:default` | De data som tillhandahålls i det här objektet representerar kundens preferenser för personalisering som helhet. |
| `xdm:details` | En array med objekt, en för varje specifik personaliseringstyp som kunden har angett inställningar för. |
| `xdm:choice` | Inställningen för kundens medgivande för personalisering i allmänhet, eller en specifik personaliseringstyp, beroende på om den tillhandahålls enligt `xdm:default` eller `xdm:details`. I [bilagan](#choice-optOutValue-values) finns godkända värden och definitioner. |
| `xdm:type` | Objekten i `xdm:details` arrayen måste tillhandahålla det här fältet för att ange det specifika användningsfallet för personalisering som kunden tillhandahåller data för samtycke. I [bilagan](#type-values) finns godkända värden och definitioner. |
| `xdm:timestamp` | En ISO 8601-tidsstämpel för när inställningen för avanmälan ändrades, om tillämpligt. |
| `xdm:basisOfProcessing` | Anger den sekretessrelaterade bas som data ska samlas in och behandlas utifrån. Som standard är det här fältet inställt på `consent`, vilket anger att data endast ska behandlas om användaren har gett sitt samtycke (vilket återspeglas i `xdm:choice`).<br><br>I vissa fall behöver kunderna inte uppmanas att ge sitt samtycke för personalisering. `xdm:basisOfProcessing` i dessa fall måste ingå i avanmälningsobjektet, vilket anger varför en uppmaning om medgivande inte har lämnats. I [bilagan](#basisOfProcessing-values) finns godkända värden och definitioner. |


### xdm:marketingPreferences {#marketingPreferences}

`xdm:marketingPreferences` hämtar in kundpreferenser för vilka marknadsföringssyften deras data kan användas för. Användare kan välja bort specifika fall av användning för marknadsföring eller välja bort direkt marknadsföring helt och hållet.

```json
"xdm:marketingPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in",
           "xdm:subscriptions": {
              "weekly_mailer": {
                 "xdm:choice": "out",
                 "xdm:timestamp": "2019-02-03T15:52:25+00:00"
              },
              "daily_newsletter": {
                 "xdm:choice": "pending"
              }
           }
        },
        {
           "xdm:type": "iot",
           "xdm:choice": "out",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:subscriptions": {
              "out_of_milk": {
                 "xdm:choice": "in"
              }
           }
        }
     ]
  }
```

| Egenskap | Beskrivning |
| --- | --- |
| `xdm:default` | De data som tillhandahålls i det här objektet representerar kundens preferenser för direktmarknadsföring som helhet. |
| `xdm:details` | En array med objekt, ett för varje specifikt marknadsföringsfall som kunden har gjort inställningar för. |
| `xdm:choice` | Fördelen med kundens samtycke för marknadsföring i allmänhet, eller ett specifikt marknadsföringsfall, beroende på om det tillhandahålls enligt `xdm:default` eller `xdm:details`. I [bilagan](#choice-optOutValue-values) finns godkända värden och definitioner. |
| `xdm:subscriptions` | Ett objekt vars nycklar representerar företagsspecifika prenumerationer, t.ex. e-postlistor eller nyhetsbrev. Varje prenumerationsobjekt ska i sin tur innehålla ett `xdm:choice` värde för den aktuella prenumerationen. |
| `xdm:type` | Objekten i `xdm:details` arrayen måste tillhandahålla det här fältet för att ange det specifika användningsfallet för marknadsföring som kunden tillhandahåller data för samtycke. I [bilagan](#type-values) finns godkända värden och definitioner. |
| `xdm:timestamp` | En ISO 8601-tidsstämpel för när inställningen för avanmälan ändrades, om tillämpligt. |
| `xdm:basisOfProcessing` | Anger den sekretessrelaterade bas som data ska samlas in och behandlas utifrån. Som standard är det här fältet inställt på `consent`, vilket anger att data endast ska behandlas om användaren har gett sitt samtycke (vilket återspeglas i `xdm:choice`).<br><br>I vissa fall behöver kunderna inte uppmanas att ge sitt medgivande för direkt marknadsföring. `xdm:basisOfProcessing` i dessa fall måste ingå i avanmälningsobjektet, vilket anger varför en uppmaning om medgivande inte har lämnats. I [bilagan](#basisOfProcessing-values) finns godkända värden och definitioner. |

## Inhämta data om samtycke med hjälp av mixinen {#ingest}

För att kunna använda den [!DNL Privacy Consent] här blandningen för att importera medgivandedata från dina kunder måste du lägga till mixinen i ett nytt eller befintligt schema och skapa en datauppsättning baserad på det schemat.

I självstudiekursen om hur du [skapar ett schema i användargränssnittet](http://www.adobe.com/go/xdm-schema-editor-tutorial-en) finns anvisningar om hur du lägger till blandningar i ett schema. Blandningen[!DNL  Privacy Consent] är kompatibel med scheman som baseras på klasserna [!DNL XDM Individual Profile] eller [!DNL XDM ExperienceEvent].

När du har skapat ett schema som innehåller [!DNL Privacy Consent] mixinen kan du läsa avsnittet om hur du [skapar en datauppsättning](../../catalog/datasets/user-guide.md#create) i användarhandboken för datauppsättningen och följa stegen för att skapa en datauppsättning med ett befintligt schema.

>[!IMPORTANT]
>
>Om du vill skicka medgivandedata till [!DNL Real-time Customer Profile]måste du skapa ett [!DNL Profile]aktiverat schema baserat på den [!DNL XDM Individual Profile] klass som innehåller [!DNL Privacy Consent] mixen. Den datauppsättning som du skapar baserat på det schemat måste också aktiveras för [!DNL Profile]. Se självstudiekurserna ovan för specifika steg som rör [!DNL Real-time Customer Profile] krav.

## Bilaga {#appendix}

I avsnitten nedan finns ytterligare referensinformation om [!DNL Privacy Consent] mixinen.

### Godkända värden för xdm:optOutType {#optOutType-values}

I följande tabell visas de godkända värdena för `xdm:optOutType`:

| Värde | Beskrivning |
| --- | --- |
| `general_opt_out` | Uppgifterna kan inte användas i något syfte. Detta blockerar vanligtvis datainsamling, utom när grunden för behandlingen inte är&quot;samtycke&quot;.<br><br>När du använder den här avanmälningstypen får du följande sammanhangsberoende betydelse `in` och följande `out` värden:<ul><li>`in`: Användaren **har gett sitt samtycke** till att deras data ska användas för allmän behandling.</li><li>`out`: Användaren samtycker **inte** till att deras data används för allmän behandling.</li></ul>Mer information finns i tabellen över [godkända värden för xdm:optOutValue](#choice-optOutValue-values) . |
| `anonymous_analysis` | Data kan inte användas för generiska webbmått som inte kräver någon typ av användar-ID, till exempel det antal gånger en viss sida visades. |
| `device_linking` | Data från en enhet som används av en besökare kan inte kombineras med data från en annan enhet som används av samma besökare. Enheter är länkade med tekniker som ett gemensamt användarnamn eller en e-postadress, ofta via Adobe enhetsgrupp eller ett privat enhetsdiagram. |
| `pseudonymous_analysis` | Data kan inte användas för webbstatistik från Adobe Analytics, som kräver pseudonyma ID:n för att identifiera sökvägar som användare tar via en webbplats (t.ex. en utfallsrapport), för att upprätta sessioner och för attribueringsändamål. |
| `sales_sharing_opt_out` | Data kan inte användas för försäljningssyften eller delas med tredje parter.<br><br>När du använder den här avanmälningstypen får du följande sammanhangsberoende betydelse `in` och följande `out` värden:<ul><li>`in`: Användaren **har gett sitt samtycke** till att deras data ska användas för försäljning och delning.</li><li>`out`: Användaren samtycker **inte** till att deras data används för försäljning och delning.</li></ul>Mer information finns i tabellen över [godkända värden för xdm:optOutValue](#choice-optOutValue-values) . |

### Godkända värden för xdm:baseOfProcessing {#basisOfProcessing-values}

I följande tabell visas de godkända värdena för `xdm:basisOfProcessing`:

| Värde | Beskrivning |
| --- | --- |
| `consent` **(Standard)** | Insamling av uppgifter för det angivna ändamålet är tillåten, eftersom den enskilda personen har gett uttryckligt tillstånd. Det här är standardvärdet för `xdm:basisOfProcessing` om inget annat värde anges. <br><br>**VIKTIGT **: Värdena för`xdm:choice`och`xdm:optOutValue`respekteras bara när`xdm:basisOfProcessing`är inställt på`consent`. Om något av de andra värdena som anges i den här tabellen används för`xdm:basisOfProcessing`i stället, ignoreras personens val av samtycke. |
| `compliance` | Insamlingen av uppgifter för det angivna ändamålet krävs för att uppfylla företagets rättsliga skyldigheter. |
| `contract` | Insamling av uppgifter för det angivna ändamålet krävs för att uppfylla avtalsförpliktelser med den enskilda personen. |
| `legitimate_interest` | Det legitima affärsintresset att samla in och behandla dessa uppgifter för det särskilda ändamålet uppväger den potentiella skada som de kan åsamka den enskilda personen. |
| `public_interest` | Insamling av uppgifter för det angivna ändamålet krävs för att utföra en uppgift i allmänhetens intresse eller vid utövandet av offentlig makt. |
| `vital_interest` | Insamling av uppgifter för det särskilda ändamålet krävs för att skydda den enskildes vitala intressen. |

### Godkända värden för xdm:choice och xdm:optOutValue {#choice-optOutValue-values}

I följande tabell visas godkända värden för `xdm:choice` och `xdm:optOutValue`:

| Värde | Beskrivning |
| --- | --- |
| `pending` | Systemet har ännu inte fått information om kundernas önskemål om samtycke. Kan användas för den första sidan på en webbplats medan samtycke inhämtas. Den kan också användas för att ange att samtycke är&quot;antaget&quot;, i stället för att uttryckligen anges. |
| `in` | Användaren har valt att godkänna. De **samtycker med andra ord** till att deras uppgifter används, vilket anges i den aktuella medgivandepreferensen. |
| `out` | Användaren har avanmält sig från inställningen för samtycke. Med andra ord **samtycker de inte** till att deras uppgifter används på det sätt som anges i den aktuella medgivandepreferensen. |
| `not_applicable` | Den aktuella medgivandepreferensen gäller inte för kunden. |
| `not_provided` | Kunden har inte lämnat någon information om samtyckespreferens. |
| `unknown` | Kundens information om samtyckespreferens är okänd. |

### Godkända värden för xdm:type {#type-values}

I följande tabell visas de godkända värdena för `xdm:type`:

| Värde | Beskrivning |
| --- | --- |
| `ads` | Annonser som kan visas från icke-relaterade webbplatser. |
| `content` | Innehåll som visas på din webbplats. |
| `customer_support` | Data för kundsupport. |
| `email` | E-postmeddelanden. |
| `iot` | Data relaterade till&quot;sakernas internet&quot; (IoT). |
| `in_app_messages` | Meddelanden i appen. |
| `in_home` | Hemmeddelanden. |
| `in_store` | Meddelanden i butiken. |
| `in_vehicle` | Meddelanden i fordon. |
| `offers` | Specialerbjudanden. |
| `phone_calls` | Data relaterade till telefonsamtalsinteraktioner. |
| `push_notifications` | Push-meddelanden. |
| `sms` | SMS-meddelanden. |
| `social_media` | Innehåll i sociala medier. |
| `snail_mail` | Meddelanden som skickas via vanlig post. |
| `third_party_content` | Innehåll eller artiklar som visas på din webbplats och som tillhandahålls av en icke-närstående enhet. |
| `third_party_offers` | Erbjudanden eller annonser som visas på er webbplats annonstjänster från en icke-närstående enhet. |

### Fullständigt [!DNL Privacy Consent] schema {#full-schema}

Följande JSON representerar det fullständiga [!DNL Privacy Consent] schemat så som det visas i schemaregistret:

```json
{
  "meta:license": [
    "Copyright 2019 Adobe Systems Incorporated. All rights reserved.",
    "This work is licensed under a Creative Commons Attribution 4.0 International (CC BY 4.0) license",
    "you may not use this file except in compliance with the License. You may obtain a copy",
    "of the License at https://creativecommons.org/licenses/by/4.0/"
  ],
  "$id": "https://ns.adobe.com/xdm/context/consent-preferences",
  "$schema": "http://json-schema.org/draft-06/schema#",
  "title": "Privacy/Marketing Preferences (Consent)",
  "description": "This schema captures privacy, personalization and marketing preferences (consents).",
  "type": "object",
  "meta:extensible": true,
  "meta:abstract": true,
  "definitions": {
    "consentValue": {
      "type": "string",
      "enum": [
        "not_provided",
        "pending",
        "in",
        "out",
        "unknown",
        "not_applicable"
      ],
      "meta:enum": {
        "not_provided": "Not provided",
        "pending": "Pending verification",
        "in": "Opt-in",
        "out": "Opt-out",
        "unknown": "Unknown",
        "not_applicable": "Not Applicable"
      }
    },
    "basisOfProcessing": {
      "title": "Basis Of Processing",
      "type": "string",
      "description": "Basis of Processing",
      "enum": [
        "consent",
        "legitimate_interest",
        "contract",
        "vital_interest",
        "compliance",
        "public_interest"
      ],
      "meta:enum": {
        "consent": "User Consent",
        "legitimate_interest": "Legitimate Interest",
        "contract": "Contract",
        "vital_interest": "Vital Interest of the Individual",
        "compliance": "Compliance with a Legal Obligation",
        "public_interest": "Public Interest"
      }
    },
    "timestamp": {
      "title": "Preference timestamp",
      "description": "Timestamp of this specific opt out or preference.",
      "type": "string",
      "format": "date-time"
    },
    "consent-preferences": {
      "properties": {
        "xdm:privacyOptOuts": {
          "title": "Privacy Preferences",
          "description": "Encapsulates data privacy preferences.",
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "xdm:optOutType": {
                "title": "Opt-out type",
                "type": "string",
                "description": "The type of user permission.",
                "enum": [
                  "general_opt_out",
                  "sales_sharing_opt_out",
                  "anonymous_analysis",
                  "pseudonymous_analysis",
                  "device_linking"
                ],
                "meta:enum": {
                  "general_opt_out": "General opt-out",
                  "sales_sharing_opt_out": "Sales/sharing opt-out",
                  "anonymous_analysis": "Anonymous Analysis",
                  "pseudonymous_analysis": "Pseudonymous Analysis",
                  "device_linking": "Device Linking"
                }
              },
              "xdm:optOutValue": {
                "title": "Opt Out Value",
                "description": "The value of the specific opt out.",
                "$ref": "#/definitions/consentValue"
              },
              "xdm:basisOfProcessing": {
                "$ref": "#/definitions/basisOfProcessing"
              },
              "xdm:timestamp": {
                "$ref": "#/definitions/timestamp"
              }
            }
          }
        },
        "xdm:personalizationPreferences": {
          "title": "Personalization Preferences",
          "description": "User's Personalization Preferences",
          "type": "object",
          "properties": {
            "xdm:default": {
              "title": "Global Personalization Preferences",
              "description": "User's Default Personalization Preference",
              "type": "object",
              "properties": {
                "xdm:choice": {
                  "title": "Default Personalization Preferences Value",
                  "description": "The default value for personalization",
                  "$ref": "#/definitions/consentValue"
                },
                "xdm:basisOfProcessing": {
                  "$ref": "#/definitions/basisOfProcessing"
                },
                "xdm:timestamp": {
                  "$ref": "#/definitions/timestamp"
                }
              }
            },
            "xdm:details": {
              "title": "Itemized Personalization Preferences",
              "description": "Preferences for specific types of personalization",
              "type": "array",
              "items": {
                "type": "object",
                "properties": {
                  "meta:enum": {
                    "content": "Personalize Content",
                    "in_app": "Personalize In App Messages",
                    "offers": "Personalize Offers",
                    "email": "Personalize eMail",
                    "snail_mail": "Personalize Regular Mail",
                    "phone_calls": "Personalize Phone Calls",
                    "push_notifications": "Personalize Push Notifications",
                    "sms": "Personalize SMS",
                    "customer_support": "Personalize Customer Support",
                    "in_store": "Personalize In Store",
                    "in_vehicle": "Personalize In Vehicle",
                    "in_home": "Personalize In Home",
                    "iot": "Personalize IoT",
                    "social_media": "Personalize Social Media",
                    "third_party_offers": "Personalize Third-party Offers",
                    "third_party_content": "Personalize Third-party Content",
                    "ads": "Personalize My Business's Ads on Other Sites"
                  }
                },
                "xdm:choice": {
                  "title": "Personalization Preference Value",
                  "description": "The value for this specific personalization preference",
                  "$ref": "#/definitions/consentValue"
                },
                "xdm:basisOfProcessing": {
                  "$ref": "#/definitions/basisOfProcessing"
                },
                "xdm:timestamp": {
                  "$ref": "#/definitions/timestamp"
                }
              }
            }
          }
        }
      },
      "xdm:marketingPreferences": {
        "title": "Marketing Preferences",
        "description": "User's Direct Marketing Preferences",
        "type": "object",
        "properties": {
          "xdm:default": {
            "title": "Default Direct Marketing Preference",
            "description": "User's Default Marketing Preference",
            "type": "object",
            "properties": {
              "xdm:choice": {
                "title": "Default Marketing Preferences Value",
                "description": "The default value for direct marketing preferences",
                "$ref": "#/definitions/consentValue"
              },
              "xdm:basisOfProcessing": {
                "$ref": "#/definitions/basisOfProcessing"
              },
              "xdm:timestamp": {
                "$ref": "#/definitions/timestamp"
              }
            }
          },
          "xdm:details": {
            "title": "Itemized Direct Marketing Preferences",
            "description": "Preferences for specific types of direct marketing",
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "xdm:type": {
                  "title": "Marketing Preference",
                  "type": "string",
                  "description": "The specific marketing preference.",
                  "enum": [
                    "email",
                    "push_notifications",
                    "in_app_messages",
                    "sms",
                    "phone_calls",
                    "snail_mail",
                    "in_vehicle_messages",
                    "in_home_messages",
                    "iot",
                    "social_media"
                  ],
                  "meta:enum": {
                    "email": "Receive eMail",
                    "push_notifications": "Receive Push Notifications",
                    "in_app_messages": "Receive In App Messages",
                    "sms": "Receive SMS",
                    "phone_calls": "Receive Phone Calls",
                    "snail_mail": "Receive Regular Mail",
                    "in_vehicle_messages": "Receive In Vehicle Messages",
                    "in_home_messages": "Receive In Home Messages",
                    "iot": "Receive IoT",
                    "social_media": "Receive Social Media Messages"
                  }
                },
                "xdm:choice": {
                  "title": "Marketing Preference Value",
                  "description": "The value for this specific marketing preference",
                  "$ref": "#/definitions/consentValue"
                },
                "xdm:basisOfProcessing": {
                  "$ref": "#/definitions/basisOfProcessing"
                },
                "xdm:timestamp": {
                  "$ref": "#/definitions/timestamp"
                },
                "xdm:subscriptions": {
                  "title": "Company-specific subscriptions",
                  "description": "Company-specific subscriptions, such as mailing lists or newsletters",
                  "type": "object",
                  "meta:xdmType": "map",
                  "additionalProperties": {
                    "xdm:choice": {
                      "title": "Marketing Preference Value",
                      "description": "The value for this specific marketing preference",
                      "$ref": "#/definitions/consentValue"
                    },
                    "xdm:timestamp": {
                      "$ref": "#/definitions/timestamp"
                    }
                  }
                }
              }
            }
          }
        }
      },
      "xdm:timestamp": {
        "title": "Consent Preferences timestamp",
        "description": "Timestamp of the complete set of user consent preferences.",
        "type": "string",
        "format": "date-time"
      },
      "xdm:version": {
        "title": "Preferences Version",
        "description": "Version of the Privacy Preferences Standard",
        "type": "string"
      },
      "xdm:userLocale": {
        "title": "User Locale",
        "description": "User location or jurisdiction that applies to the consents for this user",
        "type": "string"
      },
      "xdm:localeSource": {
        "title": "Locale Source",
        "description": "Method used to determine the user's locale",
        "enum": [
          "ip",
          "gps",
          "user_provided",
          "website_location",
          "inferred",
          "other"
        ],
        "meta:enum": {
          "ip": "IP Address",
          "gps": "Device GPS",
          "user_provided": "User Provided",
          "website_location": "Website eTDL",
          "inferred": "Inferred",
          "other": "Other"
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/common/extensible#/definitions/@context"
    },
    {
      "$ref": "#/definitions/consent-preferences"
    }
  ],
  "meta:status": "experimental"
}
```
