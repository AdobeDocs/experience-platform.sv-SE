---
keywords: Experience Platform;hem;populära ämnen;Data Landing Zone;datalandningszon
solution: Experience Platform
title: Anslut datalandningszonen till plattformen med användargränssnittet
topic-legacy: overview
type: Tutorial
description: Lär dig hur du skapar en källanslutning för en Data Landing Zone med hjälp av användargränssnittet för plattformen.
exl-id: 653c9958-5d89-4b0c-af3d-a3e74aa47a08
source-git-commit: ca7197036283ee15dbf60c113d361a5ea34d65c1
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# Anslut [!DNL Data Landing Zone] till plattformen med användargränssnittet

[!DNL Data Landing Zone] är en molnbaserad datalagringsfunktion för tillfällig fillagring som tillhandahålls med Adobe Experience Platform. [!DNL Data Landing Zone] används endast för att lägga in och ta bort data i och från plattformen. Data tas automatiskt bort från [!DNL Data Landing Zone] efter sju dagar.

I den här självstudiekursen beskrivs hur du skapar en [!DNL Data Landing Zone]-källanslutning med hjälp av användargränssnittet för plattformen.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

## Hämta filer från [!DNL Data Landing Zone] till plattformen

Välj **[!UICONTROL Sources]** från vänster navigering i plattformsgränssnittet för att komma åt arbetsytan [!UICONTROL Sources]. Skärmen [!UICONTROL Catalog] innehåller en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också använda sökfältet till att hitta den källa du vill arbeta med.

Under kategorin [!UICONTROL cloud storage] väljer du [!DNL Data Landing Zone] och sedan **[!UICONTROL Add data]**.

![katalog](../../../../images/tutorials/create/dlz/catalog.png)

[!UICONTROL Add data]-steget visas och du får ett gränssnitt där du kan välja och förhandsgranska de data du vill hämta till plattformen.

![tilläggsdata](../../../../images/tutorials/create/dlz/add-data.png)

En detaljerad steg-för-steg-guide om hur du skapar ett dataflöde för en molnlagringskälla finns i självstudiekursen om att [skapa ett molnlagringsdataflöde för att överföra data till plattformen](../../dataflow/batch/cloud-storage.md).

## Hämta och uppdatera dina [!DNL Data Landing Zone]-autentiseringsuppgifter

[!DNL Data Landing Zone] är en körklar källa som medföljer din Adobe Experience Platform Sources-licens. [!DNL Data Landing Zone] använder en SAS-URI och SAS-tokenbaserad autentisering. Du kan hämta och uppdatera autentiseringsuppgifterna från sidan [!UICONTROL Sources catalog].

Markera ellipserna (**) under kategorin [!UICONTROL Cloud storage] i [!UICONTROL Sources catalog]..**) från **[!UICONTROL Data Landing Zone]**-kortet. Välj **[!UICONTROL View credentials]** i listrutan som visas.

![alternativ](../../../../images/tutorials/create/dlz/options.png)

En pover visas med ditt behållarnamn, SAS-token, lagringskontonamn och SAS-URI.

Välj **[!UICONTROL Refresh credentials]** och vänta i några sekunder på att de uppdaterade autentiseringsuppgifterna ska behandlas.

![view-credentials](../../../../images/tutorials/create/dlz/credentials.png)

## Nästa steg

Genom att följa den här självstudiekursen har du öppnat din [!DNL Data Landing Zone]-behållare och lärt dig att hämta och uppdatera dina inloggningsuppgifter. Du kan nu gå vidare till nästa självstudiekurs om att [skapa ett dataflöde för att hämta data från ett molnlagringsutrymme till plattformen](../../dataflow/batch/cloud-storage.md).
