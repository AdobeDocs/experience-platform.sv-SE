---
title: Hantera lagring av Experience Event-datauppsättningar i Data Lake med TTL
description: Lär dig hur du utvärderar, ställer in och hanterar lagring av Experience Event-datauppsättningar i datasjön med hjälp av TTL-konfigurationer (Time-To-Live) med Adobe Experience Platform API:er. Den här guiden förklarar hur TTL-radnivåförfallodatum stöder principer för datalagring, optimerar lagringseffektiviteten och säkerställer effektiv livscykelhantering. Här finns också användningsexempel och metodtips som hjälper dig att effektivt tillämpa TTL.
exl-id: d688d4d0-aa8b-4e93-a74c-f1a1089d2df0
source-git-commit: 13db0477c0f42d0808647937d40c25b47a270894
workflow-type: tm+mt
source-wordcount: '2451'
ht-degree: 0%

---

# Hantera lagring av Experience Event-datauppsättningar i datavjön med hjälp av TTL

Effektiv datahantering är avgörande för optimala prestanda, kostnadskontroll och dataintegritet. Använd Experience Event Data Retention Time-To-Live (TTL) för att framtvinga utgångsdatum på radnivå och automatiskt ta bort föråldrade poster från datauppsättningar i datasjön samtidigt som optimal lagringseffektivitet och datarelevans garanteras.

I den här handboken beskrivs hur du utvärderar, ställer in och hanterar TTL med hjälp av katalogtjänstens API. Du får lära dig när och varför du ska använda TTL, hur du konfigurerar och uppdaterar TTL-värden med API-anrop och bästa praxis för att säkerställa en effektiv implementering.

>[!IMPORTANT]
>
>TTL är utformat för att optimera livscykelhantering och lagringseffektivitet. Det är inte ett verktyg för regelefterlevnad och bör inte förlitas för lagstadgade krav. Efterlevnad kräver ofta bredare strategier för datastyrning.

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

Använd TTL-konfigurationer för att optimera lagring baserat på berättiganden. Data från Profile Store (används i Real-Time CDP) kan anses vara inaktuella och tas bort efter 30 dagar, men samma händelsedata i datasjön kan vara tillgängliga i 12-13 månader (eller längre baserat på tillstånd) för analyser och dataanvändning i Distiller.

>[!TIP]
>
>Berättiganden avser de lagrings- och kvarhållningsbidrag som definieras i Adobe prenumeration och licensavtal.

### Branschexempel {#industry-example}

Som ett exempel kan vi titta på en direktuppspelningstjänst för video som spårar användarinteraktioner, till exempel videovyer, sökningar och rekommendationer. Även om aktuella engagemangsdata är avgörande för personalisering förlorar äldre aktivitetsloggar (till exempel interaktioner från över ett år sedan) relevansen. Genom att använda radnivåförfallodatum tar Experience Platform automatiskt bort inaktuella loggar och ser till att endast aktuella och meningsfulla data används för analyser och rekommendationer.

## Utvärdera TTL-lämplighet {#evaluate-ttl-suitability}

Innan du tillämpar en kvarhållningsprincip måste du bedöma om datauppsättningen är en bra kandidat för radförfallodatum. Tänk på följande:

- Datarelevans över tid: Tillhandahåller äldre data ett värde eller blir det föråldrat?
- Påverkan på processerna längre fram i kedjan: Kommer borttagning av data att påverka rapportering, analys eller integreringar?
- Lagringskostnad kontra lagringsvärde: Beväger värdet av äldre data kostnaden för att lagra dem?

Om historiska uppgifter är väsentliga för långtidsanalys eller affärstransaktioner är TTL kanske inte rätt metod. Genom att granska dessa faktorer ser du till att TTL-värdet anpassas efter dina datalagringsbehov utan att datatillgängligheten påverkas negativt.

## Bästa tillvägagångssätt för att ange TTL {#best-practices}

