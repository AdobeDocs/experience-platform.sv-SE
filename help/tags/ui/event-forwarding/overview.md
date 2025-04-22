---
title: Översikt över vidarebefordran av händelser
description: Lär dig mer om vidarebefordran av händelser i Adobe Experience Platform, där du kan använda Experience Platform Edge Network för att utföra uppgifter utan att ändra taggimplementeringen.
feature: Event Forwarding
exl-id: 18e76b9c-4fdd-4eff-a515-a681bc78d37b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1181'
ht-degree: 6%

---

# Översikt över vidarebefordran av händelser

>[!NOTE]
>
>Vidarebefordran är en betalfunktion som ingår i Adobe Real-Time Customer Data Platform Connections, Prime eller Ultimate.

>[!NOTE]
>
>Adobe Experience Platform Launch har omprofilerats till en serie tekniker för datainsamling i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar genomförts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad referens av terminologiändringarna.

Med händelsevidarebefordran i Adobe Experience Platform kan du skicka insamlade händelsedata till ett mål för bearbetning på serversidan. Vidarebefordran av händelser minskar webbsidans och appens vikt genom att använda Adobe Experience Platform Edge Network för att utföra åtgärder som normalt utförs på klienten. Regler för vidarebefordran av händelser implementeras på liknande sätt som taggar, och kan omvandla och skicka data till nya destinationer, men i stället för att skicka dessa data från ett klientprogram som en webbläsare skickas de från Adobe servrar.

Det här dokumentet innehåller en översikt över vidarebefordran av händelser i Experience Platform.

![Vidarebefordran av händelser i datainsamlingens ekosystem.](../../../collection/images/home/event-forwarding.png)

>[!NOTE]
>
>Information om hur händelsevidarebefordran passar in i datainsamlingens ekosystem i Experience Platform finns i [datainsamlingsöversikten](../../../collection/home.md).

