---
title: Översikt över vidarebefordran av händelser
description: Lär dig mer om vidarebefordran av händelser i Adobe Experience Platform, där du kan använda Platform Edge Network för att utföra uppgifter utan att ändra taggimplementeringen.
feature: Event Forwarding
exl-id: 18e76b9c-4fdd-4eff-a515-a681bc78d37b
source-git-commit: d48b746b477ffa6977ce04b72fe77e8ddb95d691
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---

# Översikt över vidarebefordran av händelser

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

Med händelsevidarebefordran i Adobe Experience Platform kan du skicka insamlade händelsedata till ett mål för bearbetning på serversidan. Vidarebefordran av händelser minskar webbsidans och appens vikt genom att använda Adobe Experience Platform Edge Network för att utföra åtgärder som normalt utförs på klienten. Regler för vidarebefordran av händelser implementeras på liknande sätt som taggar, och kan omvandla och skicka data till nya destinationer, men i stället för att skicka dessa data från ett klientprogram som en webbläsare skickas de från Adobe-servrar.

Det här dokumentet innehåller en översikt på hög nivå över vidarebefordran av händelser i Platform.

![Vidarebefordran av händelser i datainsamlingens ekosystem](../../../collection/images/home/event-forwarding.png)

>[!NOTE]
>
>Mer information om hur händelsevidarebefordran passar in i ekosystemet för datainsamling i Platform finns i [datainsamling - översikt](../../../collection/home.md).

