---
keywords: Experience Platform;hem;populära ämnen;källor;kopplingar;källkopplingar;källor sdk;sdk;SDK
title: Självbetjäningsdokumentationsmall för användargränssnittet
description: Lär dig hur du skapar en källanslutning till YOURSOURCE med hjälp av Adobe Experience Platform-gränssnittet.
exl-id: 6471c0a2-22e8-4133-a76f-ee3c5c669ef8
source-git-commit: 4d7799b01c34f4b9e4a33c130583eadcfdc3af69
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 1%

---

# Skapa en *DIN KÄLLA* källanslutning i användargränssnittet

*När du går igenom den här mallen ersätter eller tar du bort alla stycken i kursiv stil (med början från det här).*

*Börja med att uppdatera metadata (rubrik och beskrivning) högst upp på sidan. Ignorera alla instanser av UICONTROL på den här sidan. Det här är en tagg som hjälper våra maskinöversättningsprocesser att översätta sidan korrekt till flera språk som stöds. Vi lägger till taggar i dokumentationen när du har skickat in den.*

Den här självstudiekursen innehåller steg för att skapa en *DIN KÄLLA* källkoppling med hjälp av användargränssnittet för plattformen.

## Översikt

*Ge en kort översikt över ditt företag, inklusive det värde det ger kunderna. Ta med en länk till startsidan för din produktdokumentation för ytterligare läsning.*

>[!IMPORTANT]
>
>Dokumentationssidan skapades av *DIN KÄLLA* team. Om du har frågor eller uppdateringsfrågor kontaktar du dem direkt på *Infoga länk- eller e-postadress där du kan komma åt uppdateringar*.

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

## Koppla samman *DIN KÄLLA* konto

Välj **[!UICONTROL Sources]** från det vänstra navigeringsfältet för att komma åt [!UICONTROL Sources] arbetsyta. The [!UICONTROL Catalog] visas en mängd olika källor som du kan använda för att skapa ett konto.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under *KATEGORIN FÖR DIN KÄLLA* kategori, välj *DIN KÄLLA* och sedan markera **[!UICONTROL Add data]**.

>[!TIP]
>
>Skärmbilderna som används nedan är exempel. När du skapar din dokumentation ska du ersätta bilderna med skärmbilder av den faktiska källan. Du kan använda samma markeringsmönster och -färg, liksom samma filnamn. Kontrollera att skärmbilden fångar hela skärmen i användargränssnittet för plattformen. Mer information om hur du överför skärmbilder finns i handboken på [skicka in dokumentation för granskning](./github.md).

![katalog](../assets/ui/catalog.png)

The **[!UICONTROL Connect YOURSOURCE account]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill använda ett befintligt konto väljer du *DIN KÄLLA* konto som du vill skapa ett nytt dataflöde med och sedan välja **[!UICONTROL Next]** för att fortsätta.

![befintlig](../assets/ui/existing.png)

### Nytt konto

Om du skapar ett nytt konto väljer du **[!UICONTROL New account]** och ange sedan ett namn, en valfri beskrivning och dina uppgifter. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![new](../assets/ui/new.png)

## Nästa steg

*Arbetsflöden för de återstående stegen för att skapa ett dataflöde är modulariserade. Om du vill ringa upp dig angående din källa kan du läsa avsnittet med ytterligare resurser nedan.*

Genom att följa den här självstudiekursen har du upprättat en anslutning till *DIN KÄLLA* konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till plattformen](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/dataflow/crm.html).

## Ytterligare resurser

*Det här är ett valfritt avsnitt där du kan tillhandahålla ytterligare länkar till din produktdokumentation eller andra steg, skärmdumpar och nyanser som du tycker är viktiga för att kunden ska lyckas. Du kan använda det här avsnittet för att lägga till information om eller tips för hela arbetsflödet i källan, särskilt om det finns särskilda gotchas som slutanvändaren kan stöta på.*