Välj rätt TTL-värde för att säkerställa att din Experience Event Data Retention-princip balanserar datalagring, lagringseffektivitet och analysbehov. En TTL som är för kort kan orsaka dataförlust, medan en som är för lång kan öka lagringskostnaderna och onödig datainsamling. Se till att TTL-värdet är anpassat efter datauppsättningens syfte genom att fundera på hur ofta data ska användas och hur länge de ska vara relevanta.

Tabellen nedan innehåller vanliga TTL-rekommendationer baserade på datamängdstyp och användningsmönster:

| Typ av datauppsättning | Rekommenderad TTL | Vanliga användningsfall |
|-----------------------------|------------------------|-------------------|
| Datauppsättningar som du använder ofta | 30-90 dagar | Loggar för användarinteraktion, klickströmsdata för webbplatser, data för kampanjresultat på kort sikt. |
| Arkiveringsdatauppsättningar | 1 år eller mer | Loggar över finansiella transaktioner, efterlevnadsdata, långsiktig trendanalys, data för maskininlärningsutbildning. |
| Apphanterade datauppsättningar | Upp till 13 månader | Systemhanterade datauppsättningar har fördefinierade TTL-begränsningar, som tillämpas automatiskt för att följa systemdefinierade begränsningar. |
| Kundhanterade datauppsättningar | 30 dagar - max TTL | Datauppsättningar som har skapats med Distiller, API:er eller Data. TTL-värdet måste vara minst 30 dagar och inom det definierade maximala TTL-värdet. |

Granska TTL-inställningarna regelbundet för att säkerställa att de fortsätter att vara i linje med dina lagringspolicyer, analytiska behov och affärskrav.

### Viktiga överväganden vid inställning av TTL {#key-considerations}

Följ dessa metodtips för att se till att TTL-inställningarna är anpassade efter din datalagringsstrategi:

- Granska TTL-ändringar regelbundet. Varje TTL-uppdatering utlöser en granskningshändelse. Använd granskningsloggar för att spåra TTL-ändringar för regelefterlevnad, datastyrning och felsökning.
- Inaktivera TTL om data måste behållas i oändlighet. Om du vill inaktivera TTL anger du `ttlValue` till `null`. Detta förhindrar automatiskt förfallodatum och bevarar alla poster permanent. Tänk på lagringskonsekvenserna innan du gör den här ändringen.

## Begränsningar för TTL {#limitations}

Tänk på följande begränsningar när du använder TTL:

- **Upplev kvarhållande av händelsedatauppsättningar med TTL gäller för radnivåförfallodatum**, inte för borttagning av datauppsättningar. TTL tar bort poster baserat på en definierad kvarhållningsperiod, men tar inte bort hela datauppsättningar. Om du vill ta bort en datauppsättning använder du [slutpunkten för datauppsättningens förfallodatum](../../hygiene/api/dataset-expiration.md) eller tar bort manuellt.
- **TTL-konfigurationen är aktiv tills explicit inaktiverad**. Konfigurationen gäller tills du inaktiverar den. Om du inaktiverar TTL upphör giltigheten och alla poster i datauppsättningen behålls.
- **TTL är inte ett kompatibilitetsverktyg**. TTL optimerar lagring och livscykelhantering, men ni måste implementera bredare strategier för styrning för att säkerställa regelefterlevnad.

## Analysera datauppsättningens storlek och relevans innan du använder TTL {#analyze-dataset-size}

Innan du använder TTL bör du använda frågor för att analysera datauppsättningens storlek och relevans. Kör riktade frågor (till exempel inventeringsposter inom specifika datumintervall) för att förhandsgranska effekten av olika TTL-värden. Använd sedan den här informationen för att välja en optimal lagringsperiod som balanserar datamöjligheter och kostnadseffektivitet.

![Ett visuellt arbetsflöde för implementering av TTL på Experience Event-datauppsättningar. Stegen är: utvärdera datalängd och påverkan av borttagning, validera TTL-inställningar med frågor, konfigurera TTL via Catalog Service API och övervaka kontinuerligt TTL-påverkan och göra justeringar.](../images/datasets/dataset-retention-ttl-guide/manage-experience-event-dataset-retention-in-the-data-lake.png)

