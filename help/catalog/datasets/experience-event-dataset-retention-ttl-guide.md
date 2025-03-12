---
title: Hantera lagring av Experience Event-datauppsättningar i Data Lake med TTL
description: Lär dig hur du utvärderar, ställer in och hanterar lagring av Experience Event-datauppsättningar i datasjön med hjälp av TTL-konfigurationer (Time-To-Live) med Adobe Experience Platform API:er. Den här guiden förklarar hur TTL-radnivåförfallodatum stöder principer för datalagring, optimerar lagringseffektiviteten och säkerställer effektiv livscykelhantering. Här finns också användningsexempel och metodtips som hjälper dig att effektivt tillämpa TTL.
exl-id: d688d4d0-aa8b-4e93-a74c-f1a1089d2df0
source-git-commit: 3b5fcc3eec6f2c2e749c86a7baf9995fb88b27d6
workflow-type: tm+mt
source-wordcount: '2335'
ht-degree: 0%

---

# Hantera lagring av Experience Event-datauppsättningar i datavjön med hjälp av TTL

Effektiv datahantering är avgörande för optimala prestanda, kostnadskontroll och dataintegritet. Använd Experience Event Data Retention Time-To-Live (TTL) för att framtvinga utgångsdatum på radnivå och automatiskt ta bort föråldrade poster från datauppsättningar i datasjön samtidigt som optimal lagringseffektivitet och datarelevans garanteras.

I den här handboken beskrivs hur du utvärderar, ställer in och hanterar TTL med hjälp av katalogtjänstens API. Du får lära dig när och varför du ska använda TTL, hur du konfigurerar och uppdaterar TTL-värden med API-anrop och bästa praxis för att säkerställa en effektiv implementering.

>[!IMPORTANT]
>
> TTL är utformat för att optimera livscykelhantering och lagringseffektivitet. Det är inte ett verktyg för regelefterlevnad och bör inte förlitas för lagstadgade krav. Efterlevnad kräver ofta bredare strategier för datastyrning.

## Varför använda TTL för datahantering på radnivå

I takt med att datauppsättningarna växer blir effektiv datahantering allt viktigare för att bevara prestanda, hålla kostnaderna i schack och för att hålla data relevanta. TTL-baserade data på radnivå som förfaller automatiserar datarensningen genom att ta bort inaktuella poster utan manuell åtgärd för att optimera lagringen och förbättra systemets effektivitet.

TTL är användbart vid hantering av tidskänsliga data som blir mindre relevanta över tid. Överväg att implementera TTL om du behöver:

- Minska lagringskostnaderna genom att automatiskt ta bort inaktuella poster.
- Förbättra frågeprestanda genom att minimera irrelevanta data.
- Upprätthåll datahygien genom att endast lagra relevant information.
- Optimera datalagringen för att stödja affärsmålen.

>[!NOTE]
>
>Experience Event DataSet Retention gäller händelsedata som lagras i datasjön. Om du hanterar kvarhållning i Real-Time Customer Data Platform bör du överväga att använda [Experience Event Expiration](../../profile/event-expirations.md) och [Pseudonymous Profile Expiration](../../profile/pseudonymous-profiles.md) tillsammans med inställningarna för kvarhållning av datarina.
>
>TTL-konfigurationer hjälper dig att optimera lagring baserat på berättiganden. Data från Profile Store (används i Real-Time CDP) kan anses vara inaktuella och tas bort efter 30 dagar, men samma händelsedata i datasjön kan vara tillgängliga i 12-13 månader (eller längre baserat på tillstånd) för analyser och dataanvändning i Distiller.

### Branschexempel {#industry-example}

Som ett exempel kan vi titta på en direktuppspelningstjänst för video som spårar användarinteraktioner, till exempel videovyer, sökningar och rekommendationer. Även om aktuella engagemangsdata är avgörande för personalisering förlorar äldre aktivitetsloggar (till exempel interaktioner från över ett år sedan) relevansen. Genom att använda radnivåförfallodatum tar Platform automatiskt bort inaktuella loggar och ser till att endast aktuella och meningsfulla data används för analyser och rekommendationer.

