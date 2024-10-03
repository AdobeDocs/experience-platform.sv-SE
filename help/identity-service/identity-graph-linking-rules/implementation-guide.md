---
title: Implementeringsguide för regler för länkning av identitetsdiagram
description: Lär dig de rekommenderade stegen som ska följas när du implementerar data med länkningsregler för identitetsdiagram.
badge: Beta
exl-id: 368f4d4e-9757-4739-aaea-3f200973ef5a
source-git-commit: 35ccc39fdfef31ca1f59e2e11f0d3d762e423635
workflow-type: tm+mt
source-wordcount: '1625'
ht-degree: 0%

---

# Implementeringsguide för regler för länkning av identitetsdiagram

>[!AVAILABILITY]
>
>Regler för länkning av identitetsdiagram är för närvarande begränsade. Kontakta ditt Adobe-kontoteam om du vill ha information om hur du kommer åt funktionen i utvecklingssandlådor.

Läs det här dokumentet för att få en stegvis handledning som du kan följa när du implementerar dina data med Adobe Experience Platform Identity Service.

Stegvisa dispositioner:


1. [Kompletta krav för implementering](#prerequisites-for-implementation)
2. [Skapa nödvändiga identitetsnamnutrymmen](#namespace)
3. [Använd verktyget för diagramsimulering för att bekanta dig med algoritmen för identitetsoptimering](#graph-simulation)
4. [Använd identitetsinställningsverktyget för att ange unika namnutrymmen och konfigurera prioritetsklassificeringar för dina namnutrymmen](#identity-settings)
5. [Skapa ett XDM-schema (Experience Data Model)](#schema)
6. [Skapa en datauppsättning](#dataset)
7. [Importera data till Experience Platform](#ingest)

## Krav för implementering {#prerequisites-for-implementation}

I det här avsnittet beskrivs nödvändiga steg som du måste slutföra innan du implementerar länkningsregler för identitetsdiagram till dina data.

### Unikt namnutrymme

#### Krav på namnutrymme för en person {#single-person-namespace-requirement}

Du måste se till att det unika namnutrymmet med den högsta prioriteten alltid finns i alla profiler. Om du gör det kan identitetstjänsten identifiera rätt personidentifierare i ett visst diagram.

+++Markera om du vill visa ett exempel på ett diagram utan ett namnutrymme för en identifierare

Utan ett unikt namnutrymme som representerar dina personidentifierare kan det uppstå ett diagram som länkar till olika personidentifierare till samma ECID. I det här exemplet är både B2BCRM och B2CCRM kopplade till samma ECID samtidigt. I det här diagrammet visas att Tom med sitt B2C-inloggningskonto delade en enhet med sommaren med hjälp av sitt B2B-inloggningskonto. Systemet kommer dock att känna igen att detta är en profil (komprimering av diagram).

![Ett diagramscenario där två personidentifierare är länkade till samma ECID.](../images/graph-examples/multi_namespaces.png)

+++

+++Markera om du vill visa ett exempel på ett diagram med ett namnutrymme för en person-ID

Med ett unikt namnutrymme (i det här fallet ett CRMID i stället för två olika namnutrymmen) kan identitetstjänsten identifiera den personidentifierare som senast var associerad med ECID. I det här exemplet, eftersom det finns ett unikt CRMID, kan identitetstjänsten identifiera ett scenario med delade enheter, där två enheter delar samma enhet.

![Ett delat enhetsgrafscenario där två personidentifierare är länkade till samma ECID, men den äldre länken tas bort.](../images/graph-examples/crmid_only_multi.png)

+++

### Konfiguration av namnområdesprioritet

Om du använder [Adobe Analytics-källkopplingen](../../sources/tutorials/ui/create/adobe-applications/analytics.md) för att importera data måste du ge dina ECID högre prioritet än Adobe Analytics ID (AAID) eftersom identitetstjänsten blockerar AAID. Genom att prioritera ECID kan du instruera kundprofilen i realtid att lagra oautentiserade händelser i ECID i stället för i AID.

### XDM-upplevelsehändelser

Under förimplementeringsprocessen måste du se till att de autentiserade händelser som skickas till Experience Platform alltid innehåller en personidentifierare, till exempel CRMID.

>[!BEGINTABS]

>[!TAB Autentiserade händelser med personidentifierare]

```json
{
  "_id": "test_id",
  "identityMap": {
      "ECID": [
          {
              "id": "62486695051193343923965772747993477018",
              "primary": false
          }
      ],
      "CRMID": [
          {
              "id": "John",
              "primary": true
          }
      ]
  },
  "timestamp": "2024-09-24T15:02:32+00:00",
  "web": {
      "webPageDetails": {
          "URL": "https://business.adobe.com/",
          "name": "Adobe Business"
      }
  }
}
```

>[!TAB Autentiserade händelser utan personidentifierare]


```json
{
    "_id": "test_id",
    "identityMap": {
        "ECID": [
            {
                "id": "62486695051193343923965772747993477018",
                "primary": false
            }
        ]
    },
    "timestamp": "2024-09-24T15:02:32+00:00",
    "web": {
        "webPageDetails": {
            "URL": "https://business.adobe.com/",
            "name": "Adobe Business"
        }
    }
}
```


>[!ENDTABS]

Skicka inte en tom sträng som identitetsvärde när händelser skickas med XDM-upplevelsehändelser. Om identitetsvärdet för namnutrymmet med den högsta namnområdesprioriteten är en tom sträng, ignoreras posten från kundprofilen i realtid. Detta gäller både identityMap och fält som är markerade som en identitet.

+++Välj för att visa ett exempel på en nyttolast med en tom sträng

I följande exempel returneras ett fel eftersom identitetsvärdet för `Phone` skickas som en tom sträng.

```json
    "identityMap": {
        "ECID": [
            {
                "id": "24165048599243194405404369473457348936",
                "primary": false
            }
        ],
        "Phone": [
            {
                "id": "",
                "primary": true
            }
        ]
    }
```

+++

Du måste se till att du har en fullständigt kvalificerad identitet när du skickar händelser med XDM-upplevelsehändelser.

+++Välj för att visa ett exempel på en händelse med en fullständigt kvalificerad identitet

```json
    "identityMap": {
        "ECID": [
            {
                "id": "24165048599243194405404369473457348936",
                "primary": false
            }
        ]
    }
```

+++

## Ange behörigheter {#set-permissions}

Det första steget i implementeringsprocessen för identitetstjänsten är att se till att ditt Experience Platform-konto läggs till i en roll som har de behörigheter som krävs. Administratören kan konfigurera behörigheter för ditt konto genom att gå till behörighetsgränssnittet i Adobe Experience Cloud. Därifrån måste ditt konto läggas till i en roll med följande behörigheter:

* [!UICONTROL View Identity Settings]: använd den här behörigheten för att kunna visa unika namnutrymmen och namnområdesprioritet på ID-namnutrymmets bläddringssida.
* [!UICONTROL Edit Identity Settings]: använd den här behörigheten för att kunna redigera och spara dina identitetsinställningar.

Mer information om behörigheter finns i [behörighetshandboken](../../access-control/abac/ui/permissions.md).

## Skapa dina identitetsnamnutrymmen {#namespace}

Om dina data kräver det måste du först skapa lämpliga namnutrymmen för din organisation. Anvisningar om hur du skapar ett anpassat namnutrymme finns i handboken [Skapa ett anpassat namnutrymme i användargränssnittet](../features/namespaces.md#create-custom-namespaces).

## Använda diagramsimuleringsverktyget {#graph-simulation}

Gå sedan till [diagramsimuleringsverktyget](./graph-simulation.md) på arbetsytan för identitetstjänstens användargränssnitt. Du kan använda verktyget för diagramsimulering för att simulera identitetsdiagram, som har skapats med olika konfigurationer av unika namnutrymmes- och namnområdesprioriteter.

Genom att skapa olika konfigurationer kan du använda verktyget för diagramsimulering för att lära dig och förstå hur identitetsoptimeringsalgoritmen och vissa konfigurationer kan påverka hur diagrammet fungerar.

## Konfigurera identitetsinställningar {#identity-settings}

När du har fått en bättre uppfattning om hur du vill att diagrammet ska fungera går du till [identitetsinställningsverktyget](./identity-settings-ui.md) på arbetsytan för identitetstjänstens gränssnitt.

Använd verktyget för identitetsinställningar för att ange unika namnutrymmen och konfigurera namnutrymmen efter prioritetsordning. När du är klar med att använda inställningarna måste du vänta minst sex timmar innan du kan fortsätta att importera data, eftersom det tar minst sex timmar innan nya inställningar återspeglas i identitetstjänsten.

## Skapa ett XDM-schema {#schema}

När dina unika namnutrymmen och namnområdesprioriteter har fastställts kan du nu fortsätta med den nödvändiga konfigurationen för att kunna importera dina data. Först måste du skapa ett XDM-schema. Beroende på dina data kan du behöva skapa ett schema för både XDM Individual Profile och XDM ExperienceEvent.

Om du vill importera data till kundprofilen i realtid måste du se till att schemat innehåller minst ett fält som har angetts som primär identitet. Genom att ställa in en primär identitet kan du aktivera ett givet schema för profilinmatning.

Instruktioner om hur du skapar ett schema finns i guiden om att [skapa ett XDM-schema i användargränssnittet](../../xdm/tutorials/create-schema-ui.md).

## Skapa en datauppsättning {#dataset}

Skapa sedan en datauppsättning som ger en struktur för de data som du ska importera. En datauppsättning är en lagrings- och hanteringskonstruktion för en datamängd, vanligtvis en tabell, som innehåller ett schema (kolumner) och fält (rader). Datauppsättningar fungerar tillsammans med scheman, och om du vill importera data till kundprofilen i realtid måste datauppsättningen aktiveras för profilinmatning. För att din datauppsättning ska kunna aktiveras för profilen måste den referera till ett schema som är aktiverat för profilinmatning.

Instruktioner om hur du skapar en datauppsättning finns i [användargränssnittsguiden för datauppsättningar](../../catalog/datasets/user-guide.md).

## Infoga era data {#ingest}

Nu bör du ha följande:

* Nödvändiga behörigheter för att komma åt identitetstjänstens funktioner.
* Namnutrymmen för dina data.
* Utformade unika namnutrymmen och konfigurerade prioriteter för dina namnutrymmen.
* Minst ett XDM-schema. (Beroende på dina data och specifika användningsfall kan du behöva skapa både profil- och upplevelsehändelsescheman.)
* En datauppsättning som baseras på ditt schema.

När du har alla objekt som listas ovan kan du börja importera dina data till Experience Platform. Du kan utföra dataöverföring på flera olika sätt. Du kan använda följande tjänster för att skicka data till Experience Platform:

* [Inmatning av gruppbearbetning och direktuppspelning](../../ingestion/home.md)
* [Datainsamling i Experience Platform](../../collection/home.md)
* [Experience Platform Källor](../../sources/home.md)

>[!TIP]
>
>När data har importerats ändras inte nyttolasten för XDM-rådata. Du kan fortfarande se dina primära identitetskonfigurationer i användargränssnittet. Dessa konfigurationer åsidosätts dock av identitetsinställningarna.

Använd alternativet **[!UICONTROL Beta feedback]** på identitetstjänstens arbetsyta för att få feedback.

## Validera dina diagram {#validate}

Använd identitetspanelen för att få insikter om identitetsgrafernas tillstånd, som det övergripande antalet identiteter och trender för antal diagram, antalet identiteter per namnområde och antalet diagram per diagramstorlek. Du kan också använda identitetspanelen för att visa trender för diagram med två eller flera identiteter, ordnade efter namnområde.

Markera ellipserna (`...`) och välj sedan **[!UICONTROL View more]** om du vill ha mer information och om du vill verifiera att det inte finns några komprimerade diagram.

![Identitetspanelen på identitetstjänstens arbetsyta.](../images/implementation/identity_dashboard.png)

Använd det fönster som visas för att visa information om komprimerade diagram. I det här exemplet markeras både e-post och telefon som unika namnutrymmen, så det finns inga komprimerade diagram i sandlådan.

![Popup-fönstret för diagram med flera identiteter.](../images/implementation/graphs.png)

## Bilaga {#appendix}

I det här avsnittet finns mer information som du kan referera till när du implementerar dina identitetsinställningar och unika namnutrymmen.

### Inloggnings-ID-scenariot kraschar {#dangling-loginid-scenario}

I följande diagram simuleras ett &quot;farligt&quot; loginID-scenario. I det här exemplet är två olika loginID bundna till samma ECID. `{loginID: ID_C}` är dock inte länkad till CRMID. Det finns därför inget sätt för identitetstjänsten att upptäcka att dessa två loginID representerar två olika enheter.

>[!BEGINTABS]

>[!TAB Tvetydigt användar-ID]

I det här exemplet lämnas `{loginID: ID_C}` farligt och inte länkat till ett CRMID. Personentiteten som detta användar-ID ska kopplas till är därför tvetydig.

![Ett exempel på ett diagram med ett &quot;farligt&quot; loginID-scenario.](../images/graph-examples/dangling_example.png)

>[!TAB loginID är länkat till ett CRMID]

I det här exemplet är `{loginID: ID_C}` länkad till `{CRMID: Tom}`. Därför kan systemet identifiera att detta användar-ID är kopplat till Tom.

![Inloggnings-ID är länkat till ett CRMID.](../images/graph-examples/id_c_tom.png)

>[!TAB loginID är länkat till ett annat CRMID]

I det här exemplet är `{loginID: ID_C}` länkad till `{CRMID: Summer}`. Därför kan systemet identifiera att detta loginID är kopplat till en annan person, i det här fallet Sommar.

I det här exemplet visas även att Tom och Sommar ska skilja på personer som delar en enhet, vilket representeras av `{ECID: 111}`.

![Inloggnings-ID är länkat till ett annat CRMID.](../images/graph-examples/id_c_summer.png)

>[!ENDTABS]

## Nästa steg

Mer information om regler för länkning av identitetsdiagram finns i följande dokumentation:

* [Översikt över regler för länkning av identitetsdiagram](./overview.md)
* [Identitetsoptimeringsalgoritm](./identity-optimization-algorithm.md)
* [Exempel på diagramkonfigurationer](./example-configurations.md)
* [Felsökning och vanliga frågor](./troubleshooting.md)
* [Namnområdesprioritet](./namespace-priority.md)
* [Gränssnitt för diagramsimulering](./graph-simulation.md)
* [Användargränssnitt för identitetsinställningar](./identity-settings-ui.md)
