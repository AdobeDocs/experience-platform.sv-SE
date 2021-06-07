---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;Schemas;identityMap;identity map;Identity map;Schema design;Map;event modeling;event modeling;best practices;event;events;
solution: Experience Platform
title: Klassen XDM ExperienceEvent
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över klassen XDM ExperienceEvent och metodtips för händelsedatamodellering.
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: ecb9c9a4158f3d2981ab60ee3bf419464ac7b8f1
workflow-type: tm+mt
source-wordcount: '1559'
ht-degree: 0%

---

# [!DNL XDM ExperienceEvent] class

[!DNL XDM ExperienceEvent] är en XDM-standardklass (Experience Data Model) som gör att du kan skapa en tidsstämplad ögonblicksbild av systemet när en viss händelse inträffar eller när en viss uppsättning villkor har nåtts.

En Experience Event är ett faktaregister över vad som inträffat, inklusive tidpunkten och identiteten för den berörda personen. Händelser kan antingen vara explicita (direkt observerbara mänskliga åtgärder) eller implicita (upphöjda utan en direkt mänsklig åtgärd) och registreras utan aggregering eller tolkning. Mer högnivåinformation om användning av den här klassen i plattformens ekosystem finns i [XDM-översikten](../home.md#data-behaviors).

Själva [!DNL XDM ExperienceEvent]-klassen tillhandahåller flera tidsserierelaterade fält till ett schema. Värdena för vissa av dessa fält fylls i automatiskt när data hämtas:

![](../images/classes/experienceevent/structure.png)

| Egenskap | Beskrivning |
| --- | --- |
| `_id` | En unik strängidentifierare för händelsen. Det här fältet används för att spåra en enskild händelses unika karaktär, för att förhindra datadubblering och för att slå upp händelsen i underordnade tjänster. I vissa fall kan `_id` vara en [UID (Universally Unique Identifier)](https://tools.ietf.org/html/rfc4122) eller [GUID (Global Unique Identifier)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>Om du direktuppspelar data från en källanslutning eller direkt inmatning från en Parquet-fil, bör du generera det här värdet genom att sammanfoga en viss kombination av fält som gör händelsen unik, till exempel ett primärt ID, en tidsstämpel, händelsetyp. Det sammanfogade värdet måste vara en `uri-reference`-formaterad sträng, vilket innebär att alla kolontecken måste tas bort. Efteråt bör det sammanfogade värdet hashas med SHA-256 eller någon annan algoritm som du väljer.<br><br>Det är viktigt att särskilja att  **detta fält inte representerar en identitet som är relaterad till en enskild person**, utan själva dataposten. Identitetsdata som relaterar till en person ska i stället begränsas till [identitetsfält](../schema/composition.md#identity) som tillhandahålls av kompatibla fältgrupper. |
| `eventMergeId` | Om du använder [Adobe Experience Platform Web SDK](../../edge/home.md) för att importera data, representerar detta ID för den inkapslade batch som gjorde att posten skapades. Det här fältet fylls i automatiskt av systemet när data hämtas. Det går inte att använda det här fältet utanför kontexten för en Web SDK-implementering. |
| `eventType` | En sträng som anger händelsens typ eller kategori. Det här fältet kan användas om du vill skilja mellan olika händelsetyper inom samma schema och datauppsättning, till exempel att skilja en produkthändelse från en tilläggshändelse i kundvagnen för ett detaljhandelsföretag.<br><br>Standardvärden för den här egenskapen finns i  [bilagan](#eventType), inklusive beskrivningar av deras avsedda användningsfall. Det här fältet är en utökningsbar uppräkning, vilket innebär att du även kan använda egna händelsetypsträngar för att kategorisera de händelser som du spårar.<br><br>`eventType` begränsar dig till att endast använda en enda händelse per träff i programmet, och därför måste du använda beräkningsfält för att tala om för systemet vilken händelse som är viktigast. Mer information finns i avsnittet [metodtips för beräkningsfält](#calculated). |
| `producedBy` | Ett strängvärde som beskriver producenten eller händelsens ursprung. Detta fält kan användas för att filtrera bort vissa händelseproducenter om det behövs för segmenteringsändamål.<br><br>Vissa föreslagna värden för den här egenskapen finns i  [bilageavsnittet](#producedBy). Det här fältet är en utökningsbar uppräkning, vilket innebär att du kan använda dina egna strängar för att representera olika händelseproducenter. |
| `identityMap` | Ett kartfält som innehåller en uppsättning namngivna identiteter för den person som händelsen gäller för. Det här fältet uppdateras automatiskt av systemet när identitetsdata hämtas. Om du vill använda det här fältet för [Kundprofil för realtid](../../profile/home.md) ska du inte försöka uppdatera fältets innehåll manuellt i dataåtgärderna.<br /><br />Mer information om hur de används finns i avsnittet om identitetskartor i  [grunderna för ](../schema/composition.md#identityMap) schemakompositioner. |
| `timestamp` | En ISO 8601-tidsstämpel för när händelsen inträffade, formaterad enligt [RFC 3339 Section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). Den här tidsstämpeln måste finnas tidigare. Mer information om hur du använder det här fältet finns i avsnittet nedan om [tidsstämplar](#timestamps). |

{style=&quot;table-layout:auto&quot;}

## Bästa tillvägagångssätt för händelsemodellering

I följande avsnitt beskrivs de effektivaste strategierna för att utforma händelsebaserade XDM-scheman (Experience Data Model) i Adobe Experience Platform.

### Tidsstämplar {#timestamps}

Rotfältet `timestamp` i ett händelseschema kan **bara** representera själva händelseobservationen och måste inträffa tidigare. Om dina användningsfall för segmentering kräver användning av tidsstämplar som kan inträffa i framtiden, måste dessa värden begränsas någon annanstans i Experience Event-schemat.

Om ett företag inom rese- och turismbranschen till exempel modellerar en flygbokningshändelse, representerar fältet på klassnivå `timestamp` tiden då reservationshändelsen observerades. Andra tidsstämplar som är relaterade till händelsen, t.ex. startdatumet för resereservationen, ska hämtas i separata fält som tillhandahålls av standardfältgrupper eller anpassade fältgrupper.

![](../images/classes/experienceevent/timestamps.png)

Genom att hålla tidsstämpeln på klassnivå åtskild från andra relaterade datetime-värden i dina händelsescheman kan du implementera flexibla användningsfall för segmentering samtidigt som du bevarar en tidsstämplad redovisning av kundresor i ditt upplevelseprogram.

### Använda beräknade fält {#calculated}

Vissa interaktioner i dina upplevelseprogram kan leda till flera relaterade händelser som tekniskt sett delar samma händelsetidsstämpel och därför kan representeras som en enda händelsepost. Om en kund till exempel visar en produkt på webbplatsen kan det resultera i en händelsepost som har två möjliga `eventType`-värden: en&quot;produktvy&quot;-händelse (`commerce.productViews`) eller en allmän&quot;sidvy&quot;-händelse (`web.webpagedetails.pageViews`). I dessa fall kan du använda beräkningsfält för att hämta de viktigaste attributen när flera händelser fångas in i en enda träff.

[Med Adobe Experience Platform Data ](../../data-prep/home.md) Prepallows du mappa, omvandla och validera data till och från XDM. Med de tillgängliga [mappningsfunktionerna](../../data-prep/functions.md) som tillhandahålls av tjänsten kan du anropa logiska operatorer för att prioritera, omvandla och/eller konsolidera data från poster med flera händelser när de hämtas till Experience Platform. I exemplet ovan kan du ange `eventType` som ett beräkningsfält som prioriterar en&quot;produktvy&quot; framför en&quot;sidvy&quot; när båda förekommer.

Om du hämtar data manuellt till plattformen via användargränssnittet kan du läsa guiden [mappa en CSV-fil till XDM](../../ingestion/tutorials/map-a-csv-file.md) om du vill ha mer information om hur du skapar beräkningsfält.

Om du direktuppspelar data till plattformen med en källanslutning kan du konfigurera källan så att beräkningsfält används i stället. I [dokumentationen för den aktuella källan](../../sources/home.md) finns anvisningar om hur du implementerar beräknade fält när du konfigurerar anslutningen.

## Kompatibla schemafältgrupper {#field-groups}

>[!NOTE]
>
>Namnen på flera fältgrupper har ändrats. Mer information finns i dokumentet om [uppdatering av fältgruppnamn](../field-groups/name-updates.md).

Adobe innehåller flera standardfältgrupper som kan användas med klassen [!DNL XDM ExperienceEvent]. Nedan följer en lista över några vanliga fältgrupper för klassen:

* [[!UICONTROL Campaign Marketing Details]](../field-groups/event/campaign-marketing-details.md)
* [[!UICONTROL Channel Details]](../field-groups/event/channel-details.md)
* [[!UICONTROL Commerce Details]](../field-groups/event/commerce-details.md)
* [[!UICONTROL End User ID Details]](../field-groups/event/enduserids.md)
* [[!UICONTROL Environment Details]](../field-groups/event/environment-details.md)
* [[!UICONTROL Web Details]](../field-groups/event/web-details.md)

## Bilaga

Följande avsnitt innehåller ytterligare information om klassen [!UICONTROL XDM ExperienceEvent].

### Godkända värden för `eventType` {#eventType}

I följande tabell visas de godkända värdena för `eventType`, tillsammans med deras definitioner:

| Värde | Definition |
| --- | --- |
| `advertising.completes` | En mediefil med en tidsgräns har bevakats tills den är klar. Det behöver inte innebära att tittaren tittade på hela videon, eftersom tittaren kunde ha hoppat över i förväg. |
| `advertising.timePlayed` | Beskriver hur mycket tid en användare har lagt på en viss medieresurs med tidsangivelser. |
| `advertising.federated` | Anger om en Experience Event skapades via datafederation (datadelning mellan kunder). |
| `advertising.clicks` | Klicka på åtgärd(er) i en annons. |
| `advertising.conversions` | Fördefinierade åtgärder som utförs av en kund och som utlöser en händelse för prestandautvärdering. |
| `advertising.firstQuartiles` | En digital videoannons har spelat upp 25 % av sin längd med normal hastighet. |
| `advertising.impressions` | Imponering(ar) av en annons till en kund som kan visas. |
| `advertising.midpoints` | En digital videoannons har spelat upp 50 % av sin längd med normal hastighet. |
| `advertising.starts` | En digital videoannons har börjat spelas upp. |
| `advertising.thirdQuartiles` | En digital videoannons har spelat upp 75 % av sin längd med normal hastighet. |
| `web.webpagedetails.pageViews` | En webbsida har fått en eller flera vyer. |
| `web.webinteraction.linkClicks` | En länk har markerats en eller flera gånger. |
| `commerce.checkouts` | En utcheckningshändelse har inträffat för en produktlista. Det kan finnas mer än en utcheckningshändelse om det finns flera steg i en utcheckningsprocess. Om det finns flera steg används tidsstämpeln och sidan/upplevelsen som refereras för varje händelse för att identifiera varje enskild händelse (steg), som representeras i ordning. |
| `commerce.productListAdds` | En produkt har lagts till i produktlistan eller i kundvagnen. |
| `commerce.productListOpens` | En ny produktlista (kundvagn) har initierats eller skapats. |
| `commerce.productListRemovals` | En eller flera produktposter har tagits bort från en produktlista eller kundvagn. |
| `commerce.productListReopens` | En produktlista (kundvagn) som inte längre var tillgänglig (övergiven) har återaktiverats av en kund, till exempel via en återmarknadsföringsaktivitet. |
| `commerce.productListViews` | En produktlista eller kundvagn har fått en eller flera vyer. |
| `commerce.productViews` | En produkt har fått en eller flera vyer. |
| `commerce.purchases` | En beställning har godkänts. Detta är den enda nödvändiga åtgärden i en handelskonvertering. En köphändelse måste ha en produktlista som refereras. |
| `commerce.saveForLaters` | En produktlista har sparats för framtida bruk, till exempel en produktönskelista. |
| `delivery.feedback` | Feedback-händelser för en leverans, till exempel en e-postleverans. |
| `message.feedback` | Feedback-händelser som skickade/studsade/fel för meddelanden som skickats till en kund. |
| `message.tracking` | Spåra händelser som öppna/klicka/anpassade åtgärder för meddelanden som skickas till en kund. |

{style=&quot;table-layout:auto&quot;}

### Föreslagna värden för `producedBy` {#producedBy}

I följande tabell visas några godkända värden för `producedBy`:

| Värde | Definition |
| --- | --- |
| `self` | Själv |
| `system` | System |
| `salesRef` | Säljare |
| `customerRep` | Kundrepresentant |
