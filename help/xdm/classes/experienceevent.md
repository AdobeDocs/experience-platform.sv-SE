---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;Schemas;identityMap;identity map;Identity map;Schema design;Map;event modeling;event modeling;best practices;event;events;
solution: Experience Platform
title: Klassen XDM ExperienceEvent
description: Lär dig mer om klassen XDM ExperienceEvent och de bästa metoderna för händelsedatamodellering.
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: f7d8cd295dd6aa11048c3cb0f9a54a3702b83473
workflow-type: tm+mt
source-wordcount: '2623'
ht-degree: 0%

---

# [!DNL XDM ExperienceEvent] class

[!DNL XDM ExperienceEvent] är en XDM-klass (Experience Data Model). Använd den här klassen för att skapa en tidsstämplad ögonblicksbild av systemet när en viss händelse inträffar eller när en viss uppsättning villkor har nåtts.

En Experience Event är ett faktaregister över vad som inträffat, inklusive tidpunkten och identiteten för den berörda personen. Händelser kan antingen vara explicita (direkt observerbara mänskliga åtgärder) eller implicita (upphöjda utan en direkt mänsklig åtgärd) och registreras utan aggregering eller tolkning. Mer högnivåinformation om användning av den här klassen i plattformens ekosystem finns i [XDM - översikt](../home.md#data-behaviors).

The [!DNL XDM ExperienceEvent] klassen innehåller flera tidsserierelaterade fält till ett schema. Två av dessa fält (`_id` och `timestamp`) är **obligatoriskt** för alla scheman baserade på den här klassen, medan resten är valfria. Värdena för vissa av fälten fylls i automatiskt när data hämtas.

![Strukturen för XDM ExperienceEvent så som den visas i användargränssnittet för plattformen.](../images/classes/experienceevent/structure.png)

| Egenskap | Beskrivning |
| --- | --- |
| `_id`<br>**(Obligatoriskt)** | Klassen Experience Event `_id` är ett unikt fält som identifierar enskilda händelser som hämtas till Adobe Experience Platform. Det här fältet används för att spåra en enskild händelses unika karaktär, för att förhindra datadubblering och för att slå upp händelsen i underordnade tjänster.<br><br>Om dubbletthändelser upptäcks kan plattformsprogram och -tjänster hantera dubbleringen på olika sätt. Duplicerade händelser i profiltjänsten tas till exempel bort om händelsen med samma `_id` finns redan i profilarkivet.<br><br>I vissa fall `_id` kan vara [Universally Unique Identifier (UUID)](https://datatracker.ietf.org/doc/html/rfc4122) eller [GUID (Global Unique Identifier)](https://learn.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>Om du direktuppspelar data från en källanslutning eller direkt hämtar data från en Parquet-fil, bör du generera det här värdet genom att sammanfoga en viss kombination av fält som gör händelsen unik. Exempel på händelser som kan sammanfogas är primärt ID, tidsstämpel, händelsetyp och så vidare. Det sammanfogade värdet måste vara ett `uri-reference` formaterad sträng, vilket innebär att alla kolontecken måste tas bort. Efteråt bör det sammanfogade värdet hashas med SHA-256 eller någon annan algoritm som du väljer.<br><br>Det är viktigt att särskilja **det här fältet representerar inte en identitet som relateras till en enskild person**, utan själva dataposten. Identitetsuppgifter som rör en person bör begränsas till [identitetsfält](../schema/composition.md#identity) tillhandahålls av kompatibla fältgrupper i stället. |
| `eventMergeId` | Om du använder [Adobe Experience Platform Web SDK](../../edge/home.md) för att importera data representerar detta ID för den inkapslade batchen som gjorde att posten skapades. Det här fältet fylls i automatiskt av systemet när data hämtas. Det går inte att använda det här fältet utanför en Web SDK-implementering. |
| `eventType` | En sträng som anger händelsens typ eller kategori. Det här fältet kan användas om du vill skilja mellan olika händelsetyper inom samma schema och datauppsättning, till exempel att skilja en produkthändelse från en tilläggshändelse i kundvagnen för ett detaljhandelsföretag.<br><br>Standardvärden för den här egenskapen finns i [appendix-avsnitt](#eventType), inklusive beskrivningar av deras avsedda användningsfall. Det här fältet är en utökningsbar uppräkning, vilket innebär att du även kan använda egna händelsetypsträngar för att kategorisera de händelser som du spårar.<br><br>`eventType` begränsar dig till att endast använda en enda händelse per träff i programmet, och därför måste du använda beräkningsfält för att tala om för systemet vilken händelse som är viktigast. Mer information finns i avsnittet om [bästa praxis för beräknade fält](#calculated). |
| `producedBy` | Ett strängvärde som beskriver producenten eller händelsens ursprung. Detta fält kan användas för att filtrera bort vissa händelseproducenter om det behövs för segmenteringsändamål.<br><br>Vissa föreslagna värden för den här egenskapen finns i [appendix-avsnitt](#producedBy). Det här fältet är en utökningsbar uppräkning, vilket innebär att du kan använda dina egna strängar för att representera olika händelseproducenter. |
| `identityMap` | Ett kartfält som innehåller en uppsättning namngivna identiteter för den person som händelsen gäller för. Det här fältet uppdateras automatiskt av systemet när identitetsdata hämtas. För att fältet ska kunna användas [Kundprofil i realtid](../../profile/home.md)försöker du inte uppdatera fältets innehåll manuellt i dataåtgärderna.<br /><br />Se avsnittet om identitetskartor i [grunderna för schemakomposition](../schema/composition.md#identityMap) om du vill ha mer information om deras användningsfall. |
| `timestamp`<br>**(Obligatoriskt)** | En ISO 8601-tidsstämpel för när händelsen inträffade, formaterad enligt [RFC 3339, avsnitt 5.6](https://datatracker.ietf.org/doc/html/rfc3339). Den här tidsstämpeln **måste** tidigare, men **måste** äger rum från och med 1970. Se avsnittet nedan [tidsstämplar](#timestamps) för bästa praxis för användning av detta fält. |

{style="table-layout:auto"}

## Bästa tillvägagångssätt för händelsemodellering

I följande avsnitt beskrivs de effektivaste strategierna för att utforma händelsebaserade XDM-scheman (Experience Data Model) i Adobe Experience Platform.

### Tidsstämplar {#timestamps}

Roten `timestamp` fältet för ett händelseschema kan **endast** representerar själva evenemangets observation och måste inträffa tidigare. Händelsen **måste** äger rum från och med 1970. Om dina användningsfall för segmentering kräver användning av tidsstämplar som kan inträffa i framtiden, måste dessa värden begränsas någon annanstans i Experience Event-schemat.

Om ett företag inom rese- och turismbranschen till exempel utformar en flygbokningshändelse, ska klassnivån `timestamp` -fältet representerar tiden då reservationshändelsen observerades. Andra tidsstämplar som är relaterade till händelsen, t.ex. startdatumet för resereservationen, ska hämtas i separata fält som tillhandahålls av standardfältgrupper eller anpassade fältgrupper.

![Ett exempel på Experience Event-schema med flygreservation och startdatum markerat.](../images/classes/experienceevent/timestamps.png)

Genom att hålla tidsstämpeln på klassnivå åtskild från andra relaterade datetime-värden i dina händelsescheman kan du implementera flexibla användningsfall för segmentering samtidigt som du bevarar en tidsstämplad redovisning av kundresor i ditt upplevelseprogram.

### Använda beräknade fält {#calculated}

Vissa interaktioner i dina upplevelseprogram kan leda till flera relaterade händelser som tekniskt sett delar samma händelsetidsstämpel och därför kan representeras som en enda händelsepost. Om en kund t.ex. tittar på en produkt på webbplatsen kan detta resultera i en händelsepost som har två möjliga `eventType` värden: en produktvy (`commerce.productViews`) eller en generisk sidvy (`web.webpagedetails.pageViews`). I dessa fall kan du använda beräkningsfält för att hämta de viktigaste attributen när flera händelser fångas in i en enda träff.

Använd [Adobe Experience Platform Data Prep](../../data-prep/home.md) att mappa, omvandla och validera data till och från XDM. Använda tillgängliga [mappningsfunktioner](../../data-prep/functions.md) som tillhandahålls av tjänsten kan du anropa logiska operatorer för att prioritera, omvandla och/eller konsolidera data från poster med flera händelser när de hämtas till Experience Platform. I exemplet ovan kan du ange `eventType` som ett beräkningsfält som prioriterar en&quot;produktvy&quot; framför en&quot;sidvy&quot; när båda finns.

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
* [[!UICONTROL MediaAnalytics Interaction Details]](../field-groups/event/mediaanalytics-interaction.md)
* [[!UICONTROL Quote Request Details]](../field-groups/event/quote-request-details.md)
* [[!UICONTROL Reservation Details]](../field-groups/event/reservation-details.md)
* [[!UICONTROL Web Details]](../field-groups/event/web-details.md)

## Bilaga

Följande avsnitt innehåller ytterligare information om [!UICONTROL XDM ExperienceEvent] klassen.

### Godkända värden för `eventType` {#eventType}

I följande tabell visas godkända värden för `eventType`och deras definitioner:

| Värde | Definition |
| --- | --- |
| `advertising.clicks` | Den här händelsen spårar när en åtgärd för att markera en annons inträffar. |
| `advertising.completes` | Den här händelsen spårar när en medieresurs med tidsangivelser har bevakats tills den har slutförts. Det behöver inte innebära att tittaren tittade på hela videon, eftersom användaren kunde ha hoppat över. |
| `advertising.conversions` | Den här händelsen spårar en fördefinierad åtgärd som utförs av en kund och som utlöser en händelse för prestandautvärdering. |
| `advertising.federated` | Den här händelsen spårar om en Experience Event skapades via datafederation (datadelning mellan kunder). |
| `advertising.firstQuartiles` | Den här händelsen spårar när en digital videoannons har spelat upp 25 % av dess längd med normal hastighet. |
| `advertising.impressions` | Den här händelsen spårar intrycket av en annons för en kund som kan visas. |
| `advertising.midpoints` | Den här händelsen spårar när en digital videoannons har spelat upp 50 % av sin längd med normal hastighet. |
| `advertising.starts` | Den här händelsen spårar när en digital videoannons har börjat spelas upp. |
| `advertising.thirdQuartiles` | Den här händelsen spårar när en digital videoannons har spelat upp 75 % av sin längd med normal hastighet. |
| `advertising.timePlayed` | Den här händelsen håller reda på hur mycket tid en användare tillbringar med en viss medieresurs. |
| `application.close` | Den här händelsen spårar när ett program stängdes eller skickades till bakgrunden. |
| `application.launch` | Den här händelsen spårar när ett program startas eller hämtas till förgrunden. |
| `commerce.backofficeCreditMemoIssued` | Den här händelsen spårar när ett kreditmeddelande har utfärdats till en kund. |
| `commerce.backofficeOrderCancelled` | Den här händelsen spårar när en tidigare initierad inköpsprocess har avslutats innan den slutförs. |
| `commerce.backofficeOrderItemsShipped` | Den här händelsen spårar när de inköpta artiklarna har skickats till kunden fysiskt. |
| `commerce.backofficeOrderPlaced` | Den här händelsen spårar placeringen av en order. |
| `commerce.backofficeShipmentCompleted` | Den här händelsen spårar slutförandet av hela leveransprocessen. |
| `commerce.checkouts` | Den här händelsen spårar när en utcheckningshändelse har inträffat för en produktlista. Det kan finnas mer än en utcheckningshändelse om det finns flera steg i en utcheckningsprocess. Om det finns flera steg används tidsstämpeln och sidan/upplevelsen som refereras för varje händelse för att identifiera varje enskild händelse (steg), som representeras i ordning. |
| `commerce.productListAdds` | Den här händelsen spårar när en produkt har lagts till i produktlistan eller i kundvagnen. |
| `commerce.productListOpens` | Den här händelsen spårar när en ny produktlista (kundvagn) har initierats eller skapats. |
| `commerce.productListRemovals` | Den här händelsen spårar när en produktpost har tagits bort från en produktlista eller en kundvagn. |
| `commerce.productListReopens` | Den här händelsen spårar när en kund har återaktiverat en produktlista (kundvagn) som inte längre var tillgänglig (övergiven), till exempel via en återmarknadsföringsaktivitet. |
| `commerce.productListViews` | Den här händelsen spårar när en produktlista eller kundvagn har fått en vy. |
| `commerce.productViews` | Den här händelsen spårar när en produkt har fått en eller flera vyer. |
| `commerce.purchases` | Den här händelsen spårar när en beställning har godkänts. Detta är den enda nödvändiga åtgärden i en handelskonvertering. En köphändelse måste ha en produktlista som refereras. |
| `commerce.saveForLaters` | Den här händelsen spårar när en produktlista har sparats för framtida bruk, till exempel en produktönskelista. |
| `decisioning.propositionDisplay` | Den här händelsen spårar när en beslutsalternativ visades för en person. |
| `decisioning.propositionDismiss` | Den här händelsen spårar när ett beslut har fattats om att inte engagera sig i det erbjudande som presenteras. |
| `decisioning.propositionInteract` | Den här händelsen spårar när en person interagerat med ett beslutsförslag. |
| `decisioning.propositionSend` | Den här händelsen spårar när man har beslutat att skicka en rekommendation eller ett erbjudande till en presumtiv kund för övervägande. |
| `decisioning.propositionTrigger` | Den här händelsen spårar aktiveringen av en förslagsprocess. Ett visst villkor eller en viss åtgärd har inträffat för att uppmana till att ett erbjudande presenteras. |
| `delivery.feedback` | Den här händelsen spårar feedbackhändelser för en leverans, t.ex. en e-postleverans. |
| `directMarketing.emailBounced` | Den här händelsen spåras när ett e-postmeddelande skickas till en person. |
| `directMarketing.emailBouncedSoft` | Den här händelsen spårar när ett e-postmeddelande till en person studsar på skärmen. |
| `directMarketing.emailClicked` | Den här händelsen spårar när en person klickade på en länk i ett marknadsföringsmeddelande. |
| `directMarketing.emailDelivered` | Den här händelsen spårar när ett e-postmeddelande levererades till en persons e-posttjänst. |
| `directMarketing.emailOpened` | Den här händelsen spårar när en person öppnar ett marknadsföringsmeddelande. |
| `directMarketing.emailSent` | Den här händelsen spårar när ett marknadsföringsmeddelande har skickats till en person. |
| `directMarketing.emailUnsubscribed` | Den här händelsen spårar när en person säger upp prenumerationen på ett marknadsföringsmejl. |
| `inappmessageTracking.dismiss` | Den här händelsen spårar när ett meddelande i appen stängdes. |
| `inappmessageTracking.display` | Den här händelsen spårar när ett meddelande visas i appen. |
| `inappmessageTracking.interact` | Den här händelsen spårar när ett meddelande i appen interagerades med. |
| `leadOperation.callWebhook` | Den här händelsen spårar när en webbkrok anropades som svar på ett lead. |
| `leadOperation.changeCampaignStream` | Den här händelsen innebär en förändring av marknadsförings- eller engagemangsstrategin för ett visst ledande företag. |
| `leadOperation.changeEngagementCampaignCadence` | Den här händelsen spårar när det har skett en förändring i hur ofta ett lead är engagerat som en del av en kampanj. |
| `leadOperation.convertLead` | Den här händelsen spårar när ett lead konverterades. |
| `leadOperation.interestingMoment` | Den här händelsen spårar när en intressant stund spelades in för en person. |
| `leadOperation.mergeLeads` | Den här händelsen spårar när information från flera leads som refererar till samma enhet konsolideras. |
| `leadOperation.newLead` | Den här händelsen spårar när ett lead skapades. |
| `leadOperation.scoreChanged` | Den här händelsen spårar när värdet för leadets poängattribut har ändrats. |
| `leadOperation.statusInCampaignProgressionChanged` | Den här händelsen spårar när status för ett lead i en kampanj har ändrats. |
| `listOperation.addToList` | Den här händelsen spårar när en person lades till i en marknadsföringslista. |
| `listOperation.removeFromList` | Den här händelsen spårar när en person har tagits bort från en marknadsföringslista. |
| `media.adBreakComplete` | Den här händelsen spårar när en `adBreakComplete` -händelsen har inträffat. Den här händelsen utlöses i början av en annonsbrytning. |
| `media.adBreakStart` | Den här händelsen spårar när en `adBreakStart` -händelsen har inträffat. Den här händelsen utlöses i slutet av en annonsbrytning. |
| `media.adComplete` | Den här händelsen spårar när en `adComplete` -händelsen har inträffat. Den här händelsen utlöses när en annons har slutförts. |
| `media.adSkip` | Den här händelsen spårar när en `adSkip` -händelsen har inträffat. Den här händelsen utlöses när en annons har hoppats över. |
| `media.adStart` | Den här händelsen spårar när en `adStart` -händelsen har inträffat. Den här händelsen utlöses när en annons har startats. |
| `media.bitrateChange` | Den här händelsen spåras när en `bitrateChange` -händelsen har inträffat. Den här händelsen utlöses när bithastigheten ändras. |
| `media.bufferStart` | Den här händelsen spåras när en `bufferStart` -händelsen har inträffat. Den här händelsen utlöses när media har börjat buffras. |
| `media.chapterComplete` | Den här händelsen spåras när en `chapterComplete` -händelsen har inträffat. Den här händelsen utlöses när ett kapitel i mediet har slutförts. |
| `media.chapterSkip` | Den här händelsen spåras när en `chapterSkip` -händelsen har inträffat. Den här händelsen utlöses när en användare går framåt eller bakåt till ett annat avsnitt eller kapitel i medieinnehållet. |
| `media.chapterStart` | Den här händelsen spåras när en `chapterStart` -händelsen har inträffat. Den här händelsen utlöses i början av ett visst avsnitt eller kapitel i medieinnehållet. |
| `media.downloaded` | Den här händelsen spårar när media har laddat ned innehåll. |
| `media.error` | Den här händelsen spårar när en `error` -händelsen har inträffat. Den här händelsen utlöses när ett fel eller problem inträffar under medieuppspelningen. |
| `media.pauseStart` | Den här händelsen spåras när en `pauseStart` -händelsen har inträffat. Den här händelsen utlöses när en användare initierar en paus i medieuppspelningen. |
| `media.ping` | Den här händelsen spårar när en `ping` -händelsen har inträffat. Detta verifierar tillgängligheten för en medieresurs. |
| `media.play` | Den här händelsen spåras när en `play` -händelsen har inträffat. Den här händelsen utlöses när medieinnehållet spelas upp, vilket indikerar användarens aktiva förbrukning. |
| `media.sessionComplete` | Den här händelsen spåras när en `sessionComplete` -händelsen har inträffat. Den här händelsen markerar slutet på en mediauppspelningssession. |
| `media.sessionEnd` | Den här händelsen spåras när en `sessionEnd` -händelsen har inträffat. Den här händelsen anger att en mediesession har avslutats. Den här slutsatsen kan innebära att mediespelaren stängs eller att uppspelningen stoppas. |
| `media.sessionStart` | Den här händelsen spåras när en `sessionStart` -händelsen har inträffat. Den här händelsen markerar början på en mediouppspelningssession. Den aktiveras när en användare börjar spela upp en mediefil. |
| `media.statesUpdate` | Den här händelsen spåras när en `statesUpdate` -händelsen har inträffat. Spårningsfunktionerna för spelartillstånd kan kopplas till ett ljud- eller videoflöde. Standardlägena är: helskärm, stängd, bildtext, bildInPicture och inFocus. |
| `opportunityEvent.addToOpportunity` | Den här händelsen spårar när en person lades till i en affärsmöjlighet. |
| `opportunityEvent.opportunityUpdated` | Händelsen spårar när en affärsmöjlighet uppdaterades. |
| `opportunityEvent.removeFromOpportunity` | Den här händelsen spårar när en person har tagits bort från en affärsmöjlighet. |
| `pushTracking.applicationOpened` | Den här händelsen spårar när en person öppnar ett program från ett push-meddelande. |
| `pushTracking.customAction` | Den här händelsen spårar när en person har valt en anpassad åtgärd i ett push-meddelande. |
| `web.formFilledOut` | Den här händelsen spårar när en person fyller i ett formulär på en webbsida. |
| `web.webinteraction.linkClicks` | Den här händelsen spårar när en länk har markerats en eller flera gånger. |
| `web.webpagedetails.pageViews` | Den här händelsen spårar när en webbsida har tagit emot en eller flera vyer. |
| `location.entry` | Den här händelsen spårar en persons eller enhets inträde på en viss plats. |
| `location.exit` | Den här händelsen spårar en persons eller enhets utträde från en viss plats. |

{style="table-layout:auto"}

### Föreslagna värden för `producedBy` {#producedBy}

I följande tabell beskrivs några godkända värden för `producedBy`:

| Värde | Definition |
| --- | --- |
| `self` | Själv |
| `system` | System |
| `salesRef` | Säljare |
| `customerRep` | Kundrepresentant |
