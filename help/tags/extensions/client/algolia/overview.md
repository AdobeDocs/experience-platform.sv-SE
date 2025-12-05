---
title: Översikt över tillägget Algolia-taggar
description: Läs mer om tillägget Algolia-taggar i Adobe Experience Platform.
exl-id: 8409bf8b-fae2-44cc-8466-9942f7d92613
source-git-commit: 6eee26df3841a7829625361fc726bf59a278f867
workflow-type: tm+mt
source-wordcount: '1954'
ht-degree: 0%

---

# Översikt över tillägget [!DNL Algolia] Taggar

Tillägget [!DNL Algolia] Taggar ger marknadsförarna möjlighet att enkelt konfigurera regler som skickar användarinteraktionsdata till [!DNL Algolia], vilket hjälper dig att leverera mer personaliserade AI-söknings- och identifieringsupplevelser.

Det här tillägget drivs av en nyckelfunktion:

* **[!DNL Algolia]Insikter**: Hämtar och skickar automatiskt användarinteraktionshändelser till [!DNL Algolia], vilket möjliggör kraftfull analys, personaliserade upplevelser och förbättrad sökrelevans.

## Förhandskrav {#prerequisites}

Du måste ha ett giltigt [!DNL Algolia]-konto för att kunna använda det här tillägget. Gå till [[!DNL Algolia] registreringssidan](https://dashboard.algolia.com/users/sign_up) och skapa ett konto om du inte redan har ett.

### Samla nödvändig konfigurationsinformation {#configuration-details}

Om du vill ansluta [!DNL Algolia] till Adobe Experience Platform behöver du följande information:

| Autentiseringsuppgifter | Beskrivning | Exempel |
| --- | --- | --- |
| Program-ID | Ditt program-ID finns i avsnittet [API-nycklar](https://www.algolia.com/account/api-keys/all) på [!DNL Algolia]-instrumentpanelen. | 0ABCDEFG12 |
| API-nyckel för sökning | Du hittar API-nyckeln för sökning i avsnittet [API-nycklar](https://www.algolia.com/account/api-keys/all) på [!DNL Algolia]-instrumentpanelen. | 1234a12345678901b1234567890c1ab1 |

## Installera och konfigurera [!DNL Algolia] Insights-tillägget {#install-configure}

Om du vill installera tillägget [!DNL Algolia] Insights går du till [!UICONTROL Data Collection UI] och väljer **[!UICONTROL Tags]** i den vänstra navigeringen. Här väljer du en egenskap som tillägget ska läggas till i eller skapar en ny egenskap i stället.

När du har markerat eller skapat den önskade egenskapen väljer du **[!UICONTROL Extensions]** i den vänstra navigeringen och väljer sedan fliken **[!UICONTROL Catalog]**. Sök efter [!DNL Algolia] Insights-kortet och välj sedan **[!UICONTROL Install]**.

![](../../../images/extensions/client/algolia/install.png)

I konfigurationsvyn som visas måste du ange följande information:

| Egenskap | Beskrivning |
| --- | --- |
| [!UICONTROL Application ID] | Ange [!UICONTROL Application Id] som du redan har samlat in i avsnittet [konfigurationsinformation](#configuration-details). |
| [!UICONTROL Search API Key] | Ange [!UICONTROL Search API Key] som du redan har samlat in i avsnittet [konfigurationsinformation](#configuration-details). |
| [!UICONTROL Index Name] | [!UICONTROL Index Name] innehåller produkterna eller innehållet.  Det här indexet används som standard. |
| [!UICONTROL User Token Data Element] | Det dataelement som returnerar användartoken. |
| [!UICONTROL Authenticated User Token Data Element] | Ange det dataelement som returnerar den autentiserade användartoken. |
| [!UICONTROL Currency Code] | Ange valutakoden i ISO-4217-format, t.ex. USD eller EUR. Det här fältet stöder dataelement. |

![](../../../images/extensions/client/algolia/configure.png)

## Åtgärdstyper för tillägg av insikter för [!DNL Algolia] {#action-types}

[!DNL Algolia] stöder en uppsättning fördefinierade standardhändelser, var och en med specifika kontexter och egenskaper. De åtgärder som är tillgängliga i tillägget [!DNL Algolia] är anpassade till de här händelsetyperna, vilket gör det enkelt att kategorisera och konfigurera händelserna som du skickar till [!DNL Algolia] utifrån deras typ.

### Läs in insikter {#load-insights}

>[!NOTE]
>
>I de flesta fall bör du läsa in [!DNL Algolia]-insikter på alla sidor på din webbplats.

Lägg till åtgärden **[!UICONTROL Load Insights]** i din taggregel var det lämpligaste för inläsning av [!DNL Algolia]-insikter baserat på regelkontext. Den här åtgärden läser in biblioteket `search-insights.js` på sidan.

Skapa en ny taggregel eller öppna en befintlig. Definiera villkoren enligt dina krav, välj sedan **[!UICONTROL Algolia]** som [!UICONTROL Extension] och välj **[!UICONTROL Load Insights]** som [!UICONTROL Action Type].

| Egenskap | Beskrivning |
| --- | --- |
| [!UICONTROL Insight Library Version] | [!DNL Algolia] Insights-versionen. Standardvärdet är `2.17.3`. |
| [!UICONTROL User Opt Out Data Element] | Det dataelement som fångar användarens spårningspreferens. |
| [!UICONTROL Use User Token Cookie] | Markera den här kryssrutan om du vill tillåta [!DNL Algolia] att generera en användartokencookie. Som standard är det här alternativet inställt på `true`. |

![](../../../images/extensions/client/algolia/load-insights.png)

### Klickat {#clicked}

Lägg till åtgärden **[!UICONTROL Click]** i taggregeln för att skicka klickade händelser till [!DNL Algolia]. Skapa en ny taggregel eller öppna en befintlig. Definiera villkoren enligt dina krav, välj sedan **[!UICONTROL Algolia]** som [!UICONTROL Extension] och välj **[!UICONTROL Clicked]** som [!UICONTROL Action Type].

| Egenskap | Beskrivning |
| --- | --- |
| [!UICONTROL Event Name] | Händelsenamnet som kan användas för att ytterligare förfina den här klickhändelsen. |
| [!UICONTROL Event Details Data Element] | Data Element returnerar händelseinformation i JSON-format, inklusive: <ul><li>`indexName`</li><li>`objectIDs`</li><li>`queryID` (valfritt)</li><li>`positions` (valfritt)</li><li>`price` (valfritt)</li><li>`quantity` (valfritt)</li><li>`discount` (valfritt)</li><li>`objectData` (valfritt)</li><li>`currency` (valfritt)</li></ul> |


>[!NOTE]
>
>Om både `queryID` och `positions` ingår, klassificeras händelsen som **objekt-ID:n som klickats efter sökning**. Annars klassas den som en **klickad objekt-ID** -händelse.
><br>
>Om dataelementet inte innehåller någon `indexName` används **standardindexnamn** när händelsen skickas.

![](../../../images/extensions/client/algolia/clicked.png)

Mer information om händelsekategorierna finns i [Klickade objekt-ID:n efter sökning](https://www.algolia.com/doc/api-reference/api-methods/clicked-object-ids-after-search/)
och [Handböcker för objekt-ID:n som klickats ](https://www.algolia.com/doc/api-reference/api-methods/clicked-object-ids/) .

### Konverterad {#converted}

Lägg till åtgärden **[!UICONTROL Converted]** i taggregeln för att skicka konverterade händelser till [!DNL Algolia]. Skapa en ny taggregel eller öppna en befintlig. Definiera villkoren enligt dina krav, välj sedan **[!UICONTROL Algolia]** som [!UICONTROL Extension] och välj **[!UICONTROL Converted]** som [!UICONTROL Action Type].

| Egenskap | Beskrivning |
| --- | --- |
| [!UICONTROL Event Name] | Händelsenamnet som ska användas för att ytterligare förfina den här **convert**-händelsen. |
| [!UICONTROL Event Details Data Element] | Dataelementet returnerar händelseinformation, inklusive: <ul><li>`indexName`</li><li>`objectIDs`</li><li>`queryID` (valfritt)</li><li>`recordID` (valfritt)</li></ul> |

>[!NOTE]
>
>Om dataelementet innehåller `queryId` klassas händelsen som **Konverterad efter sökning**. Annars kommer den att klassas som en **Konverterad**-händelse.
><br>
>Om dataelementet inte innehåller någon `indexName` används **standardindexnamn** när händelsen skickas.

![](../../../images/extensions/client/algolia/converted.png)

Mer information om händelsekategorierna finns i handböckerna [Konverterade objekt-ID:n efter sökning](https://www.algolia.com/doc/api-reference/api-methods/converted-object-ids-after-search/) och [Konverterade objekt-ID:n](https://www.algolia.com/doc/api-reference/api-methods/converted-object-ids/).

### Tillagd i kundvagnen {#added-to-cart}

Lägg till åtgärden **[!UICONTROL Added to Cart]** i taggregeln för att skicka tillagda i kundvagnshändelser till [!DNL Algolia]. Skapa en ny taggregel eller öppna en befintlig. Definiera villkoren enligt dina krav, välj sedan **[!UICONTROL Algolia]** som [!UICONTROL Extension] och välj **[!UICONTROL Added to cart]** som [!UICONTROL Action Type].

| Egenskap | Beskrivning |
| --- | --- |
| [!UICONTROL Event Name] | Händelsenamnet som ska användas för att ytterligare förfina den här **Lägg till i kundvagnen**. |
| [!UICONTROL Event Details Data Element] | Data Element returnerar händelseinformation i JSON-format, inklusive: <ul><li>`indexName`</li><li>`objectIDs`</li><li>`objectData`</li><li>`price`</li><li>`quantity`</li><li>`discount` (valfritt)</li><li>`queryID` (valfritt)</li><li>`currency` (valfritt)</li></ul>. |

>[!NOTE]
>
>Om dataelementet innehåller `queryId` kommer händelsen att klassas som **Added to cart object IDs after Search**. I annat fall kommer den att klassas som en **tillagd i cart-objekt-ID:n** .
><br>
>Om dataelementet inte innehåller någon `indexName` används **standardindexnamn** när händelsen skickas.
><br>
>Om standarddataelementen inte uppfyller dina krav kan ett anpassat dataelement skapas för att returnera den önskade händelseinformationen.

![](../../../images/extensions/client/algolia/added-to-cart.png)

Mer information om händelsekategorierna finns i [Added to cart object IDs after search](https://www.algolia.com/doc/api-reference/api-methods/added-to-cart-object-ids-after-search/) and [Added to cart object IDs](https://www.algolia.com/doc/api-reference/api-methods/added-to-cart-object-ids/) guides.

### Köpt {#purchased}

Lägg till åtgärden **[!UICONTROL Purchased]** i taggregeln för att skicka köpta händelser till [!DNL Algolia]. Skapa en ny taggregel eller öppna en befintlig. Definiera villkoren enligt dina krav, välj sedan **[!UICONTROL Algolia]** som [!UICONTROL Extension] och välj **[!UICONTROL Purchased]** som [!UICONTROL Action Type].

| Egenskap | Beskrivning |
| --- | --- |
| [!UICONTROL Event Name] | Händelsenamnet som ska användas för att ytterligare förfina den här **purchase**-händelsen. |
| [!UICONTROL Event Details Data Element] | Data Element returnerar händelseinformation i JSON-format, inklusive: <ul><li>`indexName`</li><li>`objectIDs`</li><li>`objectData`</li><li>`price`</li><li>`quantity`</li><li>`discount` (valfritt)</li><li>`queryID` (valfritt)</li><li>`currency` (valfritt)</li></ul>. |

>[!NOTE]
>
>Åtgärden Inköpt hämtar händelsedata från webbläsarlagringen baserat på det köpta artikel-ID:t. Om något av de köpta objekten innehåller `queryID` i sina lagrade data kommer händelsen att klassas som **Inköpta objekt-ID:n efter sökning**. Annars kommer den att klassas som en **Inköpt objekt-ID** -händelse.
><br>
>Med den här metoden kan köphändelsen automatiskt inkludera alla relevanta kontexter (fråge-ID, indexnamn, pris, kvantitet, rabatt) från användarens tidigare interaktioner med artiklarna.

![](../../../images/extensions/client/algolia/purchased.png)

Mer information om händelsekategorierna finns i [Inköpta objekt-ID:n efter sökning](https://www.algolia.com/doc/api-reference/api-methods/purchased-object-ids-after-search/)
och [ Inköpta objekt-ID:n ](https://www.algolia.com/doc/api-reference/api-methods/purchased-object-ids/) .

### Visad {#viewed}

Lägg till åtgärden **[!UICONTROL Viewed]** i taggregeln för att skicka köpta händelser till [!DNL Algolia]. Skapa en ny taggregel eller öppna en befintlig. Definiera villkoren enligt dina krav, välj sedan **[!UICONTROL Algolia]** som [!UICONTROL Extension] och välj **[!UICONTROL Viewed]** som [!UICONTROL Action Type].

| Egenskap | Beskrivning |
| --- | --- |
| [!UICONTROL Event Name] | Händelsenamnet som ska användas för att ytterligare förfina den här **vyn**-händelsen. |
| [!UICONTROL Event Details Data Element] | Data Element returnerar händelseinformation i JSON-format, inklusive: <ul><li>`indexName`</li><li>`objectIDs`</li></ul> |

>[!NOTE]
>
>Om dataelementet inte innehåller någon `indexName` används **standardindexnamn** när händelsen skickas.

![](../../../images/extensions/client/algolia/viewed.png)

Mer information om händelsen view finns i guiden [Visade objekt-ID](https://www.algolia.com/doc/api-reference/api-methods/viewed-object-ids/).

## Dataelement för [!DNL Algolia] Insights-tillägg {#data-elements}

[!DNL Algolia] har stöd för en uppsättning fördefinierade dataelement, där vart och ett har specifika kontexter och egenskaper. I följande avsnitt beskrivs de dataelement som är tillgängliga i [!DNL Algolia] Insights-tillägget.

### DataSet {#dataset}

DataSet Data Element hämtar data som är associerade med HTML-element, som sedan används i [!DNL Algolia]-åtgärder. Det här dataelementet lagrar automatiskt hämtade händelsedata i webbläsarlagringen för senare användning (t.ex. vid konverterings- eller köphändelser).

**Allmän konfiguration:**

| Egenskap | Beskrivning |
| --- | --- |
| [!UICONTROL Hit Element Div/Class Name] | HTML-elementnamnet och/eller CSS-klassnamnet som innehåller datauppsättningsattributen inklusive `data-insights-object-id` och eventuellt `data-insights-query-id` och `data-insights-position` i HTML-elementet. |
| [!UICONTROL Index Name Element Div/Class Name] | HTML-elementnamnet och/eller CSS-klassnamnet som har datauppsättningsattributen (`data-indexname`) i HTML-elementet. |

**Commerce-konfiguration (valfritt):**

| Egenskap | Beskrivning |
| --- | --- |
| [!UICONTROL Price Data Element] | Dataelement som returnerar priset för artikeln. Om det anges inkluderas detta i de lagrade händelsedata för e-handelshändelser. |
| [!UICONTROL Quantity Data Element] | Dataelement som returnerar kvantiteten för artikeln. Standardvärdet är 1 om inget anges. |
| [!UICONTROL Discount Data Element] | Dataelement som returnerar artikelns decimalrabattvärde. |
| [!UICONTROL Currency Code] | Valutakoden i ISO-4217-format. Om ingen valutakod anges används standardvalutan från tilläggskonfigurationen. |

**Åsidosättningar (valfritt):**

Med dessa fält kan du åsidosätta standardbeteendet för att hämta data från HTML-datauppsättningsattribut.

| Egenskap | Beskrivning |
| --- | --- |
| [!UICONTROL Record ID Data Element] | Åsidosätt standardmetoden för att använda sidans URL som post-ID. Post-ID används för att lagra och söka efter data som ska skickas till [!DNL Algolia] för den här produkten/sidan. |
| [!UICONTROL Query ID Data Element] | Fråge-ID hämtas från datauppsättningen i HTML-elementet. Om du vill åsidosätta detta beteende använder du den här egenskapen för att tillhandahålla ett dataelement som returnerar fråge-ID som en sträng. |
| [!UICONTROL Object IDs Data Element] | Objekt-ID:n hämtas från datauppsättningen i HTML-elementet. Om du vill åsidosätta det här beteendet använder du den här egenskapen för att tillhandahålla ett dataelement som returnerar objekt-ID:n som en array. |
| [!UICONTROL Positions Data Element] | Positionerna hämtas från datauppsättningen i HTML-elementet. Om du vill åsidosätta det här beteendet använder du den här egenskapen för att tillhandahålla ett dataelement som returnerar positionerna som en array. |
| [!UICONTROL Index Name Data Element] | Indexnamnet hämtas från datauppsättningen i HTML-elementet. Om du vill åsidosätta detta beteende använder du den här egenskapen för att ange ett dataelement som returnerar indexnamnet som en sträng. |

![](../../../images/extensions/client/algolia/dataset.png)

Detta dataelement returnerar:

```javascript
{
  timestamp,
  queryID,
  indexName,
  objectIDs,
  positions,
  objectData,  // Optional: commerce data if price is provided
  currency,    // Optional: if provided
  recordID
}
```

Ett exempel på HTML som innehåller datauppsättningen:

```html
<div data-indexname="acme_master_default_products" class="instant-search-comp__hits">
  <div class="hit-card"
    data-insights-object-id="${hit.objectID}"
    data-insights-position="${hit.__position}"
    data-insights-query-id="${hit.__queryID}">
    <h4 class="hit-name">...</h4>   
  </div>
</div>
```

### Frågesträng {#query-string}

Dataelementet för frågesträngen extraherar data från URL-frågesträngen som ska användas i [!DNL Algolia]-åtgärder.

| Egenskap | Beskrivning |
| --- | --- |
| [!UICONTROL Object ID Param Name] | Frågeparameternamnet som innehåller objekt-ID:t. |
| [!UICONTROL Index Name Param Name] | Frågeparameternamnet som innehåller indexnamnet. |
| [!UICONTROL Query ID Param Name] | Frågeparameternamnet som innehåller fråge-ID:t. |
| [!UICONTROL Position Param Name] | Frågeparameternamnet som innehåller positionen. |

![](../../../images/extensions/client/algolia/query-string.png)

Detta dataelement returnerar:

```javascript
{
  timestamp,
  queryID,
  indexName,
  objectIDs,
  positions
}
```

Ett exempel på HTML som innehåller frågeparametrar:

```html
<a href="product.html?objectID=${hit.objectID}&queryID=${hit.__queryID}&indexName=${indexName}&position=${hit.position}">Read More</a>
```

### Lagring {#storage}

Lagringsdataelementet hämtar data från webbläsarens sessionslagring för användning i [!DNL Algolia] åtgärder. Det här dataelementet kan även användas för att förstärka lagrade data med ytterligare e-handelsinformation.

Det här dataelementet hämtar händelseinformation som tidigare lagrats i sessionslager (vanligtvis av DataSet-dataelementet under klickningshändelser). Data tas automatiskt bort under konverteringshändelser om inte borttagningen uttryckligen inaktiveras.

**Åsidosättningar (valfritt):**

| Egenskap | Beskrivning |
| --- | --- |
| [!UICONTROL Record ID Data Element] | Post-ID används som nyckel för att söka efter händelsedata som lagras i webbläsarlagringen. Sidans URL är standardpost-ID. Om du vill åsidosätta detta beteende använder du den här egenskapen för att tillhandahålla ett dataelement som returnerar post-ID som en sträng. |
| [!UICONTROL Price Data Element] | Dataelement som returnerar priset för artikeln. Om detta anges uppdateras de lagrade händelsedata med prisinformation. |
| [!UICONTROL Quantity Data Element] | Dataelement som returnerar kvantiteten för artikeln. Om det anges uppdateras de lagrade händelsedata med kvantitetsinformation. |
| [!UICONTROL Discount Data Element] | Dataelement som returnerar artikelns decimalrabattvärde. Om detta anges uppdateras de lagrade händelsedata med rabattinformation. |
| [!UICONTROL Currency Code] | Ange valutakoden i ISO-4217-format. Om det anges uppdateras de lagrade händelsedata med valutainformation. |

![](../../../images/extensions/client/algolia/storage.png)

Det här dataelementet returnerar det som lagras i sessionslagringen, inklusive utökade handelsdata:

```javascript
{
  timestamp,
  queryID,
  indexName,
  objectIDs,
  positions,      // If available from original event
  objectData,     // Optional: commerce data if price is provided
  currency,       // Optional: if provided
  recordID
}
```

## Klickad eller konverterad efter sökning {#clicked-converted-after-search}

Händelserna *som klickats efter sökning* eller *Konverterats efter sökning* kräver `queryID` och `positions` krävs även för *klickade efter sökning*. De här egenskaperna är tillgängliga när flaggan `insights` aktiveras i parametrarna InstantSearch och/eller Autocomplete. Läs om följande resurser för att lära dig hur du konfigurerar insikter för din webbplats:

* [Ställa in insikter för Autocomplete](https://www.algolia.com/doc/ui-libraries/autocomplete/api-reference/autocomplete-js/autocomplete/#param-insights)
* [Ställa in insikter på InstantSearch.js](https://www.algolia.com/doc/guides/building-search-ui/events/js/#set-the-insights-option-to-true)
* [Kom igång med klicknings- och konverteringshändelser](https://www.algolia.com/doc/guides/sending-events/implementing/how-to/sending-events-backend/)
* [Skickar [!DNL Algolia] Insights-händelser](https://www.algolia.com/doc/ui-libraries/autocomplete/guides/sending-algolia-insights-events/)
* [[!DNL Algolia] Starta GitHub-databasen för tillägg](https://github.com/algolia/algolia-launch-extension)
* [InstantSearch.js-dokumentation](https://www.algolia.com/doc/guides/building-search-ui/what-is-instantsearch/js/)
* [[!DNL Algolia] API-dokumentation för insikter](https://www.algolia.com/doc/rest-api/insights/)
* [Algolia Launch Extension Code Repo](https://github.com/algolia/algolia-launch-extension)

## Nästa steg {#next-steps}

I den här guiden beskrivs hur du skickar data till [!DNL Algolia] med taggtillägget [!DNL Algolia Insights]. Om du planerar att även skicka händelser på serversidan till [!DNL Algolia] kan du nu fortsätta installera och konfigurera tillägget [[!DNL Conversions API] för vidarebefordran av händelser](../../server/algolia/overview.md).

Mer information om taggar i Experience Platform finns i [taggöversikten](../../../home.md).
