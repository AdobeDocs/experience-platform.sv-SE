---
keywords: Experience Platform;hem;populära ämnen;Snowflake
title: Skapa en Snowflake-källanslutning i användargränssnittet
type: Tutorial
description: Lär dig hur du skapar en Snowflake-källanslutning med Adobe Experience Platform användargränssnitt.
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 2%

---

# Skapa en [!DNL Snowflake] källanslutning i användargränssnittet

Den här självstudiekursen innehåller steg för att skapa en [!DNL Snowflake] källanslutning med Adobe Experience Platform användargränssnitt.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande plattformskomponenter:

* [Källor](../../../../home.md): [!DNL Experience Platform] tillåter att data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till ditt Snowflake-konto på [!DNL Platform]måste du ange följande autentiseringsvärde:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| Konto | Det fullständiga kontonamnet som är kopplat till ditt [!DNL Snowflake] konto. En fullständigt kvalificerad [!DNL Snowflake] kontonamnet innehåller ditt kontonamn, din region och din molnplattform. Exempel, `cj12345.east-us-2.azure`. Mer information om kontonamn finns i [[!DNL Snowflake document on account identifiers]](https://docs.snowflake.com/en/user-guide/admin-account-identifier.html). |
| Lagerställe | The [!DNL Snowflake] dist.lager hanterar frågekörningsprocessen för programmet. Varje [!DNL Snowflake] lagerstället är oberoende av varandra och måste nås individuellt när data överförs till plattformen. |
| Databas | The [!DNL Snowflake] databasen innehåller de data som du vill ta med plattformen. |
| Användarnamn | Användarnamnet för [!DNL Snowflake] konto. |
| Lösenord | Lösenordet för [!DNL Snowflake] användarkonto. |
| Anslutningssträng | Anslutningssträngen som används för att ansluta till [!DNL Snowflake] -instans. Anslutningssträngsmönstret för [!DNL Snowflake] är `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

Mer information om dessa värden finns i [det här Snowflake-dokumentet](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

## Anslut ditt Snowflake-konto

Välj **[!UICONTROL Sources]** från vänster navigering för att komma åt [!UICONTROL Sources] arbetsyta. The [!UICONTROL Catalog] I visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också använda sökfältet till att hitta den källa du vill arbeta med.

Under [!UICONTROL Databases] kategori, välj **[!UICONTROL Snowflake]** och sedan markera **[!UICONTROL Add data]**.

![](../../../../images/tutorials/create/snowflake/catalog.png)

The **[!UICONTROL Connect to Snowflake]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill ansluta till ett befintligt konto väljer du det Snowflake-konto du vill ansluta till och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![](../../../../images/tutorials/create/snowflake/existing.png)

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och dina inloggningsuppgifter för Snowflake i det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![](../../../../images/tutorials/create/snowflake/new.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt Snowflake-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till [!DNL Platform]](../../dataflow/databases.md).
