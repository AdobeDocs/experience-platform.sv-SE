---
keywords: Experience Platform;hem;populära ämnen;Data Landing Zone;datalandningszon
title: Anslut datalandningszonen till plattformen med användargränssnittet
description: Lär dig hur du skapar en källanslutning för en Data Landing Zone med hjälp av användargränssnittet för plattformen.
exl-id: 653c9958-5d89-4b0c-af3d-a3e74aa47a08
source-git-commit: d57060ddeed64d3863f71ac1ea34ccc5c97265ea
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 0%

---

# Anslut [!DNL Data Landing Zone] till plattform med användargränssnittet

>[!IMPORTANT]
>
>Den här sidan är specifik för [!DNL Data Landing Zone] *källa* i Experience Platform. Information om hur du ansluter till [!DNL Data Landing Zone] *mål* koppling, se [[!DNL Data Landing Zone] måldokumentationssida](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] är en säker, molnbaserad fillagringsfunktion för att överföra filer till Adobe Experience Platform. Data tas automatiskt bort från [!DNL Data Landing Zone] efter sju dagar.

Den här självstudiekursen innehåller steg för att skapa en [!DNL Data Landing Zone] källanslutning med hjälp av användargränssnittet för plattformen.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

## Hämta filer från [!DNL Data Landing Zone] till plattform

Välj **[!UICONTROL Sources]** från vänster navigering för att komma åt [!UICONTROL Sources] arbetsyta. The [!UICONTROL Catalog] I visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också använda sökfältet till att hitta den källa du vill arbeta med.

Under [!UICONTROL cloud storage] kategori, välj [!DNL Data Landing Zone] och sedan markera **[!UICONTROL Add data]**.

![katalog](../../../../images/tutorials/create/dlz/catalog.png)

The [!UICONTROL Add data] visas så att du får ett gränssnitt där du kan välja och förhandsgranska de data du vill hämta till plattformen.

* Den vänstra delen av gränssnittet är en mappläsare som visar en lista över filer från behållaren som du sedan kan hämta till plattformen.
* Med den högra delen av gränssnittet kan du förhandsgranska upp till 100 rader data från en kompatibel fil.

Markera filen som du vill hämta till plattformen och vänta en stund tills rätt gränssnitt uppdateras till en förhandsgranskningsskärm.

![tilläggsdata](../../../../images/tutorials/create/dlz/add-data.png)

>[!TIP]
>
>Plattformen identifierar automatiskt egenskapsinformation för filen som du valde, inklusive information om filens dataformat, angiven kolumnavgränsare och komprimeringstyp.

I förhandsvisningsgränssnittet kan du inspektera innehållet och strukturen i en fil. Som standard visas den första filen i den markerade mappen i förhandsvisningsgränssnittet.

Om du vill förhandsgranska en annan fil markerar du förhandsvisningsikonen bredvid namnet på filen som du vill inspektera.

När du är klar väljer du **[!UICONTROL Next]**.

![filidentifiering](../../../../images/tutorials/create/dlz/file-detection.png)

En detaljerad steg-för-steg-guide om hur du skapar ett dataflöde för en molnlagringskälla finns i självstudiekursen om [skapa ett molnlagringsdataflöde för att överföra data till plattformen](../../dataflow/batch/cloud-storage.md).

## Hämta och uppdatera dina [!DNL Data Landing Zone] autentiseringsuppgifter

[!DNL Data Landing Zone] är en körklar källa som medföljer din Adobe Experience Platform Sources-licens. [!DNL Data Landing Zone] använder en SAS-URI och SAS-tokenbaserad autentisering. Du kan hämta och uppdatera dina autentiseringsuppgifter från [!UICONTROL Sources catalog] sida.

I [!UICONTROL Sources catalog], under [!UICONTROL Cloud storage] väljer du ellipserna (**...**) från **[!UICONTROL Data Landing Zone]** kort. I listrutan som visas väljer du **[!UICONTROL View credentials]**.

![alternativ](../../../../images/tutorials/create/dlz/options.png)

En pover visas med ditt behållarnamn, SAS-token, lagringskontonamn och SAS-URI.

Välj **[!UICONTROL Refresh credentials]** och under några sekunder kan de uppdaterade inloggningsuppgifterna behandlas.

>[!TIP]
>
>Dina [!DNL Data Landing Zone] inloggningsuppgifterna är inställda på att automatiskt förfalla efter 90 dagar och du måste använda nya autentiseringsuppgifter för att återansluta till [!DNL Data Landing Zone] efter utgångsdatum. Dina dataflöden i Platform påverkas inte av att autentiseringsuppgifterna har upphört att gälla och du kan fortfarande arbeta med nya och befintliga dataflöden med dina nya autentiseringsuppgifter.

![view-credentials](../../../../images/tutorials/create/dlz/credentials.png)

## Nästa steg

Genom att följa den här självstudiekursen har du använt [!DNL Data Landing Zone] och lärde sig att hämta och uppdatera dina inloggningsuppgifter. Du kan nu gå vidare till nästa självstudiekurs på [skapa ett dataflöde för att hämta data från en molnlagring till plattformen](../../dataflow/batch/cloud-storage.md).
