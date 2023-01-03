---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;Schemas;identityMap;identity map;Identity map;Schema design;Map;event modeling;event modeling;best practices;event;events;
solution: Experience Platform
title: Klassen XDM ExperienceEvent
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över klassen XDM ExperienceEvent och metodtips för händelsedatamodellering.
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1785'
ht-degree: 0%

---

# [!DNL XDM ExperienceEvent] class

[!DNL XDM ExperienceEvent] är en XDM-standardklass (Experience Data Model) som gör att du kan skapa en tidsstämplad ögonblicksbild av systemet när en viss händelse inträffar eller när en viss uppsättning villkor har nåtts.

En Experience Event är ett faktaregister över vad som inträffat, inklusive tidpunkten och identiteten för den berörda personen. Händelser kan antingen vara explicita (direkt observerbara mänskliga åtgärder) eller implicita (upphöjda utan en direkt mänsklig åtgärd) och registreras utan aggregering eller tolkning. Mer högnivåinformation om användning av den här klassen i plattformens ekosystem finns i [XDM - översikt](../home.md#data-behaviors).

The [!DNL XDM ExperienceEvent] klassen innehåller flera tidsserierelaterade fält till ett schema. Två av dessa fält (`_id` och `timestamp`) är **obligatoriskt** för alla scheman baserade på klassen, medan resten är valfria. Värdena för vissa av fälten fylls i automatiskt när data hämtas.

![Strukturen för XDM ExperienceEvent som den visas i plattformens användargränssnitt](../images/classes/experienceevent/structure.png)

| Egenskap | Beskrivning |
| --- | --- |
| `_id`<br>**(Obligatoriskt)** | En unik strängidentifierare för händelsen. Det här fältet används för att spåra en enskild händelses unika karaktär, för att förhindra datadubblering och för att slå upp händelsen i underordnade tjänster. I vissa fall `_id` kan vara en [Universally Unique Identifier (UUID)](https://tools.ietf.org/html/rfc4122) eller [GUID (Global Unique Identifier)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>Om du direktuppspelar data från en källanslutning eller direkt inmatning från en Parquet-fil, bör du generera det här värdet genom att sammanfoga en viss kombination av fält som gör händelsen unik, till exempel ett primärt ID, en tidsstämpel, händelsetyp. Det sammanfogade värdet måste vara ett `uri-reference` formaterad sträng, vilket innebär att alla kolontecken måste tas bort. Efteråt bör det sammanfogade värdet hashas med SHA-256 eller någon annan algoritm som du väljer.<br><br>Det är viktigt att särskilja **detta fält inte representerar en identitet som relateras till en enskild person**, utan själva dataposten. Identitetsuppgifter som rör en person bör begränsas till [identitetsfält](../schema/composition.md#identity) tillhandahålls av kompatibla fältgrupper i stället. |
| `eventMergeId` | Om du använder [Adobe Experience Platform Web SDK](../../edge/home.md) för att importera data representerar detta ID för den inkapslade batchen som gjorde att posten skapades. Det här fältet fylls i automatiskt av systemet när data hämtas. Det går inte att använda det här fältet utanför kontexten för en Web SDK-implementering. |
| `eventType` | En sträng som anger händelsens typ eller kategori. Det här fältet kan användas om du vill skilja mellan olika händelsetyper inom samma schema och datauppsättning, till exempel att skilja en produkthändelse från en tilläggshändelse i kundvagnen för ett detaljhandelsföretag.<br><br>Standardvärden för den här egenskapen finns i [appendix-avsnitt](#eventType), inklusive beskrivningar av användningsfallet. Det här fältet är en utökningsbar uppräkning, vilket innebär att du även kan använda egna händelsetypsträngar för att kategorisera de händelser som du spårar.<br><br>`eventType` begränsar dig till att endast använda en enda händelse per träff i programmet, och därför måste du använda beräkningsfält för att tala om för systemet vilken händelse som är viktigast. Mer information finns i avsnittet om [bästa praxis för beräknade fält](#calculated). |
| `producedBy` | Ett strängvärde som beskriver producenten eller händelsens ursprung. Detta fält kan användas för att filtrera bort vissa händelseproducenter om det behövs för segmenteringsändamål.<br><br>Vissa föreslagna värden för den här egenskapen finns i [appendix-avsnitt](#producedBy). Det här fältet är en utökningsbar uppräkning, vilket innebär att du kan använda dina egna strängar för att representera olika händelseproducenter. |
| `identityMap` | Ett kartfält som innehåller en uppsättning namngivna identiteter för den person som händelsen gäller för. Det här fältet uppdateras automatiskt av systemet när identitetsdata hämtas. För att fältet ska kunna användas på rätt sätt [Kundprofil i realtid](../../profile/home.md)försöker du inte uppdatera fältets innehåll manuellt i dataåtgärderna.<br /><br />Se avsnittet om identitetskartor i [grunderna för schemakomposition](../schema/composition.md#identityMap) om du vill ha mer information om deras användningsfall. |
| `timestamp`<br>**(Obligatoriskt)** | En ISO 8601-tidsstämpel för när händelsen inträffade, formaterad enligt [RFC 3339, avsnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). Den här tidsstämpeln måste finnas tidigare. Se avsnittet nedan [tidsstämplar](#timestamps) för bästa praxis för användning av detta fält. |

{style=&quot;table-layout:auto&quot;}

## Bästa tillvägagångssätt för händelsemodellering

I följande avsnitt beskrivs de effektivaste strategierna för att utforma händelsebaserade XDM-scheman (Experience Data Model) i Adobe Experience Platform.

### Tidsstämplar {#timestamps}

Roten `timestamp` fältet för ett händelseschema kan **endast** representerar själva evenemangets observation och måste inträffa tidigare. Om dina användningsfall för segmentering kräver användning av tidsstämplar som kan inträffa i framtiden, måste dessa värden begränsas någon annanstans i Experience Event-schemat.

Om ett företag inom rese- och turismbranschen till exempel utformar en flygbokningshändelse, ska klassnivån `timestamp` -fältet representerar tiden då reservationshändelsen observerades. Andra tidsstämplar som är relaterade till händelsen, t.ex. startdatumet för resereservationen, ska hämtas i separata fält som tillhandahålls av standardfältgrupper eller anpassade fältgrupper.

![](../images/classes/experienceevent/timestamps.png)

Genom att hålla tidsstämpeln på klassnivå åtskild från andra relaterade datetime-värden i dina händelsescheman kan du implementera flexibla användningsfall för segmentering samtidigt som du bevarar en tidsstämplad redovisning av kundresor i ditt upplevelseprogram.

### Använda beräknade fält {#calculated}

Vissa interaktioner i dina upplevelseprogram kan leda till flera relaterade händelser som tekniskt sett delar samma händelsetidsstämpel och därför kan representeras som en enda händelsepost. Om en kund t.ex. tittar på en produkt på webbplatsen kan detta resultera i en händelsepost som har två möjliga `eventType` värden: en produktvy (`commerce.productViews`) eller en generisk sidvy (`web.webpagedetails.pageViews`). I dessa fall kan du använda beräkningsfält för att hämta de viktigaste attributen när flera händelser fångas in i en enda träff.

[Adobe Experience Platform Data Prep](../../data-prep/home.md) gör att du kan mappa, omvandla och validera data till och från XDM. Använda tillgängliga [mappningsfunktioner](../../data-prep/functions.md) som tillhandahålls av tjänsten kan du anropa logiska operatorer för att prioritera, omvandla och/eller konsolidera data från poster med flera händelser när de hämtas till Experience Platform. I exemplet ovan kan du ange `eventType` som ett beräkningsfält som prioriterar en&quot;produktvy&quot; framför en&quot;sidvy&quot; när båda finns.

Om du hämtar data manuellt till plattformen via användargränssnittet läser du i handboken [beräknade fält](../../data-prep/ui/mapping.md#calculated-fields) för specifika steg om hur du skapar beräkningsfält.

Om du direktuppspelar data till plattformen med en källanslutning kan du konfigurera källan så att beräkningsfält används i stället. Se [dokumentation för just din källa](../../sources/home.md) för instruktioner om hur beräknade fält implementeras när anslutningen konfigureras.

## Kompatibla schemafältgrupper {#field-groups}

>[!NOTE]
>
>Namnen på flera fältgrupper har ändrats. Visa dokumentet på [uppdaterar fältgruppnamn](../field-groups/name-updates.md) för mer information.

Adobe har flera standardfältgrupper som kan användas med [!DNL XDM ExperienceEvent] klassen. Nedan följer en lista över några vanliga fältgrupper för klassen:

* [[!UICONTROL Adobe Analytics ExperienceEvent Full Extension]](../field-groups/event/analytics-full-extension.md)
* [[!UICONTROL Balance Transfers]](../field-groups/event/balance-transfers.md)
* [[!UICONTROL Campaign Marketing Details]](../field-groups/event/campaign-marketing-details.md)
* [[!UICONTROL Card Actions]](../field-groups/event/card-actions.md)
* [[!UICONTROL Channel Details]](../field-groups/event/channel-details.md)
* [[!UICONTROL Commerce Details]](../field-groups/event/commerce-details.md)
* [[!UICONTROL Deposit Details]](../field-groups/event/deposit-details.md)
* [[!UICONTROL Device Trade-In Details]](../field-groups/event/device-trade-in-details.md)
* [[!UICONTROL Dining Reservation]](../field-groups/event/dining-reservation.md)
* [[!UICONTROL End User ID Details]](../field-groups/event/enduserids.md)
* [[!UICONTROL Environment Details]](../field-groups/event/environment-details.md)
* [[!UICONTROL Flight Reservation]](../field-groups/event/flight-reservation.md)
* [[!UICONTROL IAB TCF 2.0 Consent]](../field-groups/event/iab.md)
* [[!UICONTROL Lodging Reservation]](../field-groups/event/lodging-reservation.md)
* [[!UICONTROL Quote Request Details]](../field-groups/event/quote-request-details.md)
* [[!UICONTROL Reservation Details]](../field-groups/event/reservation-details.md)
* [[!UICONTROL Web Details]](../field-groups/event/web-details.md)

## Bilaga

Följande avsnitt innehåller ytterligare information om [!UICONTROL XDM ExperienceEvent] klassen.

### Godkända värden för `eventType` {#eventType}

I följande tabell visas godkända värden för `eventType`och deras definitioner:

| Värde | Definition |
| --- | --- |
| `advertising.clicks` | Klicka på åtgärd(er) i en annons. |
| `advertising.completes` | En mediefil med en tidsgräns har bevakats tills den är klar. Det behöver inte innebära att tittaren tittade på hela videon, eftersom tittaren kunde ha hoppat över i förväg. |
| `advertising.conversions` | Fördefinierade åtgärder som utförs av en kund och som utlöser en händelse för prestandautvärdering. |
| `advertising.federated` | Anger om en Experience Event skapades via datafederation (datadelning mellan kunder). |
| `advertising.firstQuartiles` | En digital videoannons har spelat upp 25 % av sin längd med normal hastighet. |
| `advertising.impressions` | Imponering(ar) av en annons till en kund som kan visas. |
| `advertising.midpoints` | En digital videoannons har spelat upp 50 % av sin längd med normal hastighet. |
| `advertising.starts` | En digital videoannons har börjat spelas upp. |
| `advertising.thirdQuartiles` | En digital videoannons har spelat upp 75 % av sin längd med normal hastighet. |
| `advertising.timePlayed` | Beskriver hur mycket tid en användare har lagt på en viss medieresurs med tidsangivelser. |
| `application.close` | Ett program stängdes eller skickades till bakgrunden. |
| `application.launch` | En ansökan startades eller togs in i förgrunden. |
| `commerce.checkouts` | En utcheckningshändelse har inträffat för en produktlista. Det kan finnas mer än en utcheckningshändelse om det finns flera steg i en utcheckningsprocess. Om det finns flera steg används tidsstämpeln och sidan/upplevelsen som refereras för varje händelse för att identifiera varje enskild händelse (steg), som representeras i ordning. |
| `commerce.productListAdds` | En produkt har lagts till i produktlistan eller i kundvagnen. |
| `commerce.productListOpens` | En ny produktlista (kundvagn) har initierats eller skapats. |
| `commerce.productListRemovals` | En eller flera produktposter har tagits bort från en produktlista eller kundvagn. |
| `commerce.productListReopens` | En produktlista (kundvagn) som inte längre var tillgänglig (övergiven) har återaktiverats av en kund, till exempel via en återmarknadsföringsaktivitet. |
| `commerce.productListViews` | En produktlista eller kundvagn har fått en eller flera vyer. |
| `commerce.productViews` | En produkt har fått en eller flera vyer. |
| `commerce.purchases` | En beställning har godkänts. Detta är den enda nödvändiga åtgärden i en handelskonvertering. En köphändelse måste ha en produktlista som refereras. |
| `commerce.saveForLaters` | En produktlista har sparats för framtida bruk, till exempel en produktönskelista. |
| `decisioning.propositionDisplay` | Ett beslutsförslag visades för en person. |
| `decisioning.propositionInteract` | En person interagerade med ett beslutsförslag. |
| `delivery.feedback` | Feedback-händelser för en leverans, till exempel en e-postleverans. |
| `directMarketing.emailBounced` | Ett e-postmeddelande till en person studsade. |
| `directMarketing.emailBouncedSoft` | Ett e-postmeddelande till en person med mjuka studsar. |
| `directMarketing.emailClicked` | En person klickade på en länk i ett marknadsföringsmejl. |
| `directMarketing.emailDelivered` | Ett e-postmeddelande har levererats till personens e-posttjänst |
| `directMarketing.emailOpened` | En person öppnade ett marknadsföringsmejl. |
| `directMarketing.emailUnsubscribed` | En person som avbrutit prenumerationen på ett marknadsföringsmejl. |
| `inappmessageTracking.dismiss` | Ett meddelande i appen stängdes. |
| `inappmessageTracking.display` | Ett meddelande i appen viserades. |
| `inappmessageTracking.interact` | Ett meddelande i appen interagerades med. |
| `leadOperation.callWebhook` | En webkrok anropades som svar på en lead. |
| `leadOperation.convertLead` | Ett lead konverterades. |
| `leadOperation.interestingMoment` | Ett intressant ögonblick spelades in för en person. |
| `leadOperation.newLead` | Ett lead skapades. |
| `leadOperation.scoreChanged` | Värdet för leadets poängattribut ändrades. |
| `leadOperation.statusInCampaignProgressionChanged` | Status för en lead i en kampanj har ändrats. |
| `listOperation.addToList` | En person har lagts till i en marknadsföringslista. |
| `listOperation.removeFromList` | En person har tagits bort från en marknadsföringslista. |
| `message.feedback` | Feedback-händelser som skickade/studsade/fel för meddelanden som skickats till en kund. |
| `message.tracking` | Spåra händelser som öppna/klicka/anpassade åtgärder för meddelanden som skickas till en kund. |
| `opportunityEvent.addToOpportunity` | En person har lagts till i en affärsmöjlighet. |
| `opportunityEvent.opportunityUpdated` | En affärsmöjlighet har uppdaterats. |
| `opportunityEvent.removeFromOpportunity` | En person har tagits bort från en affärsmöjlighet. |
| `pushTracking.applicationOpened` | En person öppnade ett program från ett push-meddelande. |
| `pushTracking.customAction` | En person klickade på en anpassad åtgärd i ett push-meddelande. |
| `web.formFilledOut` | En person fyllde i ett formulär på en webbsida. |
| `web.webinteraction.linkClicks` | En länk har markerats en eller flera gånger. |
| `web.webpagedetails.pageViews` | En webbsida har fått en eller flera vyer. |

{style=&quot;table-layout:auto&quot;}

### Föreslagna värden för `producedBy` {#producedBy}

I följande tabell beskrivs några godkända värden för `producedBy`:

| Värde | Definition |
| --- | --- |
| `self` | Själv |
| `system` | System |
| `salesRef` | Säljare |
| `customerRep` | Kundrepresentant |
