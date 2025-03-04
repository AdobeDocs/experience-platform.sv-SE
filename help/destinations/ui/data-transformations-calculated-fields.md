---
title: Utför omformningar av data som exporteras till molnlagringsmål med beräkningsfält
type: Tutorial
description: Förstå hur du använder funktionen för beräknade fält för att utföra omformningar av data som exporteras till molnlagringsmål
exl-id: 1e14f964-4c03-4d0c-be8d-c3dcb48a335a
source-git-commit: 14c672ef57e0b0247020075552c782ed18db8484
workflow-type: tm+mt
source-wordcount: '1574'
ht-degree: 0%

---

# Utför omformningar av data som exporteras till molnlagringsmål med beräkningsfält {#data-transformation-calculated-fields}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="Lägg till beräknade fält"
>abstract="<p>Använd kontrollen **Lägg till beräknat fält** för att utföra olika dataomvandlingar på data som exporteras till molnlagringsmål. Du kan till exempel tillämpa hash-kodning på data, sammanfoga arrayer i strängar och mycket mer."

<!--

disable additional URLs for a while

>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-maps-objects.html#examples" text="Examples"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-maps-objects.html#known-limitations" text="Known limitations"

-->

>[!AVAILABILITY]
>
>Funktionen för att utföra transformeringar av data som exporteras till molnlagringsmål är vanligtvis tillgänglig för följande mål: [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md), [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md), [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md), [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md), [[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md), [[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md), samt för anpassade partnerskapade molnlagringsmål som har skapats via [Destination SDK](/help/destinations/destination-sdk/overview.md).

Om du vill utföra olika omformningar av data som exporteras till molnlagringsmål måste du använda funktionen för beräknade fält i mappningssteget i exportarbetsflödet. Detaljerad information om beräkningsfält finns på de sidor som är länkade nedan. På dessa sidor finns en introduktion till beräknade fält i Data Prep och mer information om alla tillgängliga funktioner:

* [Användargränssnittsguide och översikt](/help/data-prep/ui/mapping.md#calculated-fields)
* [Förinställningsfunktioner för data](/help/data-prep/functions.md)

## Förhandskrav {#prerequisites}

Så här använder du beräknade fält för dataomvandlingar:

1. [Anslut](/help/destinations/ui/connect-destination.md) till önskat molnlagringsmål. När du ansluter till det önskade molnmålet växlar du **[!UICONTROL Export arrays, maps, objects]** [alternativet av](/help/destinations/ui/export-arrays-maps-objects.md##export-arrays-maps-objects-toggle).
2. Gå igenom [aktiveringsstegen för molnlagringsmål](/help/destinations/ui/activate-batch-profile-destinations.md) och gå till [mappningssteget](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).

## Så här arbetar du med beräknade fält {#how-to-export-calculated-fields}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_control"
>title="Aktivera hierarkiskt utdataschema"
>abstract="Aktivera den här inställningen för att aktivera export av arrayer, kartor och objekt till JSON- eller Parquet-filer."

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_calculated_field_disabled"
>title="Lägg till beräknade fält inaktiverat"
>abstract="Den här kontrollen är inaktiverad eftersom du valde **Exportera arrayer, kartor, objekt** växla *på* när du konfigurerade den här målanslutningen. Om du vill använda beräkningsfält och de funktioner som är tillgängliga i dem skapar du en ny målanslutning med **Exportera arrayer, kartor, objekt** och *av*."

Välj **[!UICONTROL Add calculated field]** i mappningssteget i aktiveringsarbetsflödet för molnlagringsmål.

>[!TIP]
>
>Kontrollen **[!UICONTROL Add calculated field]** är inaktiverad för målanslutningar där kontrollen **[!UICONTROL Export arrays, maps, and objects]** stängdes av. [Läs mer](/help/destinations/ui/export-arrays-maps-objects.md#export-arrays-maps-objects-toggle).

![Lägg till beräknat fält markerat i mappningssteget i gruppaktiveringsarbetsflödet.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

Då öppnas ett modalt fönster där du kan välja funktioner och fält för att exportera attribut från Experience Platform.

![Modalt fönster för funktionen för beräknat fält utan funktion vald ännu.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-2.png)

Använd till exempel funktionen `array_to_string` i fältet `organizations` så som visas nedan för att exportera organisationsarrayen som en sträng i en CSV-fil. Visa [mer information om det här och andra exempel längre fram nedan](#array-to-string-function-export-arrays).

![Modalt fönster för funktionen för beräknat fält med funktionen matris-till-sträng markerad.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-3.png)

Välj **[!UICONTROL Save]** om du vill behålla det beräknade fältet och återgå till mappningssteget.

![Modalt fönster för funktionen för beräknat fält med funktionen matris-till-sträng markerad och kontrollen Spara markerad.](/help/destinations/assets/ui/export-arrays-calculated-fields/save-calculated-field.png)

I mappningssteget i arbetsflödet fyller du i **[!UICONTROL Target field]** med ett värde för kolumnrubriken som du vill använda för det här fältet i de exporterade filerna.

![Mappningssteg med målfältet markerat.](/help/destinations/assets/ui/export-arrays-calculated-fields/fill-in-target-field.png)

![Välj målfält 2](/help/destinations/assets/ui/export-arrays-calculated-fields/target-field-filled-in.png)

När du är klar väljer du **[!UICONTROL Next]** för att fortsätta till nästa steg i aktiveringsarbetsflödet.

![Mappningssteg med målfältet markerat och ett målvärde fyllt i.](/help/destinations/assets/ui/export-arrays-calculated-fields/select-next-to-proceed.png)

## Exempelfunktioner som stöds för att utföra dataomvandlingar {#supported-functions}

Alla dokumenterade [dataprep-funktioner](/help/data-prep/functions.md) stöds när data aktiveras till filbaserade mål.

Funktionerna nedan, som är specifika för att hantera export av arrayer eller tillämpa hash-kodning på fält, dokumenteras tillsammans med exempel.

* `array_to_string`
* `flattenArray`
* `filterArray`
* `transformArray`
* `coalesce`
* `size_of`
* `iif`
* `index-based array access`
* `add_to_array`
* `to_array`
* `first`
* `last`

## Exempel på funktioner som används för att utföra dataomvandlingar {#examples}

Se exempel och mer information i avsnitten nedan för några av funktionerna som listas ovan. För resten av funktionerna i listan finns mer information i [dokumentationen om allmänna funktioner i avsnittet Dataprep](/help/data-prep/functions.md).

### `array_to_string`-funktion för att exportera arrayer {#array-to-string-function-export-arrays}

Använd funktionen `array_to_string` för att sammanfoga elementen i en array till en sträng med en önskad avgränsare, till exempel `_` eller `|`. Den här funktionen är användbar när du vill exportera elementen i en array från Experience Platform till en CSV-fil.

Du kan t.ex. kombinera följande XDM-fält nedan som visas på mappningsskärmbilden med en `array_to_string('_',organizations)`-syntax:

* `organizations`-matris
* `person.name.firstName` sträng
* `person.name.lastName` sträng
* `personalEmail.address` sträng

![Mappningsexempel med funktionen array_to_string.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-array-to-string-function.png)

I det här fallet ser utdatafilen ut så här nedan. Observera hur elementen i arrayen sammanfogas till en enda sträng med tecknet `_`.

```
First_Name,Last_Name,Personal_Email,Organization
John,Doe,johndoe@acme.org, "{'id':123,'orgName':'Acme Inc','founded':1990,'latestInteraction':1708041600000}_{'id':456,'orgName':'Superstar Inc','founded':2004,'latestInteraction':1692921600000}_{'id':789,'orgName':'Energy Corp','founded':2021,'latestInteraction':1725753600000}"
```

### funktionen `filterArray` för att exportera filtrerade arrayer {#filter-array}

Använd funktionen `filterArray` för att filtrera elementen i en exporterad array. Du kan kombinera den här funktionen med funktionen `array_to_string` som beskrivs ytterligare ovan.

Om du fortsätter med arrayobjektet `organizations` ovan kan du skriva en funktion som `array_to_string('_', filterArray(organizations, org -> org.founded > 2021))`, som returnerar organisationerna med värdet `founded` för 2021 eller senare.

![Exempel på funktionen filterArray.](/help/destinations/assets/ui/export-arrays-calculated-fields/filter-array-function.png)

I det här fallet ser utdatafilen ut så här nedan. Observera hur de två elementen i arrayen som uppfyller villkoret sammanfogas till en enda sträng med tecknet `_`.

```
John,Doe,johndoe@acme.org, "{'id':123,'orgName':'Acme Inc','founded':1990,'latestInteraction':1708041600000}_{'id':789,'orgName':'Energy Corp','founded':2021,'latestInteraction':1725753600000}"
```

### funktionen `transformArray` för att exportera omformade arrayer {#transform-array}

Använd funktionen `transformArray` för att omforma elementen i en exporterad array. Du kan kombinera den här funktionen med funktionen `array_to_string` som beskrivs ytterligare ovan.

Om du fortsätter med arrayobjektet `organizations` ovan kan du skriva en funktion som `array_to_string('_', transformArray(organizations, org -> ucase(org.orgName)))` och returnera namnen på organisationerna konverterade till versaler.

![Exempel på funktionen transformArray.](/help/destinations/assets/ui/export-arrays-calculated-fields/transform-array-function.png)

I det här fallet ser utdatafilen ut så här nedan. Observera hur arrayens tre element omformas och sammanfogas till en enda sträng med tecknet `_`.

```
John,Doe,johndoe@acme.org,ACME INC_SUPERSTAR INC_ENERGY CORP
```

### `iif`-funktion för att exportera arrayer {#iif-function-export-arrays}

Använd funktionen `iif` för att exportera element i en array under vissa villkor. Om du till exempel fortsätter med arrayobjektet `organizations` ovan kan du skriva en enkel villkorsstyrd funktion som `iif(organizations[0].equals("Marketing"), "isMarketing", "isNotMarketing")`.

![Mappningsexempel inklusive if-funktionen.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-iif-function.png)

I det här fallet ser utdatafilen ut så här nedan. I det här fallet är det första elementet i matrisen Marketing, så personen är medlem i marknadsföringsavdelningen.

```
`First_Name,Last_Name, Personal_Email, Is_Member_Of_Marketing_Dept
John,Doe, johndoe@acme.org, "isMarketing"
```

### `add_to_array`-funktion för att exportera arrayer {#add-to-array-function-export-arrays}

Använd funktionen `add_to_array` för att lägga till element i en exporterad array. Du kan kombinera den här funktionen med funktionen `array_to_string` som beskrivs ytterligare ovan.

Om du fortsätter med arrayobjektet `organizations` ovan kan du skriva en funktion som `source: array_to_string('_', add_to_array(organizations,"2023"))`, som returnerar de organisationer som en person är medlem i under 2023.

![Mappningsexempel med funktionen add_to_array.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-add-to-array-function.png)

I det här fallet ser utdatafilen ut så här nedan. Observera hur arrayens tre element sammanfogas till en enda sträng med tecknet `_` och 2023 också läggs till i slutet av strängen.

```
`First_Name,Last_Name,Personal_Email,Organization_Member_2023
John,Doe, johndoe@acme.org,"Marketing_Sales_Finance_2023"
```

### Funktionen `flattenArray` för att exportera separerade arrayer {#flatten-array}

Använd funktionen `flattenArray` för att förenkla en exporterad flerdimensionell array. Du kan kombinera den här funktionen med funktionen `array_to_string` som beskrivs ytterligare ovan.

Om du fortsätter med arrayobjektet `organizations` ovan kan du skriva en funktion som `array_to_string('_', flattenArray(organizations))`. Observera att funktionen `array_to_string` förenklar inmatningsarrayen som standard till en sträng.

Resultatet är detsamma som för funktionen `array_to_string` som beskrivs ovan.

### `coalesce`-funktion för att exportera arrayer {#coalesce-function-export-arrays}

Använd funktionen `coalesce` för att komma åt och exportera det första icke-null-elementet i en array till en sträng.

Du kan till exempel kombinera följande XDM-fält nedan så som visas på mappningsskärmbilden genom att använda en `coalesce(subscriptions.hasPromotion)`-syntax för att returnera det första `true` av `false` värdet i arrayen:

* `"subscriptions.hasPromotion": [null, true, null, false, true]`-matris
* `person.name.firstName` sträng
* `person.name.lastName` sträng
* `personalEmail.address` sträng

![Mappningsexempel med sammanslagningsfunktionen.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-coalesce-function.png)

I det här fallet ser utdatafilen ut så här nedan. Observera hur det första icke-null `true`-värdet i arrayen exporteras i filen.

```
First_Name,Last_Name,hasPromotion
John,Doe,true
```

### `size_of`-funktion för att exportera arrayer {#sizeof-function-export-arrays}

Använd funktionen `size_of` för att ange hur många element som finns i en array. Om du till exempel har ett `purchaseTime`-arrayobjekt med flera tidsstämplar kan du använda funktionen `size_of` för att ange hur många separata inköp som har gjorts av en person.

Du kan t.ex. kombinera följande XDM-fält nedan så som visas på mappningsskärmbilden.

* `"purchaseTime": ["1538097126","1569633126,"1601255526","1632791526","1664327526"]`-matris som anger fem separata inköpstider för kunden
* `personalEmail.address` sträng

![Mappningsexempel med funktionens size_of.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-size-of-function.png)

I det här fallet ser utdatafilen ut så här nedan. Observera hur den andra kolumnen anger antalet element i arrayen, vilket motsvarar antalet separata inköp som kunden gör.

```
`Personal_Email,Times_Purchased
johndoe@acme.org,"5"
```

### Indexbaserad arrayåtkomst {#index-based-array-access}

>[!IMPORTANT]
>
>Till skillnad från andra funktioner som beskrivs på den här sidan behöver du *inte* för att kunna exportera enskilda element i en array med kontrollen **[!UICONTROL Calculated fields]** i användargränssnittet.

Du kan komma åt ett index för en array och exportera ett enskilt objekt från arrayen. Om du till exempel, som i exemplet ovan för funktionen `size_of`, bara vill komma åt och exportera första gången som en kund har köpt en viss produkt, kan du använda `purchaseTime[0]` för att exportera det första elementet i tidsstämpeln, `purchaseTime[1]` för att exportera det andra elementet i tidsstämpeln, `purchaseTime[2]` för att exportera det tredje elementet i tidsstämpeln och så vidare.

![Mappningsexempel som visar hur ett element i en array kan nås.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-index.png)

I det här fallet ser utdatafilen ut så här nedan och exporterar första gången som kunden har gjort ett köp:

```
`Personal_Email,First_Purchase
johndoe@acme.org,"1538097126"
```

### `first`- och `last`-funktioner för att exportera arrayer {#first-and-last-functions-export-arrays}

Använd funktionerna `first` och `last` för att exportera det första eller sista elementet i en array. Om du till exempel fortsätter med arrayobjektet `purchaseTime` med flera tidsstämplar från de föregående exemplen kan du använda dessa för funktioner för att exportera den första eller sista inköpstiden som gjorts av en person.

![Mappningsexempel med den första och sista funktionen.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-first-last-functions.png)

I det här fallet ser utdatafilen ut så här nedan och exporterar den första och sista gången kunden har gjort ett köp:

```
`Personal_Email,First_Purchase, Last_Purchase
johndoe@acme.org,"1538097126","1664327526"
```

### Hash-funktioner {#hashing-functions}

Andra tillgängliga funktioner är specifika för export av arrayer eller element från en array. Du kan använda hash-funktioner för att hash-koda attribut i de exporterade filerna. Om du till exempel har någon personligt identifierbar information i attribut kan du hash-koda dessa fält när du exporterar dem.

Du kan hash-koda strängvärden direkt, till exempel `md5(personalEmail.address)`. Om du vill kan du även hash-koda enskilda element i matrisfält, förutsatt att elementen i matrisen är strängar, så här: `md5(purchaseTime[0])`

De hash-funktioner som stöds är:

| Funktion | Exempeluttryck |
|---------|----------|
| `sha1` | `sha1(organizations[0])` |
| `sha256` | `sha256(organizations[0])` |
| `sha512` | `sha512(organizations[0])` |
| `hash` | `hash("crc32", organizations[0], "UTF-8")` |
| `md5` | `md5(organizations[0], "UTF-8")` |
| `crc32` | `crc32(organizations[0])` |

{style="table-layout:auto"}