## Utvärdera TTL-lämplighet

Innan du tillämpar en kvarhållningsprincip måste du bedöma om datauppsättningen är en bra kandidat för radförfallodatum. Tänk på följande:

- Datarelevans över tid: Tillhandahåller äldre data ett värde eller blir det föråldrat?
- Påverkan på processerna längre fram i kedjan: Kommer borttagning av data att påverka rapportering, analys eller integreringar?
- Lagringskostnad kontra lagringsvärde: Beväger värdet av äldre data kostnaden för att lagra dem?

Om historiska uppgifter är väsentliga för långtidsanalys eller affärstransaktioner är TTL kanske inte rätt metod. Genom att granska dessa faktorer ser du till att TTL-värdet anpassas efter dina datalagringsbehov utan att datatillgängligheten påverkas negativt.

## Planera dina frågor

Innan du använder TTL bör du använda frågor för att analysera datauppsättningens storlek och relevans. Genom att köra riktade frågor kan du avgöra hur mycket data som ska behållas eller tas bort under olika TTL-konfigurationer.

I följande SQL-fråga räknas till exempel antalet poster som har skapats under de senaste 30 dagarna:

```sql
SELECT COUNT(1) FROM [datasetName] WHERE timestamp > date_sub(now(), INTERVAL 30 DAY);
```

Genom att köra liknande frågor för olika tidsintervall kan du validera TTL-inställningarna och se till att de balanserar lagringseffektivitet och datatillgänglighet.

## Kom igång med TTL-hantering

Innan du kan utvärdera, ange och hantera lagring av Experience Event-datauppsättningar med hjälp av API:t för katalogtjänsten måste du förstå hur du formaterar dina begäranden på rätt sätt. Detta innefattar att känna till API-sökvägarna, tillhandahålla nödvändiga huvuden och formatera nyttolaster för begäranden. Information om detta finns i [API:t för att komma igång](../api/getting-started.md) för katalogtjänsten.

>[!NOTE]
>
>Det här dokumentet täcker förfallodatum på radnivå, vilket innebär att enskilda utgångna rader i en datauppsättning tas bort samtidigt som själva datauppsättningen bevaras intakt. Det gäller inte för förfallodatum för datauppsättningar, vilket tar bort hela datauppsättningar och hanteras av en separat funktion. Information om förfallodatum på datauppsättningsnivå finns i [API-dokumentationen för datauppsättningens förfallodatum](../../hygiene/api/dataset-expiration.md).

### Kontrollera aktuella TTL-inställningar

Kontrollera först de aktuella TTL-inställningarna för att börja hantera TTL. Gör en GET-begäran till slutpunkten `/ttl/{datasetId}` om du vill hämta standardinställningarna, maximiinställningarna och minimiinställningarna för TTL för en datauppsättning. Det här steget är nödvändigt eftersom TTL-reglerna kan variera beroende på datamängdstypen.

>[!TIP]
>
>Plattformsgatewayens URL och bassökväg för katalogtjänstens API är: `https://platform.adobe.io/data/foundation/catalog`.

**API-format**

```http
GET /ttl/{DATASET_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{DATASET_ID}` | En systemgenererad sträng som unikt identifierar en datauppsättning. Använd slutpunkten `/datasets` om du vill hitta ett datauppsättnings-ID. I [listan med katalogobjekts-API:t](../api/list-objects.md) finns anvisningar om hur du filtrerar svar för relevanta datauppsättningar. |

**Begäran**

Följande begäran hämtar organisationens TTL-inställningar för en viss datauppsättning.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/ttl/5ba9452f7de80408007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Svar**

Ett lyckat svar returnerar TTL-konfigurationen för datauppsättningen, inklusive standard-, maximum- och minimum-TTL-värden för både `adobe_lakeHouse` och `adobe_unifiedProfile`-lagring.

+++Välj för att visa svaret

