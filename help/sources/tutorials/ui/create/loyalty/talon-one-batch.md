---
title: Infoga batchdata från Talon.one i Experience Platform med användargränssnittet
description: Lär dig hur du importerar batchdata från Talon.En till Adobe Experience Platform med hjälp av användargränssnittet. Den här guiden innehåller inställningar, dataurval och konfiguration av dataflöde.
badge: Beta
hide: true
hidefromtoc: true
source-git-commit: 558a9d6ff3222acbf77edea0a82ef50725cd6203
workflow-type: tm+mt
source-wordcount: '1361'
ht-degree: 0%

---

# Infoga batchdata från [!DNL Talon.One] till Experience Platform med användargränssnittet

>[!AVAILABILITY]
>
>Källan [!DNL Talon.One] är i betaversion. Läs [villkoren](../../../../home.md#terms-and-conditions) i källresursöversikten om du vill ha mer information om hur du använder betatecknade källor.

Läs den här självstudiekursen om du vill lära dig hur du importerar gruppdata från ditt [!DNL Talon.One]-konto till Adobe Experience Platform med hjälp av källarbetsytan i användargränssnittet.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

>[!IMPORTANT]
>
>Läs [[!DNL Talon.One] översikten](../../../../connectors/loyalty/talon-one.md) om du vill veta mer om nödvändiga åtgärder som du måste utföra innan du kan ansluta ditt konto till Experience Platform.

## Navigera i källkatalogen

I Experience Platform-gränssnittet väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i *[!UICONTROL Sources]*. Välj lämplig kategori på panelen *[!UICONTROL Categories]*. Du kan också använda sökfältet för att navigera till den specifika källa som du vill använda.

Om du vill importera data från [!DNL Talon.One] väljer du **[!UICONTROL Talon.One Batch Source Connector]**-källkortet under *[!UICONTROL Loyalty]* och sedan **[!UICONTROL Add data]**.

>[!TIP]
>
>Källor i källkatalogen visar alternativet **[!UICONTROL Set up]** när en angiven källa ännu inte har något autentiserat konto. När ett autentiserat konto har skapats ändras alternativet till **[!UICONTROL Add data]**.

![Källkatalogen med Talon.Ett batchkällanslutningskort har valts.](../../../../images/tutorials/create/talon-one-batch/catalog.png)

### Skapa ett nytt konto

Om du vill skapa ett nytt konto för källan [!DNL Talon.One] väljer du **[!UICONTROL New account]** och anger ett namn och en valfri beskrivning för kontot. Ange sedan din [!DNL Talon.One]-domän och din [!UICONTROL Talon.One Management API Key]. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt en stund så att anslutningen kan upprättas.

![Det nya kontosteget i källarbetsflödet.](../../../../images/tutorials/create/talon-one-batch/new.png)

### Använd ett befintligt konto

Om du vill använda ett befintligt konto markerar du **[!UICONTROL Existing account]** och väljer det [!DNL Talon.One]-konto som du vill använda i kontogränssnittet.

## Markera data

När du har autentiserat anger du värden för **applicationId** och **sessionType**. Under det här steget kan du använda förhandsvisningsfunktionerna för att kontrollera datastrukturen. När du är klar väljer du **[!UICONTROL Next]** för att fortsätta.

![Stegen för val av data och förhandsgranskning av källarbetsflödet.](../../../../images/tutorials/create/talon-one-batch/select-data.png)

## Konfigurera datauppsättning och dataflödesinformation

Därefter måste du ange information om datauppsättningen och dataflödet.

### Information om datauppsättning

En datauppsättning är en lagrings- och hanteringskonstruktion för en datamängd, vanligtvis en tabell, som innehåller ett schema (kolumner/fält) och poster (rader). Data som har inhämtats till Experience Platform lagras i datasjön som datauppsättningar.

Under det här steget kan du antingen använda en befintlig datauppsättning eller skapa en ny datauppsättning.

>[!NOTE]
>
>Oavsett om du använder en befintlig datauppsättning eller skapar en ny datauppsättning måste du se till att din datauppsättning är **aktiverad för**-profilinmatning.

+++Välj för steg om du vill aktivera profilinmatning, feldiagnostik och partiell inmatning.

Om din datauppsättning är aktiverad för kundprofil i realtid kan du under det här steget växla **[!UICONTROL Profile dataset]** för att aktivera dina data för profilinmatning. Du kan också använda det här steget för att aktivera **[!UICONTROL Error diagnostics]** och **[!UICONTROL Partial ingestion]**.

* **[!UICONTROL Error diagnostics]**: Välj **[!UICONTROL Error diagnostics]** om du vill instruera källan att skapa feldiagnostik som du kan referera till senare när du övervakar datauppsättningsaktiviteten och dataflödesstatusen.
* **[!UICONTROL Partial ingestion]**: Partiell gruppinmatning är möjligheten att importera data som innehåller fel, upp till ett visst konfigurerbart tröskelvärde. Med den här funktionen kan du importera alla korrekta data till Experience Platform, medan alla felaktiga data batchas separat med information om varför de är ogiltiga.

+++

## Information om dataflöde

När datauppsättningen har konfigurerats måste du ange information om dataflödet, inklusive ett namn, en valfri beskrivning och aviseringskonfigurationer.

![Gränssnittet för dataflödesinformation.](../../../../images/tutorials/create/talon-one-batch/dataflow-detail.png)

| Dataflödeskonfigurationer | Beskrivning |
| --- | --- |
| Dataflödesnamn | Dataflödets namn. Som standard används namnet på filen som importeras. |
| Beskrivning | (Valfritt) En kort beskrivning av dataflödet. |
| Aviseringar | Experience Platform kan skapa händelsebaserade aviseringar som användare kan prenumerera på. Dessa alternativ gör att ett löpande dataflöde kan aktivera dessa.  Mer information finns i [varningsöversikten](../../alerts.md) <ul><li>**Källdataflödeskörning Start**: Välj den här aviseringen för att få ett meddelande när dataflödeskörningen börjar.</li><li>**Källdataflödet har körts**: Välj den här aviseringen om du vill få ett meddelande om dataflödet slutar utan fel.</li><li>**Körningsfel för källdataflöde**: Välj den här aviseringen för att få ett meddelande om dataflödet avslutas med fel.</li></ul> |

{style="table-layout:auto"}

## Mappning

Med datauppsättningen och dataflödesinformationen konfigurerade kan du nu mappa källdatafälten till lämpliga mål-XDM-fält. Använd mappningsgränssnittet för att mappa källdata till rätt schemafält innan data importeras till Experience Platform. Mer information finns i [mappningsguiden i användargränssnittet](../../../../../data-prep/ui/mapping.md).

>[!IMPORTANT]
>
>Mer information om hur du mappar [!DNL Talon.One]-källdata finns i [[!DNL Talon.One] översikten](../../../../connectors/loyalty/talon-one.md#mapping).

![Mappningsgränssnittet för källarbetsflödet.](../../../../images/tutorials/create/talon-one-batch/mapping.png)

## Schemalägg inmatning av dataflöde

[!UICONTROL Scheduling]-steget visas. Använd gränssnittet för att konfigurera ett matningsschema för automatisk import av valda källdata med de konfigurerade mappningarna. Som standard är schemaläggningen inställd på `Once`. Välj **[!UICONTROL Frequency]** och välj sedan ett alternativ i listrutan om du vill justera din inmatningsfrekvens.

>[!TIP]
>
>Intervall och bakåtfyllnad syns inte vid engångsbruk.

Om du ställer in matningsfrekvensen på `Minute`, `Hour`, `Day` eller `Week` måste du ange ett intervall för att skapa en fast tidsram mellan varje intag. En matningsfrekvens som till exempel är inställd på `Day` och ett intervall på `15` innebär att dataflödet är schemalagt att importera data var 15:e dag.

Under det här steget kan du även aktivera **bakgrundsfyllning** och definiera en kolumn för inkrementellt dataintag. Backfill används för att importera historiska data, medan kolumnen som du definierar för inkrementellt intag gör att nya data kan skiljas från befintliga data.

Se tabellen nedan för mer information om schemaläggningskonfigurationer.

| Schemaläggningskonfiguration | Beskrivning |
| --- | --- |
| Frekvens | Konfigurera frekvens för att ange hur ofta dataflödet ska köras. Du kan ange frekvensen till: <ul><li>**En gång**: Ställ in din frekvens på `once` för att skapa en engångsinmatning. Konfigurationer för intervall och bakåtfyllnad är inte tillgängliga när ett dataflöde för engångsinmatning skapas. Som standard är schemaläggningsfrekvensen inställd på en gång.</li><li>**Minut**: Ställ in din frekvens på `minute` för att schemalägga ditt dataflöde att importera data per minut.</li><li>**Timme**: Ställ in din frekvens på `hour` för att schemalägga ditt dataflöde att importera data per timme.</li><li>**Dag**: Ställ in din frekvens på `day` för att schemalägga ditt dataflöde att importera data per dag.</li><li>**Vecka**: Ställ in din frekvens på `week` för att schemalägga ditt dataflöde att importera data per vecka.</li></ul> |
| Intervall | När du har valt en frekvens kan du konfigurera intervallinställningen för att upprätta en tidsram mellan varje intag. Om du t.ex. anger din frekvens som dag och konfigurerar intervallet till 15, kommer dataflödet att köras var 15:e dag. Du kan inte ange intervallet till noll. Det minsta tillåtna intervallvärdet för varje frekvens är följande:<ul><li>**En gång**: ingen/a</li><li>**Minut**: 15</li><li>**Timme**: 1</li><li>**Dag**: 1</li><li>**Vecka**: 1</li></ul> |
| Starttid | Tidsstämpeln för den projicerade körningen visas i UTC-tidszonen. |
| Backfill | Backfill avgör vilka data som hämtas från början. Om bakåtfyllning är aktiverad, kommer alla aktuella filer i den angivna sökvägen att importeras under det första schemalagda intaget. Om underfyllning är inaktiverad importeras endast de filer som läses in mellan den första importkörningen och starttiden. Filer som lästs in före starttiden importeras inte. |

![Schemakonfigurationssteget för källarbetsflödet.](../../../../images/tutorials/create/talon-one-batch/scheduling.png)

## Granska

Steget *[!UICONTROL Review]* visas så att du kan granska informationen om dataflödet innan det skapas. Informationen är grupperad i följande kategorier:

* **[!UICONTROL Connection]**: Visar kontonamnet, källplattformen och källnamnet.
* **[!UICONTROL Assign dataset and map fields]**: Visar måldatauppsättningen och det schema som datauppsättningen följer.

När du har bekräftat att informationen är korrekt väljer du **[!UICONTROL Finish]**.

![Granskningssteget för källarbetsflödet.](../../../../images/tutorials/create/talon-one-batch/review.png)

## Övervaka dataflödet

När dataflödet har skapats kan du övervaka de data som importeras genom det för att se information om hur mycket data som har intagits, hur bra de är och vilka fel som har uppstått. Mer information om hur du övervakar dataflöde finns i självstudiekursen [Övervaka konton och dataflöden i användargränssnittet](../../../../../dataflows/ui/monitor-sources.md).