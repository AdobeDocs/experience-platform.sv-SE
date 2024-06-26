---
title: Självbetjäningsmall för direktuppspelning av SDK-gränssnitt
description: Lär dig hur du hämtar strömmande data från en källa till Adobe Experience Platform med användargränssnittet.
exl-id: 82254be0-fa31-4114-a0ec-179a990e0904
badge: Beta
source-git-commit: 256857103b4037b2cd7b5b52d6c5385121af5a9f
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 0%

---

# Skapa en källanslutning och ett dataflöde för direktuppspelning *DIN KÄLLA* data med användargränssnittet

*När du går igenom den här mallen ersätter eller tar du bort alla stycken i kursiv stil (med början från det här).*

*Börja med att uppdatera metadata (rubrik och beskrivning) högst upp på sidan. Please ignore all instances of UICONTROL on this page. Det här är en tagg som hjälper våra maskinöversättningsprocesser att översätta sidan korrekt till flera språk som stöds. Vi lägger till taggar i dokumentationen när du har skickat in den.*

Den här självstudiekursen innehåller steg för att skapa en *DIN KÄLLA* källkoppling med hjälp av användargränssnittet för plattformen.

## Översikt

*Ge en kort översikt över ditt företag, inklusive det värde det ger kunderna. Ta med en länk till startsidan för din produktdokumentation för ytterligare läsning.*

>[!IMPORTANT]
>
>Den här källanslutnings- och dokumentationssidan skapas och underhålls av *DIN KÄLLA* team. Om du har frågor eller uppdateringsfrågor kontaktar du dem direkt på *Infoga länk- eller e-postadress där du kan komma åt uppdateringar*.

## Förutsättningar

*Lägg till information i det här avsnittet om allt som kunderna behöver känna till innan de börjar konfigurera källan i Adobe Experience Platform användargränssnitt. Det här kan handla om:*

* *behöver läggas till tillåtelselista*
* *krav för e-posthashning*
* *kontoinformation på din sida*
* *hur du får inloggningsuppgifterna för att ansluta till din plattform*

### Samla in nödvändiga inloggningsuppgifter

För att kunna ansluta *DIN KÄLLA* till Platform måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning | Exempel |
| --- | --- | --- |
| *autentiseringsuppgifter ett* | *Lägg till en kort beskrivning till källans autentiseringsuppgifter här* | *Lägg till ett exempel på källans autentiseringsuppgifter här* |
| *autentiseringsuppgifter två* | *Lägg till en kort beskrivning till källans autentiseringsuppgifter här* | *Lägg till ett exempel på källans autentiseringsuppgifter här* |
| *autentiseringsuppgifter tre* | *Lägg till en kort beskrivning till källans autentiseringsuppgifter här* | *Lägg till ett exempel på källans autentiseringsuppgifter här* |

Mer information om dessa autentiseringsuppgifter finns i *DIN KÄLLA* autentiseringsdokumentation. *Lägg till en länk till plattformens autentiseringsdokumentation här*.

### Integrera *DIN KÄLLA* med din webbkrok

*SDK för direktuppspelning kräver att din källa har stöd för webbhooks för att kunna kommunicera med Experience Platform. I det här avsnittet måste du ange de steg som användarna måste följa för att kunna integrera YOURSOURCE med en webkrok.*

## Koppla samman *DIN KÄLLA* konto

Välj **[!UICONTROL Sources]** från det vänstra navigeringsfältet för att komma åt [!UICONTROL Sources] arbetsyta. The [!UICONTROL Catalog] visas en mängd olika källor som du kan använda för att skapa ett konto.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under **Direktuppspelning** kategori, välj *DIN KÄLLA* och sedan markera **[!UICONTROL Add data]**.

>[!TIP]
>
>Skärmbilderna som används nedan är exempel. När du skapar din dokumentation ska du ersätta bilderna med skärmbilder av den faktiska källan. Du kan använda samma markeringsmönster och -färg, liksom samma filnamn. Kontrollera att skärmbilden fångar hela skärmen i användargränssnittet för plattformen. Mer information om hur du överför skärmbilder finns i handboken på [skicka in dokumentation för granskning](../documentation/github.md).

![Katalogen Experience Platform-källor](../assets/streaming/catalog.png)

## Markera data

The **[!UICONTROL Select data]** visas, där du får ett gränssnitt där du kan välja de data som ska hämtas till plattformen.

