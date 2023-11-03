---
title: Användargränssnittshandbok för beräknade attribut
description: Lär dig hur du skapar, visar och uppdaterar beräknade attribut med Adobe Experience Platform-gränssnittet.
exl-id: bc621167-6dba-473e-90e4-aac7ceb6579a
source-git-commit: cf01c18c8ea710492c8a2c8542c8a4580d5f0dcf
workflow-type: tm+mt
source-wordcount: '1488'
ht-degree: 0%

---

# Användargränssnittshandbok för beräknade attribut

>[!NOTE]
>
>För att få åtkomst till beräknade attribut måste du ha rätt behörighet (**Visa beräknade attribut** och **Hantera beräknade attribut**). Mer information om vilka behörigheter som krävs finns i [dokumentation om åtkomstkontroll](../../access-control/home.md). Läs mer om hur du tillämpar dessa behörigheter i [hantera behörighetshandbok](../../access-control/ui/permissions.md).

I Adobe Experience Platform är beräknade attribut funktioner som används för att samla data på händelsenivå i attribut på profilnivå. Funktionerna beräknas automatiskt så att de kan användas för segmentering, aktivering och personalisering.

I det här dokumentet finns en guide om hur du skapar och uppdaterar beräknade attribut med hjälp av användargränssnittet i Adobe Experience Platform.

## Komma igång

Användargränssnittshandboken kräver förståelse för de olika [!DNL Experience Platform] tjänster som ingår i hantering av [!DNL Real-Time Customer Profiles]. Innan du läser den här handboken eller arbetar i användargränssnittet bör du läsa dokumentationen för följande tjänster:

- [[!DNL Real-Time Customer Profile]](../home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.

## Visa beräknade attribut {#view}

I användargränssnittet för Experience Platform väljer du **[!UICONTROL Profiles]** i den vänstra navigeringen, följt av **[!UICONTROL Computed attributes]** om du vill se en lista över de beräknade attributen som är tillgängliga för din organisation. Detta innehåller information om det beräknade attributets namn, beskrivning, senaste utvärderingsdatum och senaste utvärderingsstatus.

![The [!UICONTROL Profile] -avsnittet och [!UICONTROL Computed attributes] flikarna markeras och användarna får se hur de får åtkomst till sidan med beräknade attribut.](./images/ui/browse.png)

Om du vill välja vilka fält som ska visas kan du välja ![ikonen Konfigurera kolumner](./images/ui/configure-icon.png) för att lägga till eller ta bort de fält som du vill ska visas.

| Fält | Beskrivning |
| ----- | ----------- |
| [!UICONTROL Name] | Det beräknade attributets visningsnamn. |
| [!UICONTROL Description] | Beskrivningen av det beräknade attributet. |
| [!UICONTROL Evaluation method] | Utvärderingsmetoden för det beräknade attributet. I nuläget är endast **batch** stöds. |
| [!UICONTROL Last evaluated] | Den här tidsstämpeln representerar den senaste lyckade utvärderingskörningen. Endast händelser som inträffade **före** denna tidsstämpel beaktas i den senaste lyckade utvärderingen. |
| [!UICONTROL Last evaluation status] | Status som anger om det beräknade attributet har beräknats korrekt i den senaste utvärderingskörningen. Möjliga värden är **[!UICONTROL Success]** eller **[!UICONTROL Failed]**. |
| [!UICONTROL Refresh frequency] | En indikation på hur ofta det beräknade attributet förväntas uppdateras. Möjliga värden är timme, dag, vecka eller månad. |
| [!UICONTROL Fast refresh] | Ett värde som visar om snabb uppdatering har aktiverats för det här beräkningsattributet eller inte. Om snabb uppdatering är aktiverad kan det beräknade attributet uppdateras dagligen i stället för varje vecka, varannan vecka eller månad. Det här värdet gäller endast för beräknade attribut med en uppslagsperiod som är större än en vecka. |
| [!UICONTROL Lifecycle status] | Det beräknade attributets aktuella status. Det finns tre möjliga statusar: <ul><li>**[!UICONTROL Draft]:** Det beräknade attributet gör **not** har skapat ett fält i schemat ännu. I det här läget kan attributet beräknas. </li><li>**[!UICONTROL Published]:** Det beräknade attributet har ett fält som har skapats i schemat och är klart att användas. I det här läget är det beräknade attributet **inte** redigeras.</li><li>**[!UICONTROL Inactive]:** Det beräknade attributet är inaktiverat. Mer information om inaktiv status finns i [Vanliga frågor och svar](./faq.md#inactive-status). </li> |
| [!UICONTROL Created] | En tidsstämpel som visar det datum och den tidpunkt då det beräknade attributet skapades. |
| [!UICONTROL Last modified] | En tidsstämpel som visar det datum och den tidpunkt då det beräknade attributet senast ändrades. |

Du kan även filtrera de beräknade attribut som visas baserat på livscykelstatusen. Välj ![tratt](./images/ui/filter-icon.png) -ikon.

![Filterikonen är markerad.](./images/ui/select-filter.png)

Nu kan du välja att filtrera de beräknade attributen efter status ([!UICONTROL Draft], [!UICONTROL Published]och [!UICONTROL Inactive]).

![De alternativ som du kan filtrera de beräknade attributen med markeras. Dessa alternativ innehåller [!UICONTROL Draft], [!UICONTROL Published]och [!UICONTROL Inactive].](./images/ui/view-filters.png)

Dessutom kan du välja ett beräknat attribut för att få mer detaljerad information om det. Mer information om beräknade attribut finns på sidan [visa ett beräknat attributs informationsavsnitt](#view-details).

## Skapa ett beräknat attribut {#create}

Om du vill skapa ett nytt beräknat attribut väljer du **[!UICONTROL Create computed attribute]** för att ange det nya arbetsflödet för beräknade attribut.

![The [!UICONTROL Create computed attributes] knappen är markerad och visar för användarna hur man kommer till sidan för att skapa ett beräknat attribut.](./images/ui/create.png)

The **[!UICONTROL Create computed attribute]** visas. På den här sidan kan du lägga till grundläggande information för det beräknade attribut som du vill skapa.

| Fält | Beskrivning |
| ----- | ----------- |
| [!UICONTROL Display name] | Namnet som det beräknade attributet kommer att vara känt av. Du bör behålla det här visningsnamnet unikt för varje beräknat attribut. Det här visningsnamnet bör innehålla identifierare som är relaterade till det beräknade attributet. Exempel:&quot;Summan av inköp av skor de senaste 7 dagarna&quot;. |
| [!UICONTROL Field name] | Ett namn som används för att referera till det beräknade attributet i andra tjänster i senare led. Det här namnet hämtas automatiskt från visningsnamnet och skrivs i camelCase. |
| [!UICONTROL Description] | En beskrivning av det beräknade attributet som du försöker skapa. |

![The [!UICONTROL Basic information] i [!UICONTROL Create computed attribute] sidan är markerad.](./images/ui/basic-information.png)

När du har lagt till den beräknade attributinformationen kan du börja definiera reglerna.

### Ange villkor för händelsefiltrering

Om du vill skapa en regel måste du först välja attribut från **[!UICONTROL Events]** för att filtrera ned händelser som du vill samla in. För närvarande stöds endast händelseattribut av icke-arraytyp.

![The [!UICONTROL Events] -avsnittet är markerat.](./images/ui/events.png)

När du har valt vilket attribut som ska användas i den beräknade attributdefinitionen kan du välja vilket det här värdet ska jämföras med.

![De tillgängliga jämförelsetyperna visas.](./images/ui/select-comparison.png)

### Använd sammanställningsfunktion

Nu kan du använda en funktion för fältet från villkorliga utdata. Välj först aggregeringsfunktionstypen. Tillgängliga alternativ inkluderar [!UICONTROL Sum], [!UICONTROL Min], [!UICONTROL Max], [!UICONTROL Count]och [!UICONTROL Most Recent]. Mer information om de här funktionerna finns i [funktionsavsnitt](./overview.md#functions) av översikten över beräknade attribut.

![De beräknade attributfunktionerna visas.](./images/ui/select-function.png)

När du har valt en funktion kan du välja vilket fält som ska användas. Vilka fält som kan väljas beror på vilken funktion som valts.

![I det markerade fältet visas det attribut som du väljer att sammanfoga funktionen med.](./images/ui/select-eligible-field.png)

### Varaktighet för uppslag

När du har använt aggregeringsfunktionen måste du definiera uppslagsperioden för det beräknade attributet. Den här uppslagsperioden anger hur lång tid du vill samla händelser på. Den här uppslagstiden kan anges i timmar, dagar, veckor eller månader.

![Uppslagets varaktighet är markerad.](./images/ui/select-lookback-duration.png)

### Snabb uppdatering {#fast-refresh}

>[!CONTEXTUALHELP]
>id="platform_profile_computedAttributes_fastRefresh"
>title="Snabb uppdatering"
>abstract="Snabb uppdatering gör att du kan uppdatera dina attribut. Om du aktiverar det här alternativet kan du uppdatera dina beräknade attribut dagligen, även under längre uppslagsperioder, så att du snabbt kan reagera på användaraktiviteter. Det här värdet gäller endast för beräknade attribut med en uppslagsperiod som är större än en vecka."

När du använder aggregeringsfunktionen kan du aktivera snabb uppdatering om uppslagsperioden är längre än en vecka.

![The [!UICONTROL Fast Refresh] är markerad.](./images/ui/enable-fast-refresh.png)

Snabb uppdatering gör att du kan uppdatera dina attribut. Om du aktiverar det här alternativet kan du uppdatera dina beräknade attribut dagligen, även under längre uppslagsperioder, så att du snabbt kan reagera på användaraktiviteter.

Mer information om snabb uppdatering finns i [snabbuppdateringsavsnitt](./overview.md#fast-refresh) av översikten över beräknade attribut.

När de här stegen är slutförda kan du nu antingen välja att spara det beräknade attributet som ett utkast eller att publicera det direkt.

![The [!UICONTROL Save as draft] och [!UICONTROL Publish] knapparna är markerade.](./images/ui/draft-or-publish.png)

## Visa information om ett beräknat attribut {#view-details}

Om du vill visa information om ett beräknat attribut markerar du det beräknade attributet som du vill se information om på [!UICONTROL **Bläddra**] sida.

![Ett beräknat attribut markeras.](./images/ui/select.png)

Innehållet på sidan varierar beroende på om attributet computed är **[!UICONTROL Published]** eller in **[!UICONTROL Draft]**.

### Publicerat beräknat attribut {#published}

När du väljer ett publicerat beräknat attribut visas detaljsidan för beräknade attribut.

![Detaljsidan för det beräknade attributet visas.](./images/ui/details.png)

På den här sidan visas en sammanfattning av det beräknade attributets detaljer samt ett diagram som visar värdefördelningen samt exempelprofiler som kvalificerar för det beräknade attributet.

>[!NOTE]
>
>Värdefördelningen återspeglar fördelningen av attributvärden för profiler vid tidpunkten för samplingsjobbet. Det beräknade attributvärdet i exempelprofilen återspeglar det senaste sammanfogade profilvärdet för ett fåtal exempelprofiler.

### Utkast för beräknat attribut {#draft}

När du väljer ett utkast till ett beräknat attribut visas **[!UICONTROL Edit computed attributes]** visas. Den här sidan liknar [!UICONTROL Create computed attributes] gör att du kan redigera det beräknade attributets grundläggande information och definition innan du låter dig uppdatera utkastet eller publicera det.

![Sidan [!UICONTROL Edit computed attributes] visas.](./images/ui/edit.png)

## Använda beräknade attribut {#usage}

>[!IMPORTANT]
>
>Om du använder ett beräknat attribut med **Senaste** funktion i en segmentdefinition **måste** include **båda** värdet och tidsstämpelvärdet i det beräknade attributobjektet.
>
>Om du till exempel skapar en segmentdefinition som söker efter&quot;Alla profiler som har en giltig e-postadress&quot; där e-postadressfältet fylls i med ett beräknat attribut med den senaste funktionen, kan du **måste** ta med både e-postadressens värde **och** e-postadressens tidsstämpel finns.

När du har skapat ett beräknat attribut kan du använda **publicerad** beräknade attribut i andra tjänster i senare led. Eftersom beräknade attribut är profilattributfält som skapats i ditt profilunionsschema kan du söka efter beräknade attributvärden för en kundprofil i realtid, använda dem i en målgrupp, aktivera dem till ett mål eller använda dem för personalisering på resor i Adobe Journey Optimizer.

![Segmentverktyget visas och visar ett beräknat attribut som en del av segmentdefinitionskompositionen.](./images/ui/use-ca.png)

## Nästa steg

Läs mer om beräknade attribut i [översikt över beräknade attribut](./overview.md). Information om hur du skapar och konfigurerar beräknade attribut med API:t finns i [utvecklarhandbok för beräknade attribut](./api.md).