```json
{
    "67976f0b4878252ab887ccd9": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "tags": {
            "adobe/pqs/table": [
                "acme_sales_20250127_113331_106"
            ],
            "adobe/siphon/table/format": [
                "delta"
            ]
        },
        "extensions": {
            "adobe_lakeHouse": {  
                "rowExpiration": {
                    "defaultValue": "P12M",
                    "maxValue": "P12M",
                    "minValue": "P30D"
                }
            },
            "adobe_unifiedProfile": {  
                "rowExpiration": {
                    "defaultValue": "P12M",
                    "maxValue": "P12M",
                    "minValue": "P7D"
                }
            }
        },
        "version": "1.0.0",
        "created": 1737977611118,
        "updated": 1737977611118,
        "createdClient": "acme_data_pipeline",
        "createdUser": "john.snow@acmecorp.com",
        "updatedUser": "arya.stark@acmecorp.com",
        "classification": {
            "managedBy": "CUSTOMER"
        }
    }
}
```

+++

| Egenskap | Beskrivning |
|--------------|-------------|
| `defaultValue` | Den TTL-punkt som används som standard om ingen anpassad TTL har angetts. |
| `maxValue` | Den längsta TTL som tillåts för datauppsättningen. Om värdet är null finns det ingen maxgräns. |
| `minValue` | Den kortaste TTL som är tillåten för att säkerställa överensstämmelse med systemprinciper. |

<!-- Q) what is the default Max and Min values and are they system-imposed? -->

### Ange TTL för en datauppsättning {#set-ttl}

>[!IMPORTANT]
>
>Utgångsdatum för rader kan bara tillämpas på händelsedatamängder som använder ett tidsserieschema. Innan du anger TTL måste du kontrollera att datasetens schema utökar `https://ns.adobe.com/xdm/data/time-series` för att se till att API-begäran lyckas. Använd API:t för schemaregister för att hämta schemainformationen och verifiera egenskapen `meta:extends`. Mer information om hur du gör detta finns i [schemaslutdokumentationen](../../xdm/api/schemas.md#lookup).

Om du vill konfigurera lagring av Experience Event-datauppsättningar för din datauppsättning anger du ett nytt TTL-värde genom att göra en PATCH-begäran till `/v2/datasets/{ID}`-slutpunkten.

**API-format**

```http
PATCH /v2/datasets/{DATASET_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{DATASET_ID}` | ID:t för den datauppsättning som du vill uppdatera TTL-värdet för. |

**Begäran**

I exempelbegäran nedan är `ttlValue` inställd på `P3M`. Detta garanterar att poster som är äldre än tre månader tas bort automatiskt. Du kan justera kvarhållningsperioden så att den passar ditt företags behov med värden som `P6M` i sex månader eller `P12M` i ett år.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/catalog/v2/datasets/{DATASET_ID}' \
  -h 'Authorization: Bearer {ACCESS_TOKEN}' \
  -h 'Content-Type: application/json' \
  -h 'x-api-key: {API_KEY}' \
  -h 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
    "extensions": {
        "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P3M"  // A 3 month retention period
            }
        }
    }
}
```

**Svar**

Ett lyckat svar visar TTL-konfigurationen för datauppsättningen. Den innehåller information om förfalloinställningar på radnivå för både `adobe_lakeHouse` och `adobe_unifiedProfile`-lagring.

+++Välj för att visa svaret

```JSON
{
    "67976f0b4878252ab887ccd9": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "tags": {
            "adobe/pqs/table": [
                "acme_sales_20250127_113331_106"
            ],
            "adobe/siphon/table/format": [
                "delta"
            ]
        },
        "extensions": {
            "adobe_lakeHouse": {
                "rowExpiration": {
                "ttlValue": "P3M",
                    "valueStatus": "custom",
                    "setBy": "user",
                    "updated": 1737977766499
                }
            },
            "adobe_unifiedProfile": {  
                "rowExpiration": {
                    "ttlValue": "P3M",
                    "valueStatus": "custom",
                    "setBy": "user",
                    "updated": 1737977766499
                }
            }
        },
        "version": "1.0.0",
        "created": 1737977611118,
        "updated": 1737977611118,
        "createdClient": "acme_data_pipeline",
        "createdUser": "john.snow@acmecorp.com",
        "updatedUser": "arya.stark@acmecorp.com",
        "classification": {
            "managedBy": "CUSTOMER"
        }
    }
}
```

+++

| Egenskap | Beskrivning |
|----------------------------------|-------------|
| `extensions` | En behållare för ytterligare metadata relaterade till datauppsättningen. |
| `extensions.adobe_lakeHouse` | Anger inställningar för lagringsarkitektur, inklusive förfallokonfigurationer på radnivå |
| `rowExpiration` | Objektet innehåller TTL-inställningar som definierar kvarhållningsperioden för datauppsättningen. |
| `rowExpiration.ttlValue` | Definierar längden innan poster i datauppsättningen tas bort automatiskt. Använder periodformatet ISO-8601 (till exempel `P3M` för 3 månader eller `P30D` för en vecka). |
| `rowExpiration.valueStatus` | Strängen anger om TTL-inställningen är ett standardsystemvärde eller ett anpassat värde som angetts av en användare. Möjliga värden är: `default`, `custom`. |
| `rowExpiration.setBy` | Anger vem som senast ändrade TTL-inställningen. Möjliga värden är: `user` (manuellt angivet) eller `service` (automatiskt tilldelat). |
| `rowExpiration.updated` | Tidsstämpeln för den senaste TTL-uppdateringen. Det här värdet anger när TTL-inställningen senast ändrades. |

### Uppdatera TTL {#update-ttl}

Förläng eller förkorta lagringstiden så att den passar dina affärsbehov genom att justera TTL-värdet. Om du till exempel tar hänsyn till den videoströmningsplattform som nämndes tidigare kan plattformen inledningsvis ställa in TTL på tre månader för att säkerställa nya engagemangsdata för personalisering. Om deras analys visar att interaktionsmönster som är äldre än tre månader fortfarande ger värdefulla insikter kan de förlänga TTL-perioden till sex månader för att behålla äldre register för bättre rekommendationsmodeller.

Om du vill ändra ett befintligt TTL-värde använder du metoden `PATCH` på slutpunkten `/v2/datasets/{DATASET_ID}`.

#### API-format

```http
PATCH /v2/datasets/{DATASET_ID}
```

**Begäran**

I följande begäran uppdateras TTL till sex månader (`P6M`), vilket förlänger kvarhållningsperioden för poster innan den automatiska borttagningen.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/catalog/v2/datasets/{DATASET_ID}' \
  -h 'Authorization: Bearer {ACCESS_TOKEN}' \
  -h 'Content-Type: application/json' \
  -h 'x-api-key: {API_KEY}' \
  -h 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
    "extensions": {
        "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P6M"  // Extend to 6 months
            }
        }
    }
}
```

