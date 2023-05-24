---
keywords: Experience Platform;komma igång;Attribution ai;populära topics;Attribution ai input;Attribution ai output;
feature: Attribution AI
title: Indata och utdata i Attribution AI
description: Följande dokument visar de olika indata och utdata som används i Attribution AI.
exl-id: d6dbc9ee-0c1a-4a5f-b922-88c7a36a5380
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '2497'
ht-degree: 0%

---

# Indata och utdata i [!DNL Attribution AI]

Följande dokument visar de olika indata och utdata som används i [!DNL Attribution AI].

## [!DNL Attribution AI] indata

Attribution AI arbetar genom att analysera följande datauppsättningar för att beräkna algoritmiska poäng:

- Adobe Analytics datasets med [Källanslutning för analyser](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Experience Event-datauppsättningar (EE) i allmänhet från Adobe Experience Platform-schema
- CEE-datauppsättningar (Consumer Experience Event)

Nu kan du lägga till flera datauppsättningar från olika källor baserat på **identitetskarta** (fält) om var och en av datauppsättningarna har samma identitetstyp (namnutrymme), t.ex. ett ECID. När du har valt en identitet och ett namnutrymme visas ID-kolumnens fullständighetsmått som anger den datavolym som sammanfogas. Mer information om hur du lägger till flera datauppsättningar finns på [Användarhandbok för Attribution AI](./user-guide.md#identity).

Kanalinformationen mappas inte alltid som standard. I vissa fall, om mediaChannel (field) är tom, kan du inte&quot;fortsätta&quot; förrän du mappar ett fält till mediaChannel som det är en obligatorisk kolumn. Om kanalen identifieras i datauppsättningen mappas den som standard till mediaChannel. Andra kolumner som **medietyp** och **medieåtgärd** är fortfarande valfria.

När du har mappat kanalfältet fortsätter du till steget &#39;Definiera händelser&#39; där du kan välja konverteringshändelser, kontakthändelser och välja specifika fält från enskilda datauppsättningar.

>[!IMPORTANT]
>
>Adobe Analytics källanslutning kan ta upp till fyra veckor att fylla i data baklänges. Om du nyligen har konfigurerat en koppling bör du kontrollera att datauppsättningen har den minsta datalängd som krävs för Attribution AI. Granska [historiska data](#data-requirements) -sektion för att verifiera att du har tillräckligt med data för att beräkna exakta algoritmiska poäng.

Mer information om hur du ställer in [!DNL Consumer Experience Event] (CEE), se [Förberedelse av data för Intelligent Services](../data-preparation.md) guide. Mer information om att mappa Adobe Analytics-data finns på [Mappningar av analysfält](../../sources/connectors/adobe-applications/analytics.md) dokumentation.

Inte alla kolumner i [!DNL Consumer Experience Event] (CEE)-schema är obligatoriskt för Attribution AI.

Du kan konfigurera kontaktpunkterna med hjälp av de fält som rekommenderas nedan i schemat eller den valda datauppsättningen.

| Rekommenderade kolumner | Behövs för |
| --- | --- |
| Primärt identitetsfält | Pekpunkt/konvertering |
| Tidsstämpel | Pekpunkt/konvertering |
| Kanal._type | Pekpunkt |
| Channel.mediaAction | Pekpunkt |
| Channel.mediaType | Pekpunkt |
| Marketing.trackingCode | Pekpunkt |
| Marketing.campaignname | Pekpunkt |
| Marketing.campaigngroup | Pekpunkt |
| Commerce | Konvertering |

Attributen körs vanligtvis på konverteringskolumner som order, inköp och utcheckningar under&quot;handel&quot;. Kolumnerna för&quot;channel&quot; och&quot;marketing&quot; används för att definiera kontaktytor för Attribution AI (till exempel `channel._type = 'https://ns.adobe.com/xdm/channel-types/email'`). För optimala resultat och insikter rekommenderar vi att du inkluderar så många konverterings- och kontaktpunktskolumner som möjligt. Dessutom är du inte begränsad till bara de ovanstående kolumnerna. Du kan inkludera andra rekommenderade eller anpassade kolumner som en konvertering eller kontaktytpunktsdefinition.

Experience event-datauppsättningar behöver inte uttryckligen ha Channel- och Marketing-mixins så länge som den kanal- eller kampanjinformation som är relevant för att konfigurera en kontaktyta finns i något av mixin- eller vidarekopplingsfälten.

>[!TIP]
>
>Om du använder Adobe Analytics-data i ditt CEE-schema, lagras kontaktpunktsinformationen för Analytics vanligtvis i `channel.typeAtSource` (t.ex. `channel.typeAtSource = 'email'`).

## Historiska data {#data-requirements}

>[!IMPORTANT]
>
> Den minsta mängden data som behövs för att Attribution AI ska fungera är följande:
> - Du måste tillhandahålla minst 3 månaders (90 dagar) data för att kunna köra en bra modell.
> - Du behöver minst 1 000 konverteringar.


Attribution AI kräver historiska data som underlag för modellutbildning. Den datalängd som krävs bestäms huvudsakligen av två huvudfaktorer: utbildningsfönster och kontrollfönster. Indata med kortare utbildningsfönster är mer känsliga för aktuella trender, medan längre utbildningsfönster hjälper till att skapa mer stabila och korrekta modeller. Det är viktigt att modellera målet med historiska data som bäst motsvarar era affärsmål.

The [konfiguration av utbildningsfönster](./user-guide.md#training-window) filterkonverteringshändelser som ska inkluderas för modellutbildning baserat på förekomsttid. För närvarande är den kortaste utbildningstiden 1 fjärdedel (90 dagar). The [uppslagsfönster](./user-guide.md#lookback-window) I finns en tidsram som anger hur många dagar före konverteringshändelsen som kontaktytor för den här konverteringshändelsen ska inkluderas. Dessa två begrepp avgör tillsammans mängden indata (mätt i dagar) som krävs för ett program.

Som standard definierar Attribution AI utbildningsfönstret som de senaste 2 kvartalen (6 månader) och uppslagsfönstret som 56 dagar. Med andra ord kommer modellen att ta hänsyn till alla definierade konverteringshändelser som har inträffat under de senaste två kvartalen och söka efter alla kontaktytor som har inträffat inom 56 dagar före de associerade konverteringshändelserna.

**Formel**:

Minsta längd på data som krävs = utbildningsfönster + uppslagsfönster

>[!TIP]
>
> Den minsta datalängd som krävs för ett program med standardkonfigurationer är: 2 kvartal (180 dagar) + 56 dagar = 236 dagar.

Exempel:

- Du vill attribuera konverteringshändelser som har inträffat under de senaste 90 dagarna (3 månader) och spåra alla kontaktytor som har inträffat inom 4 veckor före konverteringshändelsen. Varaktigheten för indata ska sträcka sig över de senaste 90 dagarna + 28 dagar (4 veckor). Utbildningsfönstret är 90 dagar och uppslagsfönstret är 28 dagar, totalt 118 dagar.

## Attribution AI utdata

Attribution AI ger följande utdata:

- [Rågranulat](#raw-granular-scores)
- [Sammanlagda bakgrundsmusik](#aggregated-attribution-scores)

**Exempel på utdataschema:**

![](./images/input-output/schema_output.gif)

### Rågranulat {#raw-granular-scores}

Attribution AI ger attribueringspoäng på så detaljnivå som möjligt så att du kan segmentera och minska poängen med valfri spalt. Om du vill visa dessa bakgrundsmusik i användargränssnittet läser du avsnittet om [visa sökvägar för råpoäng](#raw-score-path). Om du vill hämta bakgrundsmusik med API:t går du till [ladda ned bakgrundsmusik i Attribution AI](./download-scores.md) -dokument.

>[!NOTE]
>
> Du kan bara se önskad rapportkolumn från indatauppsättningen i utdatamängden för bakgrundsmusik om något av följande stämmer:
> - Rapporteringskolumnen inkluderas på konfigurationssidan antingen som en del av konfigurationen av kontaktyta eller konverteringsdefinition.
> - Rapporteringskolumnen ingår i ytterligare spalter för spaltdata.


I följande tabell visas schemafälten i utdata för råpoängsexempel:

| Kolumnnamn (datatyp) | Nullable | Beskrivning |
| --- | --- | --- |
| tidsstämpel (DateTime) | Falskt | Den tid då en konverteringshändelse eller observation inträffade. <br> **Exempel:** 2020-06-09T00:01:51 000Z |
| identityMap (Map) | True | användarens identityMap liknar CEE XDM-formatet. |
| eventType (String) | True | Den primära händelsetypen för den här tidsserieposten. <br> **Exempel:** &quot;Order&quot;, &quot;Purchase&quot;, &quot;Visit&quot; |
| eventMergeId (String) | True | Ett ID som korrelerar eller sammanfogar flera [!DNL Experience Events] som i allt väsentligt är samma händelse eller bör sammanfogas. Detta ska fyllas i av den som producerar uppgifterna före intag. <br> **Exempel:** 575525617716-0-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _id (sträng) | Falskt | En unik identifierare för tidsseriehändelsen. <br> **Exempel:** 4461-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _tenantId (Object) | Falskt | Objektbehållaren på den översta nivån som motsvarar ditt tält-ID. <br> **Exempel:** _atsdsnrmmsv2 |
| your_schema_name (Object) | Falskt | Poängrad med konverteringshändelse, alla kontaktyteshändelser som är associerade med den och deras metadata. <br> **Exempel:** Attribution AI - modellnamn__2020 |
| segmentering (sträng) | True | Konverteringssegment, t.ex. geosegmentering, som modellen är byggd mot. Om segment saknas är segmentet detsamma som conversionName. <br> **Exempel:** ORDER_US |
| conversionName (String) | True | Namnet på konverteringen som konfigurerades under installationen. <br> **Exempel:** Beställning, lead, besök |
| konvertering (objekt) | Falskt | Konvertera metadatakolumner. |
| dataSource (String) | True | Global unik identifiering av en datakälla. <br> **Exempel:** Adobe Analytics |
| eventSource (String) | True | Källan när den faktiska händelsen inträffade. <br> **Exempel:** Adobe.com |
| eventType (String) | True | Den primära händelsetypen för den här tidsserieposten. <br> **Exempel:** Order |
| geo (String) | True | Den geografiska plats där konverteringen levererades `placeContext.geo.countryCode`. <br> **Exempel:** USA |
| priceTotal (dubbel) | True | Inkomster som erhållits genom konverteringen <br> **Exempel:** 99.9 |
| product (String) | True | XDM-identifieraren för själva produkten. <br> **Exempel:** RX 1080 ti |
| productType (String) | True | Visningsnamnet för produkten som det visas för användaren för den här produktvyn. <br> **Exempel:** Gpus |
| kvantitet (heltal) | True | Kvantitet som köpts under konverteringen. <br> **Exempel:** 1 1080 ti |
| receiveTimestamp (DateTime) | True | Tidsstämpel för konverteringen togs emot. <br> **Exempel:** 2020-06-09T00:01:51 000Z |
| skuId (String) | True | Lagerhållningsenhet (SKU), den unika identifieraren för en produkt som definieras av leverantören. <br> **Exempel:** MJ-03-XS-Black |
| tidsstämpel (DateTime) | True | Tidsstämpel för konverteringen. <br> **Exempel:** 2020-06-09T00:01:51 000Z |
| passThrough (Object) | True | Ytterligare kolumner för Score-datamängd som anges av användaren när modellen konfigureras. |
| commerce_order_purchaseCity (String) | True | Kolumn med extra bakgrundsuppsättning. <br> **Exempel:** stad: San Jose |
| customerProfile (Object) | Falskt | Identitetsinformation om användaren som användes för att skapa modellen. |
| identity (Object) | Falskt | Innehåller information om användaren som används för att skapa modellen, t.ex. `id` och `namespace`. |
| id (String) | True | Identitets-ID för användaren, till exempel cookie-ID, Adobe Analytics-ID (AAID) eller Experience Cloud-ID (ECID, även kallat MCID eller besökar-ID) osv. <br> **Exempel:** 17348762725408656344688320891369597404 |
| namespace (String) | True | Identitetsnamnutrymme som används för att skapa sökvägarna och därmed modellen. <br> **Exempel:** aaid |
| touchPointsDetail (Object Array) | True | Listan med kontaktpunktsinformation som leder till konverteringen som sorteras av | förekomst av kontaktyta eller tidsstämpel. |
| touchpointName (String) | True | Namnet på den kontaktyta som konfigurerades under installationen. <br> **Exempel:** PAID_SEARCH_CLICK |
| bakgrundsmusik (Object) | True | Pekpunktsbidrag till den här konverteringen som poäng. Mer information om bakgrundsmusik finns i [aggregerade attribueringspoäng](#aggregated-attribution-scores) -avsnitt. |
| touchPoint (Object) | True | Kontaktpunktsmetadata. Mer information om bakgrundsmusik finns i [aggregerade poäng](#aggregated-scores) -avsnitt. |

### Visa sökvägar för Raw-poäng (UI) {#raw-score-path}

Du kan visa sökvägen till dina bakgrundsmusik i användargränssnittet. Börja genom att välja **[!UICONTROL Schemas]** i plattformsgränssnittet söker du efter och väljer ditt AI-poängschema för attribuering inifrån **[!UICONTROL Browse]** -fliken.

![Välj schema](./images/input-output/schemas_browse.png)

Välj sedan ett fält i **[!UICONTROL Structure]** fönstret för användargränssnittet, **[!UICONTROL Field properties]** -fliken öppnas. Inom **[!UICONTROL Field properties]** är sökvägsfältet som mappar till dina Raw-resultat.

![Välj ett schema](./images/input-output/field_properties.png)

### Sammanlagda attribueringspoäng {#aggregated-attribution-scores}

Samlade poäng kan hämtas i CSV-format från plattformsgränssnittet om datumintervallet är mindre än 30 dagar.

Attribution AI har stöd för två kategorier av attribueringspoäng, algoritmiska och regelbaserade poäng.

Attribution AI ger två olika typer av algoritmiska poäng, inkrementellt och påverkat. En påverkad poäng är den del av konverteringen som varje marknadsföringskontaktyta ansvarar för. En inkrementell poäng är mängden marginell påverkan som direkt orsakas av kontaktytan för marknadsföring. Den största skillnaden mellan det stegvisa poängvärdet och det poängvärde som påverkas är att det stegvisa poängvärdet tar baslinjeeffekten i beaktande. Man utgår inte från att en konvertering enbart orsakas av de föregående kontaktytorna.

Här följer ett kort exempel på en Attribution AI-schemautdata från Adobe Experience Platform-gränssnittet:

![](./images/input-output/schema_screenshot.png)

Se tabellen nedan för mer information om var och en av dessa attribueringspoäng:

| Attributionspoäng | Beskrivning |
| ----- | ----------- |
| Influerad (algoritmisk) | Påverkade poäng är den del av konverteringen som varje kontaktyta för marknadsföring ansvarar för. |
| Inkrementell (algoritmisk) | Inkrementell poäng är mängden marginell påverkan som direkt orsakas av en kontaktyta för marknadsföring. |
| Första beröring | Regelbaserat attribueringspoäng som tilldelar alla krediter till den första kontaktytan på en konverteringsbana. |
| Sista beröring | Regelbaserat attribueringspoäng som tilldelar all kredit till den kontaktyta som ligger närmast konverteringen. |
| Linjär | Regelbaserat attribueringspoäng som tilldelar varje kontaktyta samma poäng på en konverteringsbana. |
| U-formad | Regelbaserat attribueringspoäng som tilldelar 40 % av krediten till den första kontaktytan och 40 % av krediten till den sista kontaktytan, där de andra kontaktytorna delar upp de återstående 20 % jämnt. |
| Tidsminskning | Regelbaserat attribueringspoäng där kontaktytor som ligger närmare konverteringen får mer kredit än kontaktytor som ligger längre bort från konverteringen. |

**Råpoängsreferens (attribueringspoäng)**

Tabellen nedan mappar attribueringspoängen till de obearbetade poängen. Om du vill ladda ned bakgrundsmusik går du till [ladda ned bakgrundsmusik i Attribution AI](./download-scores.md) dokumentation.

| Attributionspoäng | Referenskolumn för råskala |
| --- | --- |
| Influerad (algoritmisk) | _tenantID.your_schema_name.element.touchpoint.algorithmicInfluenced |
| Inkrementell (algoritmisk) | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.algorithmicInfluenced |
| Första beröring | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.firstTouch |
| Sista beröring | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.lastTouch |
| Linjär | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.linear |
| U-formad | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.uShape |
| Tidsminskning | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.decayUnits |

### Sammanlagda bakgrundsmusik {#aggregated-scores}

Samlade poäng kan hämtas i CSV-format från plattformsgränssnittet om datumintervallet är mindre än 30 dagar. Se tabellen nedan för mer information om var och en av dessa aggregerade kolumner.

| Kolumnnamn | Begränsning | Nullable | Beskrivning |
| --- | --- | --- | --- |
| customer_events_date (DateTime) | Användardefinierat och fast format | Falskt | Kundhändelsedatum i formatet ÅÅÅ-MM-DD. <br> **Exempel**: 2016-05-02 |
| mediatouchpoints_date (DateTime) | Användardefinierat och fast format | True | Media Touchpoint-datum i formatet ÅÅÅ-MM-DD <br> **Exempel**: 2017-04-21 |
| segment (String) | Beräknat | Falskt | Konverteringssegment, t.ex. geosegmentering, som modellen är byggd mot. Om segment saknas är segmentet detsamma som conversion_scope. <br> **Exempel**: ORDER_AMER |
| conversion_scope (String) | Användardefinierad | Falskt | Namnet på konverteringen enligt användarens konfiguration. <br> **Exempel**: BESTÄLL |
| touchpoint_scope (String) | Användardefinierad | True | Namn på kontaktpunkten enligt användarens inställningar <br> **Exempel**: PAID_SEARCH_CLICK |
| product (String) | Användardefinierad | True | Produktens XDM-identifierare. <br> **Exempel**: CC |
| product_type (String) | Användardefinierad | True | Visningsnamnet för produkten som det visas för användaren för den här produktvyn. <br> **Exempel**: gpus, bärbara datorer |
| geo (String) | Användardefinierad | True | Den geografiska plats där konverteringen levererades (placeContext.geo.countryCode) <br> **Exempel**: USA |
| event_type (String) | Användardefinierad | True | Den primära händelsetypen för den här tidsserieposten <br> **Exempel**: Betalkonvertering |
| media_type (String) | ENUM | Falskt | Anger om medietypen är betald, ägd eller förtjänad. <br> **Exempel**: BETALD, ÄGEN |
| channel (String) | ENUM | Falskt | The `channel._type` egenskap som används för att tillhandahålla en grov klassificering av kanaler med liknande egenskaper i [!DNL Consumer Experience Event] XDM. <br> **Exempel**: SÖK |
| action (String) | ENUM | Falskt | The `mediaAction` -egenskapen används för att tillhandahålla en typ av åtgärd för upplevelsehändelsemedia. <br> **Exempel**: KLICKA |
| campaign_group (String) | Användardefinierad | True | Namnet på kampanjgruppen där flera kampanjer grupperas tillsammans, till exempel &quot;50%_DISCOUNT&quot;. <br> **Exempel**: KOMMERSIELL |
| campaign_name (String) | Användardefinierad | True | Namnet på kampanjen som används för att identifiera marknadsföringskampanjer som 50%_DISCOUNT_USA eller 50%_DISCOUNT_ASIA. <br> **Exempel**: Thanksgiving Sale |

**Råpoängsreferens (aggregerad)**

Tabellen nedan mappar de aggregerade poängen till de obearbetade poängen. Om du vill ladda ned bakgrundsmusik går du till [ladda ned bakgrundsmusik i Attribution AI](./download-scores.md) dokumentation. Om du vill visa sökvägarna för råpoängen inifrån användargränssnittet går du till avsnittet på [visa sökvägar för råpoäng](#raw-score-path) i det här dokumentet.

| Kolumnnamn | Referenskolumn för Raw-bakgrundsmusik |
| --- | --- |
| customerevents_date | tidsstämpel |
| mediatouchpoints_date | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.timestamp |
| segment | _tenantID.your_schema_name.segmentation |
| conversion_scope | _tenantID.your_schema_name.conversion.conversionName |
| touchpoint_scope | _tenantID.your_schema_name.touchpointsDetail.element.touchpointName |
| produkt | _tenantID.your_schema_name.conversion.product |
| product_type | _tenantID.your_schema_name.conversion.product_type |
| geo | _tenantID.your_schema_name.conversion.geo |
| event_type | eventType |
| media_type | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaType |
| kanal | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaChannel |
| åtgärd | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaAction |
| campaign_group | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.campaignGroup |
| campaign_name | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.campaignName |

>[!IMPORTANT]
>
> - Attribution AI använder endast uppdaterade data för vidare utbildning och poängsättning. När du begär att få ta bort data avstår kundens AI från att använda de borttagna data.
> - Attribution AI utnyttjar plattformsdatauppsättningar. För att ge stöd åt konsumenträttigheter som ett varumärke kan ta emot bör varumärken använda Platform Privacy Service för att skicka in konsumentförfrågningar om åtkomst och ta bort sina data i datasjön, identitetstjänst och kundprofil i realtid.
> - Alla datauppsättningar som vi använder för in-/utdata av modeller följer riktlinjerna för plattformen. Plattformsdatakryptering gäller för data i vila och under överföring. Läs mer om [datakryptering](../../../help/landing/governance-privacy-security/encryption.md)


## Nästa steg {#next-steps}

När du har förberett dina data och har alla dina autentiseringsuppgifter och scheman på plats börjar du med att följa följande [Användarhandbok för Attribution AI](./user-guide.md). I den här guiden får du hjälp med att skapa en instans för Attribution AI.
