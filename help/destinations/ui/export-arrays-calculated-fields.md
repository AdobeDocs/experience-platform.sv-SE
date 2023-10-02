---
title: (Beta) Använd beräkningsfält för att exportera arrayer i platta schemafiler
type: Tutorial
description: Lär dig hur du använder beräkningsfält för att exportera arrayer i platta schemafiler från Real-Time CDP till molnlagringsmål.
badge: Beta
exl-id: ff13d8b7-6287-4315-ba71-094e2270d039
source-git-commit: 8b8abea65ee0448594113ca77f75b84293646146
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 0%

---

# (Beta) Använd beräkningsfält för att exportera arrayer i platta schemafiler {#use-calculated-fields-to-export-arrays-in-flat-schema-files}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="(Beta) Stöd för exportarrayer"
>abstract="Använd **Lägg till beräknat fält** kan du exportera enkla matriser med int-, string- eller booleska värden från Experience Platform till önskat molnlagringsmål. Vissa begränsningar gäller. I dokumentationen finns omfattande exempel och funktioner som stöds."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#examples" text="Exempel"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#known-limitations" text="Kända begränsningar"

>[!AVAILABILITY]
>
>* Funktionen för att exportera arrayer via beräknade fält finns för närvarande i Beta. Dokumentationen och funktionaliteten kan komma att ändras.

Lär dig hur du exporterar arrayer via beräknade fält från Real-Time CDP i platta schemafiler till [molnlagringsdestinationer](/help/destinations/catalog/cloud-storage/overview.md). Läs det här dokumentet om du vill veta mer om de användningsområden som den här funktionen har aktiverat.

Få omfattande information om beräkningsfält - vad dessa är och varför de spelar någon roll. Läs de länkade sidorna nedan för en introduktion till beräknade fält i Data Prep och mer information om alla tillgängliga funktioner:

