---
title: (Beta) Använd beräkningsfält för att exportera arrayer i platta schemafiler
type: Tutorial
description: Lär dig hur du använder beräkningsfält för att exportera arrayer i platta schemafiler från Real-Time CDP till molnlagringsmål.
badge: Beta
exl-id: ff13d8b7-6287-4315-ba71-094e2270d039
source-git-commit: 787aaef26fab5ca3acff8303f928efa299cafa93
workflow-type: tm+mt
source-wordcount: '1468'
ht-degree: 0%

---

# (Beta) Använd beräkningsfält för att exportera arrayer i platta schemafiler {#use-calculated-fields-to-export-arrays-in-flat-schema-files}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="(Beta) Stöd för Exportera arrayer"
>abstract="Använd kontrollen **Lägg till beräknat fält** om du vill exportera enkla matriser med int-, string- eller booleska värden från Experience Platform till önskat molnlagringsmål. Vissa begränsningar gäller. I dokumentationen finns omfattande exempel och funktioner som stöds."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#examples" text="Exempel"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#known-limitations" text="Kända begränsningar"

>[!AVAILABILITY]
>
>* Funktionen för att exportera arrayer via beräknade fält finns för närvarande i Beta. Dokumentationen och funktionaliteten kan komma att ändras.

Lär dig hur du exporterar arrayer via beräknade fält från Real-Time CDP i platta schemafiler till [molnlagringsmål](/help/destinations/catalog/cloud-storage/overview.md). Läs det här dokumentet om du vill veta mer om de användningsområden som den här funktionen har aktiverat.

Få omfattande information om beräkningsfält - vad dessa är och varför de spelar någon roll. Läs de länkade sidorna nedan för en introduktion till beräknade fält i Data Prep och mer information om alla tillgängliga funktioner:

