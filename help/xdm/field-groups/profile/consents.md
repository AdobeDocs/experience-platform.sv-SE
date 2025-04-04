---
solution: Experience Platform
title: Fältgrupp för innehåll och inställningar
description: Läs mer om schemafältgruppen Innehåll och inställningar.
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 0%

---

# Fältgrupp [!UICONTROL Consents and Preferences]

[!UICONTROL Consents and Preferences] är en standardfältgrupp för [[!DNL XDM Individual Profile] klassen](../../classes/individual-profile.md) som samlar in samtycke och inställningsinformation för en enskild kund.

>[!NOTE]
>
>Eftersom den här fältgruppen bara är kompatibel med [!DNL XDM Individual Profile] kan den inte användas för [!DNL XDM ExperienceEvent]-scheman. Om du vill inkludera samtycke och inställningsdata i Experience Event-schemat lägger du till datatypen [[!UICONTROL Consent for Privacy, Personalization and Marketing Preferences] ](../../data-types/consents.md) i schemat med hjälp av en [anpassad fältgrupp](../../ui/resources/field-groups.md#create) i stället.

## Fältgruppstruktur {#structure}

Fältgruppen [!UICONTROL Consents and Preferences] tillhandahåller ett enskilt fält av objekttyp, `consents`, för att hämta information om samtycke och inställningar. Det här fältet utökar datatypen [[!UICONTROL Consent for Privacy, Personalization and Marketing Preferences], tar bort fältet `adID` och lägger till ett `idSpecific`-mappningsfält.](../../data-types/consents.md)

![](../../images/field-groups/consent.png)

>[!TIP]
>
>I guiden om [att utforska XDM-resurser](../../ui/explore.md) finns anvisningar om hur du söker efter en XDM-resurs och inspekterar dess struktur i Experience Platform användargränssnitt.

I följande JSON visas ett exempel på vilken typ av data som fältgruppen [!UICONTROL Consents and Preferences] kan bearbeta. Mer information om hur du använder de flesta fält som finns i fältgruppen finns i guiden för datatypen [Consents and Preferences](../../data-types/consents.md). Underavsnitten nedan fokuserar på de unika attribut som fältgruppen lägger till i datatypen.

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
>Du kan generera exempel på JSON-data för alla XDM-scheman som du definierar i Experience Platform för att visualisera hur kundens samtycke och inställningsdata ska mappas. Mer information finns i följande dokumentation:
>
>* [Generera exempeldata i användargränssnittet](../../ui/sample.md)
>* [Generera exempeldata i API](../../api/sample-data.md)

### `idSpecific`

`idSpecific` kan användas när ett visst samtycke eller en viss inställning inte gäller för en kund, men är begränsad till en enda enhet eller ett enda ID. En kund kan till exempel välja att inte ta emot e-post till en adress, samtidigt som e-post kan tillåtas på en annan adress.

>[!IMPORTANT]
>
>Medgivande och inställningar på kanalnivå (dvs. de som anges under `consents` utanför `idSpecific`) gäller för alla ID:n i den kanalen. Därför påverkar allt innehåll och alla inställningar på kanalnivå direkt om motsvarande ID- eller enhetsspecifika inställningar uppfylls:
>
>* Om kunden har valt att inte göra det på kanalnivå, ignoreras alla motsvarande samtycke eller inställningar i `idSpecific`.
>* Om godkännande eller inställning på kanalnivå inte har angetts, eller om kunden har valt att göra det, respekteras motsvarande samtycke eller inställningar i `idSpecific`.

Varje nyckel i objektet `idSpecific` representerar ett specifikt ID-namnområde som känns igen av Adobe Experience Platform Identity Service. Du kan definiera egna namnutrymmen för att kategorisera olika identifierare, men vi rekommenderar att du använder ett av de standardnamnutrymmen som ingår i identitetstjänsten för att minska lagringsstorlekarna för kundprofilen i realtid. Mer information om identitetsnamnutrymmen finns i [översikten över identitetsnamnrymden](../../../identity-service/features/namespaces.md) i dokumentationen för identitetstjänsten.

Nycklarna för varje namnområdesobjekt representerar de unika identitetsvärden som kunden har angett inställningar för. Varje identitetsvärde kan innehålla en komplett uppsättning med innehåll och inställningar, formaterade på samma sätt som `consents`.

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
  "ECID": {
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

I `marketing`-objekt som anges i avsnittet `idSpecific` stöds inte fälten `any` och `preferred`. Dessa fält kan bara konfigureras på användarnivå. Dessutom stöder inte marknadsföringsinställningarna `idSpecific` för `email`, `sms` och `push` `subscriptions` fält.

Det finns också ett samtycke som bara kan ges i avsnittet `idSpecific`: `adID`. Detta fält beskrivs i underavsnittet nedan.

#### `adID`

`adID`-medgivandet representerar kundens samtycke för huruvida ett annonser-ID (IDFA eller GAID) kan användas för att länka kunden mellan appar på den här enheten. Det här värdet kan bara konfigureras under identitetsnamnområdet `ECID` i avsnittet `idSpecific` och kan inte anges för andra namnutrymmen eller på användarnivå för den här fältgruppen.

```json
"idSpecific": {
  "ECID": {
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
>
>Du förväntas inte ange det här värdet direkt eftersom Adobe Experience Platform Mobile SDK automatiskt anger det när det är lämpligt.

## Inmatning av data med fältgruppen {#ingest}

Om du vill använda fältgruppen [!UICONTROL Consents and Preferences] för att importera medgivandedata från dina kunder måste du skapa en datauppsättning som baseras på ett schema som innehåller den fältgruppen.

I självstudiekursen [Skapa ett schema i användargränssnittet](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) finns anvisningar om hur du tilldelar fältgrupper till fält. När du har skapat ett schema som innehåller ett fält med fältgruppen [!UICONTROL Consents and Preferences] kan du läsa avsnittet om att [skapa en datauppsättning](../../../catalog/datasets/user-guide.md#create) i användarhandboken för datauppsättningen och följa stegen för att skapa en datauppsättning med ett befintligt schema.

>[!IMPORTANT]
>
>Om du vill skicka medgivandedata till [!DNL Real-Time Customer Profile] måste du skapa ett [!DNL Profile]-aktiverat schema baserat på klassen [!DNL XDM Individual Profile] som innehåller fältgruppen [!UICONTROL Consents and Preferences]. Den datauppsättning som du skapar baserat på det schemat måste också aktiveras för [!DNL Profile]. Se självstudiekurserna som är länkade ovan för specifika steg som rör [!DNL Real-Time Customer Profile]-krav för scheman och datauppsättningar.
>
>Dessutom måste du se till att dina sammanfogningsprinciper är konfigurerade för att prioritera de datauppsättningar som innehåller de senaste samtycke- och inställningsdata, så att kundprofilerna uppdateras korrekt. Mer information finns i översikten om [sammanfogningsprinciper](../../../rtcdp/profile/merge-policies.md).

## Hantera samtycke och ändringar av inställningar

När en kund ändrar sitt samtycke eller sina inställningar på webbplatsen bör dessa ändringar samlas in och tillämpas omedelbart med [Adobe Experience Platform Web SDK](../../../web-sdk/commands/setconsent.md). Om en kund väljer bort från datainsamlingen måste all datainsamling omedelbart upphöra. Om en kund väljer bort personalisering bör det inte finnas någon personalisering på nästa sida som de laddar.

## Nästa steg

Det här dokumentet innehåller strukturen och användningen av fältgruppen [!UICONTROL Consents and Preferences]. Mer information om andra fält som tillhandahålls av fältgruppen finns i dokumentet om datatypen [[!UICONTROL Consent for Privacy, Personalization and Marketing Preferences] ](../../data-types/consents.md).