Genom att köra riktade frågor kan du avgöra hur mycket data som ska behållas eller tas bort under olika TTL-konfigurationer. I följande SQL-fråga räknas till exempel antalet poster som har skapats under de senaste 30 dagarna:

```sql
SELECT COUNT(1) FROM [datasetName] WHERE timestamp > date_sub(now(), INTERVAL 30 DAY);
```

Genom att köra liknande frågor för olika tidsintervall kan du validera TTL-inställningarna och se till att de balanserar lagringseffektivitet och datatillgänglighet.

## Kom igång med TTL-hantering

Innan du kan utvärdera, ange och hantera lagring av Experience Event-datauppsättningar med hjälp av API:t för katalogtjänsten måste du förstå hur du formaterar dina begäranden på rätt sätt. Detta innefattar att känna till API-sökvägarna, tillhandahålla nödvändiga huvuden och formatera nyttolaster för begäranden. Information om detta finns i [API:t för att komma igång](../api/getting-started.md) för katalogtjänsten.

>[!NOTE]
>
>Det här dokumentet täcker förfallodatum på radnivå, vilket innebär att enskilda utgångna rader i en datauppsättning tas bort samtidigt som själva datauppsättningen bevaras intakt. Det gäller inte för förfallodatum för datauppsättningar, vilket tar bort hela datauppsättningar och hanteras av en separat funktion. Information om förfallodatum på datauppsättningsnivå finns i [API-dokumentationen för datauppsättningens förfallodatum](../../hygiene/api/dataset-expiration.md).

### Kontrollera dina TTL-begränsningar {#check-ttl-constraints}

Använd Data Hygiene API:t `/ttl/{DATASET_ID}` för att planera TTL-konfigurationer. Den här slutpunkten returnerar de lägsta och högsta TTL-värden som stöds för din organisation, tillsammans med det rekommenderade värdet (`defaultValue`) för datamängdstypen.

