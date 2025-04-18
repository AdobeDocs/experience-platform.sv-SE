---
title: Användargränssnittshandbok för beräknade attribut
description: Lär dig hur du skapar, visar och uppdaterar beräknade attribut med Adobe Experience Platform-gränssnittet.
exl-id: bc621167-6dba-473e-90e4-aac7ceb6579a
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1497'
ht-degree: 0%

---

# Användargränssnittshandbok för beräknade attribut

>[!NOTE]
>
>För att få åtkomst till beräknade attribut måste du ha rätt behörighet (**Visa beräknade attribut** och **Hantera beräknade attribut**). Mer information om vilka behörigheter som krävs finns i [åtkomstkontrollsdokumentationen](../../access-control/home.md). Om du vill lära dig hur du tillämpar de här behörigheterna läser du [handboken om att hantera behörigheter](../../access-control/ui/permissions.md).

I Adobe Experience Platform är beräknade attribut funktioner som används för att samla data på händelsenivå i attribut på profilnivå. Funktionerna beräknas automatiskt så att de kan användas för segmentering, aktivering och personalisering.

I det här dokumentet finns en guide om hur du skapar och uppdaterar beräknade attribut med hjälp av användargränssnittet i Adobe Experience Platform.

## Komma igång

Den här gränssnittshandboken kräver förståelse för de olika [!DNL Experience Platform]-tjänsterna som används för att hantera [!DNL Real-Time Customer Profiles]. Innan du läser den här handboken eller arbetar i användargränssnittet bör du läsa dokumentationen för följande tjänster:

