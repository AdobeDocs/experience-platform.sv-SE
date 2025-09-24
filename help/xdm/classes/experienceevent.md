---
keywords: Experience Platform;home;populära topics;schema;Schema;XDM;fields;schemas;Schemas;identityMap;identity map;identity map;Schema design;map;event modeling;event modeling;best practices;event;events;
solution: Experience Platform
title: Klassen XDM ExperienceEvent
description: Lär dig mer om klassen XDM ExperienceEvent och de bästa metoderna för händelsedatamodellering.
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: 8aa8a1c42e9656716be746ba447a5f77a8155b4c
workflow-type: tm+mt
source-wordcount: '2728'
ht-degree: 0%

---

# klassen [!DNL XDM ExperienceEvent]

[!DNL XDM ExperienceEvent] är en XDM-standardklass (Experience Data Model). Använd den här klassen för att skapa en tidsstämplad ögonblicksbild av systemet när en viss händelse inträffar eller när en viss uppsättning villkor har nåtts.

En Experience Event är ett faktaregister över vad som inträffat, inklusive tidpunkten och identiteten för den berörda personen. Händelser kan antingen vara explicita (direkt observerbara mänskliga åtgärder) eller implicita (upphöjda utan en direkt mänsklig åtgärd) och registreras utan aggregering eller tolkning. Mer högnivåinformation om hur den här klassen används i Experience Platform ekosystem finns i [XDM-översikten](../home.md#data-behaviors).

Själva klassen [!DNL XDM ExperienceEvent] tillhandahåller flera tidsserierelaterade fält till ett schema. Två av dessa fält (`_id` och `timestamp`) är **obligatoriska** för alla scheman som baseras på den här klassen, medan resten är valfria. Värdena för vissa av fälten fylls i automatiskt när data hämtas.

![Strukturen för XDM ExperienceEvent så som den visas i Experience Platform-gränssnittet.](../images/classes/experienceevent/structure.png)

| Egenskap | Beskrivning |
| --- | --- |
| `_id`<br>**(Obligatoriskt)** | Fältet Experience Event Class `_id` identifierar unika händelser som är inkapslade i Adobe Experience Platform. Det här fältet används för att spåra en enskild händelses unika karaktär, för att förhindra datadubblering och för att slå upp händelsen i underordnade tjänster.<br><br>Om dubbletthändelser upptäcks kan Experience Platform-program och -tjänster hantera dubbletterna på olika sätt. Duplicerade händelser i profiltjänsten tas till exempel bort om händelsen med samma `_id` redan finns i profilarkivet. Dessa händelser kommer dock fortfarande att registreras i datasjön.<br><br>I vissa fall kan `_id` vara en [Universally Unique Identifier (UUID)](https://datatracker.ietf.org/doc/html/rfc4122) eller [Global Unique Identifier (GUID)](https://learn.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>Om du direktuppspelar data från en källanslutning eller direkt hämtar från en Parquet-fil, bör du generera det här värdet genom att sammanfoga en viss kombination av fält som gör händelsen unik. Exempel på händelser som kan sammanfogas är primärt ID, tidsstämpel, händelsetyp och så vidare. Det sammanfogade värdet måste vara en `uri-reference`-formaterad sträng, vilket innebär att alla kolontecken måste tas bort. Efteråt bör det sammanfogade värdet hashas med SHA-256 eller någon annan algoritm som du väljer.<br><br>Det är viktigt att särskilja att **det här fältet inte representerar en identitet som är relaterad till en enskild person**, utan själva dataposten. Identitetsdata som relaterar till en person ska i stället begränsas till [identitetsfält](../schema/composition.md#identity) som tillhandahålls av kompatibla fältgrupper. |
| `eventMergeId` | Om du använder [Adobe Experience Platform Web SDK](/help/web-sdk/home.md) för att importera data representerar detta ID för den inkapslade batchen som gjorde att posten skapades. Det här fältet fylls i automatiskt av systemet när data hämtas. Det går inte att använda det här fältet utanför en Web SDK-implementering. |
| `eventType` | En sträng som anger händelsens typ eller kategori. Det här fältet kan användas om du vill skilja mellan olika händelsetyper inom samma schema och datauppsättning, till exempel att skilja en produkthändelse från en tilläggshändelse i kundvagnen för ett detaljhandelsföretag.<br><br>Standardvärden för den här egenskapen finns i [appendix-avsnittet](#eventType), inklusive beskrivningar av deras avsedda användningsfall. Det här fältet är en utökningsbar uppräkning, vilket innebär att du även kan använda egna händelsetypsträngar för att kategorisera de händelser som du spårar.<br><br>`eventType` begränsar dig till att endast använda en händelse per träff i ditt program, och därför måste du använda beräkningsfält för att tala om för systemet vilken händelse som är viktigast. Mer information finns i avsnittet [Bästa tillvägagångssätt för beräknade fält](#calculated). |
| `producedBy` | Ett strängvärde som beskriver producenten eller händelsens ursprung. Detta fält kan användas för att filtrera bort vissa händelseproducenter om det behövs för segmenteringsändamål.<br><br>Vissa föreslagna värden för den här egenskapen finns i avsnittet [appendix](#producedBy). Det här fältet är en utökningsbar uppräkning, vilket innebär att du kan använda dina egna strängar för att representera olika händelseproducenter. |
| `identityMap` | Ett kartfält som innehåller en uppsättning namngivna identiteter för den person som händelsen gäller för. Det här fältet uppdateras automatiskt av systemet när identitetsdata hämtas. Om du vill använda det här fältet för [Kundprofil i realtid](../../profile/home.md) ska du inte försöka uppdatera fältets innehåll manuellt i dataåtgärderna.<br /><br />Mer information om hur de används finns i avsnittet om identitetskartor i [grunderna i schemakomposition](../schema/composition.md#identityMap). |
| `timestamp`<br>**(Obligatoriskt)** | En ISO 8601-tidsstämpel för när händelsen inträffade, formaterad enligt [RFC 3339 Section 5.6](https://datatracker.ietf.org/doc/html/rfc3339). Den här tidsstämpeln **måste** inträffa tidigare, men **måste** äga rum från och med 1970. Mer information om hur du använder det här fältet finns i avsnittet nedan om [tidsstämplar](#timestamps). |

{style="table-layout:auto"}

## Bästa tillvägagångssätt för händelsemodellering

I följande avsnitt beskrivs de effektivaste strategierna för att utforma händelsebaserade XDM-scheman (Experience Data Model) i Adobe Experience Platform.

### Tidsstämplar {#timestamps}

Rotfältet `timestamp` i ett händelseschema kan **endast** representera själva händelseobservationen och måste inträffa i det förflutna. Händelsen **måste** äga rum från och med 1970. Om dina användningsfall för segmentering kräver användning av tidsstämplar som kan inträffa i framtiden, måste dessa värden begränsas någon annanstans i Experience Event-schemat.

Om en verksamhet inom rese- och turismbranschen till exempel modellerar en flygbokningshändelse, representerar fältet `timestamp` på klassnivå tiden när reservationshändelsen observerades. Andra tidsstämplar som är relaterade till händelsen, t.ex. startdatumet för resereservationen, ska hämtas i separata fält som tillhandahålls av standardfältgrupper eller anpassade fältgrupper.

![Ett exempel på Experience Event-schema med flygreservation och startdatum markerat.](../images/classes/experienceevent/timestamps.png)

Genom att hålla tidsstämpeln på klassnivå åtskild från andra relaterade datetime-värden i dina händelsescheman kan du implementera flexibla användningsfall för segmentering samtidigt som du bevarar en tidsstämplad redovisning av kundresor i ditt upplevelseprogram.

### Använda beräknade fält {#calculated}

Vissa interaktioner i dina upplevelseprogram kan leda till flera relaterade händelser som tekniskt sett delar samma händelsetidsstämpel och därför kan representeras som en enda händelsepost. Om en kund t.ex. visar en produkt på din webbplats kan detta resultera i en händelsepost som har två möjliga `eventType`-värden: en produktvyhändelse (`commerce.productViews`) eller en allmän sidvyhändelse (`web.webpagedetails.pageViews`). I dessa fall kan du använda beräkningsfält för att hämta de viktigaste attributen när flera händelser fångas in i en enda träff.

Använd [Adobe Experience Platform Data Prep](../../data-prep/home.md) för att mappa, omvandla och validera data till och från XDM. Med de tillgängliga [mappningsfunktionerna](../../data-prep/functions.md) från tjänsten kan du anropa logiska operatorer för att prioritera, omvandla och/eller konsolidera data från poster med flera händelser när de hämtas till Experience Platform. I exemplet ovan kan du ange `eventType` som ett beräkningsfält som prioriterar en&quot;produktvy&quot; framför en&quot;sidvy&quot; när båda förekommer.

Om du hämtar data manuellt till Experience Platform via användargränssnittet kan du läsa guiden om [beräknade fält](../../data-prep/ui/mapping.md#calculated-fields) för att få mer information om hur du skapar beräkningsfält.

Om du direktuppspelar data till Experience Platform via en källanslutning kan du konfigurera källan så att beräkningsfält används i stället. Mer information om hur du implementerar beräknade fält när du konfigurerar anslutningen finns i [dokumentationen för den aktuella källan](../../sources/home.md).

## Kompatibla schemafältgrupper {#field-groups}

>[!NOTE]
>
>Namnen på flera fältgrupper har ändrats. Mer information finns i dokumentet om [uppdatering av fältgruppnamn](../field-groups/name-updates.md).

Adobe innehåller flera standardfältgrupper som kan användas med klassen [!DNL XDM ExperienceEvent]. Nedan följer en lista över några vanliga fältgrupper för klassen:

* [[!UICONTROL Adobe Analytics ExperienceEvent Full Extension]](../field-groups/event/analytics-full-extension.md)
* [[!UICONTROL Adobe Advertising Cloud ExperienceEvent Full Extension]](../field-groups/event/advertising-full-extension.md)
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

Följande avsnitt innehåller ytterligare information om klassen [!UICONTROL XDM ExperienceEvent].

### Godkända värden för `eventType` {#eventType}

I följande tabell visas de godkända värdena för `eventType` tillsammans med deras definitioner:

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
| `click` | **Föråldrat** Använd `decisioning.propositionInteract` i stället. |
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
| `decisioning.propositionDisplay` | Den här händelsen används när SDK för webben automatiskt skickar information om vad som visas på en sida. Du behöver dock inte den här händelsetypen om du redan inkluderar visningsinformation på andra sätt, som med sidträffar uppifrån och ned. Du kan välja vilken händelsetyp du vill längst ned i sidträffar. |
| `decisioning.propositionDismiss` | Den här händelsetypen används när ett Adobe Journey Optimizer-meddelande eller innehållskort stängs. |
| `decisioning.propositionFetch` | Används för att indikera att en händelse främst är att hämta beslut. Adobe Analytics släpper det här evenemanget automatiskt. |
| `decisioning.propositionInteract` | Den här händelsetypen används för att spåra interaktioner, som klickningar, i personaliserat innehåll. |
| `decisioning.propositionSend` | Den här händelsen spårar när man har beslutat att skicka en rekommendation eller ett erbjudande till en presumtiv kund för övervägande. |
| `decisioning.propositionTrigger` | Händelser av den här typen lagras i lokalt lager av [Web SDK](../../web-sdk/home.md), men skickas inte till Experience Edge. Varje gång en regeluppsättning är uppfylld genereras en händelse som lagras i ett lokalt lager (om den inställningen är aktiverad). |
| `delivery.feedback` | Den här händelsen spårar feedbackhändelser för en leverans, t.ex. en e-postleverans. |
| `directMarketing.emailBounced` | Den här händelsen spåras när ett e-postmeddelande skickas till en person. |
| `directMarketing.emailBouncedSoft` | Den här händelsen spårar när ett e-postmeddelande till en person studsar på skärmen. |
| `directMarketing.emailClicked` | Den här händelsen spårar när en person klickade på en länk i ett marknadsföringsmeddelande. |
| `directMarketing.emailDelivered` | Den här händelsen spårar när ett e-postmeddelande levererades till en persons e-posttjänst. |
| `directMarketing.emailOpened` | Den här händelsen spårar när en person öppnar ett marknadsföringsmeddelande. |
| `directMarketing.emailSent` | Den här händelsen spårar när ett marknadsföringsmeddelande har skickats till en person. |
| `directMarketing.emailUnsubscribed` | Den här händelsen spårar när en person säger upp prenumerationen på ett marknadsföringsmejl. |
| `display` | **Föråldrat** Använd `decisioning.propositionDisplay` i stället. |
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
| `media.adBreakComplete` | Den här händelsen signalerar att en annonsbrytning har slutförts. |
| `media.adBreakStart` | Den här händelsen signalerar början på ett annonsavbrott. |
| `media.adComplete` | Den här händelsen signalerar att en annons har slutförts. |
| `media.adSkip` | Den här händelsen signalerar när en annons har hoppats över. |
| `media.adStart` | Den här händelsen signalerar början på en annons. |
| `media.bitrateChange` | Den här händelsen signalerar när bithastigheten ändras. |
| `media.bufferStart` | Händelsetypen `media.bufferStart` skickas när bufferten börjar. Det finns ingen specifik `bufferResume`-händelsetyp. Buffertfunktionen anses ha återupptagits när en `play` -händelse skickas efter en `bufferStart` -händelse. |
| `media.chapterComplete` | Den här händelsen signalerar att ett kapitel har slutförts. |
| `media.chapterSkip` | Den här händelsen utlöses när en användare hoppar framåt eller bakåt till ett annat avsnitt eller kapitel. |
| `media.chapterStart` | Den här händelsen signalerar början på ett kapitel. |
| `media.downloaded` | Den här händelsen spårar när media har laddat ned innehåll. |
| `media.error` | Den här händelsen signalerar när ett fel har inträffat under medieuppspelning. |
| `media.pauseStart` | Den här händelsen spårar när en `pauseStart`-händelse har inträffat. Den här händelsen utlöses när en användare initierar en paus i medieuppspelningen. Det finns ingen CV-händelsetyp. Ett cv-värde erhålls när du skickar en uppspelningshändelse efter en `pauseStart`. |
| `media.ping` | Händelsetypen `media.ping` används för att ange pågående uppspelningsstatus. För huvudinnehåll måste den här händelsen skickas var 10:e sekund under uppspelningen, med början 10 sekunder efter uppspelningen. För annonsinnehåll måste det skickas varje sekund under annonsspårning. Ping-händelser ska inte innehålla parameterkartan i begärandetexten. |
| `media.play` | Händelsetypen `media.play` skickas när spelaren övergår till läget `playing` från ett annat läge, till exempel `buffering,` `paused` (när den återupptas av användaren) eller `error` (när den återställs), inklusive scenarier som automatisk uppspelning. Den här händelsen utlöses av spelarens `on('Playing')`-återanrop. |
| `media.sessionComplete` | Den här händelsen skickas när slutet av huvudinnehållet nås. |
| `media.sessionEnd` | Händelsetypen `media.sessionEnd` meddelar Media Analytics-backend om att omedelbart stänga en session när en användare avbryter sin visning och sannolikt inte kommer att returnera. Om den här händelsen inte skickas kommer sessionen att gå ut efter 10 minuters inaktivitet eller 30 minuter utan att spelhuvudet flyttas. Eventuella efterföljande medieanrop med detta sessions-ID ignoreras. |
| `media.sessionStart` | Händelsetypen `media.sessionStart` skickas med sessionsinitieringsanropet. När du får ett svar extraheras sessions-ID från platshuvudet och används för alla efterföljande händelseanrop till samlingsservern. |
| `media.statesUpdate` | Den här händelsen spårar när en `statesUpdate`-händelse har inträffat. Spårningsfunktionerna för spelartillstånd kan kopplas till ett ljud- eller videoflöde. Standardlägena är: `fullscreen`, `mute`, `closedCaptioning`, `pictureInPicture` och `inFocus`. |
| `opportunityEvent.addToOpportunity` | Den här händelsen spårar när en person lades till i en affärsmöjlighet. |
| `opportunityEvent.opportunityUpdated` | Händelsen spårar när en affärsmöjlighet uppdaterades. |
| `opportunityEvent.removeFromOpportunity` | Den här händelsen spårar när en person har tagits bort från en affärsmöjlighet. |
| `personalization.request` | **Föråldrat** Använd `decisioning.propositionFetch` i stället. |
| `pushTracking.applicationOpened` | Den här händelsen spårar när en person öppnar ett program från ett push-meddelande. |
| `pushTracking.customAction` | Den här händelsen spårar när en person har valt en anpassad åtgärd i ett push-meddelande. |
| `web.formFilledOut` | Den här händelsen spårar när en person fyller i ett formulär på en webbsida. |
| `web.webinteraction.linkClicks` | Händelsen signalerar att ett länkklick har spelats in automatiskt av Web SDK. |
| `web.webpagedetails.pageViews` | Den här händelsetypen är standardmetoden för att markera träffen som en sidvy. |
| `location.entry` | Den här händelsen spårar en persons eller enhets inträde på en viss plats. |
| `location.exit` | Den här händelsen spårar en persons eller enhets utträde från en viss plats. |

{style="table-layout:auto"}

### Föreslagna värden för `producedBy` {#producedBy}

I följande tabell visas några godkända värden för `producedBy`:

| Värde | Definition |
| --- | --- |
| `self` | Själv |
| `system` | System |
| `salesRef` | Säljare |
| `customerRep` | Kundrepresentant |
