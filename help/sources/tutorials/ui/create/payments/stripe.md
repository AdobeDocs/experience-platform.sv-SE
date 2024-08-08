---
title: Hämta in betalningsdata från ditt Stripe-konto till Experience Platform via användargränssnittet.
description: Lär dig hur du importerar betalningsdata från ditt Stripe-konto till Experience Platform med användargränssnittet.
badge: Beta
exl-id: f20c5935-a7c0-4387-b29e-73e78cab4972
source-git-commit: dd9afe650f4c83b3877f980acac66e703e9ae5d8
workflow-type: tm+mt
source-wordcount: '1610'
ht-degree: 0%

---

# Infoga betalningsdata från ditt [!DNL Stripe]-konto till Experience Platform med användargränssnittet

>[!NOTE]
>
>Källan [!DNL Stripe] är i betaversion. Läs [villkoren](../../../../home.md#terms-and-conditions) i källresursöversikten om du vill ha mer information om hur du använder betatecknade källor.

Läs följande självstudiekurs om du vill veta mer om hur du importerar betalningsdata från ditt [!DNL Stripe]-konto till Adobe Experience Platform via användargränssnittet.

## Kom igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata med.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

### Autentisering

Läs [[!DNL Stripe] översikten](../../../../connectors/payments/stripe.md) om du vill ha mer information om hur du hämtar autentiseringsuppgifter.

## Anslut ditt [!DNL Stripe]-konto {#connect}

I plattformsgränssnittet väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i [!UICONTROL Sources]. Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under kategorin *Betalningar* väljer du **[!DNL Stripe]** och sedan **[!UICONTROL Set up]**.

>[!TIP]
>
>Källor i källkatalogen visar alternativet **[!UICONTROL Set up]** när en angiven källa ännu inte har något autentiserat konto. När det finns ett autentiserat konto ändras det här alternativet till **[!UICONTROL Add data]**.

![Källkatalogen i användargränssnittet i Experience Platform med källkortet Stripe markerat.](../../../../images/tutorials/create/stripe/catalog.png)

Sidan **[!UICONTROL Connect Stripe account]** visas. På den här sidan kan du antingen använda nya eller befintliga autentiseringsuppgifter.

>[!BEGINTABS]

>[!TAB Skapa ett nytt konto]

Om du vill skapa ett nytt konto väljer du **[!UICONTROL New account]** och anger ett namn, en valfri beskrivning och dina autentiseringsuppgifter.

När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![Det nya gränssnittet för att skapa konton i källarbetsflödet.](../../../../images/tutorials/create/stripe/new.png)

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Åtkomsttoken | Åtkomsttoken för [!DNL Stripe]. Mer information om hur du hämtar din åtkomsttoken finns i [[!DNL Stripe] autentiseringsguiden](../../../../connectors/payments/stripe.md). |

>[!TAB Använd ett befintligt konto]

Om du vill använda ett befintligt konto väljer du **[!UICONTROL Existing account]** och sedan det konto som du vill använda i den befintliga kontokatalogen.

Välj **[!UICONTROL Next]** om du vill fortsätta.

![Den befintliga kontourvalssidan för källkatalogen.](../../../../images/tutorials/create/stripe/existing.png)

>[!ENDTABS]

## Markera data {#select-data}

Nu när du har åtkomst till ditt konto måste du identifiera rätt sökväg till de [!DNL Stripe]-data som du vill importera. Markera **[!UICONTROL Resource path]** och välj sedan den slutpunkt från vilken du vill importera data. De tillgängliga [!DNL Stripe] slutpunkterna är:

* Avgifter
* Prenumerationer
* Återbetalningar
* Saldotransaktioner
* Kunder
* Priser

![Listrutan Resurssökväg.](../../../../images/tutorials/create/stripe/select-resource-path.png)

När du har valt slutpunkten uppdateras gränssnittet till en förhandsgranskningsskärm och datastrukturen för den [!DNL Stripe]-slutpunkt du valde visas. Välj **[!UICONTROL Next]** om du vill fortsätta.

![Förhandsgranskningsfönstret för dina Stripe-data.](../../../../images/tutorials/create/stripe/preview.png)

## Ange information om datauppsättning och dataflöde {#provide-dataset-and-dataflow-details}

Därefter måste du ange information om datauppsättningen och dataflödet.

### Information om datauppsättning {#dataset-details}

En datauppsättning är en lagrings- och hanteringskonstruktion för en datamängd, vanligtvis en tabell, som innehåller ett schema (kolumner) och fält (rader). Data som har inhämtats till Experience Platform lagras i datasjön som datauppsättningar. Under det här steget kan du skapa en ny datauppsättning eller använda en befintlig datauppsättning.

>[!BEGINTABS]

>[!TAB Använd en ny datauppsättning]

Om du vill använda en ny datauppsättning väljer du **[!UICONTROL New dataset]** och anger sedan ett namn och en valfri beskrivning för datauppsättningen. Du måste också välja ett XDM-schema (Experience Data Model) som datauppsättningen följer.

![Det nya gränssnittet för val av datauppsättning.](../../../../images/tutorials/create/stripe/new-dataset.png)

| Ny datauppsättningsinformation | Beskrivning |
| --- | --- |
| Namn på utdatauppsättning | Namnet på den nya datauppsättningen. |
| Beskrivning | (Valfritt) En kort förklaring av den nya datauppsättningen. |
| Schema | En listruta med scheman som finns i organisationen. Du kan också skapa ett eget schema före källkonfigurationsprocessen. Mer information finns i guiden om att [skapa ett XDM-schema i användargränssnittet](../../../../../xdm/tutorials/create-schema-ui.md). |

>[!TAB Använd en befintlig datamängd]

Om du redan har en befintlig datauppsättning väljer du **[!UICONTROL Existing dataset]** och använder sedan alternativet **[!UICONTROL Advanced search]** för att visa ett fönster med alla datauppsättningar i organisationen, inklusive deras respektive information, t.ex. om de har aktiverats för förtäring i kundprofilen i realtid eller inte.

![Det befintliga gränssnittet för val av datauppsättning.](../../../../images/tutorials/create/stripe/existing-dataset.png)

>[!ENDTABS]

+++Välj om du vill ha steg för att aktivera profilintagning, feldiagnostik och partiell förtäring.

Om din datauppsättning är aktiverad för kundprofil i realtid kan du under det här steget växla **[!UICONTROL Profile dataset]** för att aktivera dina data för profilinmatning. Du kan också använda det här steget för att aktivera **[!UICONTROL Error diagnostics]** och **[!UICONTROL Partial ingestion]**.

* **[!UICONTROL Error diagnostics]**: Välj **[!UICONTROL Error diagnostics]** om du vill instruera källan att skapa feldiagnostik som du kan referera till senare när du övervakar datauppsättningsaktiviteten och dataflödesstatusen.
* **[!UICONTROL Partial ingestion]**: Partiell gruppinmatning är möjligheten att importera data som innehåller fel, upp till ett visst konfigurerbart tröskelvärde. Med den här funktionen kan du importera alla korrekta data till Experience Platform, medan alla felaktiga data batchas separat med information om varför de är ogiltiga.

+++

### Information om dataflöde {#dataflow-details}

När datauppsättningen har konfigurerats måste du ange information om dataflödet, inklusive ett namn, en valfri beskrivning och aviseringskonfigurationer.

![Konfigurationssteget för dataflödesinformation.](../../../../images/tutorials/create/stripe/dataflow-detail.png)

| Dataflödeskonfigurationer | Beskrivning |
| --- | --- |
| Dataflödesnamn | Dataflödets namn.  Som standard används namnet på filen som importeras. |
| Beskrivning | (Valfritt) En kort beskrivning av dataflödet. |
| Larm | Experience Platform kan skapa händelsebaserade aviseringar som användare kan prenumerera på. Dessa alternativ kräver alla ett öppet dataflöde för att de ska aktiveras.  Mer information finns i [varningsöversikten](../../alerts.md) <ul><li>**Källdataflödeskörning Start**: Välj den här aviseringen för att få ett meddelande när dataflödeskörningen börjar.</li><li>**Källdataflödet har körts**: Välj den här aviseringen om du vill få ett meddelande om dataflödet slutar utan fel.</li><li>**Körningsfel för källdataflöde**: Välj den här aviseringen för att få ett meddelande om dataflödet avslutas med fel.</li></ul> |

När du är klar väljer du **[!UICONTROL Next]** för att fortsätta.

## Mappa fält till ett XDM-schema {#mapping}

**[!UICONTROL Mapping]**-steget visas. Använd mappningsgränssnittet för att mappa källdata till rätt schemafält innan data hämtas till Experience Platform. En utförlig guide om hur du använder mappningsgränssnittet finns i [Användargränssnittshandboken för dataförberedelser](../../../../../data-prep/ui/mapping.md) för mer information.

![Mappningsgränssnittet för källarbetsflödet.](../../../../images/tutorials/create/stripe/mapping.png)

## Konfigurera matningsschema {#scheduling}

Använd sedan schemaläggningsgränssnittet för att skapa ett intag-schema för dataflödet.

Välj frekvenslistrutan för att konfigurera dataflödets matningsfrekvens.

![Listrutan med frekvens.](../../../../images/tutorials/create/stripe/frequency.png)

Du kan också välja kalenderikonen och använda en popup-kalender för att konfigurera starttiden för inmatningen.

![Den konfigurerbara kalendern för schemaläggning.](../../../../images/tutorials/create/stripe/calendar.png)

| Schemaläggningskonfiguration | Beskrivning |
| --- | --- |
| Frekvens | Konfigurera frekvens för att ange hur ofta dataflödet ska köras. Du kan ange frekvensen till: <ul><li>**En gång**: Ställ in din frekvens på `once` för att skapa en engångsinmatning. Konfigurationer för intervall och bakåtfyllnad är inte tillgängliga när ett dataflöde för engångsinmatning skapas. Som standard är schemaläggningsfrekvensen inställd på en gång.</li><li>**Minut**: Ställ in din frekvens på `minute` för att schemalägga ditt dataflöde att importera data per minut.</li><li>**Timme**: Ställ in din frekvens på `hour` för att schemalägga ditt dataflöde att importera data per timme.</li><li>**Dag**: Ställ in din frekvens på `day` för att schemalägga ditt dataflöde att importera data per dag.</li><li>**Vecka**: Ställ in din frekvens på `week` för att schemalägga ditt dataflöde att importera data per vecka.</li></ul> |
| Intervall | När du har valt en frekvens kan du konfigurera intervallinställningen för att upprätta en tidsram mellan varje intag. Om du t.ex. anger din frekvens som dag och konfigurerar intervallet till 15, kommer dataflödet att köras var 15:e dag. Du kan inte ange intervallet till noll. Det minsta tillåtna intervallvärdet för varje frekvens är följande:<ul><li>**En gång**: ingen/a</li><li>**Minut**: 15</li><li>**Timme**: 1</li><li>**Dag**: 1</li><li>**Vecka**: 1</li></ul> |
| Starttid | Tidsstämpeln för den projicerade körningen visas i UTC-tidszonen. |
| Backfill | Backfill avgör vilka data som hämtas från början. Om bakåtfyllning är aktiverad, kommer alla aktuella filer i den angivna sökvägen att importeras under det första schemalagda intaget. Om underfyllning är inaktiverad importeras endast de filer som läses in mellan den första importkörningen och starttiden. Filer som lästs in före starttiden importeras inte. |

Välj **[!UICONTROL Next]** när du har konfigurerat dataflödets schema för inmatning.

![Källarbetsflödets schemaläggningsgränssnitt.](../../../../images/tutorials/create/stripe/scheduling.png)

## Granska ditt dataflöde

Det sista steget i processen för att skapa dataflöde är att granska dataflödet innan det körs. Använd steget **[!UICONTROL Review]** om du vill granska informationen om det nya dataflödet innan det körs. Detaljerna är grupperade i följande kategorier:

* **Anslutning**: Visar källtypen, den relevanta sökvägen för den valda källfilen och antalet kolumner i källfilen.
* **Tilldela datauppsättnings- och mappningsfält**: Visar vilka datauppsättningar som källdata importeras till, inklusive det schema som datauppsättningen följer.
* **Schemaläggning**: Visar den aktiva perioden, frekvensen och intervallet för intagsschemat.

När du har granskat dataflödet väljer du **[!UICONTROL Finish]** och tillåt en tid innan dataflödet skapas.

![Granskningssteget för källarbetsflödet.](../../../../images/tutorials/create/stripe/review.png)

## Nästa steg

Genom att följa den här självstudiekursen har du skapat ett dataflöde som skickar betalningsdata från källan [!DNL Stripe] till Experience Platform. Ytterligare resurser finns i dokumentationen nedan.

### Övervaka dataflödet

När dataflödet har skapats kan du övervaka de data som hämtas genom det för att visa information om hur mycket data som har importerats, hur bra de är och vilka fel som har uppstått. Mer information om hur du övervakar dataflöde finns i självstudiekursen [Övervaka konton och dataflöden i användargränssnittet](../../../../../dataflows/ui/monitor-sources.md).

### Uppdatera ditt dataflöde

Om du vill uppdatera konfigurationer för schemaläggning, mappning och allmän information för dina dataflöden går du till självstudiekursen [Uppdatera källornas dataflöden i användargränssnittet](../../update-dataflows.md).

### Ta bort ditt dataflöde

Du kan ta bort dataflöden som inte längre är nödvändiga eller som har skapats felaktigt med funktionen **[!UICONTROL Delete]** som finns på arbetsytan i **[!UICONTROL Dataflows]**. Mer information om hur du tar bort dataflöden finns i självstudiekursen [Ta bort dataflöden i användargränssnittet](../../delete.md).
