---
title: Licenshantering och kapacitet
description: Läs mer om licensanvändningen och kapacitetsbegränsningarna i Adobe Experience Platform.
exl-id: 38dad2f1-bd0f-4cc3-a3a6-5105ea866ea4
source-git-commit: 568a0ba7707402496167145ce2673181b240496e
workflow-type: tm+mt
source-wordcount: '1577'
ht-degree: 0%

---


# Licensanvändning och licenskapacitet

>[!AVAILABILITY]
>
>Om du vill använda den här funktionen måste du ha följande behörigheter:
>
>- **Visa kontrollpanel för licensanvändning**
>   - Med den här behörigheten kan du **visa** kapaciteten hemma.
>- **Hantera sandlådor**
>   - Med den här behörigheten kan du **redigera** dina kapacitetstilldelningar.
>
>Mer information om behörigheter i Experience Platform finns i [åtkomstkontrollsöversikten](/help/access-control/home.md#permissions)
>
>Om du har köpt segmentering med hög dataströmning kan du **inte** tilldela din kapacitet med hjälp av Kapacitet. Kontakta Adobe kundtjänst om du vill uppdatera din kapacitet.

I Adobe Experience Platform kan du ta reda på om din organisation har överskridit några av dina skyddsprofiler och få information om hur du åtgärdar dessa problem.

Mer information om skyddsutkast i Experience Platform finns i [Real-Time CDP skyddsöversikt](../../rtcdp/guardrails/overview.md).

## Kapacitet, beteende {#behavior}

>[!CONTEXTUALHELP]
>id="platform_capacity_streamingthroughput"
>title="Strömmande genomströmning"
>abstract="Värdet för direktuppspelningsgenomströmning mäter de kombinerade topphändelserna för inkommande trafik per sekund för direktuppspelning till profiltjänsten, i alla dina produktions- och utvecklingssandlådor."

>[!CONTEXTUALHELP]
>id="platform_capacity_streamingaudiences"
>title="Antal direktuppspelade målgrupper"
>abstract="Maximalt antal direktuppspelade målgrupper per sandlåda. Detta antal är inklusive antalet kantmålgrupper du har i din sandlåda."

>[!CONTEXTUALHELP]
>id="platform_capacity_edgeaudiences"
>title="Edge målgrupper"
>abstract="Maximalt antal kantmålgrupper per sandlåda."

För närvarande stöder Capacity följande tjänster:

- Direktuppspelningssegmentering
- Direktinmatning

Inom dessa tjänster spåras följande skyddsräcken:

- Det högsta antalet direktuppspelade målgrupper är 500
   - Av dessa 500 direktuppspelade målgrupper är det maximala antalet kantmålgrupper 150
- Den initiala kombinerade genomströmningen för direktuppspelning är 1 500 poster per sekund (rps)
   - Detta kombinerade strömmande dataflöde mäter de kombinerade topphändelserna för inkommande trafik per sekund för strömning till kundprofilen i realtid i era produktions- och utvecklingssandlådor.
   - Du kan köpa ytterligare stöd för direktuppspelningssegmentering på upp till 13 500 poster per sekund. Mer information om hur du köper ytterligare berättiganden finns i [Real-Time CDP produktbeskrivning](https://helpx.adobe.com/se/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).

Målgruppskapaciteten är på en **sandbox**-nivå. Det innebär att ni för varje sandlåda ni har i organisationen kan ha 500 direktuppspelade målgrupper, varav 150 av dessa kan vara gränspubliken.

Strömmande genomströmningskapacitet är på **organisationsnivå** och kan distribueras till dina enskilda sandlådor. Med till exempel 1500 rps för strömmande ingspessel kan du ställa in din produktionssandlåda till 1300 rps och din utvecklingssandlåda till 200 rps.

Experience Platform beräknar sandlådans genomströmning i 15 minuters rullande intervall. Detta genomflöde mäts i realtid och data uppdateras var 60:e sekund.

Om din användning når upp till 80 % och 90 % av den licensierade kapaciteten skickar Experience Platform ut ett varningsmeddelande som meddelar att du har nått den angivna kapaciteten. Du kan ändra inställningarna för att anpassa kapacitetsprocenten för att ta emot aviseringen eller ta bort aviseringen helt.

Om din användning överstiger 100 % av den licensierade kapaciteten anses du bryta mot din kapacitet. I det här skedet kommer du att uppleva prestandatlatens och dina servicenivåmål (SLT) **inte** kommer att garanteras.

## Åtkomst {#access}

Välj **[!UICONTROL License usage]** följt av **[!UICONTROL Capacity]** om du vill få åtkomst till översikten över kapacitet.

![Metoden för att komma åt avsnittet Kapacitet är markerad.](/help/landing/images/capacity/access-capacity.png)

Sidan Kapacitetsöversikt visas med information om bland annat en historik över aviseringar och information om din organisations kapacitet.

![Översiktssidan för kapacitet visas i sin helhet, med varningshistorik och kapacitetsinformation.](/help/landing/images/capacity/capacity-overview.png) {zoomable="yes" width="80%"}

### Aviseringshistorik {#alert-history}

Avsnittet **[!UICONTROL Alert history]** visar en lista över de senaste kapacitetsbristerna i din organisation.

![Avsnittet Varningshistorik visas.](/help/landing/images/capacity/alert-history.png)

| Kolumnnamn | Beskrivning |
| ----------- | ----------- |
| Sandbox | Namnet på sandlådan där kapacitetsöverträdelsen inträffade. |
| Varning | Den kapacitet som har brutits i sandlådan. |
| Tidsstämpel | Data och tid då överträdelsen inträffade. |

Om du vill visa en fullständig historik över aviseringar för din organisation väljer du ikonen ![tre punkter](/help/images/icons/more.png) följt av **[!UICONTROL View all]**.

![Den fullständiga aviseringshistoriken visas för en organisation.](/help/landing/images/capacity/full-alert-history.png)

### Kapacitetsinformation {#capacity-details}

Avsnittet Kapacitetsinformation innehåller information om organisationens kapacitet. I det här avsnittet kan du filtrera efter sandlåda och ändra uppslagsperioden.

![Sandlådeväljaren och datumväljaren för uppslagsperioden markeras.](/help/landing/images/capacity/filter-sandbox-and-date.png)

För närvarande visas kapacitetsinformation om strömmande dataflöde, direktuppspelande målgrupper och edge-målgrupper.

#### Strömmande genomströmning {#streaming-throughput}

I avsnittet för direktuppspelning visas information om direktuppspelningsflödet i organisationens sandlådor. Värdet för direktuppspelningsgenomströmning mäter de kombinerade topphändelserna för inkommande trafik per sekund för direktuppspelning till profiltjänsten.

![Avsnittet för direktuppspelad dataflöde på sidan med kapacitetsinformation visas.](/help/landing/images/capacity/streaming-throughput-section.png)

| Kolumnnamn | Beskrivning |
| ----------- | ----------- |
| Sandbox | Namnet på sandlådan. |
| Tjänster | Tjänsten som används av sandlådan. För närvarande är det enda värdet som stöds Profil. |
| Användning (högsta) | Högsta strömningsflöde för data i sandlådan inom den valda uppslagsperioden. |
| Kapacitet | Högsta strömningsgenomströmning för sandlådan. |
| Överträdelse | Om en överträdelse har inträffat, typen av överträdelse för strömmande dataflöde. |
| Rekommenderade åtgärder | En kolumn som beskriver den rekommenderade åtgärden för att åtgärda överträdelsen. |

Du kan markera den enskilda sandlådan om du vill se en mer detaljerad vy över sandlådans strömningsflöde.

![En sandlåda är markerad i avsnittet för direktuppspelning.](/help/landing/images/capacity/select-sandbox.png)

Sidan med information om direktuppspelad dataflöde visas. Du kan se ett diagram som visar flödet för förfrågningar jämfört med kapacitetsgränsen, en lista över sandlådor och deras genomströmningar samt en knapp för att allokera organisationens kapacitet.

![Genomströmningssidan för direktuppspelning visas, med detaljerad information om strömningsflödet för den valda sandlådan.](/help/landing/images/capacity/streaming-capacity-allocation.png)

Välj **[!UICONTROL Allocate capacities]** om du vill uppdatera organisationens kapacitet för direktuppspelning.

![Knappen Allokera kapacitet är markerad på sidan med information om direktuppspelad dataflöde.](/help/landing/images/capacity/select-allocate.png)

Allokeringssidan visas. På den här sidan kan du ange din kapacitet för dina olika sandlådor. Summan av all kapacitet **måste** som är lika med organisationens totala kapacitet.

![Sidan för kapacitetstilldelning visas.](/help/landing/images/capacity/allocate-capacity.png)

>[!NOTE]
>
>Du kan bara ange den nya kapaciteten i order om **100**. Du kan till exempel ange värdet för sandlådans nya kapacitet till 300 eller 500, men du **kan inte** ange värdet 450.
>
>Om värdet inte ligger i storleksordningen 100 avrundas det uppåt eller nedåt.

När du har uppdaterat kapacitetsallokeringarna väljer du **[!UICONTROL Save]** för att slutföra uppdateringarna. Observera att det kan ta upp till 10 minuter innan ändringarna återspeglas i organisationen.

#### Antal målgrupper {#audience-count}

I avsnitten **[!UICONTROL Streaming audience count]** och **[!UICONTROL Edge audience count]** visas antalet målgrupper för direktuppspelning och kant i sandlådan samt det maximala antalet målgrupper för direktuppspelning och kant som tillåts i sandlådan.

![Avsnitten för antal målgrupper visas.](/help/landing/images/capacity/audience-count.png)

| Kolumnnamn | Beskrivning |
| ----------- | ----------- |
| Sandbox | Namnet på sandlådan. |
| Tjänster | Tjänsten som används för sandlådan. |
| Användning | Antalet målgrupper av den listade typen i sandlådan. |
| Kapacitet | Det maximala antalet målgrupper av den listade typen som tillåts i sandlådan. |

## Bästa praxis för direktuppspelning {#suggestions}

Du kan lösa dina dataströmningsfel genom att följa någon av följande rekommendationer:

1. Öka den tilldelade kapaciteten för sandlådan.
2. Identifiera dataflöden med högt dataflöde i [övervakningsinstrumentpanelen](/help/dataflows/ui/monitor-streaming-profile.md) och tillämpa strypning eller filtrering mot dessa dataflöden vid behov.
3. Optimera ditt intag genom att använda batchintag för att få lägre latenstid.

Dessutom kan ni titta på era dataflöden och se om ni kan optimera er datastrategi.

| Medverkande faktor | Vad det är | Inverkan på användningsfall | Bästa praxis |
| --- | --- | --- | --- |
| Konvertering från batch till direktuppspelning | Batcharbetsbelastningar som konverteras till strömning kan öka genomströmningen avsevärt, vilket påverkar prestanda och resursallokering. Du kan till exempel utföra en gruppprofilsuppdatering efter en händelse utan hastighetsbegränsningar. | Direktuppspelningsstrategier är inte nödvändiga för gruppanvändning när bearbetning med låg fördröjning inte krävs. | Utvärdera kraven för användningsfall. För utgående batchmarknadsföring bör du överväga att använda [batchingång](/help/ingestion/batch-ingestion/overview.md) i stället för direktuppspelning för att hantera datainmatningen mer effektivt. |
| Onödig datainmatning | Inmatning av data som inte behövs för personalisering ökar genomströmningen utan att något mervärde läggs till, vilket slösar med resurser. Om du till exempel samlar in all analystrafik i profiler, oavsett relevans. | För mycket data som inte är relevanta skapar brus, vilket gör det svårare att identifiera viktiga datapunkter. Det kan också orsaka friktion när man definierar och hanterar målgrupper och profiler. | Importera endast data som behövs för dina användningsfall. Se till att du filtrerar bort onödiga data.<ul><li>**Adobe Analytics**: Använd [radnivåfiltrering](/help/sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-real-time-customer-profile) för att optimera dataanvändningen.</li><li>**Källor**: Använd [[!DNL Flow Service] API:t för att filtrera radnivådata](/help/sources/tutorials/api/filter.md) för källor som stöds, som [!DNL Snowflake] och [!DNL Google BigQuery].</li></li>**Edge datastream**: Konfigurera [dynamiska datastreams](/help/datastreams/configure-dynamic-datastream.md) för filtrering på radnivå av trafik som kommer in från WebSDK.</li></ul> |

## Vanliga frågor och svar {#faq}

I följande avsnitt beskrivs vanliga frågor om kapacitet.

### Kan jag ha en maximal kombinerad genomströmningsgräns som summerar till mindre än min högsta målgräns?

+++ Svar

Nej. Den maximala sammanlagda genomströmningsgränsen **måste** summeras till din organisations säkerhetsgräns.

+++

### Vad händer om jag överskrider min maximala kapacitet?

+++ Svar

Detta beror på vilken kapacitet som överskrids.

Om du för närvarande överskrider det högsta tillåtna antalet målgrupper påverkas inte de överdrivna målgrupperna. Möjligheten att skapa nya målgrupper kan dock begränsas i framtiden.

Om du överskrider strömningsflödet kommer du att uppleva prestandatlatens i din inmatning och segmentering.

+++

### Varför ska jag hålla mig till min maximala kapacitet?

+++ Svar

Om ni arbetar inom era maximala möjligheter kan ni säkerställa att era data är enhetliga och att dataintegriteten är intakt.

Ni ser till att resultatet blir konsekvent vid högbelastade händelser och undviker tekniska problem som kan påverka systemets prestanda negativt och påverka kundupplevelserna längre fram i kedjan, vilket i slutänden förbättrar er datthygien och övergripande systemprestanda.

+++

### Vilka är de bästa sätten att hantera strömmande ingång?

+++ Svar

För att på bästa sätt hantera strömmande ingång bör ni utvärdera era datauppsättningar för att säkerställa att de prioriterar data som är nödvändiga för personalisering.


Om realtidsbearbetning inte behövs bör du använda batchinmatning i stället för direktuppspelning.

+++