* [Användargränssnittsguide och översikt](/help/data-prep/ui/mapping.md#calculated-fields)
* [Förinställningsfunktioner för data](/help/data-prep/functions.md)

<!--

>[!IMPORTANT]
>
>Not all functions listed above are supported *when exporting fields to cloud storage destinations* using the calculated fields functionality. See the [supported functions section](#supported-functions) further below for more information.

-->

## Arrayer och andra objekttyper i Platform {#arrays-strings-other-objects}

I Experience Platform kan du använda [XDM-scheman](/help/xdm/home.md) för att hantera olika fälttyper. Tidigare kunde du exportera enkla nyckelvärdepar, t.ex. strängar från Experience Platform till önskade mål. Ett exempel på ett sådant fält som tidigare hade stöd för export är `personalEmail.address`:`johndoe@acme.org`.

Andra fälttyper i Experience Platform är arrayfält. Läs mer om att [hantera matrisfält i användargränssnittet för Experience Platform](/help/xdm/ui/fields/array.md). Förutom de fälttyper som tidigare stöds kan du nu exportera arrayobjekt som: `organizations:[marketing, sales, engineering]`. Se fler [exempel](#examples) nedan på hur du kan använda olika funktioner för att komma åt element i arrayer, förena arrayelement i en sträng och mycket mer.

## Kända begränsningar {#known-limitations}

Observera följande kända begränsningar för betaversionen av den här funktionen:

* Export till JSON- eller Parquet-filer med hierarkiska scheman stöds inte just nu. Du kan bara exportera arrayer till platta CSV-, JSON- och Parquet-schemafiler.
* För närvarande kan *du bara exportera enkla matriser (eller matriser med primitiva värden) till molnlagringsmål*. Det innebär att du kan exportera arrayobjekt som innehåller strängar, int eller booleska värden. Det går inte att exportera kartor eller arrayer med kartor eller objekt. Det modala fönstret för beräknade fält visar bara de arrayer som du kan exportera.

## Förhandskrav {#prerequisites}

[Anslut](/help/destinations/ui/connect-destination.md) till önskat molnlagringsmål, gå igenom [aktiveringsstegen för molnlagringsmål](/help/destinations/ui/activate-batch-profile-destinations.md) och gå till [mappningssteget](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).

## Så här exporterar du beräknade fält {#how-to-export-calculated-fields}

Välj **[!UICONTROL (Beta) Add calculated field]** i mappningssteget i aktiveringsarbetsflödet för molnlagringsmål.

![Lägg till beräknat fält markerat i mappningssteget i gruppaktiveringsarbetsflödet.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

Då öppnas ett modalt fönster där du kan välja attribut som du kan använda för att exportera attribut från Experience Platform.

>[!IMPORTANT]
>
>Endast vissa av fälten från XDM-schemat är tillgängliga i vyn **[!UICONTROL Field]**. Du kan se strängvärden och arrayer med strängar, int och booleska värden. Arrayen `segmentMembership` visas till exempel inte, eftersom den innehåller andra arrayvärden.

![Modalt fönster för funktionen för beräknat fält utan funktion vald ännu.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-2.png)

Använd till exempel funktionen `join` i fältet `loyaltyID` så som visas nedan om du vill exportera en array med ID:n för lojalitet som en sträng sammanfogad med ett understreck i en CSV-fil. Visa [mer information om det här och andra exempel längre fram nedan](#join-function-export-arrays).

![Modalt fönster för funktionen för beräknat fält med kopplingsfunktionen vald.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-3.png)

Välj **[!UICONTROL Save]** om du vill behålla det beräknade fältet och återgå till mappningssteget.

![Modalt fönster för funktionen för beräknat fält med kopplingsfunktionen markerad och kontrollen Spara markerad.](/help/destinations/assets/ui/export-arrays-calculated-fields/save-calculated-field.png)

I mappningssteget i arbetsflödet fyller du i **[!UICONTROL Target field]** med ett värde för kolumnrubriken som du vill använda för det här fältet i de exporterade filerna.

![Mappningssteg med målfältet markerat.](/help/destinations/assets/ui/export-arrays-calculated-fields/fill-in-target-field.png)

![Välj målfält 2](/help/destinations/assets/ui/export-arrays-calculated-fields/target-field-filled-in.png)

När du är klar väljer du **[!UICONTROL Next]** för att fortsätta till nästa steg i aktiveringsarbetsflödet.

![Mappningssteg med målfältet markerat och ett målvärde fyllt i.](/help/destinations/assets/ui/export-arrays-calculated-fields/select-next-to-proceed.png)

## Funktioner som stöds {#supported-functions}

Alla dokumenterade [dataprep-funktioner](/help/data-prep/functions.md) stöds när data aktiveras till filbaserade mål.

Observera dock att omfattande fallbeskrivningar och exempelutdata för närvarande endast tillhandahålls för följande funktioner i betaversionen av beräknade fält och stöd för matriser för destinationer:

* `join`
* `coalesce`
* `size_of`
* `iif`
* `index-based array access`
* `add_to_array`
* `to_array`
* `first`
* `last`
* `sha256`
* `md5`

## Exempel på funktioner som används för att exportera arrayer {#examples}

Se exempel och mer information i avsnitten nedan för några av funktionerna som listas ovan. För resten av funktionerna i listan finns mer information i [dokumentationen om allmänna funktioner i avsnittet Dataprep](/help/data-prep/functions.md).

### `join`-funktion för att exportera arrayer {#join-function-export-arrays}

Använd funktionen `join` för att sammanfoga elementen i en array till en sträng med en önskad avgränsare, till exempel `_` eller `|`.

Du kan t.ex. kombinera följande XDM-fält nedan som visas på mappningsskärmbilden med en `join('_',loyalty.loyaltyID)`-syntax:

* `"organizations": ["Marketing","Sales,"Finance"]`-matris
* `person.name.firstName` sträng
* `person.name.lastName` sträng
* `personalEmail.address` sträng

![Mappningsexempel med kopplingsfunktionen.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-join-function.png)

I det här fallet ser utdatafilen ut så här nedan. Observera hur arrayens tre element sammanfogas till en enda sträng med tecknet `_`.

```
`First_Name,Last_Name,Personal_Email,Organization
John,Doe,johndoe@acme.org, "Marketing_Sales_Finance"
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

Använd funktionen `add_to_array` för att lägga till element i en exporterad array. Du kan kombinera den här funktionen med funktionen `join` som beskrivs ytterligare ovan.

Om du fortsätter med arrayobjektet `organizations` ovan kan du skriva en funktion som `source: join('_', add_to_array(organizations,"2023"))`, som returnerar de organisationer som en person är medlem i under 2023.

![Mappningsexempel med funktionen add_to_array.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-add-to-array-function.png)

I det här fallet ser utdatafilen ut så här nedan. Observera hur arrayens tre element sammanfogas till en enda sträng med tecknet `_` och 2023 också läggs till i slutet av strängen.

```
`First_Name,Last_Name,Personal_Email,Organization_Member_2023
John,Doe, johndoe@acme.org,"Marketing_Sales_Finance_2023"
```

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

Förutom de funktioner som är specifika för att exportera arrayer eller element från en array, kan du använda hash-funktioner för att hash-formatera attribut i de exporterade filerna. Om du till exempel har någon personligt identifierbar information i attribut kan du hash-koda dessa fält när du exporterar dem.

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