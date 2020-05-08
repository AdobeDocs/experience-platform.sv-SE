---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en Azure Table Storage-källanslutning i användargränssnittet
topic: overview
translation-type: tm+mt
source-git-commit: 899c4fbe8a1bb3fef24f606e77f13ef5184d1eda
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---


# Skapa en Azure Table Storage-källanslutning i användargränssnittet

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källdata på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en källanslutning för Azure Table Storage (nedan kallad ATS) med hjälp av användargränssnittet för plattformen.

## Komma igång

Den här självstudien kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Experience Data Model (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att organisera kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [Kundprofil](../../../../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig ATS-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om hur du [konfigurerar ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

För att få tillgång till ditt ATS-konto på Platform måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `connectionString` | En anslutningssträng som ska anslutas till din Azure Table Storage-instans. |

Mer information om hur du kommer igång finns i [det här Azure Table Storage-dokumentet](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction).

## Anslut ditt Azure Table Storage-konto

När du har samlat in de nödvändiga inloggningsuppgifterna kan du följa stegen nedan för att skapa ett nytt ATS-konto för att ansluta till plattformen.

Logga in på <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> och välj sedan **Källor** i det vänstra navigeringsfältet för att komma åt arbetsytan *Källor* . På *katalogskärmen* visas en mängd olika källor som du kan skapa inkommande konto för, och varje källa visar antalet befintliga konton och datauppsättningsflöden som är kopplade till dem.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under kategorin *Databaser* väljer du **Azure Table Storage** för att visa ett informationsfält till höger på skärmen. Informationsfältet innehåller en kort beskrivning av den valda källan samt alternativ för att ansluta till källan eller visa dess dokumentation. Om du vill skapa en ny inkommande anslutning väljer du **Anslut källa**.

![katalog](../../../../images/tutorials/create/ats/catalog.png)

Sidan *Anslut till Azure Table Storage* visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **Nytt konto**. På det indataformulär som visas anger du ett namn, en valfri beskrivning och dina ATS-autentiseringsuppgifter för anslutningen. När du är klar väljer du **Anslut** och tillåt sedan en tid för det nya kontot att upprätta.

![koppla](../../../../images/tutorials/create/ats/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det ATS-konto du vill ansluta till och sedan väljer du **Nästa** för att fortsätta.

![befintlig](../../../../images/tutorials/create/ats/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt ATS-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till plattformen](../../dataflow/databases.md).