* Den vänstra delen av gränssnittet är en webbläsare som gör att du kan visa tillgängliga dataströmmar på ditt konto;
* Med den högra delen av gränssnittet kan du förhandsgranska upp till 100 rader data från en JSON-fil.

Välj **[!UICONTROL Upload files]** för att överföra en JSON-fil från ditt lokala system. Du kan också dra och släppa den JSON-fil som du vill överföra till [!UICONTROL Drag and drop files] -panelen.

![Steget Lägg till data i källarbetsflödet.](../assets/streaming/add-data.png)

När filen har överförts uppdateras förhandsvisningsgränssnittet för att visa en förhandsgranskning av schemat som du har överfört. I förhandsvisningsgränssnittet kan du inspektera innehållet och strukturen i en fil. Du kan också använda [!UICONTROL Search field] för att komma åt specifika objekt inifrån schemat.

När du är klar väljer du **[!UICONTROL Next]**.

![Förhandsgranskningssteget för källarbetsflödet.](../assets/streaming/preview.png)

## Dataflödesdetaljer

The **Dataflödesdetaljer** visas. Här finns alternativ för att använda en befintlig datauppsättning eller skapa en ny datauppsättning för dataflödet samt en möjlighet att ange ett namn och en beskrivning för dataflödet. Under det här steget kan du även konfigurera inställningar för profilinmatning, feldiagnostik, partiell inmatning och aviseringar.

När du är klar väljer du **[!UICONTROL Next]**.

![Dataflödesdetaljsteget i källarbetsflödet.](../assets/streaming/dataflow-detail.png)

## Mappning

The [!UICONTROL Mapping] visas med ett gränssnitt för att mappa källfälten från källschemat till rätt mål-XDM-fält i målschemat.

Plattformen ger intelligenta rekommendationer för automatiskt mappade fält baserat på det målschema eller den datamängd du valt. Du kan justera mappningsreglerna manuellt så att de passar dina användningsfall. Beroende på dina behov kan du välja att mappa fält direkt eller använda förinställningsfunktioner för data för att omvandla källdata för att härleda beräknade eller beräknade värden. Mer information om hur du använder mappningsgränssnittet och beräkningsfälten finns i [Användargränssnittsguide för dataprep](https://experienceleague.adobe.com/docs/experience-platform/data-prep/ui/mapping.html).

När källdata har mappats väljer du **[!UICONTROL Next]**.

![Mappningssteget för källarbetsflödet.](../assets/streaming/mapping.png)

## Granska

The **[!UICONTROL Review]** visas så att du kan granska det nya dataflödet innan det skapas. Informationen är grupperad i följande kategorier:

* **[!UICONTROL Connection]**: Visar källtypen, den relevanta sökvägen till den valda källfilen och mängden kolumner i källfilen.
* **[!UICONTROL Assign dataset & map fields]**: Visar vilken datauppsättning källdata hämtas till, inklusive det schema som datauppsättningen följer.

När du har granskat dataflödet klickar du på **[!UICONTROL Finish]** så att dataflödet kan skapas.

![Granskningssteget för källarbetsflödet.](../assets/streaming/review.png)

## Hämta din URL för direktuppspelningsslutpunkt

När du har skapat ett dataflöde för direktuppspelning kan du nu hämta URL:en för din slutpunkt för direktuppspelning. Den här slutpunkten används för att prenumerera på din webkrok, vilket gör att strömningskällan kan kommunicera med Experience Platform.

Om du vill hämta strömningsslutpunkten går du till [!UICONTROL Dataflow activity] sidan med dataflödet som du just skapade och kopierar slutpunkten från nederkanten av [!UICONTROL Properties] -panelen.

![Slutpunkten för direktuppspelning i dataflödesaktivitet.](../assets/testing/endpoint-test.png)

## Nästa steg

*Arbetsflöden för de återstående stegen för att skapa ett dataflöde är modulariserade. Om du vill ringa upp dig angående din källa kan du läsa avsnittet med ytterligare resurser nedan.*

Genom att följa den här självstudien har du upprättat en anslutning till *DIN KÄLLA* konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till plattformen](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/dataflow/crm.html).

## Ytterligare resurser

*Det här är ett valfritt avsnitt där du kan tillhandahålla ytterligare länkar till din produktdokumentation eller andra steg, skärmdumpar och nyanser som du tycker är viktiga för att kunden ska lyckas. Du kan använda det här avsnittet för att lägga till information om eller tips för hela arbetsflödet i källan, särskilt om det finns särskilda gotchas som slutanvändaren kan stöta på.*
