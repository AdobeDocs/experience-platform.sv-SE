---
solution: Experience Platform
title: Fältgrupp för innehåll och inställningar
description: Läs mer om schemafältgruppen Innehåll och inställningar.
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 0%

---

# [!UICONTROL Consents and Preferences] fältgrupp

[!UICONTROL Consents and Preferences] är en standardfältgrupp för [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md) som samlar in information om samtycke och preferenser för en enskild kund.

>[!NOTE]
>
>Eftersom fältgruppen bara är kompatibel med [!DNL XDM Individual Profile]kan den inte användas för [!DNL XDM ExperienceEvent] scheman. Om du vill inkludera samtycke och inställningsdata i Experience Event-schemat lägger du till [[!UICONTROL Consent for Privacy, Personalization and Marketing Preferences] datatyp](../../data-types/consents.md) till schemat med hjälp av en [anpassad fältgrupp](../../ui/resources/field-groups.md#create) i stället.

## Fältgruppstruktur {#structure}

The [!UICONTROL Consents and Preferences] fältgruppen innehåller ett enda fält av objekttyp, `consents`, för att få information om samtycke och preferenser. Det här fältet utökar [[!UICONTROL Consent for Privacy, Personalization and Marketing Preferences] datatyp](../../data-types/consents.md), tar bort `adID` fält och lägga till ett `idSpecific` kartfält.

![](../../images/field-groups/consent.png)

>[!TIP]
>
>Se guiden på [utforska XDM-resurser](../../ui/explore.md) om du vill ha steg om hur du söker upp en XDM-resurs och inspekterar dess struktur i plattformens användargränssnitt.

I följande JSON visas ett exempel på den datatyp som [!UICONTROL Consents and Preferences] fältgruppen kan bearbeta. Information om hur du använder de flesta fält som finns i fältgruppen finns i handboken på [Datatypen Innehåll och inställningar](../../data-types/consents.md). Underavsnitten nedan fokuserar på de unika attribut som fältgruppen lägger till i datatypen.

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
>* [Generera exempeldata i API](../../api/sample-data.md)

### `idSpecific`

`idSpecific` kan användas när ett visst samtycke eller en viss preferens inte gäller för en kund, utan är begränsad till en enda enhet eller ett enda ID. En kund kan till exempel välja att inte ta emot e-post till en adress, samtidigt som e-post kan tillåtas på en annan adress.

>[!IMPORTANT]
>
>Samtycken och preferenser på kanalnivå (dvs. de som anges i `consents` utanför `idSpecific`) gäller för alla ID:n i den kanalen. Därför påverkar allt innehåll och alla inställningar på kanalnivå direkt om motsvarande ID- eller enhetsspecifika inställningar uppfylls:
>
>* Om kunden har valt att inte göra det på kanalnivå, finns motsvarande samtycke eller inställningar i `idSpecific` ignoreras.
>* Om samtycke eller inställning på kanalnivå inte har angetts, eller om kunden har valt att göra det, kommer motsvarande samtycke eller inställningar i `idSpecific` är stolta.

Varje tangent i `idSpecific` -objektet representerar ett specifikt ID-namnområde som känns igen av Adobe Experience Platform Identity Service. Du kan definiera egna namnutrymmen för att kategorisera olika identifierare, men vi rekommenderar att du använder ett av de standardnamnutrymmen som ingår i identitetstjänsten för att minska lagringsstorlekarna för kundprofilen i realtid. Mer information om namnutrymmen för identiteter finns i [Översikt över namnutrymmet identity](../../../identity-service/features/namespaces.md) i identitetstjänstens dokumentation.

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

Inom `marketing` objekt som anges i `idSpecific` -avsnittet, `any` och `preferred` fält stöds inte. Dessa fält kan bara konfigureras på användarnivå. Dessutom är `idSpecific` marknadsföringsinställningar för `email`, `sms`och `push` stöder inte `subscriptions` fält.

Det finns också ett samtycke som bara kan ges i `idSpecific` avsnitt: `adID`. Detta fält beskrivs i underavsnittet nedan.

#### `adID`

The `adID` samtycke representerar kundens samtycke för om ett annonser-ID (IDFA eller GAID) kan användas för att länka kunden mellan appar på den här enheten. Det här värdet kan bara konfigureras under `ECID` identity namespace in the `idSpecific` och kan inte anges för andra namnutrymmen eller på användarnivå för den här fältgruppen.

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

För att kunna använda [!UICONTROL Consents and Preferences] fältgrupp för att kunna importera medgivandedata från dina kunder, måste du skapa en datauppsättning baserad på ett schema som innehåller den fältgruppen.

Se självstudiekursen om [skapa ett schema i användargränssnittet](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) för steg om hur du tilldelar fältgrupper till fält. När du har skapat ett schema som innehåller ett fält med [!UICONTROL Consents and Preferences] fältgrupp, se avsnittet om [skapa en datauppsättning](../../../catalog/datasets/user-guide.md#create) i användarhandboken för datauppsättningen följer du stegen för att skapa en datauppsättning med ett befintligt schema.

>[!IMPORTANT]
>
>Om du vill skicka medgivandedata till [!DNL Real-Time Customer Profile]måste du skapa en [!DNL Profile]-aktiverat schema baserat på [!DNL XDM Individual Profile] klassen som innehåller [!UICONTROL Consents and Preferences] fältgrupp. Den datauppsättning som du skapar baserat på det schemat måste också aktiveras för [!DNL Profile]. Se självstudiekurserna som är länkade ovan för specifika steg som rör [!DNL Real-Time Customer Profile] krav för scheman och datauppsättningar.
>
>Dessutom måste du se till att dina sammanfogningsprinciper är konfigurerade för att prioritera de datauppsättningar som innehåller de senaste samtycke- och inställningsdata, så att kundprofilerna uppdateras korrekt. Se översikten på [sammanfogningsprinciper](../../../rtcdp/profile/merge-policies.md) för mer information.

## Hantera samtycke och ändringar av inställningar

När en kund ändrar sitt samtycke eller sina inställningar på webbplatsen bör dessa ändringar samlas in och tillämpas omedelbart med hjälp av [Adobe Experience Platform Web SDK](../../../edge/consent/supporting-consent.md). Om en kund väljer bort från datainsamlingen måste all datainsamling omedelbart upphöra. Om en kund väljer bort personalisering bör det inte finnas någon personalisering på nästa sida de besöker.

## Nästa steg

Detta dokument innehöll strukturen och användningen av [!UICONTROL Consents and Preferences] fältgrupp. Mer information om de andra fälten som finns i fältgruppen finns i dokumentet på [[!UICONTROL Consent for Privacy, Personalization and Marketing Preferences] datatyp](../../data-types/consents.md).
