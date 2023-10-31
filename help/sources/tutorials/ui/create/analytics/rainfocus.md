---
title: Anslut ditt RainFocus-konto till Experience Platform med hjälp av användargränssnittet
description: Lär dig hur du ansluter ditt RainFocus-konto till Experience Platform med hjälp av användargränssnittet.
badge: Beta
exl-id: a349e37e-9f2c-47ff-8360-ccbe578dce27
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%

---

# Koppla samman [!DNL RainFocus] konto till Experience Platform med användargränssnittet

>[!NOTE]
>
>The [!DNL RainFocus] källan är i betaversion. Se [källöversikt](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betamärkta källor.

Den här självstudiekursen innehåller steg för hur du ansluter [!DNL RainFocus] hantera och strömma händelsehantering och analysdata till Adobe Experience Platform.

>[!IMPORTANT]
>
>Den här källanslutnings- och dokumentationssidan skapas och underhålls av [!DNL RainFocus] team. Om du har frågor eller uppdateringsfrågor kontaktar du dem direkt på kundtjänst<span>@rainfocus.com eller besök [[!DNL RainFocus] Help Center](https://help.rainfocus.com/hc/en-us)

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet i Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

### Förutsättningar

Innan du kan ansluta [!DNL RainFocus] måste du först slutföra följande uppgifter som krävs:

* [Samla in nödvändiga inloggningsuppgifter](../../../../connectors/analytics/rainfocus.md#gather-required-credentials)
* [Skapa ett XDM-schema och definiera identitetsfältet](../../../../connectors/analytics/rainfocus.md#create-an-xdm-schema-and-define-the-identity-field)
* [Skapa en integreringsprofil i RainFocus](../../../../connectors/analytics/rainfocus.md#create-an-integration-profile-in-rainfocus)

När du har slutfört kravkonfigurationen kan du gå vidare till stegen som beskrivs nedan.

## Anslut ditt RainFocus-konto till Experience Platform

Välj **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt källarbetsytan. The *[!UICONTROL Catalog]* visas en mängd olika källor som du kan använda för att skapa ett konto.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under *[!UICONTROL Analytics]* kategori, välj **[!UICONTROL RainFocus Experience]** och sedan markera **[!UICONTROL Add data]**.

![Källkatalogen i användargränssnittet i Experience Platform med RainFocus-källan markerad.](/help/sources/images/tutorials/create/rainfocus/rainfocus_sources-rf.png)

## Markera data

Steget Välj data visas med ett gränssnitt där du kan välja de data du vill hämta till Experience Platform.

* Den vänstra delen av gränssnittet är en webbläsare som gör att du kan visa tillgängliga dataströmmar på ditt konto;
* Med den högra delen av gränssnittet kan du förhandsgranska upp till 100 rader data från en JSON-fil.

Välj **[!UICONTROL Upload files]** för att överföra en JSON-fil från ditt lokala system. Du kan också dra och släppa den JSON-fil som du vill överföra till filpanelen genom att dra och släppa.

Överför JSON-exempelnyttolasten som hämtats från **Regnfokus**.

![Steg för val av data i källarbetsflödet.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-json-upload.png)

När filen har överförts uppdateras förhandsvisningsgränssnittet för att visa en förhandsgranskning av schemat som du har överfört. I förhandsvisningsgränssnittet kan du inspektera innehållet och strukturen i en fil. Du kan också använda sökfältverktyget för att komma åt specifika objekt inifrån schemat.

När du är klar väljer du **[!UICONTROL Next]**.

![Förhandsgranskningssteget för källarbetsflödet.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-json-preview.png)

## Dataflödesdetaljer

The **Dataflödesdetaljer** visas. Här finns alternativ för att använda en befintlig datauppsättning eller skapa en ny datauppsättning för dataflödet samt en möjlighet att ange ett namn och en beskrivning för dataflödet. Under det här steget kan du även konfigurera inställningar för profilinmatning, feldiagnostik, partiell inmatning och aviseringar.

När du är klar väljer du **[!UICONTROL Next]**.

![Dataflödesdetaljsteget i källarbetsflödet.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-dataflow-setup.png)

## Mappning {#mapping}

Mappningssteget visas. Du får ett gränssnitt där du kan mappa källfälten från källschemat till rätt mål-XDM-fält i målschemat.

Experience Platform ger intelligenta rekommendationer för automatiskt mappade fält baserat på det målschema eller den datamängd som du har valt. Du kan justera mappningsreglerna manuellt så att de passar dina användningsfall. Beroende på dina behov kan du välja att mappa fält direkt eller använda förinställningsfunktioner för data för att omvandla källdata för att härleda beräknade eller beräknade värden. Mer information om hur du använder mappningsgränssnittet och beräkningsfälten finns i [Användargränssnittsguide för dataprep](../../../../../data-prep/ui/mapping.md).

När källdata har mappats väljer du **[!UICONTROL Next]**.

![Mappningssteget för källarbetsflödet.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-mappings.png)

## Granska

The **Granska** visas så att du kan granska det nya dataflödet innan det skapas. Informationen är grupperad i följande kategorier:

* **Anslutning**: Visar källtypen, den relevanta sökvägen till den valda källfilen och mängden kolumner i källfilen.
* **Tilldela datauppsättnings- och kartfält**: Visar vilken datauppsättning källdata hämtas till, inklusive det schema som datauppsättningen följer.

När du har granskat dataflödet väljer du **Slutför** så att dataflödet kan skapas.

![Granskningssteget för källarbetsflödet.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-compelete.png)

## Hämta din URL för direktuppspelningsslutpunkt {#get-your-streaming-endpoint-url}

När du har skapat ett dataflöde för direktuppspelning kan du nu hämta URL:en för din slutpunkt för direktuppspelning. Den här slutpunkten används för att prenumerera på din webkrok, vilket gör att strömningskällan kan kommunicera med Experience Platform.

Om du vill hämta strömningsslutpunkten går du till *[!UICONTROL Dataflow activity]* sidan med dataflödet som du just skapade och kopierar slutpunkten från nederkanten av *[!UICONTROL Properties]* -panelen.

![Aktivitetssidan för dataflöde i källarbetsytan med URL:en för direktuppspelningsslutpunkten markerad.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-dataflow-api.png)

## Aktivera integreringsprofilen i RainFocus

När dataflödet är klart och du har hämtat din URL för direktuppspelningsslutpunkt kan du nu aktivera [!DNL Integration Profile] in [!DNL RainFocus].

* Logga in på [[!DNL RainFocus] plattform](https://app.rainfocus.com). I den primära navigeringen väljer du **[!DNL Libraries]** och **[!DNL Integration Profiles]**
* Öppna [!DNL Integration Profile] som du skapade tidigare som en del av [krav](../../../../connectors/analytics/rainfocus.md#create-an-integration-profile-in-rainfocus).
* Klistra in **Dataflödes-ID** och **Slutpunkt för direktuppspelning** kopieras från dataflödet i Experience Platform och väljer **Spara**

## Nästa steg

Genom att följa den här självstudien har du upprättat en anslutning för [!DNL RainFocus] så att ni kan strömma händelsehanterings- och analysdata till Experience Platform.

## Ytterligare resurser

Följande dokument innehåller ytterligare vägledning om enheter som omger [!DNL RainFocus] källa.

* [RainFocus Help Center](https://help.rainfocus.com/hc/en-us)
* [Skapa ett Adobe-tjänstkonto (JWT) i Adobe Developer Portal](https://developer.adobe.com/developer-console/docs/guides/authentication/ServiceAccountIntegration/)
* [Skapa ett schema i API:t](../../../../../xdm/tutorials/create-schema-api.md)
* [Skapa ett schema i användargränssnittet](../../../../../xdm/tutorials/create-schema-ui.md)
* [Definiera identitetsfält i användargränssnittet](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/fields/identity.html)
