---
title: Adobe Analytics produktsträngstillägg - översikt
description: Läs mer om taggtillägget Adobe Analytics Product String i Adobe Experience Platform.
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---

# Översikt över Adobe Analytics produktsträngstillägg

>[!NOTE]
>
>Adobe Experience Platform Launch omdöms till en serie datainsamlingstekniker i Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad referens till terminologiska ändringar.

Variabeln `products` spårar hur användare interagerar med produkter på webbplatsen. Variabeln `products` kan t.ex. spåra hur många gånger en produkt visas, läggs till i kundvagnen, checkas ut och köpas. Det kan också spåra hur effektiva marknadsföringskategorierna är på er webbplats.

Variabeln `products` ska alltid anges tillsammans med en success-händelse.

Tillägget [!DNL Adobe Analytics Product String Builder] anger automatiskt variabeln `products` genom att slinga igenom datalagret, hämta alla nödvändiga produktrelaterade data och formatera dem med rätt syntax som visas nedan. Du behöver inte längre skriva och underhålla anpassad JavaScript för att utföra dessa komplexa åtgärder.

## Syntax för produktvariabeln

```bash
Category;Product;Quantity;Price;eventN=X|eventN2=X2;eVarN=merch_category|eVarN2=merch_category2
```

Fullständig dokumentation finns på [Produkter](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html).

## Tilläggsanvisningar

### Åtgärdskonfiguration

Lägg till åtgärden&quot;Adobe Analytics Product String - Set s.products&quot; i regeln.

![Åtgärdskonfiguration](./images/screenshot-action-config.png)

### Ställa in standardproduktdata

Definiera sedan datalagrets variabler. När du har konfigurerat åtgärden enligt föregående steg visas följande skärm:

![Standardfält](./images/screenshot-standard-fields.png)

För varje datapunkt som du vill ta med i produktsträngen anger du sökvägen till rätt datalagervariabel.

Om datalagret till exempel är strukturerat så här:

```json
digitalData = {
  "transaction": {
    "item": [{
      "productInfo": {
        "productName": "My Product"
      }
    }]
  }
};
```

Du anger följande sökväg i fältet Variabel för produkt-ID/namn för att hämta variabeln `productName`:

```json
digitalData.transaction.item.productInfo.productName
```

>[!NOTE]
>
>Om du använder ett dataelement för att fylla i fältet, bör det konfigureras med datatabellen Konstant eller Anpassad kod och måste returnera sökvägen ovan som en stränglitteral.

### Pristyp

Parametern `price` i [!DNL Adobe Analytics]-produktsträngen måste återspegla det totala priset för det antal enheter som köpts, inte enhetspriset, för den produkten. När du aktiverar fältet Pris i tilläggsåtgärden måste du ange om datalagret visar totalpriset eller enhetspriset. När du använder enhetspriset multiplicerar tillägget [!DNL Adobe Analytics Product String] automatiskt enhetspriset med kvantiteten för att få det totala priset och ange produktsträngen korrekt.

![Pristyp](./images/screenshot-price-type.png)

### Custom Events &amp; Merchandising eVars

![Event och eVars](./images/screenshot-events-evars.png)

Om implementeringen använder anpassade händelser eller eVars-produkter för marknadsföring gör du så här:

1. Markera den associerade **[!UICONTROL Add]**-knappen.
1. Välj den händelse eller eVar som du vill ange i listrutan.
1. Ange sökvägen till rätt datalagervariabel med samma syntax som beskrivs ovan.

### Åtgärdssekvens

Den här åtgärden måste åtföljas av en&quot;Adobe Analytics - Ange variabler&quot;-åtgärd som anger motsvarande lyckade händelser samt en&quot;Adobe Analytics - skicka Beacon&quot;-åtgärd. En lämplig sekvens av åtgärder visas nedan.

![Standardfält](./images/screenshot-price-type.png)

### Krav

* Ett objektbaserat [datalager](https://theblog.adobe.com/data-layers-buzzword-best-practice/) med variabler för alla produktrelaterade data (som produkt-ID, kvantitet, pris). Det här tillägget fungerar inte med arraybaserade datalager.
* Tillägget [Adobe Analytics](../analytics/overview.md) måste vara installerat.