Vidarebefordran av händelser i kombination med Adobe Experience Platform [Web SDK](/help/web-sdk/home.md) och [Mobile SDK](https://experienceleague.adobe.com/docs/platform-learn/data-collection/mobile-sdk/overview.html) ger följande fördelar:

**Prestanda**:

* ringa ett enda samtal från en sida som innehåller datanyttolast som sedan federeras på serversidan för att minska nätverkstrafiken på klientsidan och ge kunderna en snabbare upplevelse.
* Minska tiden det tar för webbsidor att läsas in för att förbättra webbplatsens prestanda.
* Minska antalet klienttekniker som krävs för att leverera din upplevelse och skicka data till många olika destinationer.

**Datastyrning**:

* Öka transparensen och kontrollera vilka data som skickas var i alla egenskaper.

## Skillnader mellan händelsevidarebefordran och taggar {#differences-from-tags}

I fråga om konfiguration används många av de begrepp som används för händelsevidarebefordran, till exempel [regler](../managing-resources/rules.md), [dataelement](../managing-resources/data-elements.md) och [tillägg](../managing-resources/extensions/overview.md). Den största skillnaden mellan de två kan sammanfattas enligt följande:

* Taggar **samlar in** händelsedata från en webbplats eller ett inbyggt mobilprogram och skickar dem till Experience Platform Edge Network.
* Händelsevidarebefordring **skickar** inkommande händelsedata från Experience Platform Edge Network till en slutpunkt som representerar ett slutligt mål eller en slutpunkt som tillhandahåller data som du vill utöka den ursprungliga nyttolasten med.

Taggar samlar in händelsedata direkt från er webbplats eller från mobilappar med Experience Platform Web och Mobile SDK, men för händelsevidarebefordran krävs att händelsedata redan skickas via Experience Platform Edge Network för att de ska kunna vidarebefordras till destinationer. Med andra ord måste du implementera Experience Platform Web eller Mobile SDK på din digitala egendom (antingen via taggar eller med råkod) för att kunna använda händelsevidarebefordran.

### Egenskaper {#properties}

Händelsevidarebefordran upprätthåller ett eget lager med egenskaper som är åtskilda från taggar, som du kan visa i användargränssnittet för Experience Platform eller användargränssnittet för datainsamling genom att välja **[!UICONTROL Event Forwarding]** i den vänstra navigeringen.

>[!TIP]
>
>Använd produkthjälpen i den högra panelen för att lära dig mer om vidarebefordran av händelser och visa ytterligare tillgängliga resurser.

![Egenskaper för vidarebefordran av händelser i användargränssnittet för datainsamling.](../../images/ui/event-forwarding/overview/properties.png)

Alla egenskaper för vidarebefordran av händelser listar **[!UICONTROL Edge]** som sin plattform. De skiljer inte mellan webb och mobiler eftersom de bara bearbetar data som tas emot från Experience Platform Edge Network, som i sin tur kan ta emot händelsedata från både webb- och mobilplattformar.

### Tillägg {#extensions}

Vidarebefordran av händelser har en egen katalog med kompatibla tillägg, till exempel tillägget [Core](../../extensions/server/core/overview.md) och tillägget [Adobe Cloud Connector](../../extensions/server/cloud-connector/overview.md). Du kan visa tillgängliga tillägg för egenskaper för vidarebefordran av händelser i användargränssnittet genom att välja **[!UICONTROL Extensions]** i den vänstra navigeringen, följt av **[!UICONTROL Catalog]**.

Du kan visa ytterligare tillgängliga resurser om du vill veta mer om den här funktionen genom att välja ![about](../../images/ui/event-forwarding/overview/about.png) i den högra panelen.

![Tillägg för vidarebefordran av händelser i användargränssnittet för datainsamling.](../../images/ui/event-forwarding/overview/extensions.png)

### Dataelement {#data-elements}

De typer av dataelement som är tillgängliga vid händelsevidarebefordran är begränsade till katalogen med kompatibla [tillägg](#extensions) som innehåller dem.

Även om dataelementen själva skapas och konfigureras på samma sätt i händelsevidarebefordran som de är för taggar, finns det viktiga syntaxskillnader när det gäller hur de refererar till data från Experience Platform Edge Network.

#### Referera till data från Experience Platform Edge Network {#data-element-path}

Om du vill referera till data från Experience Platform Edge Network måste du skapa ett dataelement som ger en giltig sökväg till dessa data. När du skapar dataelementet i användargränssnittet väljer du **[!UICONTROL Core]** som tillägg och **[!UICONTROL Path]** som typ.

Värdet **[!UICONTROL Path]** för dataelementet måste följa mönstret `arc.event.{ELEMENT}` (till exempel: `arc.event.xdm.web.webPageDetails.URL`). Den här sökvägen måste anges korrekt för att data ska kunna skickas.

Du kan visa ytterligare tillgängliga resurser om du vill veta mer om den här funktionen genom att välja ![about](../../images/ui/event-forwarding/overview/about.png) i den högra panelen.

![Exempel på ett dataelement av typen path för händelsevidarebefordran.](../../images/ui/event-forwarding/overview/data-reference.png)

### Regler {#rules}

Att skapa regler i egenskaper för händelsevidarebefordran fungerar på ungefär samma sätt som taggar, med den största skillnaden är att du inte kan välja händelser som regelkomponenter. I stället bearbetar en regel för vidarebefordran av händelser alla händelser som tas emot från [datastream](../../../datastreams/overview.md) och vidarebefordrar dessa händelser till mål om vissa villkor uppfylls.

Dessutom finns det en 30-sekunderstimeout som gäller för en enskild händelse när den bearbetas över alla regler (och därmed alla åtgärder) i en händelsevidarebefordringsegenskap. Det innebär att alla regler och alla åtgärder för en enskild händelse måste slutföras i den här tidsramen.

Du kan visa ytterligare tillgängliga resurser om du vill veta mer om den här funktionen genom att välja ![about](../../images/ui/event-forwarding/overview/about.png) i den högra panelen.

![Regler för vidarebefordran av händelser i användargränssnittet för datainsamling.](../../images/ui/event-forwarding/overview/rules.png)

#### Tokenisering av dataelement {#tokenization}

I taggregler tokeniseras dataelement med `%` i början och slutet av dataelementnamnet (till exempel: `%viewportHeight%`). I regler för vidarebefordran av händelser tokeniseras dataelement i stället med `{{` i början och `}}` i slutet av dataelementnamnet (till exempel: `{{viewportHeight}}`).

Du kan visa ytterligare tillgängliga resurser om du vill veta mer om den här funktionen genom att välja ![about](../../images/ui/event-forwarding/overview/about.png) i den högra panelen.

![Exempel på ett dataelement av typen path för händelsevidarebefordran.](../../images/ui/event-forwarding/overview/tokenization.png)

#### Regelåtgärdssekvens {#action-sequencing}

Avsnittet [!UICONTROL Actions] i en regel för vidarebefordran av händelser körs alltid sekventiellt. Om en regel till exempel har två åtgärder kommer den andra åtgärden inte att starta körningen förrän den föregående åtgärden är slutförd (och i de fall där ett svar förväntas från en slutpunkt har den slutpunkten svarat). Kontrollera att åtgärdsordningen är korrekt när du sparar en regel. Den här körningssekvensen kan inte köras asynkront på samma sätt som den kan med taggregler.

## Hemligheter {#secrets}

Med händelsevidarebefordran kan du skapa, hantera och lagra hemligheter som kan användas för att autentisera till de servrar som du skickar data till. Se guiden om [hemligheter](./secrets.md) om de olika typerna av tillgängliga hemligheter och hur de implementeras i användargränssnittet.

## Videoöversikt {#video}

Följande video är tänkt att hjälpa dig att förstå händelsevidarebefordran och Real-Time CDP-anslutningar bättre.

>[!VIDEO](https://video.tv.adobe.com/v/3429308)

## Nästa steg

Det här dokumentet innehåller en introduktion på hög nivå till vidarebefordran av händelser. Mer information om hur du konfigurerar den här funktionen för din organisation finns i guiden [Komma igång](./getting-started.md).
