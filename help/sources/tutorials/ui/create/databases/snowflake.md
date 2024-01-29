---
title: Skapa en Snowflake-källanslutning i användargränssnittet
type: Tutorial
description: Lär dig hur du skapar en Snowflake-källanslutning med Adobe Experience Platform användargränssnitt.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: 4de2193a45fc2925af310b5e2475eabe26d13adc
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 1%

---

# Skapa en [!DNL Snowflake] källanslutning i användargränssnittet

>[!IMPORTANT]
>
>The [!DNL Snowflake] Källan är tillgänglig i källkatalogen för användare som har köpt Real-time Customer Data Platform Ultimate.

Den här självstudiekursen innehåller steg för att skapa en [!DNL Snowflake] källanslutning med Adobe Experience Platform användargränssnitt.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../../../home.md): [!DNL Experience Platform] tillåter att data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

### Samla in nödvändiga inloggningsuppgifter

Du måste ange värden för följande autentiseringsegenskaper för att kunna autentisera dina [!DNL Snowflake] källa.

>[!BEGINTABS]

>[!TAB Autentisering av kontonyckel]

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| Konto | Ett kontonamn identifierar unikt ett konto inom organisationen. I det här fallet måste du unikt identifiera ett konto för olika [!DNL Snowflake] organisationer. Om du vill göra det måste du lägga till ditt organisationsnamn i kontonamnet. Till exempel: `orgname-account_name`. Mer information om kontonamn finns i [!DNL Snowflake] dokumentation om [kontoidentifierare](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| Lagerställe | The [!DNL Snowflake] dist.lager hanterar frågekörningsprocessen för programmet. Varje [!DNL Snowflake] lagerstället är oberoende av varandra och måste nås individuellt när data överförs till plattformen. |
| Databas | The [!DNL Snowflake] databasen innehåller de data som du vill ta med plattformen. |
| Användarnamn | Användarnamnet för [!DNL Snowflake] konto. |
| Lösenord | Lösenordet för [!DNL Snowflake] användarkonto. |
| Roll | Den standardroll för åtkomstkontroll som ska användas i [!DNL Snowflake] session. Rollen ska vara en befintlig roll som redan har tilldelats den angivna användaren. Standardrollen är `PUBLIC`. |
| Anslutningssträng | Anslutningssträngen som används för att ansluta till [!DNL Snowflake] -instans. Anslutningssträngsmönstret för [!DNL Snowflake] är `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB Autentisering med nyckelpar]

Om du vill använda autentisering med nyckelpar måste du generera ett 2 048-bitars RSA-nyckelpar och sedan ange följande värden när du skapar ett konto för [!DNL Snowflake] källa.

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Konto | Ett kontonamn identifierar unikt ett konto inom organisationen. I det här fallet måste du unikt identifiera ett konto för olika [!DNL Snowflake] organisationer. Om du vill göra det måste du lägga till ditt organisationsnamn i kontonamnet. Till exempel: `orgname-account_name`. Mer information om kontonamn finns i [!DNL Snowflake] dokumentation om [kontoidentifierare](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| Användarnamn | Användarnamnet för [!DNL Snowflake] konto. |
| Privat nyckel | The [!DNL Base64-]kodad privat nyckel för din [!DNL Snowflake] konto. Du kan generera antingen krypterade eller okrypterade privata nycklar. Om du använder en krypterad privat nyckel måste du även ange en lösenfras för den privata nyckeln vid autentisering mot Experience Platform. |
| Lösenfras för privat nyckel | Lösenfrasen för den privata nyckeln är ett extra säkerhetslager som du måste använda när du autentiserar med en krypterad privat nyckel. Du behöver inte ange lösenfrasen om du använder en okrypterad privat nyckel. |
| Databas | The [!DNL Snowflake] databas som innehåller de data som du vill importera till Experience Platform. |
| Lagerställe | The [!DNL Snowflake] dist.lager hanterar frågekörningsprocessen för programmet. Varje [!DNL Snowflake] lagerstället är oberoende av varandra och måste nås individuellt när data överförs till plattformen. |

Mer information om dessa värden finns i [det här Snowflake-dokumentet](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

För att få åtkomst till ditt Snowflake-konto på Experience Platform måste du ange följande autentiseringsvärde:

>[!NOTE]
>
>Du måste ange `PREVENT_UNLOAD_TO_INLINE_URL` flagga till `FALSE` för att tillåta att data tas bort från [!DNL Snowflake] databas till Experience Platform.

## Anslut ditt Snowflake-konto

Välj **[!UICONTROL Sources]** från vänster navigering för att komma åt [!UICONTROL Sources] arbetsyta.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också använda sökfältet till att hitta den källa du vill arbeta med.

Under [!UICONTROL Databases] kategori, välj **[!UICONTROL Snowflake]** och sedan **[!UICONTROL Add data]**.

![Källkatalogen med [!DNL Snowflake] markerad.](../../../../images/tutorials/create/snowflake/catalog.png)

The **[!UICONTROL Connect to Snowflake]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Välj [!DNL Snowflake] konto som du vill ansluta till och sedan välja **[!UICONTROL Next]** för att fortsätta.

![Det befintliga kontogränssnittet i källarbetsflödet.](../../../../images/tutorials/create/snowflake/existing.png)

### Nytt konto

Om du vill skapa ett nytt konto väljer du **[!UICONTROL New account]** och ange sedan ett namn och en valfri beskrivning av ditt nya [!DNL Snowflake] konto.

![Det nya kontogränssnittet i källarbetsflödet.](../../../../images/tutorials/create/snowflake/new.png)

>[!BEGINTABS]

>[!TAB Autentisering av kontonyckel]

Om du vill använda kontonyckelautentisering anger du anslutningssträngen i indataformuläret och väljer sedan **[!UICONTROL Connect to source]**.

![Autentiseringsgränssnittet för kontonyckeln.](../../../../images/tutorials/create/snowflake/connection-string.png)

>[!TAB Autentisering med nyckelpar]

Om du vill använda nyckelparsverifiering anger du värden för ditt konto, ditt användarnamn, din privata nyckel, lösenfras för privat nyckel, databas och lagerställe och väljer sedan **[!UICONTROL Connect to source]**.

![Autentiseringsgränssnittet för kontonyckelpar.](../../../../images/tutorials/create/snowflake/key-pair.png)

>[!ENDTABS]

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt Snowflake-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till [!DNL Platform]](../../dataflow/databases.md).