<!-- Q) For Clarity, should this example show both data stores being updated by expanding the example payload above? -->

**Svar**

```JSON
{  "extensions": {
        "adobe_lakeHouse": {
            "rowExpiration": {
              "ttlValue": "P6M",
              "valueStatus": "custom",
              "setBy": "user",
              "updated": "1737977766499"
            }
        },
        "adobe_unifiedProfile": {
            "rowExpiration": {
                "ttlValue": "P3M",
                "valueStatus": "custom",
                "setBy": "user",
                "updated": "17379754766355"
            }
        }
    }
}
```

## Bästa tillvägagångssätt för att ange TTL {#best-practices}

Att välja rätt TTL-värde är avgörande för att säkerställa att er Experience Event-datalagringspolicy balanserar datalagring, lagringseffektivitet och analysbehov. En TTL som är för kort kan orsaka dataförlust, medan en som är för lång kan öka lagringskostnaderna och onödig datainsamling. Se till att TTL-värdet är anpassat efter datauppsättningens syfte genom att fundera på hur ofta data ska användas och hur länge de ska vara relevanta.

Tabellen nedan innehåller vanliga TTL-rekommendationer baserade på datamängdstyp och användningsmönster:

| Typ av datauppsättning | Rekommenderad TTL | Vanliga användningsfall |
|-----------------------------|------------------------|-------------------|
| Datauppsättningar som du använder ofta | 30-90 dagar | Loggar för användarinteraktion, klickströmsdata för webbplatser, data för kampanjresultat på kort sikt. |
| Arkiveringsdatauppsättningar | 1 år eller mer | Loggar över finansiella transaktioner, efterlevnadsdata, långsiktig trendanalys, data för maskininlärningsutbildning. |
| Apphanterade datauppsättningar | Upp till 13 månader | Systemhanterade datauppsättningar har fördefinierade TTL-begränsningar, som tillämpas automatiskt för att följa systemdefinierade begränsningar. |
| Kundhanterade datauppsättningar | 30 dagar - max TTL | Datauppsättningar som har skapats med Distiller, API:er eller Data. TTL-värdet måste vara minst 30 dagar och inom det definierade maximala TTL-värdet. |

