---
keywords: Experience Platform;hem;populära ämnen;Snowflake
title: Skapa en Snowflake-källanslutning i användargränssnittet
topic-legacy: overview
type: Tutorial
description: Lär dig hur du skapar en Snowflake-källanslutning med Adobe Experience Platform användargränssnitt.
source-git-commit: 2e717f33b487430220bd3bb7812558cde81d8852
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 1%

---

# Skapa en [!DNL Snowflake]-källanslutning i användargränssnittet

>[!NOTE]
>
> [!DNL Snowflake]-kopplingen är i betaversion. Se [Källöversikt](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade anslutningar.

I den här självstudiekursen beskrivs hur du skapar en [!DNL Snowflake]-källkoppling med Adobe Experience Platform användargränssnitt.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande plattformskomponenter:

* [Källor](../../../../home.md):  [!DNL Experience Platform] gör att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av  [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md):  [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda  [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till ditt Snowflake-konto på [!DNL Platform] måste du ange följande autentiseringsvärde:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| Konto | Det [!DNL Snowflake]-konto som du vill ansluta till plattformen. |
| Lagerställe | Lagret [!DNL Snowflake] hanterar frågekörningsprocessen för programmet. Varje [!DNL Snowflake] lagerställe är oberoende av varandra och måste nås individuellt när data skickas till plattformen. |
| Databas | [!DNL Snowflake] innehåller de data som du vill ta med plattformen. |
| Användarnamn | Användarnamnet för [!DNL Snowflake]-kontot. |
| Lösenord | Lösenordet för användarkontot [!DNL Snowflake]. |
| Anslutningssträng | Anslutningssträngen som används för att ansluta till din [!DNL Snowflake]-instans. Anslutningssträngsmönstret för [!DNL Snowflake] är `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |

Mer information om dessa värden finns i [det här Snowflake-dokumentet](https://docs.snowflake.com/en/user-guide/oauth-custom.html).

## Anslut ditt Snowflake-konto

Välj **[!UICONTROL Sources]** från vänster navigering i plattformsgränssnittet för att komma åt arbetsytan [!UICONTROL Sources]. Skärmen [!UICONTROL Catalog] innehåller en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också använda sökfältet till att hitta den källa du vill arbeta med.

Under kategorin [!UICONTROL Databases] väljer du **[!UICONTROL Snowflake]** och sedan **[!UICONTROL Add data]**.

![](../../../../images/tutorials/create/snowflake/catalog.png)

Sidan **[!UICONTROL Connect to Snowflake]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill ansluta ett befintligt konto markerar du det Snowflake-konto du vill ansluta till och fortsätter sedan med **[!UICONTROL Next]**.

![](../../../../images/tutorials/create/snowflake/existing.png)

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och dina inloggningsuppgifter för Snowflake i det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![](../../../../images/tutorials/create/snowflake/new.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt Snowflake-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till [!DNL Platform]](../../dataflow/databases.md).