Mer information finns i dokumentationen för Adobe Developer [Data Hygiene API](https://developer.adobe.com/experience-platform-apis/references/data-hygiene/#operation/getTtl) .

Om du vill [kontrollera TTL-värdet som används för en datamängd](#check-applied-ttl-values) gör du en GET-begäran till [katalogtjänstens API](https://developer.adobe.com/experience-platform-apis/references/catalog/) `/dataSets/{DATASET_ID}` -slutpunkt i stället.

>[!TIP]
>
>Experience Platform Gateway-URL och grundsökvägen för katalogtjänstens API är: `https://platform.adobe.io/data/foundation/catalog`. Bassökvägen för API:t för datahygien är: `https://platform.adobe.io/data/core/hygiene`

**API-format**

```http
GET /ttl/{DATASET_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{DATASET_ID}` | En systemgenererad sträng som unikt identifierar en datauppsättning. Använd slutpunkten `/datasets` om du vill hitta ett datauppsättnings-ID. I [listan med katalogobjekts-API:t](../api/list-objects.md) finns anvisningar om hur du filtrerar svar för relevanta datauppsättningar. |

**Begäran**

Följande begäran hämtar organisationens TTL-begränsningar för en viss datauppsättning.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/ttl/{DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Svar**

Ett lyckat svar returnerar de rekommenderade, högsta och lägsta TTL-värdena baserat på organisationens berättiganden, tillsammans med en föreslagen TTL (`defaultValue`) för datauppsättningen. `defaultValue` är en rekommenderad TTL-varaktighet, endast som vägledning. Den tillämpas inte om den inte uttryckligen har konfigurerats av dig. Svaret innehåller inga anpassade TTL-värden som redan har angetts. Använd GET `/catalog/dataSets/{DATASET_ID}`-slutpunkten om du vill visa aktuell TTL för en datauppsättning.

+++Välj för att visa svaret

```json
{
  "extensions": {
    "adobe_lakeHouse": {
      "rowExpiration": {
        "defaultValue": "P12M",
        "maxValue": "P12M",
        "minValue": "P7D"
      }
    }
  }
}
```

+++

| Egenskap | Beskrivning |
|--------------|-------------|
| `defaultValue` | Ett rekommenderat TTL-värde för datauppsättningen. Värdet används **inte** automatiskt. Du måste uttryckligen ange en TTL för att den ska börja gälla. |
| `maxValue` | Den maximala TTL-varaktighet som tillåts av organisationens berättigande. Vanligtvis är den här längden 10 år (`P10Y`). |
| `minValue` | Den minsta TTL-varaktighet som tillåts av din organisations berättigande. Vanligtvis är den här längden 30 dagar (`P30D`). |

### Kontrollera använda TTL-värden {#check-applied-ttl-values}

Om du vill kontrollera det aktuella TTL-värdet som har tillämpats på en datauppsättning använder du följande API-anrop:

```http
GET /dataSets/{DATASET_ID}
```

Det här anropet returnerar aktuell `ttlValue` (om den angetts) i avsnittet `extensions.adobe_lakeHouse.rowExpiration`.

**Begäran**

Följande begäran hämtar organisationens TTL-värde för en viss datauppsättning.

```shell
curl -X GET \
https://platform.adobe.io/data/foundation/catalog/dataSets/{DATASET_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar inkluderar objektet `extensions`, som innehåller den aktuella TTL-konfigurationen som används för datauppsättningen. Svarsexemplet nedan är förkortat för att vara kortfattat.

```json
{
    "{DATASET_ID}": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "extensions": {
            "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P3M",
            }
            }
        }
        ...
    }
}
```

### Ange eller uppdatera TTL för en datauppsättning {#set-update-ttl}

>[!IMPORTANT]
>
>TTL-baserad förfallotid på radnivå kan bara tillämpas på händelsedatamängder som använder ett tidsserieschema. Detta inkluderar datauppsättningar som baseras på XDM ExperienceEvent-standardklassen samt anpassade scheman som utökar Time Series-schemat (`https://ns.adobe.com/xdm/data/time-series`).
>
>Innan du tillämpar TTL ska du använda API:t för schemaregister för att verifiera att datasetens schema innehåller rätt tillägg genom att kontrollera egenskapen `meta:extends`. Mer information om hur du gör detta finns i [slutpunktsdokumentationen för schemat](../../xdm/api/schemas.md#lookup).

Du kan konfigurera lagring av Experience Event-datauppsättningar genom att ange en ny TTL eller uppdatera en befintlig TTL med samma API-metod. Använd en PATCH-begäran för slutpunkten `/v2/datasets/{DATASET_ID}` om du vill använda eller justera TTL.

**API-format**

```http
PATCH /v2/datasets/{DATASET_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{DATASET_ID}` | ID:t för den datauppsättning som du vill uppdatera TTL-värdet för. |

**Begäran**

I exemplet nedan är `ttlValue` inställt på `P3M`. Detta innebär att poster som är äldre än tre månader tas bort automatiskt. Justera kvarhållningsperioden så att den passar ditt företags behov (till exempel `P6M` för sex månader eller `P12M` för ett år).

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/catalog/v2/datasets/{DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

| Egenskap | Beskrivning |
|----------------------------------|-------------|
| `rowExpiration.ttlValue` | Definierar längden innan poster i datauppsättningen tas bort automatiskt. Använder periodformatet ISO-8601 (till exempel `P3M` för 3 månader eller `P30D` för 30 dagar). |

**Svar**

Ett lyckat svar returnerar en referens till den uppdaterade datauppsättningen, men inkluderar inte TTL-inställningarna explicit. Om du vill bekräfta TTL-konfigurationen gör du en uppföljningsförfrågan `GET /dataSets/{DATASET_ID}`.

```JSON
[
  "@/dataSets/{DATASET_ID}"
]
```

#### Exempel på scenario {#example-scenario}

Överväg en videoströmningsplattform som inledningsvis ställer in TTL på tre månader för att säkerställa nya engagemangsdata för personalisering. Om ytterligare analyser visar att äldre interaktioner fortfarande ger värdefulla insikter kan TTL-värdet förlängas till sex månader med följande begäran:

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/catalog/v2/datasets/{DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

## Vanliga frågor om lagringsprinciper för datauppsättning {#faqs}

Vanliga frågor och svar behandlar praktiska frågor om kvarhållningsjobb för datauppsättningar, omedelbara effekter av TTL-ändringar, återställningsalternativ och hur kvarhållningsperioder skiljer sig mellan olika plattformstjänster.

### Vilka typer av datauppsättningar kan jag tillämpa regler för lagringspolicy på?

+++Svar
Du kan tillämpa TTL-baserade bevarandeprinciper på alla datauppsättningar som använder tidsseriebeteende. Detta inkluderar datauppsättningar som baseras på standardklassen för XDM ExperienceEvent, samt anpassade scheman som utformats för att hämta data från tidsserier.

Giltighetstid på radnivå kräver följande tekniska villkor:

- Schemat måste vara utformat för att samla in data från tidsserier.
- Schemat måste innehålla ett tidsstämpelfält som används för att utvärdera förfallodatum.
- Datauppsättningen ska lagra data på händelsenivå, vanligtvis med klassen XDM ExperienceEvent eller som utökning.
- Datauppsättningen måste registreras i katalogtjänsten eftersom TTL-inställningarna tillämpas via `extensions.adobe_lakeHouse.rowExpiration`.
- TTL-värden måste använda varaktighetsformatet ISO-8601 (till exempel `P30D`, `P6M`, `P1Y`).
+++

### Hur snart raderas data från sjödatatjänsterna?

+++Svar
TTL-värden för datauppsättningar utvärderas och bearbetas var 30:e dag, vilket innebär att alla poster som har gått ut tas bort. En händelse anses ha upphört att gälla om den förtärdes i Experience Platform för mer än 30 dagar sedan (importdatum > 30 dagar) och dess händelsedatum överskrider den definierade kvarhållningsperioden (TTL).
+++

<!-- ### How soon will the Dataset Retention job delete data from Profile services?

+++Answer
Once a retention policy is set, existing events that already exceed the newly defined TTL are immediately deleted. Newer events remain until their timestamps surpass the retention period.

For example, if you apply a 30-day expiration policy on May 15th, the following occurs:

- New events receive a 30-day expiration as they are ingested.
- Existing events with a timestamp older than April 15th are immediately deleted.
- Existing events with a timestamp after April 15th are set to expire 30 days after their timestamp (for example, an event from April 18th would be deleted on May 18th).
+++ -->

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

Du kan även göra en GET-begäran till följande slutpunkt:

`GET https://platform.adobe.io/data/foundation/catalog/dataSets/{DATASET_ID}`

Svaret innehåller egenskapen `extensions.adobe_lakeHouse.rowExpiration.lastCompleted`, som anger Unix-tidsstämpeln (i millisekunder) för när det senaste TTL-jobbet slutfördes.

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

- Kvarhållningsjobb: Lär dig att schemalägga och automatisera datauppsättningens förfallodatum i Experience Platform-gränssnittet med [gränssnittsguiden för datalivscykel](../../hygiene/ui/dataset-expiration.md), eller kontrollera konfigurationer för kvarhållande av datauppsättningar och verifiera att utgångna poster tas bort.
- [API-slutpunktsguide för förfallodatum för datauppsättning](../../hygiene/api/dataset-expiration.md): Upptäck hur du tar bort hela datauppsättningar i stället för bara rader. Lär dig hur du schemalägger, hanterar och automatiserar utgångsdatum för datauppsättningar med API:t för att säkerställa effektiv datalagring.
- [Översikt över dataanvändningsprinciper](../../data-governance/policies/overview.md): Lär dig hur du anpassar din datalagringsstrategi till bredare efterlevnadskrav och begränsningar för användning av marknadsföringsmaterial.