- [[!DNL Real-Time Customer Profile]](../home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata med.

## Visa beräknade attribut {#view}

I Experience Platform-gränssnittet väljer du **[!UICONTROL Profiles]** i den vänstra navigeringen, följt av **[!UICONTROL Computed attributes]**, för att se en lista över beräknade attribut som är tillgängliga för din organisation. Detta innehåller information om det beräknade attributets namn, beskrivning, senaste utvärderingsdatum och senaste utvärderingsstatus.

![Avsnittet [!UICONTROL Profile] och flikarna [!UICONTROL Computed attributes] är markerade och visar hur användarna kommer åt bläddringssidan för beräknade attribut.](./images/ui/browse.png)

Om du vill välja vilka fält som ska visas kan du välja ![ikonen för att konfigurera kolumner](/help/images/icons/column-settings.png) och lägga till eller ta bort vilka fält som ska visas.

| Fält | Beskrivning |
| ----- | ----------- |
| [!UICONTROL Name] | Det beräknade attributets visningsnamn. |
| [!UICONTROL Description] | Beskrivningen av det beräknade attributet. |
| [!UICONTROL Evaluation method] | Utvärderingsmetoden för det beräknade attributet. För närvarande stöds bara **batch**. |
| [!UICONTROL Last evaluated] | Den här tidsstämpeln representerar den senaste lyckade utvärderingskörningen. Endast händelser som inträffade **före** den här tidsstämpeln beaktas vid den senaste lyckade utvärderingen. |
| [!UICONTROL Last evaluation status] | Status som anger om det beräknade attributet har beräknats korrekt i den senaste utvärderingskörningen. Möjliga värden är **[!UICONTROL Success]** eller **[!UICONTROL Failed]**. |
| [!UICONTROL Refresh frequency] | En indikation på hur ofta det beräknade attributet förväntas uppdateras. Möjliga värden är timme, dag, vecka eller månad. |
| [!UICONTROL Fast refresh] | Ett värde som visar om snabb uppdatering har aktiverats för det här beräkningsattributet eller inte. Om snabb uppdatering är aktiverad kan det beräknade attributet uppdateras dagligen i stället för varje vecka, varannan vecka eller månad. Det här värdet gäller endast för beräknade attribut med en uppslagsperiod som är större än en vecka. |
| [!UICONTROL Lifecycle status] | Det beräknade attributets aktuella status. Det finns tre möjliga statusar: <ul><li>**[!UICONTROL Draft]:** Det beräknade attributet har **inte** ett fält på schemat än. I det här läget kan attributet beräknas. </li><li>**[!UICONTROL Published]:** Det beräknade attributet har ett fält skapat i schemat och är klart att användas. I det här läget kan det beräknade attributet **inte redigeras**.</li><li>**[!UICONTROL Inactive]:** Det beräknade attributet är inaktiverat. Mer information om inaktiv status finns på sidan [Frågor och svar](./faq.md#inactive-status). </li> |
| [!UICONTROL Created] | En tidsstämpel som visar det datum och den tidpunkt då det beräknade attributet skapades. |
| [!UICONTROL Last modified] | En tidsstämpel som visar det datum och den tidpunkt då det beräknade attributet senast ändrades. |

Du kan även filtrera de beräknade attribut som visas baserat på livscykelstatusen. Välj ikonen ![tratt](/help/images/icons/filter.png) .

![Filterikonen är markerad.](./images/ui/select-filter.png)

Du kan nu välja att filtrera de beräknade attributen efter status ([!UICONTROL Draft], [!UICONTROL Published] och [!UICONTROL Inactive]).

![De alternativ som du kan filtrera de beräknade attributen med markeras. De här alternativen är [!UICONTROL Draft], [!UICONTROL Published] och [!UICONTROL Inactive].](./images/ui/view-filters.png)

Dessutom kan du välja ett beräknat attribut för att få mer detaljerad information om det. Mer information om informationssidan för beräknade attribut finns i avsnittet [Visa information om ett beräknat attribut](#view-details).

## Skapa ett beräknat attribut {#create}

Om du vill skapa ett nytt beräknat attribut väljer du **[!UICONTROL Create computed attribute]** för att ange det nya beräknade attributarbetsflödet.

![Knappen [!UICONTROL Create computed attributes] är markerad och visar för användarna hur man kommer till sidan Skapa ett beräknat attribut.](./images/ui/create.png)

Sidan **[!UICONTROL Create computed attribute]** visas. På den här sidan kan du lägga till grundläggande information för det beräknade attribut som du vill skapa.

| Fält | Beskrivning |
| ----- | ----------- |
| [!UICONTROL Display name] | Namnet som det beräknade attributet kommer att vara känt av. Du bör behålla det här visningsnamnet unikt för varje beräknat attribut. Det här visningsnamnet bör innehålla identifierare som är relaterade till det beräknade attributet. Exempel:&quot;Summan av inköp av skor de senaste 7 dagarna&quot;. |
| [!UICONTROL Field name] | Ett namn som används för att referera till det beräknade attributet i andra tjänster i senare led. Det här namnet hämtas automatiskt från visningsnamnet och skrivs i camelCase. |
| [!UICONTROL Description] | En beskrivning av det beräknade attributet som du försöker skapa. |

![Avsnittet [!UICONTROL Basic information] på sidan [!UICONTROL Create computed attribute] är markerat.](./images/ui/basic-information.png)

När du har lagt till den beräknade attributinformationen kan du börja definiera reglerna.

### Ange villkor för händelsefiltrering

Om du vill skapa en regel väljer du först attribut från avsnittet **[!UICONTROL Events]** för att filtrera ned händelser som du vill aggregera på. För närvarande stöds endast händelseattribut av icke-arraytyp.

![Avsnittet [!UICONTROL Events] är markerat.](./images/ui/events.png)

När du har valt vilket attribut som ska användas i den beräknade attributdefinitionen kan du välja vilket det här värdet ska jämföras med.

![De tillgängliga jämförelsetyperna visas.](./images/ui/select-comparison.png)

### Använd sammanställningsfunktion

Nu kan du använda en funktion för fältet från villkorliga utdata. Välj först aggregeringsfunktionstypen. De tillgängliga alternativen är [!UICONTROL Sum], [!UICONTROL Min], [!UICONTROL Max], [!UICONTROL Count] och [!UICONTROL Most Recent]. Mer information om de här funktionerna finns i avsnittet [funktioner](./overview.md#functions) i översikten över beräknade attribut.

![De beräknade attributfunktionerna visas.](./images/ui/select-function.png)

När du har valt en funktion kan du välja vilket fält som ska användas. Vilka fält som kan väljas beror på vilken funktion som valts.

![Det markerade fältet visar attributet som du väljer att samla funktionen på.](./images/ui/select-eligible-field.png)

### Varaktighet för uppslag

När du har använt aggregeringsfunktionen måste du definiera uppslagsperioden för det beräknade attributet. Den här uppslagsperioden anger hur lång tid du vill samla händelser på. Den här uppslagstiden kan anges i timmar, dagar, veckor eller månader.

![Uppslagets varaktighet är markerad.](./images/ui/select-lookback-duration.png)

### Snabb uppdatering {#fast-refresh}

>[!CONTEXTUALHELP]
>id="platform_profile_computedAttributes_fastRefresh"
>title="Snabb uppdatering"
>abstract="Snabb uppdatering gör att du kan uppdatera dina attribut. Om du aktiverar det här alternativet kan du uppdatera dina beräknade attribut dagligen, även under längre uppslagsperioder, så att du snabbt kan reagera på användaraktiviteter. Det här värdet gäller endast för beräknade attribut med en uppslagsperiod som är större än en vecka."

När du använder aggregeringsfunktionen kan du aktivera snabb uppdatering om uppslagsperioden är längre än en vecka.

![Kryssrutan [!UICONTROL Fast Refresh] är markerad.](./images/ui/enable-fast-refresh.png)

Snabb uppdatering gör att du kan uppdatera dina attribut. Om du aktiverar det här alternativet kan du uppdatera dina beräknade attribut dagligen, även under längre uppslagsperioder, så att du snabbt kan reagera på användaraktiviteter.

Mer information om snabb uppdatering finns i avsnittet [snabbuppdatering](./overview.md#fast-refresh) i översikten över beräknade attribut.

När de här stegen är slutförda kan du nu antingen välja att spara det beräknade attributet som ett utkast eller att publicera det direkt.

![Knapparna [!UICONTROL Save as draft] och [!UICONTROL Publish] är markerade.](./images/ui/draft-or-publish.png)

## Visa information om ett beräknat attribut {#view-details}

Om du vill visa information om ett beräknat attribut markerar du det beräknade attributet som du vill se information om på sidan [!UICONTROL **Bläddra**].

![Ett beräknat attribut är markerat.](./images/ui/select.png)

Sidans innehåll skiljer sig åt beroende på om det beräknade attributet är **[!UICONTROL Published]** eller **[!UICONTROL Draft]**.

### Publicerat beräknat attribut {#published}

När du väljer ett publicerat beräknat attribut visas detaljsidan för beräknade attribut.

![Detaljsidan för det beräknade attributet visas.](./images/ui/details.png)

På den här sidan visas en sammanfattning av det beräknade attributets detaljer samt ett diagram som visar värdefördelningen samt exempelprofiler som kvalificerar för det beräknade attributet.

>[!NOTE]
>
>Värdefördelningen återspeglar fördelningen av attributvärden för profiler vid tidpunkten för samplingsjobbet. Det beräknade attributvärdet i exempelprofilen återspeglar det senaste sammanfogade profilvärdet för ett fåtal exempelprofiler.

### Utkast för beräknat attribut {#draft}

När du väljer ett utkast till beräknat attribut visas sidan **[!UICONTROL Edit computed attributes]**. På den här sidan, på liknande sätt som på sidan [!UICONTROL Create computed attributes], kan du redigera det beräknade attributets grundläggande information samt dess definition innan du låter dig uppdatera utkastet eller publicera det.

![Sidan [!UICONTROL Edit computed attributes] visas.](./images/ui/edit.png)

## Använda beräknade attribut {#usage}

>[!IMPORTANT]
>
>Om du använder ett beräknat attribut med funktionen **Senaste** i en segmentdefinition måste **du** inkludera **både** värdet och tidsstämpelvärdet i det beräknade attributobjektet.
>
>Om du till exempel skapar en segmentdefinition som söker efter&quot;Alla profiler som har en giltig e-postadress&quot; där e-postadressfältet fylls i med ett beräknat attribut med den senaste funktionen, **måste** inkludera både e-postadressens värde finns **och** e-postadressens tidsstämpel finns.

När du har skapat ett beräknat attribut kan du använda **publicerade** beräknade attribut i andra underordnade tjänster. Eftersom beräknade attribut är profilattributfält som skapats i ditt profilunionsschema kan du söka efter beräknade attributvärden för en kundprofil i realtid, använda dem i en målgrupp, aktivera dem till ett mål eller använda dem för personalisering på resor i Adobe Journey Optimizer.

>[!NOTE]
>
>De beräknade attributen **kan inte** användas i målgruppens **kompositioner**.

![Segmentbyggaren visas och visar ett beräknat attribut som en del av segmentdefinitionskompositionen.](./images/ui/use-ca.png)

## Nästa steg

Läs [översikten över beräknade attribut](./overview.md) om du vill veta mer om beräknade attribut. Mer information om hur du skapar och konfigurerar beräknade attribut med API finns i [utvecklarhandboken för beräknade attribut](./api.md).