* [Användargränssnittsguide och översikt](/help/data-prep/ui/mapping.md#calculated-fields)
* [Förinställningsfunktioner för data](/help/data-prep/functions.md)

>[!IMPORTANT]
>
>Alla funktioner ovan stöds inte *vid export av fält till molnlagringsmål* med funktionen för beräknade fält. Se [funktionsavsnitt som stöds](#supported-functions) mer information nedan.

## Arrayer och andra objekttyper i Platform {#arrays-strings-other-objects}

I Experience Platform kan du använda [XDM-scheman](/help/xdm/home.md) för att hantera olika fälttyper. Tidigare kunde du exportera enkla nyckelvärdepar, t.ex. strängar från Experience Platform till önskade mål. Ett exempel på ett sådant fält som tidigare kunde exporteras är `personalEmail.address`:`johndoe@acme.org`.

Andra fälttyper i Experience Platform är arrayfält. Läs mer om [hantera matrisfält i användargränssnittet för Experience Platform](/help/xdm/ui/fields/array.md). Förutom de fälttyper som tidigare stöds kan du nu exportera arrayobjekt som: `organizations:[marketing, sales, engineering]`. Se mer nedan [omfattande exempel](#examples) av hur du kan använda olika funktioner för att komma åt element i arrayer, koppla arrayelement till en sträng och mycket mer.

## Kända begränsningar {#known-limitations}

Observera följande kända begränsningar för betaversionen av den här funktionen:

* Export till JSON- eller Parquet-filer med hierarkiska scheman stöds inte just nu. Du kan bara exportera arrayer till platta CSV-, JSON- och Parquet-schemafiler.
* För närvarande *du kan bara exportera enkla matriser (eller matriser med primitiva värden) till molnlagringsmål*. Det innebär att du kan exportera arrayobjekt som innehåller strängar, int eller booleska värden. Det går inte att exportera kartor eller arrayer med kartor eller objekt. Det modala fönstret för beräknade fält visar bara de arrayer som du kan exportera.

## Förutsättningar {#prerequisites}

[Anslut](/help/destinations/ui/connect-destination.md) till önskat molnlagringsmål, gå igenom [aktiveringssteg för molnlagringsmål](/help/destinations/ui/activate-batch-profile-destinations.md) och kom till [mappning](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) steg.

## Så här exporterar du beräknade fält {#how-to-export-calculated-fields}

I mappningssteget för aktiveringsarbetsflödet för molnlagringsmål väljer du **[!UICONTROL (Beta) Add calculated field]**.

![Lägg till beräknat fält markerat i mappningssteget i batchaktiveringsarbetsflödet.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

Då öppnas ett modalt fönster där du kan välja attribut som du kan använda för att exportera attribut från Experience Platform.

>[!IMPORTANT]
>
>Endast en del av fälten från XDM-schemat är tillgängliga i **[!UICONTROL Field]** vy. Du kan se strängvärden och arrayer med strängar, int och booleska värden. Till exempel `segmentMembership` arrayen visas inte eftersom den innehåller andra arrayvärden.

![Modalt fönster för funktionen för beräknat fält där ingen funktion har valts ännu.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-2.png)

Använd till exempel `join` funktionen på `loyaltyID` så som visas nedan om du vill exportera en array med ID:n för lojalitet som en sträng sammanfogad med ett understreck i en CSV-fil. Visa [mer information om detta och andra exempel nedan](#join-function-export-arrays).

![Modalt fönster för funktionen för beräknat fält med kopplingsfunktionen markerad.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-3.png)

Välj **[!UICONTROL Save]** för att behålla beräkningsfältet och återgå till mappningssteget.

![Modalt fönster för funktionen för beräknat fält med kopplingsfunktionen markerad och kontrollen Spara markerad.](/help/destinations/assets/ui/export-arrays-calculated-fields/save-calculated-field.png)

Tillbaka i mappningssteget i arbetsflödet, fyll i **[!UICONTROL Target field]** med ett värde för den kolumnrubrik som du vill använda för det här fältet i de exporterade filerna.

![Mappningssteget med målfältet markerat.](/help/destinations/assets/ui/export-arrays-calculated-fields/fill-in-target-field.png)

![Välj målfält 2](/help/destinations/assets/ui/export-arrays-calculated-fields/target-field-filled-in.png)

När du är klar väljer du **[!UICONTROL Next]** för att gå vidare till nästa steg i aktiveringsarbetsflödet.

![Mappningssteg med målfältet markerat och ett målvärde fyllt i.](/help/destinations/assets/ui/export-arrays-calculated-fields/select-next-to-proceed.png)

## Funktioner som stöds {#supported-functions}

Observera att endast följande funktioner stöds i betaversionen av beräkningsfält och matrisstöd för destinationer:

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

Se exempel och mer information i avsnitten nedan för några av funktionerna som listas ovan. För resten av funktionerna i listan finns mer information i [dokumentation om allmänna funktioner i avsnittet Dataprep](/help/data-prep/functions.md).

### `join` funktion för att exportera arrayer {#join-function-export-arrays}

Använd `join` funktion för att sammanfoga elementen i en array till en sträng med en önskad avgränsare, som `_` eller `|`.

Du kan t.ex. kombinera följande XDM-fält nedan som de visas på mappningsskärmbilden med hjälp av en `join('_',loyalty.loyaltyID)` syntax:

* `"organizations": ["Marketing","Sales,"Finance"]` array
* `person.name.firstName` string
* `person.name.lastName` string
* `personalEmail.address` string

![Mappningsexempel inklusive kopplingsfunktionen.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-join-function.png)

I det här fallet ser utdatafilen ut så här nedan. Observera hur arrayens tre element sammanfogas till en enda sträng med `_` tecken.

```
`First_Name,Last_Name,Personal_Email,Organization
John,Doe,johndoe@acme.org, "Marketing_Sales_Finance"
```

### `iif` funktion för att exportera arrayer {#iif-function-export-arrays}

Använd `iif` -funktion för att exportera element i en array under vissa villkor. Du kan till exempel fortsätta med `organizations` arrayobjekt ovan kan du skriva en enkel villkorsstyrd funktion som `iif(organizations[0].equals("Marketing"), "isMarketing", "isNotMarketing")`.

![Mappningsexempel inklusive if-funktionen.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-iif-function.png)

I det här fallet ser utdatafilen ut så här nedan. I det här fallet är det första elementet i matrisen Marketing, så personen är medlem i marknadsföringsavdelningen.

```
`First_Name,Last_Name, Personal_Email, Is_Member_Of_Marketing_Dept
John,Doe, johndoe@acme.org, "isMarketing"
```

### `add_to_array` funktion för att exportera arrayer {#add-to-array-function-export-arrays}

Använd `add_to_array` funktion för att lägga till element i en exporterad array. Du kan kombinera funktionen med `join` funktionen som beskrivs närmare ovan.

Fortsätta med `organizations` arrayobjekt ovan kan du skriva en funktion som `source: join('_', add_to_array(organizations,"2023"))`, som återlämnar organisationer som en person är medlem i under 2023.

![Mappningsexempel med funktionen add_to_array.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-add-to-array-function.png)

I det här fallet ser utdatafilen ut så här nedan. Observera hur arrayens tre element sammanfogas till en enda sträng med `_` och 2023 läggs också till i slutet av strängen.

```
`First_Name,Last_Name,Personal_Email,Organization_Member_2023
John,Doe, johndoe@acme.org,"Marketing_Sales_Finance_2023"
```

### `coalesce` funktion för att exportera arrayer {#coalesce-function-export-arrays}

Använd `coalesce` -funktion för att komma åt och exportera det första icke-null-elementet i en array till en sträng.

Du kan t.ex. kombinera följande XDM-fält nedan som de visas på mappningsskärmbilden med hjälp av en `coalesce(subscriptions.hasPromotion)` syntax för att returnera den första `true` av `false` värde i arrayen:

* `"subscriptions.hasPromotion": [null, true, null, false, true]` array
* `person.name.firstName` string
* `person.name.lastName` string
* `personalEmail.address` string

![Mappningsexempel med sammanslagningsfunktionen.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-coalesce-function.png)

I det här fallet ser utdatafilen ut så här nedan. Lägg märke till hur det första icke-null-värdet `true` värdet i arrayen exporteras i filen.

```
First_Name,Last_Name,hasPromotion
John,Doe,true
```

### `size_of` funktion för att exportera arrayer {#sizeof-function-export-arrays}

Använd `size_of` för att ange hur många element som finns i en array. Om du till exempel har en `purchaseTime` arrayobjekt med flera tidsstämplar kan du använda `size_of` för att ange hur många separata inköp som gjorts av en person.

Du kan t.ex. kombinera följande XDM-fält nedan så som visas på mappningsskärmbilden.

* `"purchaseTime": ["1538097126","1569633126,"1601255526","1632791526","1664327526"]` matris som anger fem separata inköpstider för kunden
* `personalEmail.address` string

![Mappningsexempel med funktionens size_of.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-size-of-function.png)

I det här fallet ser utdatafilen ut så här nedan. Observera hur den andra kolumnen anger antalet element i arrayen, vilket motsvarar antalet separata inköp som kunden gör.

```
`Personal_Email,Times_Purchased
johndoe@acme.org,"5"
```

### Indexbaserad arrayåtkomst {#index-based-array-access}

Du kan komma åt ett index för en array och exportera ett enskilt objekt från arrayen. Liknar till exempel exemplet ovan för `size_of` om du bara vill få åtkomst till och exportera första gången en kund har köpt en viss produkt, kan du använda `purchaseTime[0]` att exportera det första elementet i tidsstämpeln, `purchaseTime[1]` att exportera det andra elementet i tidsstämpeln, `purchaseTime[2]` om du vill exportera det tredje elementet i tidsstämpeln och så vidare.

![Mappningsexempel som visar hur ett element i en array kan nås.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-index.png)

I det här fallet ser utdatafilen ut så här nedan och exporterar första gången som kunden har gjort ett köp:

```
`Personal_Email,First_Purchase
johndoe@acme.org,"1538097126"
```

### `first` och `last` funktioner för att exportera arrayer {#first-and-last-functions-export-arrays}

Använd `first` och `last` funktioner för att exportera det första eller sista elementet i en array. Du kan till exempel fortsätta med `purchaseTime` arrayobjekt med flera tidsstämplar från de föregående exemplen kan du använda dessa funktioner för att exportera den första eller sista inköpstiden som gjorts av en person.

![Mappningsexempel med den första och sista funktionen.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-first-last-functions.png)

I det här fallet ser utdatafilen ut så här nedan och exporterar den första och sista gången kunden har gjort ett köp:

```
`Personal_Email,First_Purchase, Last_Purchase
johndoe@acme.org,"1538097126","1664327526"
```

### `md5` och `sha256` hash-funktioner {#hashing-functions}

Förutom de funktioner som är specifika för att exportera arrayer eller element från en array, kan du använda hash-funktioner för att hash-attribut. Om du till exempel har någon personligt identifierbar information i attribut kan du hash-koda dessa fält när du exporterar dem.

Du kan hash-koda strängvärden direkt, till exempel `md5(personalEmail.address)`. Om du vill kan du även hash-koda enskilda element i arrayfält enligt följande: `md5(purchaseTime[0])`