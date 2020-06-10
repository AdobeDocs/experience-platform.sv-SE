---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en Couchbase-källanslutning i användargränssnittet
topic: overview
translation-type: tm+mt
source-git-commit: adb9c46e7337897e2336971e58ebc90b0e497ea0
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---


# Skapa en Couchbase-källanslutning i användargränssnittet

> [!NOTE]
> Couchbase-kopplingen är i betaversion. Funktionerna och dokumentationen kan komma att ändras.

Källkopplingar i [!DNL Adobe Experience Platform] ger möjlighet att importera externt källkodsdata på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en Couchbase-källkoppling med [!DNL Platform] användargränssnittet.

## Komma igång

Den här självstudien kräver en fungerande förståelse av följande komponenter i [!DNL Platform]:

* [Experience Data Model (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [Kundprofil](../../../../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig Couchbase-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om hur du [konfigurerar ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

För att kunna autentisera din källanslutning till Couchbase måste du ange värden för följande anslutningsegenskap:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `connectionString` | Anslutningssträngen som används för att ansluta till din Couchbase-instans. Anslutningssträngsmönstret för Couchbase är `Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];`. Mer information om hur du hämtar en anslutningssträng finns i dokumentationen om [Couchbase-anslutningen](https://docs.Couchbase.com/c-sdk/2.10/client-settings.html#configuring-overview). |

## Anslut ditt Couchbase-konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att skapa ett nytt Couchbase-konto att ansluta till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt *[!UICONTROL Sources]* arbetsytan. På *[!UICONTROL Catalog]* skärmen visas en mängd olika källor som du kan skapa ett inkommande konto för, och varje källa visar antalet befintliga konton och datauppsättningsflöden som är kopplade till dem.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under *[!UICONTROL Databases]* kategorin väljer du **[!UICONTROL Couchbase]** klicka **på +-ikonen (+)** för att skapa en ny Couchbase-koppling.

![katalog](../../../../images/tutorials/create/couchbase/catalog.png)

Sidan visas *[!UICONTROL Connect to Couchbase]* . På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. På indataformuläret som visas anger du en anslutning med ett namn, en valfri beskrivning och dina Couchbase-autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan en tid för det nya kontot att upprätta.

![koppla](../../../../images/tutorials/create/couchbase/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det Couchbase-konto du vill ansluta till och fortsätter sedan **[!UICONTROL Next]** i det övre högra hörnet.

![befintlig](../../../../images/tutorials/create/couchbase/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt Couchbase-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till plattformen](../../dataflow/databases.md).