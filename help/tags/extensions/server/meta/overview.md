---
title: Översikt över API-tillägg för metakonvertering
description: Läs mer om Meta Conversions API-tillägget för händelsevidarebefordran i Adobe Experience Platform.
exl-id: 6b5836d6-6674-4978-9165-0adc1d7087b7
source-git-commit: f7fdfbf9afcecb255668d5d6393b87918114b067
workflow-type: tm+mt
source-wordcount: '2432'
ht-degree: 0%

---

# [!DNL Meta Conversions API] tilläggsöversikt

The [[!DNL Meta Conversions API]](https://developers.facebook.com/docs/marketing-api/conversions-api/) kan ni koppla marknadsföringsdata på serversidan till [!DNL Meta] för att optimera er annonsinriktning, minska kostnaden per åtgärd och mäta resultaten. Händelser är länkade till en [[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) ID och behandlas på ett liknande sätt som händelser på klientsidan.

Använda [!DNL Meta Conversions API] kan du utnyttja API:ts funktioner i [händelsevidarebefordran](../../../ui/event-forwarding/overview.md) regler att skicka data till [!DNL Meta] från Adobe Experience Platform Edge Network. Det här dokumentet beskriver hur du installerar tillägget och använder dess funktioner vid en händelsevidarebefordring [regel](../../../ui/managing-resources/rules.md).

## Demo

Följande video är avsedd att ge stöd för din förståelse av [!DNL Meta Conversions API].

>[!VIDEO](https://unlockmarketingdata.com/video-meta-conversions-api)

## Förutsättningar

Vi rekommenderar starkt att du använder [!DNL Meta Pixel] och [!DNL Conversions API] för att dela och skicka samma händelser från klienten respektive serversidan, eftersom detta kan hjälpa till att återställa händelser som inte plockats upp av [!DNL Meta Pixel]. Innan du installerar [!DNL Conversions API] -tillägget, se guiden på [[!DNL Meta Pixel] extension](../../client/meta/overview.md) om du vill ha steg för hur du kan integrera det i implementeringar av taggar på klientsidan.

>[!NOTE]
>
>Avsnittet på [deduplicering av händelser](#deduplication) längre fram i det här dokumentet beskriver stegen för att säkerställa att samma händelse inte används två gånger, eftersom den kan tas emot både från webbläsaren och servern.

För att kunna använda [!DNL Conversions API] måste du ha tillgång till händelsevidarebefordran och ha en giltig [!DNL Meta] konto med tillgång till [!DNL Ad Manager] och [!DNL Event Manager]. Du måste kopiera ID:t för en befintlig [[!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755?id=1205376682832142) (eller [skapa en ny [!DNL Pixel]](https://www.facebook.com/business/help/952192354843755) i stället) så att tillägget kan konfigureras för ditt konto.

>[!INFO]
>
>Om du tänker använda det här tillägget med mobilappsdata, eller om du även arbetar med offlinehändelsedata i [!DNL Meta] -kampanjer måste ni skapa datauppsättningen via en befintlig app och välja **Skapa från ett pixel-ID** när du uppmanas till det. Se artikeln [Bestäm vilket datamängdsalternativ som passar ditt företag](https://www.facebook.com/business/help/5270377362999582?id=490360542427371) för mer information. Se [Konverterings-API för apphändelser](https://developers.facebook.com/docs/marketing-api/conversions-api/app-events) för alla obligatoriska och valfria parametrar för appspårning.

## Installera tillägget

Installera [!DNL Meta Conversions API] navigerar du till användargränssnittet för datainsamling eller användargränssnittet för Experience Platform och väljer **[!UICONTROL Event Forwarding]** från vänster navigering. Här väljer du en egenskap som tillägget ska läggas till i eller skapar en ny egenskap i stället.

När du har valt eller skapat den önskade egenskapen väljer du **[!UICONTROL Extensions]** i den vänstra navigeringen väljer du **[!UICONTROL Catalog]** -fliken. Sök efter [!UICONTROL Meta Conversions API] kort, välj **[!UICONTROL Install]**.

![The [!UICONTROL Install] det alternativ som väljs för [!UICONTROL Meta Conversions API] i användargränssnittet för datainsamling.](../../../images/extensions/server/meta/install.png)

I konfigurationsvyn som visas måste du ange [!DNL Pixel] ID som du kopierade tidigare för att länka tillägget till ditt konto. Du kan klistra in ID:t direkt i indata eller använda ett dataelement i stället.

Du måste också ange en åtkomsttoken för att kunna använda [!DNL Conversions API] specifikt. Se [!DNL Conversions API] dokumentation om [generera en åtkomsttoken](https://developers.facebook.com/docs/marketing-api/conversions-api/get-started#access-token) om du vill se steg för hur du får fram det här värdet.

När du är klar väljer du **[!UICONTROL Save]**

![The [!DNL Pixel] ID som anges som ett dataelement i tilläggskonfigurationsvyn.](../../../images/extensions/server/meta/configure.png)

Tillägget är installerat och du kan nu använda dess funktioner i reglerna för vidarebefordran av händelser.

## Integrering med Meta Business Extension (MBE) {#mbe}

Tack vare integreringen med MBE (Meta Business Extensions) kan du snabbt autentisera med ditt Meta Business Account. Detta fyller sedan i [!UICONTROL Pixel ID] och Meta Conversions API [!UICONTROL Access Token], vilket gör det enklare att installera och konfigurera API:t för metakonvertering.

En dialogruta för autentisering i MBE visas när du installerar [!UICONTROL Meta Conversions API] tillägg.

![The [!UICONTROL Meta Conversions API Extension] markering av installationssidor [!UICONTROL Connect to Meta].](../../../images/extensions/server/meta/mbe-extension-install.png)

En dialogruta för att autentisera i MBE visas också i snabbstartsgränssnittet vid vidarebefordran av händelser.

![Gränssnittet för snabbstartsarbetsflödet [!UICONTROL Connect to Meta].](../../../images/extensions/server/meta/mbe-extension-quick-start.png)

## Integrering med EMQ (Event Quality Match Score) {#emq}

Integrationen med EMQ (Event Quality Match Score) gör att du enkelt kan se hur effektiv implementeringen är genom att visa EMQ-poäng. Den här integreringen minimerar kontextväxling och hjälper dig att förbättra framgången för implementeringarna av Meta Conversions API. De här händelserumren visas i [!UICONTROL Meta Conversions API extension] konfigurationsskärmen.

![The [!UICONTROL Meta Conversions API Extension] markering av konfigurationssida [!UICONTROL View EMQ Score].](../../../images/extensions/server/meta/emq-score.png)

## Integrering med LiveRamp (Alpha) {#alpha}

[!DNL LiveRamp] kunder som har [!DNL LiveRamp]ATS (Authenticated Traffic Solution) som distribueras på deras webbplatser kan välja att dela RampID:n som en kundinformationsparameter. Var vänlig och arbeta med [!DNL Meta] kontoteam för att gå med i Alpha för den här funktionen.

![Vidarebefordran av Meta-händelser [!UICONTROL Rule] markering av konfigurationssida [!UICONTROL Partner Name (alpha)] och [!UICONTROL Partner ID (alpha)].](../../../images/extensions/server/meta/live-ramp.png)

## Konfigurera en regel för vidarebefordran av händelser {#rule}

I det här avsnittet beskrivs hur du använder [!DNL Conversions API] tillägg i en allmän regel för vidarebefordran av händelser. I praktiken bör du konfigurera flera regler för att skicka alla godkända [standardhändelser](https://developers.facebook.com/docs/meta-pixel/reference) via [!DNL Meta Pixel] och [!DNL Conversions API]. Information om mobilappsdata finns i obligatoriska fält, appdatafält, kundinformationsparametrar och anpassad datainformation [här](https://developers.facebook.com/docs/marketing-api/conversions-api/app-events).

>[!NOTE]
>
>Händelser bör vara [skickas i realtid](https://www.facebook.com/business/help/379226453470947?id=818859032317965) eller så nära realtid som möjligt för bättre optimering av annonskampanjer.

Börja skapa en ny regel för vidarebefordring av händelser och konfigurera villkoren efter behov. När du väljer åtgärder för regeln väljer du **[!UICONTROL Meta Conversions API Extension]** för tillägget väljer du **[!UICONTROL Send Conversions API Event]** för åtgärdstypen.

![The [!UICONTROL Send Page View] åtgärdstypen som väljs för en regel i användargränssnittet för datainsamling.](../../../images/extensions/server/meta/select-action.png)

Det visas kontroller som gör att du kan konfigurera händelsedata som ska skickas till [!DNL Meta] via [!DNL Conversions API]. Dessa alternativ kan anges direkt i de angivna inmatningarna eller så kan du välja befintliga dataelement som ska representera värdena i stället. Konfigurationsalternativen är uppdelade i fyra huvudavsnitt enligt nedan.

| Konfig.avsnitt | Beskrivning |
| --- | --- |
| [!UICONTROL Server Event Parameters] | Allmän information om händelsen, inklusive tidpunkten då den inträffade och källåtgärden som utlöste den. Se [!DNL Meta] utvecklardokumentation för mer information om [standardhändelseparametrar](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event) som godkänts av [!DNL Conversions API].<br><br>Om du använder båda [!DNL Meta Pixel] och [!DNL Conversions API] om du vill skicka händelser, se till att inkludera både en **[!UICONTROL Event Name]** (`event_name`) och **[!UICONTROL Event ID]** (`event_id`) med varje händelse eftersom dessa värden används för [deduplicering av händelser](#deduplication).<br><br>Du kan också välja att **[!UICONTROL Enable Limited Data Use]** för att hjälpa till att följa kundernas avval. Se [!DNL Conversions API] dokumentation om [databearbetningsalternativ](https://developers.facebook.com/docs/marketing-apis/data-processing-options/) för mer information om den här funktionen. |
| [!UICONTROL Customer Information Parameters] | Användar-ID-data som används för att tilldela händelsen till en kund. Vissa av dessa värden måste hashas innan de kan skickas till API:t.<br><br>För att säkerställa en bra gemensam API-anslutning och hög händelsematchningskvalitet (EMQ) rekommenderar vi att du skickar alla [godkända parametrar för kundinformation](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/customer-information-parameters) tillsammans med serverhändelser. Dessa parametrar bör också [prioriterad baserat på deras betydelse och inverkan på det europeiska folkhälsoområdet](https://www.facebook.com/business/help/765081237991954?id=818859032317965). |
| [!UICONTROL Custom Data] | Ytterligare data som ska användas för annonsleveransoptimering, tillhandahålls i form av ett JSON-objekt. Se [[!DNL Conversions API] dokumentation](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/custom-data) om du vill ha mer information om godkända egenskaper för det här objektet.<br><br>Om du skickar en köphändelse måste du använda det här avsnittet för att ange de attribut som krävs `currency` och `value`. |
| [!UICONTROL Test Event] | Det här alternativet används för att verifiera om konfigurationen gör att serverhändelser tas emot av [!DNL Meta] som förväntat. Om du vill använda den här funktionen väljer du **[!UICONTROL Send as Test Event]** och ange sedan en testhändelsekod i indata nedan. När regeln för vidarebefordran av händelser har distribuerats och du har konfigurerat tillägget och åtgärden korrekt, bör du se aktiviteter som visas i **[!DNL Test Events]** visa i [!DNL Meta Events Manager]. |

{style="table-layout:auto"}

När du är klar väljer du **[!UICONTROL Keep Changes]** för att lägga till åtgärden i regelkonfigurationen.

![[!UICONTROL Keep Changes] väljs för åtgärdskonfigurationen.](../../../images/extensions/server/meta/keep-changes.png)

När du är nöjd med regeln väljer du **[!UICONTROL Save to Library]**. Publicera slutligen en ny händelsevidarebefordring [bygg](../../../ui/publishing/builds.md) för att aktivera ändringar som gjorts i biblioteket.

## Borttagning av händelser {#deduplication}

Som nämndes i [kravsektion](#prerequisites)rekommenderar vi att du använder båda [!DNL Meta Pixel] taggtillägg och [!DNL Conversions API] tillägg för händelsevidarebefordran för att skicka samma händelser från klienten och servern i en redundant konfiguration. Detta kan hjälpa till att återställa händelser som inte har hämtats av ett tillägg eller av ett annat.

Om du skickar olika händelsetyper från klienten och servern utan överlappning mellan de båda behöver du inte deduplicera. Om en enda händelse delas av båda [!DNL Meta Pixel] och [!DNL Conversions API]måste du se till att dessa redundanta händelser dedupliceras så att rapporteringen inte påverkas negativt.

När du skickar delade händelser måste du se till att du inkluderar ett händelse-ID och namn för varje händelse som du skickar från både klienten och servern. När flera händelser med samma ID och namn tas emot, [!DNL Meta] använder automatiskt flera strategier för att deduplicera dem och behålla de mest relevanta data. Se [!DNL Meta] dokumentation om [deduplicering för [!DNL Meta Pixel] och [!DNL Conversions API] händelser](https://www.facebook.com/business/help/823677331451951?id=1205376682832142) om du vill ha mer information om processen.

## Snabbstartarbetsflöde: API-tillägg för metakonveringar (beta) {#quick-start}

>[!IMPORTANT]
>
>* Snabbstartsfunktionen är tillgänglig för kunder som har köpt Real-Time CDP Prime- och Ultimate-paketet. Kontakta din Adobe-representant om du vill ha mer information.
>* Den här funktionen är avsedd för nya implementeringar och stöder för närvarande inte automatisk installation av tillägg och konfigurationer i befintliga taggar och egenskaper för händelsevidarebefordran.

>[!NOTE]
>
>Alla befintliga klienter kan använda snabbstartsarbetsflödena för att skapa en referensimplementering som kan användas för följande:
>* Använd det som början på en helt ny implementering.
>* Utnyttja det som en referensimplementering som du kan undersöka för att se hur det har konfigurerats och sedan replikera i dina nuvarande produktionsimplementationer.

Med snabbstartsfunktionen blir det enklare och effektivare att konfigurera med Meta Conversions API och Meta Pixel-tilläggen. Det här verktyget automatiserar flera steg som utförs i taggar för Adobe och vidarebefordran av händelser, vilket avsevärt minskar konfigurationstiden.

Den här funktionen installerar och konfigurerar automatiskt både Meta Conversion API och Meta Pixel-tilläggen på en nyligen genererad tagg och händelsevidarebefordringsegenskap med nödvändiga regler och dataelement. Dessutom installeras och konfigureras Experience Platform Web SDK och Datastream automatiskt. Slutligen publicerar snabbstartsfunktionen automatiskt biblioteket till den angivna URL:en i en utvecklingsmiljö, vilket möjliggör datainsamling på klientsidan och vidarebefordran av händelser på serversidan i realtid via händelsevidarebefordring och Experience Platform Edge Network.

I följande video visas en introduktion till snabbstartsfunktionen.

>[!VIDEO](https://video.tv.adobe.com/v/3416939?quality=12&learn=on)

### Installera snabbstartsfunktion

>[!NOTE]
>
>Den här funktionen är utformad för att hjälpa dig att komma igång med en implementering av vidarebefordran av händelser. Den ger inte en komplett, fullt funktionell implementering som passar alla användningsfall.

Den här installationen installerar både Meta Conversion API och Meta Pixel-tilläggen automatiskt. Den här hybridimplementeringen rekommenderas av Meta för att samla in och vidarebefordra händelsekonverteringar på serversidan.
Snabbinstallationsfunktionen är utformad för att hjälpa kunderna att komma igång med en händelsevidarebefordringsimplementering och är inte avsedd att leverera en heltäckande, fullt fungerande implementering som passar alla användningsfall.

Installera funktionen genom att välja **[!UICONTROL Get Started]** for **[!DNL Send Conversions Data to Meta]** om Adobe Experience Platform Data Collection **[!UICONTROL Home]** sida.

![Startsida för datainsamling som visar konverteringsdata till metadata](../../../images/extensions/server/meta/conversion-data-to-meta.png)

Ange **[!UICONTROL Domain]** väljer **[!UICONTROL Next]**. Den här domänen kommer att användas som namngivningskonvention för dina automatiskt genererade taggar och egenskaper för händelsevidarebefordran, regler, dataelement, datastreams osv.

![Välkomstskärmen begär domännamn](../../../images/extensions/server/meta/welcome.png)

I **[!UICONTROL Initial Setup]** genom att **[!UICONTROL Meta Pixel ID]**, **[!UICONTROL Meta Conversion API Access Token]** och **[!UICONTROL Data Layer Path]** väljer **[!UICONTROL Next]**.

![Inledande installationsdialogruta](../../../images/extensions/server/meta/initial-setup.png)

Tillåt några minuter innan den första installationsprocessen är klar och välj sedan **[!UICONTROL Next]**.

![Bekräftelseskärmen för den första konfigurationen slutförd](../../../images/extensions/server/meta/setup-complete.png)

Från **[!UICONTROL Add Code on Your Site]** kopierar koden som anges med kopian ![Kopiera](../../../images/extensions/server/meta/copy-icon.png) funktionen och klistra in den i `<head>` på källwebbplatsen. När implementeringen är klar väljer du **[!UICONTROL Start Validation]**

![Lägga till kod i webbplatsdialogrutan](../../../images/extensions/server/meta/add-code-on-your-site.png)

The [!UICONTROL Validation Results] visas implementeringsresultatet för metatillägget. Välj **[!UICONTROL Next]**. Du kan även se ytterligare valideringsresultat genom att välja **[!UICONTROL Assurance]** länk.

![Dialogrutan Testresultat visar implementeringsresultat](../../../images/extensions/server/meta/test-results.png)

The **[!UICONTROL Next Steps]** skärmvisningen bekräftar att installationen har slutförts. Härifrån har du möjlighet att optimera implementeringen genom att lägga till nya händelser, som visas i nästa avsnitt.

Om du inte vill lägga till fler händelser väljer du **[!UICONTROL Close]**.

![Dialogrutan Nästa steg](../../../images/extensions/server/meta/next-steps.png)

#### Lägga till ytterligare händelser

Välj om du vill lägga till nya händelser **[!UICONTROL Edit Your Tags Web Property]**.

![Dialogrutan Nästa steg som visar hur du redigerar din tagg för webbegenskaper](../../../images/extensions/server/meta/edit-your-tags-web-property.png)

Markera den regel som motsvarar metahändelsen som du vill redigera. Till exempel: **MetaConversion_AddToCart**.

>[!NOTE]
>
>Om det inte finns någon händelse körs inte den här regeln. Detta gäller alla regler med **MetaConversion_PageView** undantagsregeln.

Lägg till en händelse genom att välja **[!UICONTROL Add]** under [!UICONTROL Events] rubrik.

![Taggegenskapssida som inte visar några händelser](../../../images/extensions/server/meta/edit-rule.png)

Markera [!UICONTROL Event Type]. I det här exemplet har vi valt [!UICONTROL Click] -händelsen och konfigurerade den att utlösas när **.add-to-cart-button** är markerat. Välj **[!UICONTROL Keep Changes]**.

![Händelsekonfigurationsskärmen visar klickningshändelse](../../../images/extensions/server/meta/event-configuration.png)

Den nya händelsen har sparats. Välj **[!UICONTROL Select a working library]** och välj det bibliotek som du vill bygga till.

![Välj en arbetsbibliotekslistruta](../../../images/extensions/server/meta/working-library.png)

Välj sedan listrutan bredvid **[!UICONTROL Save to Library]** och markera **[!UICONTROL Save to Library and Build]**. Ändringen publiceras i biblioteket.

![Välj Spara i bibliotek och bygg](../../../images/extensions/server/meta/save-and-build.png)

Upprepa dessa steg för alla andra metakonverteringshändelser som du vill konfigurera.

#### Datalagerkonfiguration {#configuration}

>[!IMPORTANT]
>
>Hur du uppdaterar det här globala datalagret beror på webbplatsens arkitektur. Ett program med en enda sida skiljer sig från ett återgivningsprogram på serversidan. Det är också möjligt att du har det fulla ansvaret för att skapa och uppdatera dessa data i Tags-produkten. I samtliga fall måste datalagret uppdateras i mellan varje gång du kör `MetaConversion_* rules`. Om du inte uppdaterar data mellan regler kan du även stöta på ett fall där du skickar inaktuella data från den senaste `MetaConversion_* rule` i aktuell `MetaConversion_* rule`.

Under konfigurationen tillfrågades du var datalagret finns. Som standard är detta `window.dataLayer.meta`och i `meta` -objektet, förväntas dina data enligt nedan.

![Information om datalagrets metadata](../../../images/extensions/server/meta/data-layer-meta.png)

Detta är viktigt att förstå `MetaConversion_*` regeln använder den här datastrukturen för att skicka relevanta datadelar till [!DNL Meta Pixel] tillägg och [!DNL Meta Conversions API]. Mer information finns i dokumentationen om [standardhändelser](https://developers.facebook.com/docs/meta-pixel/reference#standard-events) för mer information om vilka data olika metahändelser kräver.

Om du till exempel vill använda `MetaConversion_Subscribe` regel, du måste uppdatera `window.dataLayer.meta.currency`, `window.dataLayer.meta.predicted_ltv`och `window.dataLayer.meta.value` enligt objektegenskaperna som beskrivs i dokumentationen om [standardhändelser](https://developers.facebook.com/docs/meta-pixel/reference#standard-events).

Nedan visas ett exempel på vad som behöver köras på en webbplats för att datalagret ska uppdateras innan regeln körs.

![Uppdatera datalagrets metainformation](../../../images/extensions/server/meta/update-data-layer-meta.png)

Som standard är `<datalayerpath>.conversionData.eventId` genereras slumpmässigt av åtgärden&quot;Generera nytt händelse-ID&quot; på någon av `MetaConversion_* rules`.

Om du vill ha en lokal referens om hur datalagret ska se ut kan du öppna den anpassade kodredigeraren på `MetaConversion_DataLayer` dataelement på din egenskap.

## Nästa steg

I den här guiden beskrivs hur du skickar händelsedata på serversidan till [!DNL Meta] med [!DNL Meta Conversions API] tillägg. Härifrån rekommenderar vi att du utökar integreringen genom att ansluta mer [!DNL Pixels] och dela med dig av fler händelser när det är tillämpligt. Om du gör något av följande kan du förbättra din annonsering ytterligare:

* Anslut andra [!DNL Pixels] som ännu inte är anslutna till en [!DNL Conversions API] integrering.
* Om du skickar vissa händelser exklusivt via [!DNL Meta Pixel] på klientsidan skickar du samma händelser till [!DNL Conversions API] även från serversidan.

Se [!DNL Meta] dokumentation om [de bästa sätten för [!DNL Conversions API]](https://www.facebook.com/business/help/308855623839366?id=818859032317965) om du vill ha mer information om hur ni kan implementera er integrering på ett effektivt sätt. Mer allmän information om taggar och vidarebefordran av händelser i Adobe Experience Cloud finns i [taggöversikt](../../../home.md).
