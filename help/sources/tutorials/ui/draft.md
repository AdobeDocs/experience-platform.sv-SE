---
title: Utkastdataflöden i användargränssnittet
description: Lär dig hur du sparar dataflöden som ett utkast och publicerar dem vid ett senare tillfälle när du använder arbetsytan för källor.
source-git-commit: 5fc433f603c6e83c621df0f4a1d0aa27e18cd582
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 0%

---

# Utkastdataflöden i användargränssnittet

Spara arbetsflödets förlopp för oavslutad datainmatning genom att ange dataflödet till utkaststatus. Du kan återuppta och slutföra de färdiga dataflödena vid ett senare tillfälle.

Det här dokumentet innehåller anvisningar om hur du sparar dataflöden när du använder källarbetsytan i Adobe Experience Platform-användargränssnittet.

## Komma igång

Dokumentet kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.

## Spara ett dataflöde som ett utkast

Du kan när som helst pausa skapandet av dataflödet efter att du har valt de data som ska hämtas till plattformen.

Om du till exempel vill spara förloppet under informationsflödet väljer du **[!UICONTROL Save as draft]**.

![Dataflödesdetaljsteget i källarbetsflödet med Spara som utkast valt.](../../images/tutorials/draft/save-as-draft.png)

När du har sparat utkastet kommer du till kontosidan där du kan se en lista över dina befintliga dataflöden, inklusive dina utkast.

![En lista med dataflöden för ett visst konto.](../../images/tutorials/draft/draft-dataflow.png)

>[!TIP]
>
>Ritade dataflöden aktiveras inte och har statusen inställd på `draft`.

Om du vill fortsätta med utkastet väljer du ellipserna (`...`) bredvid dataflödets namn och välj **[!UICONTROL Update dataflow]**.

>[!NOTE]
>
>Om utkastet innehåller schemaläggningsinformation kan du även välja att **[!UICONTROL Edit schedule]**.

![Ett rullgardinsfönster med uppdateringsdataflöde valt.](../../images/tutorials/draft/update-dataflow.png)

### Få åtkomst till dina utkast från källkatalogen

Du kan även komma åt dina utkast via dataflödeskatalogen. Välj **[!UICONTROL Dataflows]** i den övre sidhuvudet för att komma åt dataflödeskatalogen. Här hittar du ditt utkast i listan över befintliga dataflöden i organisationen och väljer ellipserna (`...`) bredvid namnet och välj **[!UICONTROL Update dataflow]**.

![En lista med dataflöden för en viss organisation.](../../images/tutorials/draft/catalog-access.png)

## Publicera ditt utkast till dataflöde

Du kommer tillbaka till [!UICONTROL Add data] steg i källarbetsflödet där du kan bekräfta dataformatet på nytt och fortsätta med dataflödet.

När du har bekräftat formatering, avgränsare och komprimeringstyp för dina data väljer du **[!UICONTROL Next]** för att fortsätta.

![Steget Lägg till data i källarbetsflödet.](../../images/tutorials/draft/select-data.png)

Bekräfta sedan dataflödesinformationen. Använd informationsgränssnittet för dataflöden för att uppdatera konfigurationer som omger dataflödets namn, beskrivning, partiellt intag, inställningar för feldiagnostik och varningsinställningar.

När du är klar med dina konfigurationer väljer du **[!UICONTROL Next]** för att fortsätta.

![Dataflödesdetaljsteget i källarbetsflödet.](../../images/tutorials/draft/dataflow-detail.png)

The [!UICONTROL Mapping] visas. Under det här steget kan du konfigurera om mappningskonfigurationerna för ditt dataflöde. En omfattande guide om förinställningsfunktionerna för data som används för mappning finns på [gränssnittsguide för dataförberedelser](../../../data-prep/ui/mapping.md).

När du är klar med mappningsomkonfigurationen väljer du **[!UICONTROL Next]** för att fortsätta.

![Mappningssteget för källarbetsflödet.](../../images/tutorials/draft/mapping.png)

Använd [!UICONTROL Scheduling] steg för att upprätta ett schema för ditt dataflöde. Du kan ställa in din matningsfrekvens på `once`, `minute`, `hour`, `day`, eller `week`. När du är klar väljer du **[!UICONTROL Next]** för att fortsätta.

![Schemaläggningssteget för källarbetsflödet.](../../images/tutorials/draft/scheduling.png)

Granska slutligen informationen om dataflödet och välj **[!UICONTROL Finish]** för att publicera utkastet.

![Granskningssteget för källarbetsflödet.](../../images/tutorials/draft/review.png)

När du har sparat och publicerat ett utkast aktiveras dataflödet och du kan inte längre återställa det som ett utkast.

## Nästa steg

Genom att följa den här självstudiekursen har du lärt dig hur du sparar förloppet och anger ett dataflöde som ett utkast. Mer information om källor finns på [källöversikt](../../home.md).