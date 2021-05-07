---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;individuell profil;fält;scheman;scheman;identityMap;identity map;identity map;Schema design;map;union schema;union schema
solution: Experience Platform
title: Klassen XDM ExperienceEvent
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över klassen XDM ExperienceEvent.
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---

# [!DNL XDM ExperienceEvent] class

[!DNL XDM ExperienceEvent] är en standard-XDM-klass som gör att du kan skapa en tidsstämplad ögonblicksbild av systemet när en viss händelse inträffar eller när en viss uppsättning villkor har nåtts.

En Experience Event är ett faktaregister över vad som inträffat, inklusive tidpunkten och identiteten för den berörda personen. Händelser kan antingen vara explicita (direkt observerbara mänskliga åtgärder) eller implicita (upphöjda utan en direkt mänsklig åtgärd) och registreras utan aggregering eller tolkning. Mer högnivåinformation om användning av den här klassen i plattformens ekosystem finns i [XDM-översikten](../home.md#data-behaviors).

Själva [!DNL XDM ExperienceEvent]-klassen tillhandahåller flera tidsserierelaterade fält till ett schema. Värdena för vissa av dessa fält fylls i automatiskt när data hämtas:

<img src="../images/classes/experienceevent.png" width="650" /><br />

| Egenskap | Beskrivning |
| --- | --- |
| `_id` | En unik systemgenererad strängidentifierare för händelsen. Det här fältet används för att spåra en enskild händelses unika karaktär, förhindra datadubblering och för att söka efter händelsen i underordnade tjänster. Eftersom det här fältet genereras av systemet bör det inte anges som ett explicit värde vid datainmatning.<br><br>Det är viktigt att särskilja att detta fält inte  **ger** en identitet som är relaterad till en enskild person, utan snarare själva registreringen av uppgifter. Identitetsdata som relaterar till en person ska i stället begränsas till [identitetsfält](../schema/composition.md#identity). |
| `eventMergeId` | ID:t för den inkapslade batchen som gjorde att posten skapades. Det här fältet fylls i automatiskt av systemet när data hämtas. |
| `eventType` | En sträng som anger postens primära händelsetyp. Godkända värden och deras definitioner finns i [appendix-avsnittet](#eventType). |
| `identityMap` | Ett kartfält som innehåller en uppsättning namngivna identiteter för den person som händelsen gäller för. Det här fältet uppdateras automatiskt av systemet när identitetsdata hämtas. Om du vill använda det här fältet för [Kundprofil för realtid](../../profile/home.md) ska du inte försöka uppdatera fältets innehåll manuellt i dataåtgärderna.<br /><br />Mer information om hur de används finns i avsnittet om identitetskartor i  [grunderna för ](../schema/composition.md#identityMap) schemakompositioner. |
| `timestamp` | En ISO 8601-tidsstämpel för när händelsen inträffade, formaterad enligt [RFC 3339 Section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6).<br><br>Den här tidsstämpeln kan  **** bara representera observationen av själva händelsen och måste inträffa i det förflutna. Om dina användningsfall för segmentering kräver användning av tidsstämplar som kan inträffa i framtiden (till exempel ett avgångsdatum), måste dessa värden begränsas någon annanstans i Experience Event-schemat. |

## Kompatibla schemafältgrupper {#field-groups}

>[!NOTE]
>
>Namnen på flera fältgrupper har ändrats. Mer information finns i dokumentet om [uppdatering av fältgruppnamn](../field-groups/name-updates.md).

Adobe innehåller flera standardfältgrupper som kan användas med klassen [!DNL XDM ExperienceEvent]. Nedan följer en lista över några vanliga fältgrupper för klassen:

* [[!UICONTROL End User ID Details]](../field-groups/event/enduserids.md)
* [[!UICONTROL Environment Details]](../field-groups/event/environment-details.md)

## Bilaga

Följande avsnitt innehåller ytterligare information om klassen [!UICONTROL XDM ExperienceEvent].

### Godkända värden för xdm:eventType {#eventType}

I följande tabell visas de godkända värdena för `xdm:eventType`, tillsammans med deras definitioner:

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
