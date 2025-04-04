---
keywords: Experience Platform;hem;populära ämnen;källor;kopplingar;källkopplingar;källor sdk;sdk;SDK
title: Självbetjäningsdokumentationsmall för användargränssnittet
description: Lär dig hur du skapar en källanslutning till YOURSOURCE med hjälp av Adobe Experience Platform-gränssnittet.
exl-id: 6471c0a2-22e8-4133-a76f-ee3c5c669ef8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 0%

---

# Skapa en *YOURSOURCE*-källanslutning i gränssnittet

*När du går igenom den här mallen ersätter eller tar du bort alla stycken i kursiv stil (med början från den här).*

*Börja med att uppdatera metadata (rubrik och beskrivning) högst upp på sidan. Please ignore all instances of UICONTROL on this page. Det här är en tagg som hjälper våra maskinöversättningsprocesser att översätta sidan korrekt till flera språk som stöds. Vi lägger till taggar i dokumentationen när du har skickat den.*

I den här självstudien beskrivs hur du skapar en *YOURSOURCE* -källkoppling med Experience Platform-användargränssnittet.

## Översikt

*Ge en kort översikt över ditt företag, inklusive det värde det ger kunderna. Inkludera en länk till din produktdokumentationsstartsida för ytterligare läsning.*

>[!IMPORTANT]
>
>Den här källkopplingen och dokumentationssidan skapas och underhålls av *YourSource* -teamet. Om du har frågor eller uppdateringsfrågor kontaktar du dem direkt på *Infoga länk eller e-postadress där du kan komma åt uppdateringar*.

## Förhandskrav

*Lägg till information i det här avsnittet om allt som kunderna behöver känna till innan de börjar konfigurera källan i Adobe Experience Platform användargränssnitt. Det här kan vara om:*

* *måste läggas till i en tillåtelselista*
* *krav för e-posthashning*
* *kontoinformation på din sida*
* *Så här hämtar du autentiseringsuppgifterna för att ansluta till din plattform*

### Samla in nödvändiga inloggningsuppgifter

För att kunna ansluta *YOURSOURCE* till Experience Platform måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning | Exempel |
| --- | --- | --- |
| *autentiseringsuppgifter en* | *Lägg till en kort beskrivning till källans autentiseringsuppgifter här* | *Lägg till ett exempel på källans autentiseringsuppgifter här* |
| *autentiseringsuppgifter två* | *Lägg till en kort beskrivning till källans autentiseringsuppgifter här* | *Lägg till ett exempel på källans autentiseringsuppgifter här* |
| *autentiseringsuppgifter tre* | *Lägg till en kort beskrivning till källans autentiseringsuppgifter här* | *Lägg till ett exempel på källans autentiseringsuppgifter här* |

Mer information om de här autentiseringsuppgifterna finns i *YOURSOURCE* -autentiseringsdokumentationen. *Lägg till en länk till din plattforms autentiseringsdokumentation här*.

## Anslut ditt *DITT*-konto

I Experience Platform-gränssnittet väljer du **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan i [!UICONTROL Sources]. På skärmen [!UICONTROL Catalog] visas en mängd olika källor som du kan använda för att skapa ett konto.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under kategorin *KATEGORI* FÖR DIN KÄLLA *KÄLLA* väljer du **[!UICONTROL Add data]**.

>[!TIP]
>
>Skärmbilderna som används nedan är exempel. När du skapar din dokumentation ska du ersätta bilderna med skärmbilder av den faktiska källan. Du kan använda samma markeringsmönster och -färg, liksom samma filnamn. Se till att skärmbilden fångar hela Experience Platform användargränssnittsskärm. Mer information om hur du överför skärmbilder finns i guiden om att [skicka din dokumentation för granskning](./github.md).

![katalog](../assets/ui/catalog.png)

Sidan **[!UICONTROL Connect YOURSOURCE account]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill använda ett befintligt konto markerar du det *YOURSOURCE*-konto som du vill skapa ett nytt dataflöde med och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![befintlig](../assets/ui/existing.png)

### Nytt konto

Om du skapar ett nytt konto väljer du **[!UICONTROL New account]** och anger sedan ett namn, en valfri beskrivning och dina autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![ny](../assets/ui/new.png)

## Nästa steg

*Arbetsflöden för de återstående stegen för att skapa ett dataflöde är modulariserade. Om det finns några specifika utlysningar som du vill göra gällande din källa kan du läsa avsnittet med ytterligare resurser nedan.*

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt *YOURCE*-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/dataflow/crm.html).

## Ytterligare resurser

*Det här är ett valfritt avsnitt där du kan tillhandahålla ytterligare länkar till din produktdokumentation eller andra steg, skärmbilder eller nyanser som du anser vara viktiga för att kunden ska lyckas. Du kan använda det här avsnittet för att lägga till information om eller tips för hela arbetsflödet i källan, särskilt om det finns särskilda gotchas som en slutanvändare kan stöta på.*
