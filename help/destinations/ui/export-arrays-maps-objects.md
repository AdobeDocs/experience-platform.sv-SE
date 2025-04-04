---
title: Exportera arrayer, kartor och objekt från Real-Time CDP
type: Tutorial
description: Lär dig hur du exporterar arrayer, kartor och objekt från Real-Time CDP till molnlagringsmål.
exl-id: ff13d8b7-6287-4315-ba71-094e2270d039
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1081'
ht-degree: 0%

---

# Exportera arrayer, kartor och objekt från Real-Time CDP {#export-arrays-cloud-storage}

>[!AVAILABILITY]
>
>Funktionen för att exportera arrayer och andra komplexa objekt till molnlagringsmål är vanligtvis tillgänglig för följande mål: [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md), [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md), [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md), [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md), [[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md), [[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md).
>
>Dessutom kan du exportera mappningsfält till följande mål: [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md), [HTTP API](/help/destinations/catalog/streaming/http-destination.md), [Azure Event Hubs](/help/destinations/catalog/cloud-storage/azure-event-hubs.md), [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md).


Lär dig hur du exporterar arrayer, kartor och objekt från Real-Time CDP till [molnlagringsmål](/help/destinations/catalog/cloud-storage/overview.md). Dessutom kan du exportera mappningsfält till [företagsmål](/help/destinations/destination-types.md#advanced-enterprise-destinations) och begränsade [kantanpassningsmål](/help/destinations/destination-types.md#edge-personalization-destinations). Läs det här dokumentet om du vill veta mer om exportarbetsflödet, vilka användningsfall som den här funktionen har aktiverat och kända begränsningar. Se tabellen nedan för att förstå vilka funktioner som är tillgängliga per måltyp.

| Typ av mål | Möjlighet att exportera arrayer, kartor och andra anpassade objekt |
|---|---|
| Adobe-skapade molnlagringsmål (Amazon S3, Azure Blob, Azure Data Lake Storage Gen2, Data Landing Zone, Google Cloud Storage, SFTP) | Ja, med Aktivera export av arrayer, kartor och objekt aktiverat när du konfigurerar en målanslutning. |
| Filbaserade mål för e-postmarknadsföring (Adobe Campaign, Oracle Eloqua, Oracle Responsys, Salesforce Marketing Cloud) | Nej |
| Befintliga anpassade partnerbyggda molnlagringsmål (anpassade filbaserade mål byggda via Destination SDK) | Nej |
| Företagsmål (Amazon Kinesis, Azure Event Hubs, HTTP API) | Delvis. Du kan markera och exportera mappningsobjekt i mappningssteget i aktiveringsarbetsflödet. |
| Direktuppspelningsmål (t.ex. Facebook, Braze, Google Customer Match) | Nej |
| Edge personaliseringsmål (Adobe Target) | Delvis. Du kan markera och exportera mappningsobjekt i mappningssteget i aktiveringsarbetsflödet. |

{style="table-layout:auto"}

Ta den här sidan som en praktisk plats där du kan hitta det du vill veta om hur du exporterar arrayer, kartor och andra objekttyper från Experience Platform.

## Nedre linje längst fram

Hämta den viktigaste informationen om funktionerna i det här avsnittet och fortsätt till de andra avsnitten i dokumentet för detaljerad information.

* För molnlagringsmål beror möjligheten att exportera arrayer, kartor och objekt på ditt val av **Exportera arrayer, kartor och objekt**. Läs mer om det [längre ned på sidan](#export-arrays-maps-objects-toggle).
* Du kan exportera arrayer, kartor och objekt till molnlagringsmål i `JSON`- och `Parquet`-filer. För företags- och kantanpassningsmål är den exporterade datatypen `JSON`. Målgrupper för människor och potentiella kunder stöds, men inte målgrupper för konton.
* För filbaserade molnlagringsmål *kan* exportera arrayer, kartor och objekt till CSV-filer, men bara genom att använda funktionen för beräknade fält och sammanfoga dem till en sträng med funktionen `array_to_string` .

## Arrayer och andra objekttyper i Experience Platform {#arrays-strings-other-objects}

I Experience Platform kan du använda [XDM-scheman](/help/xdm/home.md) för att hantera olika fälttyper. Innan stöd för matrisexport lades till kunde du exportera enkla nyckelvärdepar, t.ex. strängar från Experience Platform, till önskade mål. Ett exempel på ett sådant fält som tidigare hade stöd för export är `personalEmail.address`:`johndoe@acme.org`.

Andra fälttyper i Experience Platform är arrayfält. Läs mer om att [hantera matrisfält i Experience Platform-gränssnittet](/help/xdm/ui/fields/array.md). Nu kan du exportera arrayobjekt som exemplet nedan.

```
organizations = [{
  id: 123,
  orgName: "Acme Inc",
  founded: 1990,
  latestInteraction: "2024-02-16"
}, {
  id: 456,
  orgName: "Superstar Inc",
  founded: 2004,
  latestInteraction: "2023-08-25"
}, {
  id: 789,
  orgName: 'Energy Corp',
  founded: 2021,
  latestInteraction: "2024-09-08"
}]
```

Förutom arrayer kan du även exportera kartor och objekt från Experience Platform till önskat molnlagringsmål. Läs mer om [kartor](/help/xdm/ui/fields/map.md) och [objekt](/help/xdm/ui/fields/object.md) i Experience Platform.

## Förhandskrav {#prerequisites}

[Anslut](/help/destinations/ui/connect-destination.md) till önskat molnlagringsmål, gå igenom [aktiveringsstegen för molnlagringsmål](/help/destinations/ui/activate-batch-profile-destinations.md) och gå till [mappningssteget](/help/destinations/ui/activate-batch-profile-destinations.md#mapping). När du ansluter till det önskade molnmålet måste du aktivera alternativet **[!UICONTROL Export arrays, maps, objects]**. Mer information finns i avsnittet nedan.

>[!NOTE]
>
>För företags- och kantanpassningsmål är exportstöd för mappningsfält tillgängligt utan att du behöver välja en **[!UICONTROL Export arrays, maps, objects]**-växel. Den här växeln är inte tillgänglig eller behövs vid anslutning till dessa typer av mål.

## Exportera arrayer, kartor, objektväxling {#export-arrays-maps-objects-toggle}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_maps_objects"
>title="Exportera arrayer, kartor och objekt"
>abstract="<p> Växla den här inställningen <b>på</b> om du vill aktivera export av arrayer, kartor och objekt till JSON- eller Parquet-filer. Du kan välja dessa objekttyper i källfältsvyn i mappningssteget. Om du aktiverar växeln kan du inte använda alternativet för beräknade fält i mappningssteget.</p><p>Med den här växlingen <b> av</b> kan du använda alternativet för beräknade fält och tillämpa olika dataomformningsfunktioner när du aktiverar målgrupper. Du kan <i>inte</i> exportera arrayer, kartor och objekt till JSON- eller Parquet-filer och måste konfigurera ett separat mål för det ändamålet.</p>"

När du ansluter till ett filbaserat molnlagringsmål kan du aktivera eller inaktivera **[!UICONTROL Export arrays, maps, objects]**.

![Exportera matriser, kartor, objekt som växlas mellan att visas med en aktiverings- eller avaktiveringsinställning, samt markera povern.](/help/destinations/assets/ui/export-arrays-calculated-fields/export-objects-toggle.gif)

Växla den här inställningen **på** om du vill aktivera export av arrayer, kartor och objekt till JSON- eller Parquet-filer. Du kan välja de här objekttyperna i källfältsvyn i [mappningssteget](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) när du aktiverar målgrupper till molnlagringsmål. Om den här inställningen är aktiverad kan du inte använda alternativet för beräknade fält för att omforma data vid aktiveringen.

Med den här växlingen **av** kan du använda alternativet för beräknade fält och tillämpa olika dataomformningsfunktioner när du aktiverar målgrupper. Du kan dock inte exportera arrayer, kartor och objekt till JSON- eller Parquet-filer och måste konfigurera ett separat mål för det ändamålet.

## Exportera arrayer, kartor, objekt som växlar *på* {#export-arrays-maps-objects-toggle-on}

Med den här inställningen aktiverad kan du exportera hela objekt (till exempel `person.name`) och arrayer genom att markera dem via källfältväljaren i mappningssteget i aktiveringsarbetsflödet.

![Markera objekt via källfältväljaren i mappningssteget i aktiveringsarbetsflödet.](/help/destinations/assets/ui/export-arrays-calculated-fields/select-object.gif)

När det här alternativet är markerat blockerar användargränssnittet användare från att använda beräkningsfält och kontrollen **[!UICONTROL Add calculated fields]** är inaktiverad, vilket visas nedan. Om du vill använda beräkningsfält för dataomvandlingar anger du en målanslutning med avaktiveringen.

![Kontrollen för beräknade fält har inaktiverats.](/help/destinations/assets/ui/export-arrays-calculated-fields/calculated-fields-disabled.png)

## Exportera arrayer, kartor, objekt som växlar *av* {#export-arrays-maps-objects-toggle-off}

Med det här alternativet inställt på *av* kan du använda alternativet för beräknade fält och tillämpa olika dataomformningsfunktioner när du aktiverar målgrupper. Du kan dock inte exportera arrayer, kartor och objekt till JSON- eller Parquet-filer och måste konfigurera ett separat mål för det ändamålet.

Du *kan* exportera arrayer, kartor och objekt till CSV-filer genom att använda funktionen för beräknade fält och sammanfoga dem i en sträng med funktionen `array_to_string`. [Läs mer](#array-to-string-function-export-arrays) om hur du använder den funktionen.

Läs mer om att arbeta med beräknade fält för att [utföra omformningar på data som exporteras till molnlagringsmål](/help/destinations/ui/data-transformations-calculated-fields.md).

## Exempel på exporterade filer {#sample-exported-files}

Med den här funktionen kan du exportera Parquet- och JSON-filer där data bevarar strukturen från Experience Platform. Visa ett exempel på en exporterad JSON-fil nedan.

+++ Välj det här alternativet om du vill visa den exporterade JSON-filen.

```json
{
  "person_name_firstName": "John",
  "person_name_lastName": "Smith",
  "_acmeinc_customer_hs_main_address_scalar": "Oak Avenue No 12",
  "_acmeinc_customer_hs_locations_array": [
    "home address 12",
    "office address 12"
  ],
  "_acmeinc_customer_hs_date_array": [
    "2024-11-14",
    "2024-11-15"
  ],
  "_acmeinc_customer_hs_customer_obj_emails_array0": "john.smith@example.com",
  "_acmeinc_customer_hs_customer_obj": {
    "emails_array": [
      "john.smith@example.com",
      "j.smith@example.com"
    ],
    "name_scalar": "John Smith"
  },
  "_acmeinc_customer_hs_addresses_array_obj": [
    {
      "is_primary": true,
      "streetName_scalar": "Maple Street",
      "streetNo_int": 12
    },
    {
      "is_primary": false,
      "streetName_scalar": "Pine Road",
      "streetNo_int": 45
    }
  ],
  "_acmeinc_customer_hs_addresses_array_obj0": {
    "is_primary": true,
    "streetName_scalar": "Maple Street",
    "streetNo_int": 12
  }
}
```

+++