Granska TTL-inställningarna regelbundet för att säkerställa att de fortsätter att vara i linje med dina lagringspolicyer, analytiska behov och affärskrav.

### Viktiga överväganden vid inställning av TTL

<!-- What are the default TTL limits for system-generated Profile Store and data lake datasets? -->

<!-- Q) Are the limits: 90 days for data in the Profile store and 13 months for data in the data lake? This is true for Journey Optimizer. -->

Följ dessa metodtips för att se till att TTL-inställningarna är anpassade efter din datalagringsstrategi:

- Granska TTL-ändringar regelbundet. Varje TTL-uppdatering utlöser en granskningshändelse. Använd granskningsloggar för att spåra TTL-ändringar för regelefterlevnad, datastyrning och felsökning.
- Ta bort TTL om data måste behållas oändligt. Om du vill inaktivera TTL anger du `ttlValue` till `null`. Detta förhindrar automatiskt förfallodatum och bevarar alla poster permanent. Tänk på lagringskonsekvenserna innan du gör den här ändringen.

<!-- Q) Are there any specific system constraints or impacts of setting TTL to null? -->

## Begränsningar för TTL {#limitations}

Tänk på följande begränsningar när du använder TTL:

- **Upplev kvarhållande av händelsedatauppsättningar med TTL gäller för radnivåförfallodatum**, inte för borttagning av datauppsättningar. TTL tar bort poster baserat på en definierad kvarhållningsperiod, men tar inte bort hela datauppsättningar. Om du vill ta bort en datauppsättning använder du [slutpunkten för datauppsättningens förfallodatum](../../hygiene/api/dataset-expiration.md) eller tar bort manuellt.
- **TTL kan inte tas bort**, utan bara uppdateras. TTL kan inte tas bort när den har tillämpats, men du kan [ändra kvarhållningsperioden](#update-ttl) om du vill förlänga eller förkorta den. Om du vill behålla data i oändlighet anger du en tillräckligt lång TTL i stället för att försöka ta bort den.
- **TTL är inte ett kompatibilitetsverktyg**. TTL optimerar lagrings- och datalivscykelhanteringen men uppfyller inte de lagstadgade kraven på datalagring. För att uppfylla dessa krav måste ni implementera bredare strategier för datastyrning.

## Vanliga frågor om lagringsprinciper för datauppsättning {#faqs}

I det här avsnittet hittar du svar på vanliga frågor om policyer för datalagring i Adobe Experience Platform.

### Vilka typer av datauppsättningar kan jag tillämpa regler för lagringspolicy på?

+++Svar
Du kan tillämpa bevarandeprinciper på datauppsättningar som skapats med klassen XDM ExperienceEvent. För profiltjänster gäller bevarandeprinciper endast för Experience Event-datamängder som har profilaktiverats.
+++

### Hur snart raderas data från sjödatatjänsterna?

+++Svar
TTL-värden för datauppsättningar utvärderas och bearbetas varje vecka, och alla poster som har gått ut tas bort. En händelse anses ha upphört att gälla om den skapades för mer än 30 dagar sedan (importdatum > 30 dagar) och dess händelsedatum överskrider den definierade kvarhållningsperioden (TTL).
+++

### Hur snart tar datauppsättningsarkiveringsjobbet bort data från profiltjänster?

+++Svar
När en kvarhållningsprincip har angetts tas befintliga händelser i plattformen bort omedelbart om deras händelsetidsstämpel överskrider kvarhållningsperioden (TTL). Nya händelser tas bort när deras tidsstämpel överskrider kvarhållningsperioden.

Om du till exempel tillämpar en 30-dagars förfalloprincip den 15 maj inträffar följande:

- Nya händelser får en 30-dagars förfallotid när de importeras.
- Befintliga händelser med en tidsstämpel som är äldre än 15 april tas omedelbart bort.
- Befintliga händelser med en tidsstämpel efter 15 april förfaller 30 dagar efter tidsstämpeln (till exempel tas en händelse från 18 april bort den 18 maj).
+++

### Kan jag ange olika bevarandepolicyer för datavinje- och profiltjänster?

+++Svar
Ja, du kan ange olika lagringspolicyer för datalinje- och profiltjänster. Lagringsperioden för profilen får dock inte vara kortare än den som angetts för datasjön.
+++

### Hur kan jag kontrollera min aktuella datauppsättningsanvändning?

+++Svar
Du kan kontrollera den senaste datalagringsstorleken för datasjön och profilarkiv som separata mått på [!UICONTROL Dataset]-lagerarbetsytan. Sortera kolumnerna för att identifiera de största datauppsättningarna och verifiera att kvarhållningsprinciper används.

Mer information om användning på sandlådenivå finns i kontrollpanelen för licensanvändning. Mer information finns i [dokumentationen om licensanvändning](../../dashboards/guides/license-usage.md).
+++

### Hur verifierar jag om datalagringsjobbet lyckades?

+++Svar
Du kan verifiera det senaste datalagringsjobbet genom att kontrollera tidsstämpeln i [användargränssnittet för datalagringskonfiguration](./user-guide.md#data-retention-policy) eller på sidan Datalager.

Historiska användningsrapporter för datauppsättningar är inte tillgängliga just nu.
+++

### Kan jag återställa borttagna data?

+++Svar
Nej, när en lagringsprincip används tas alla data som är äldre än kvarhållningsperioden bort permanent och kan inte återställas.
+++

### Vilken är den minsta TTL-gräns jag kan konfigurera för en Data Lake Experience Event-datauppsättning?

+++Svar
Den minsta TTL-värdet för en Data Lake Experience Event-datamängd är 30 dagar. Datasjön fungerar som ett säkerhetskopierings- och återställningssystem vid första intag och bearbetning. Därför måste data finnas kvar i datasjön i minst 30 dagar efter intag innan de kan upphöra att gälla.
+++

### Hur gör jag om jag behöver behålla vissa datavinefält längre än vad min TTL-policy tillåter?

+++Svar
Använd Data Distiller för att bevara specifika fält utanför datamängdens TTL-värde samtidigt som du håller dig inom användningsgränserna. Skapa ett jobb som regelbundet bara skriver de fält som behövs till en härledd datauppsättning. Det här arbetsflödet säkerställer överensstämmelse med en kortare TTL-gräns samtidigt som viktiga data bevaras för utökad användning.

Mer information finns i [Skapa härledda datauppsättningar med SQL-guiden](../../query-service/data-distiller/derived-datasets/create-derived-datasets-with-sql.md).
+++

## Nästa steg {#next-steps}

Nu när du har lärt dig hur du hanterar TTL-inställningar för förfallodatum på radnivå kan du läsa följande dokumentation för att få en bättre förståelse för hur du hanterar TTL:

- Kvarhållningsjobb: Lär dig att schemalägga och automatisera datauppsättningens förfallodatum i plattformsgränssnittet med [gränssnittsguiden för datalivscykler](../../hygiene/ui/dataset-expiration.md), eller kontrollera konfigurationer för kvarhållande av datauppsättningar och verifiera att utgångna poster tas bort.
- [API-slutpunktsguide för förfallodatum för datauppsättning](../../hygiene/api/dataset-expiration.md): Upptäck hur du tar bort hela datauppsättningar i stället för bara rader. Lär dig hur du schemalägger, hanterar och automatiserar utgångsdatum för datauppsättningar med API:t för att säkerställa effektiv datalagring.
- [Översikt över dataanvändningsprinciper](../../data-governance/policies/overview.md): Lär dig hur du anpassar din datalagringsstrategi till bredare efterlevnadskrav och begränsningar för användning av marknadsföringsmaterial.