Vidarebefordran av händelser i kombination med Adobe Experience Platform [Web SDK](../../../edge/home.md) och [Mobile SDK](https://aep-sdks.gitbook.io/docs/) ger följande fördelar:

**Prestanda**:

* ringa ett enda samtal från en sida som innehåller datanyttolast som sedan federeras på serversidan för att minska nätverkstrafiken på klientsidan och ge kunderna en snabbare upplevelse.
* Minska tiden det tar för webbsidor att läsas in för att förbättra webbplatsens prestanda.
* Minska antalet klienttekniker som krävs för att leverera din upplevelse och skicka data till många olika destinationer.

**Datastyrning**:

* Öka transparensen och kontrollera vilka data som skickas var i alla egenskaper.

## Skillnader mellan händelsevidarebefordran och taggar {#differences-from-tags}

Vid vidarebefordran av händelser används i stort sett samma koncept som taggar, till exempel [regler](../managing-resources/rules.md), [dataelement](../managing-resources/data-elements.md)och [tillägg](../managing-resources/extensions/overview.md). Den största skillnaden mellan de två kan sammanfattas enligt följande:

* Taggar **samlingar** händelsedata från en webbplats eller ett inbyggt mobilprogram och skickar dem till Platform Edge Network.
* Vidarebefordran av händelser **skickar** inkommande händelsedata från Platform Edge Network till en slutpunkt som representerar ett slutmål eller en slutpunkt som tillhandahåller data som du vill berika den ursprungliga nyttolasten med.

Medan taggar samlar in händelsedata direkt från din webbplats eller från ett mobilprogram som använder plattformens webb- och Mobile SDK:er, kräver händelsevidarebefordran att händelsedata redan skickas via Platform Edge Network för att kunna vidarebefordra dem till destinationer. Med andra ord måste du implementera Platform Web eller Mobile SDK på din digitala egendom (antingen via taggar eller med raw-kod) för att kunna använda händelsevidarebefordran.

### Egenskaper {#properties}

Händelsevidarebefordran upprätthåller ett eget lager med egenskaper som är åtskilda från taggar, som du kan visa i användargränssnittet för Experience Platform eller användargränssnittet för datainsamling genom att välja **[!UICONTROL Event Forwarding]** i den vänstra navigeringen.

![Egenskaper för vidarebefordran av händelser i användargränssnittet för datainsamling](../../images/ui/event-forwarding/overview/properties.png)

Alla egenskaper för händelsevidarebefordran **[!UICONTROL Edge]** som sin plattform. De skiljer inte mellan webb och mobiler eftersom de bara bearbetar data som tas emot från Platform Edge Network, som i sin tur kan ta emot händelsedata från både webb- och mobilplattformar.

### Tillägg {#extensions}

Vidarebefordran av händelser har en egen katalog med kompatibla tillägg, till exempel [Core](../../extensions/server/core/overview.md) tillägg och [Adobe Cloud Connector](../../extensions/server/cloud-connector/overview.md) tillägg. Du kan visa tillgängliga tillägg för egenskaper för vidarebefordran av händelser i användargränssnittet genom att välja **[!UICONTROL Extensions]** i den vänstra navigeringen, följt av **[!UICONTROL Catalog]**.

![Tillägg för vidarebefordran av händelser i användargränssnittet för datainsamling](../../images/ui/event-forwarding/overview/extensions.png)

### Dataelement {#data-elements}

De typer av dataelement som är tillgängliga vid händelsevidarebefordran är begränsade till katalogen med kompatibla [tillägg](#extensions) som ger dem.

Även om dataelementen själva skapas och konfigureras på samma sätt i händelsevidarebefordran som de är för taggar, finns det vissa viktiga syntaxskillnader när det gäller hur de refererar till data från Platform Edge Network.

#### Referera till data från Platform Edge Network {#data-element-path}

Om du vill referera till data från Platform Edge Network måste du skapa ett dataelement som ger en giltig sökväg till dessa data. När du skapar dataelementet i användargränssnittet väljer du **[!UICONTROL Core]** för tillägget och **[!UICONTROL Path]** för typen.

The **[!UICONTROL Path]** värdet för dataelementet måste följa mönstret `arc.event.{ELEMENT}` (till exempel: `arc.event.xdm.web.webPageDetails.URL`). Den här sökvägen måste anges korrekt för att data ska kunna skickas.

![Exempel på ett dataelement av typen path för händelsevidarebefordran](../../images/ui/event-forwarding/overview/data-reference.png)

### Regler {#rules}

Att skapa regler i egenskaper för händelsevidarebefordran fungerar på ungefär samma sätt som taggar, med den största skillnaden är att du inte kan välja händelser som regelkomponenter. I stället bearbetar en regel för vidarebefordran av händelser alla händelser som tas emot från [datastream](../../../edge/datastreams/overview.md) och vidarebefordrar dessa händelser till destinationer om vissa villkor är uppfyllda.

![Regler för vidarebefordran av händelser i användargränssnittet för datainsamling](../../images/ui/event-forwarding/overview/rules.png)

#### Tokenisering av dataelement {#tokenization}

I taggregler tokeniseras dataelement med en `%` i början och slutet av dataelementnamnet (till exempel: `%viewportHeight%`). I händelse av vidarebefordringsregler tokeniseras dataelement istället med `{{` i början och `}}` i slutet av dataelementnamnet (till exempel: `{{viewportHeight}}`).

![Exempel på ett dataelement av typen path för händelsevidarebefordran](../../images/ui/event-forwarding/overview/tokenization.png)

#### Regelåtgärdssekvens {#action-sequencing}

The [!UICONTROL Actions] -avsnittet i en regel för vidarebefordran av händelser körs alltid sekventiellt. Om en regel till exempel har två åtgärder kommer den andra åtgärden inte att starta körningen förrän den föregående åtgärden är slutförd (och i de fall där ett svar förväntas från en slutpunkt, har den slutpunkten svarat). Kontrollera att åtgärdsordningen är korrekt när du sparar en regel. Den här körningssekvensen kan inte köras asynkront på samma sätt som den kan med taggregler.

## Hemligheter {#secrets}

Med händelsevidarebefordran kan du skapa, hantera och lagra hemligheter som kan användas för att autentisera till de servrar som du skickar data till. Se guiden [hemligheter](./secrets.md) på olika typer av tillgängliga hemliga typer och hur de implementeras i användargränssnittet.

## Nästa steg

Det här dokumentet innehåller en introduktion på hög nivå till vidarebefordran av händelser. Mer information om hur du konfigurerar den här funktionen för din organisation finns i [komma igång-guide](./getting-started.md).
