---
title: Acxiom-datainmatning
description: Använd Acxiom-datainmatning för att importera Acxiom-data till Real-Time CDP och berika förstahandsprofiler. Använd era Acxiom-berikade förstapartsprofiler för att förbättra målgrupperna och aktivera i alla marknadsföringskanaler.
last-substantial-update: 2024-03-19T00:00:00Z
badge: Beta
exl-id: a0a080ef-4603-437f-8a68-11dbf530ac90
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1791'
ht-degree: 0%

---

# Skapa en [!DNL Acxiom Data Ingestion]-källanslutning och ett dataflöde i användargränssnittet

>[!NOTE]
>
>Källan [!DNL Acxiom Data Ingestion] är i betaversion. Läs [villkoren](../../../../home.md#terms-and-conditions) i källresursöversikten om du vill ha mer information om hur du använder betatecknade källor.

Använd källan [!DNL Acxiom Data Ingestion] för att importera [!DNL Acxiom]-data till Real-Time Customer Data Platform och berika förstapartsprofiler. Sedan kan du använda dina [!DNL Acxiom]-berikade förstahandsprofiler för att förbättra målgrupper och aktivera i alla marknadsföringskanaler.

I den här självstudiekursen får du lära dig hur du skapar en [!DNL Acxiom Data Ingestion]-källanslutning och ett dataflöde med Adobe Experience Platform användargränssnitt. Källan [!DNL Acxiom Data Ingestion] används för att hämta och mappa svar från förbättringstjänsten [!DNL Acxiom] med Amazon S3 som släpppunkt.

## Förhandskrav {#prerequisites}

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

### Samla in nödvändiga inloggningsuppgifter

Om du vill komma åt din bucket på Experience Platform måste du ange giltiga värden för följande autentiseringsuppgifter:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| [!DNL Acxiom] autentiseringsnyckel | Autentiseringsnyckeln. Du kan hämta värdet från [!DNL Acxiom]-teamet. |
| [!DNL Amazon S3] åtkomstnyckel | Åtkomstnyckel-ID för din bucket. Du kan hämta värdet från [!DNL Acxiom]-teamet. |
| [!DNL Amazon S3] hemlig nyckel | Det hemliga nyckel-ID:t för din bucket. Du kan hämta värdet från [!DNL Acxiom]-teamet. |
| Buckennamn | Det här är din bucket där filer delas. Du kan hämta värdet från [!DNL Acxiom]-teamet. |

>[!IMPORTANT]
>
>Du måste ha både behörighet **[!UICONTROL View Sources]** och behörighet **[!UICONTROL Manage Sources]** aktiverat för ditt konto för att kunna ansluta ditt [!DNL Acxiom]-konto till Experience Platform. Kontakta produktadministratören för att få den behörighet som krävs. Mer information finns i [användargränssnittsguiden för åtkomstkontroll](../../../../../access-control/ui/overview.md).

## Anslut ditt [!DNL Acxiom]-konto

I Experience Platform-gränssnittet väljer du **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan i [!UICONTROL Sources]. På skärmen [!UICONTROL Catalog] visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under kategorin **[!UICONTROL Data & Identity Partners]** väljer du **[!UICONTROL Acxiom Data Ingestion]** och sedan **[!UICONTROL Set up]**.

>[!TIP]
>
>Ett källkort som visar **[!UICONTROL Add data]** betyder att källan redan har ett autentiserat konto. Ett källkort som visar **[!UICONTROL Set up]** innebär å andra sidan att du måste ange autentiseringsuppgifter och skapa ett nytt konto för att kunna använda källan.

![Källkatalogen med Acxiom-källan markerad.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-catalog.png)

### Skapa ett nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och dina [!DNL Acxiom]-inloggningsuppgifter på det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![Källarbetsflödets nya kontogränssnitt.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-new-account.png)

| Referenser | Beskrivning |
| --- | --- |
| Kontonamn | Namnet på kontot. |
| Beskrivning | (Valfritt) En kort förklaring av syftet med kontot. |
| [!DNL Acxiom] autentiseringsnyckel | Den [!DNL Acxiom]-tillhandahållna nyckeln som krävs för kontogodkännande. Detta måste matcha rätt värde innan det går att ansluta till databasen.  Nyckeln måste innehålla 24 tecken och kan bara innehålla: A-Z, a-z och 0-9. |
| S3-åtkomstnyckel | S3-åtkomstnyckeln refererar till Amazon S3-platsen. Detta tillhandahålls av administratören när rollbehörigheter för S3 definieras. |
| S3 hemlig nyckel | Den hemliga nyckeln för S3 refererar till Amazon S3-platsen. Detta tillhandahålls av administratören när rollbehörigheter för S3 definieras. |
| s3SessionToken | (Valfritt) Värdet för autentiseringstoken vid anslutning till S3. |
| serviceUrl | (Valfritt) Den URL-plats som ska användas vid anslutning till S3 på en plats som inte är standard. |
| Buckennamn | (Valfritt) Namnet på den S3-bucket som är inställd på S3 och som fungerar som en startsökväg i datamarkeringen. |
| Mappsökväg | Om du använder underkataloger i en bucket kan du även ange en sökväg som en startsökväg när du väljer data. |

### Använd ett befintligt konto

Om du vill använda ett befintligt konto väljer du **[!UICONTROL Existing account]**.

Välj ett konto i listan om du vill visa information om det kontot. När du har valt ett konto väljer du **[!UICONTROL Next]** för att fortsätta.

![Källarbetsflödets befintliga kontogränssnitt.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-existing-account.png)

## Välj data

Markera den fil som du vill importera från önskad bucket och underkatalog. Du kan förhandsgranska data när du har definierat avgränsare och komprimeringstyp. När du har valt filen väljer du **[!UICONTROL Next]** för att fortsätta.

![Källarbetsflödets gränssnitt för förhandsgranskning av valda data och filer.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-preview.png)

>[!NOTE]
>
>JSON- och Parquet-filtyperna visas, men du behöver eller förväntas inte använda dem under [!DNL Acxiom]-källarbetsflödet.

## Ange information om datauppsättning och dataflöde

Därefter måste du ange information om datauppsättningen och dataflödet.

### Information om datauppsättning

>[!BEGINTABS]

>[!TAB Använd en ny datauppsättning]

En datauppsättning är en lagrings- och hanteringskonstruktion för en datamängd, vanligtvis en tabell, som innehåller ett schema (kolumner) och fält (rader). Data som har inhämtats till Experience Platform lagras i datasjön som datauppsättningar. Om du vill använda en ny datauppsättning väljer du **[!UICONTROL New dataset]**.

![Det nya datauppsättningsgränssnittet.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-new-dataset.png)

| Ny datauppsättningsinformation | Beskrivning |
| --- | --- |
| Namn på utdatauppsättning | Namnet på den nya datauppsättningen. |
| Beskrivning | (Valfritt) En kort förklaring av syftet med datauppsättningen. |
| Schema | En listruta med scheman som finns i organisationen. Du kan också skapa ett eget schema före källkonfigurationsprocessen. Mer information finns i guiden om att [skapa schema i användargränssnittet](../../../../../xdm/tutorials/create-schema-ui.md). |

>[!TAB Använd en befintlig datamängd]

Om du vill använda en befintlig datauppsättning väljer du **[!UICONTROL Existing dataset]**.

Du kan välja **[!UICONTROL Advanced search]** om du vill visa ett fönster med alla datauppsättningar som din organisation använder, inklusive deras respektive information, t.ex. om de har aktiverats för förtäring i kundprofilen i realtid.

![Det befintliga datauppsättningsgränssnittet.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-dataset.png)

>[!ENDTABS]

+++Välj om du vill ha steg för att aktivera profilintagning, feldiagnostik och partiell förtäring.

Om din datauppsättning är aktiverad för kundprofil i realtid kan du under det här steget växla **[!UICONTROL Profile dataset]** för att aktivera dina data för profilinmatning. Du kan också använda det här steget för att aktivera **[!UICONTROL Error diagnostics]** och **[!UICONTROL Partial ingestion]**.

* **[!UICONTROL Error diagnostics]**: Välj **[!UICONTROL Error diagnostics]** om du vill instruera källan att skapa feldiagnostik som du kan referera till senare när du övervakar datauppsättningsaktiviteten och dataflödesstatusen.
* **[!UICONTROL Partial ingestion]**: Partiell gruppinmatning är möjligheten att importera data som innehåller fel, upp till ett visst konfigurerbart tröskelvärde. Med den här funktionen kan du importera alla korrekta data till Experience Platform, medan alla felaktiga data batchas separat med information om varför de är ogiltiga.

+++

### Information om dataflöde

När datauppsättningen har konfigurerats måste du ange information om dataflödet, inklusive ett namn, en valfri beskrivning och aviseringskonfigurationer.

![Gränssnittet för konfiguration av dataflöde.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-dataset-details.png)

| Dataflödeskonfigurationer | Beskrivning |
| --- | --- |
| Dataflödesnamn | Dataflödets namn.  Som standard används namnet på filen som importeras. |
| Beskrivning | (Valfritt) En kort beskrivning av dataflödet. |
| Aviseringar | Experience Platform kan skapa händelsebaserade aviseringar som användare kan prenumerera på. Dessa alternativ är alla ett öppet dataflöde som utlöser dem.  Mer information finns i [varningsöversikten](../../alerts.md) <ul><li>**Källdataflödeskörning Start**: Välj den här aviseringen för att få ett meddelande när dataflödeskörningen börjar.</li><li>**Källdataflödet har körts**: Välj den här aviseringen om du vill få ett meddelande om dataflödet slutar utan fel.</li><li>**Körningsfel för källdataflöde**: Välj den här aviseringen för att få ett meddelande om dataflödet avslutas med fel.</li></ul> |

## Mappning

Använd mappningsgränssnittet för att mappa källdata till rätt schemafält innan data importeras till Experience Platform.  Mer information finns i [mappningsguiden i användargränssnittet](../../../../../data-prep/ui/mapping.md)

![Mappningsgränssnittet.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-mapping.png)

## Schemalägg inmatning av dataflöde

Använd sedan schemaläggningsgränssnittet för att definiera inmatningsschemat för dataflödet.

![Konfigurationsgränssnittet för schemaläggning.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-scheduling.png)

| Schemaläggningskonfiguration | Beskrivning |
| --- | --- |
| Frekvens | Konfigurera frekvens för att ange hur ofta dataflödet ska köras. Du kan ange frekvensen till: <ul><li>**En gång**: Ställ in din frekvens på `once` för att skapa en engångsinmatning. Konfigurationer för intervall och bakåtfyllnad är inte tillgängliga när ett dataflöde för engångsinmatning skapas. Som standard är schemaläggningsfrekvensen inställd på en gång.</li><li>**Minut**: Ställ in din frekvens på `minute` för att schemalägga ditt dataflöde att importera data per minut.</li><li>**Timme**: Ställ in din frekvens på `hour` för att schemalägga ditt dataflöde att importera data per timme.</li><li>**Dag**: Ställ in din frekvens på `day` för att schemalägga ditt dataflöde att importera data per dag.</li><li>**Vecka**: Ställ in din frekvens på `week` för att schemalägga ditt dataflöde att importera data per vecka.</li></ul> |
| Intervall | När du har valt en frekvens kan du konfigurera intervallinställningen för att upprätta en tidsram mellan varje intag. Om du t.ex. anger din frekvens som dag och konfigurerar intervallet till 15, kommer dataflödet att köras var 15:e dag. Du kan inte ange intervallet till noll. Det minsta tillåtna intervallvärdet för varje frekvens är följande:<ul><li>**En gång**: ingen/a</li><li>**Minut**: 15</li><li>**Timme**: 1</li><li>**Dag**: 1</li><li>**Vecka**: 1</li></ul> |
| Starttid | Tidsstämpeln för den projicerade körningen visas i UTC-tidszonen. |
| Backfill | Backfill avgör vilka data som hämtas från början. Om bakåtfyllning är aktiverad, kommer alla aktuella filer i den angivna sökvägen att importeras under det första schemalagda intaget. Om underfyllning är inaktiverad importeras endast de filer som läses in mellan den första importkörningen och starttiden. Filer som lästs in före starttiden importeras inte. |

## Granska ditt dataflöde

Använd granskningssidan för att få en sammanfattning av dataflödet före intag. Detaljerna är grupperade i följande kategorier:

* **Anslutning** - Visar källtypen, den relevanta sökvägen för den valda källfilen och antalet kolumner i källfilen.
* **Tilldela datauppsättnings- och mappningsfält** - Visar vilka datauppsättningar som källdata importeras till, inklusive det schema som datauppsättningen följer.
* **Schemaläggning** - Visar den aktiva perioden, frekvensen och intervallet för intagsschemat.
När du har granskat dataflödet klickar du på Slutför och anger en tid innan dataflödet skapas.

![Granskningssidan.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-review.png)

## Nästa steg

Genom att följa den här självstudiekursen har du skapat ett dataflöde för att hämta batchdata från din [!DNL Acxiom]-källa till Experience Platform. Ytterligare resurser finns i dokumentationen nedan.

### Övervaka dataflödet

När dataflödet har skapats kan du övervaka de data som hämtas genom det för att visa information om hur mycket data som har importerats, hur bra de är och vilka fel som har uppstått. Mer information om hur du övervakar dataflöde finns i självstudiekursen [Övervaka konton och dataflöden i användargränssnittet](../../../../../dataflows/ui/monitor-sources.md).

### Uppdatera ditt dataflöde

Om du vill uppdatera konfigurationer för schemaläggning, mappning och allmän information för dina dataflöden går du till självstudiekursen [Uppdatera källornas dataflöden i användargränssnittet](../../update-dataflows.md).

### Ta bort ditt dataflöde

Du kan ta bort dataflöden som inte längre är nödvändiga eller som har skapats felaktigt med funktionen **[!UICONTROL Delete]** som finns på arbetsytan i **[!UICONTROL Dataflows]**. Mer information om hur du tar bort dataflöden finns i självstudiekursen [Ta bort dataflöden i användargränssnittet](../../delete.md).

## Ytterligare resurser {#additional-resources}

Mer information finns i [[!DNL Acxiom] InfoBase](https://www.acxiom.com/wp-content/uploads/2022/02/fs-acxiom-infobase_AC-0268-22.pdf).
