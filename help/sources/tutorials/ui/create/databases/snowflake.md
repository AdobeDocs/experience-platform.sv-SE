---
title: Ansluta Snowflake till Experience Platform med användargränssnittet
type: Tutorial
description: Lär dig hur du skapar en källanslutning till Snowflake med Adobe Experience Platform användargränssnitt.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: cde31b692e9a11b15cf91a505133f75f69604cba
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 1%

---

# Anslut [!DNL Snowflake] till Experience Platform med användargränssnittet

>[!IMPORTANT]
>
>Källan [!DNL Snowflake] är tillgänglig i källkatalogen för användare som har köpt Real-Time Customer Data Platform Ultimate.

Läs den här vägledningen när du vill lära dig hur du ansluter ditt [!DNL Snowflake]-konto till Adobe Experience Platform med användargränssnittet.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av [!DNL Platform]-tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Experience Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

>[!NOTE]
>
>Du måste ange flaggan `PREVENT_UNLOAD_TO_INLINE_URL` till `FALSE` för att tillåta dataradering från din [!DNL Snowflake]-databas till Experience Platform.

## Navigera i källkatalogen {#navigate}

I plattformsgränssnittet väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i [!UICONTROL Sources]. Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj **[!DNL Snowflake]** under kategorin *[!UICONTROL Databases]* och välj sedan **[!UICONTROL Set up]**.

>[!TIP]
>
>Källor i källkatalogen visar alternativet **[!UICONTROL Set up]** när en angiven källa ännu inte har något autentiserat konto. När det finns ett autentiserat konto ändras det här alternativet till **[!UICONTROL Add data]**.

![Källkatalogen med Snowflake-kortet valt..](../../../../images/tutorials/create/snowflake/catalog.png)

## Använd ett befintligt konto {#existing}

Därefter går du till autentiseringssteget i arbetsflödet för källor. Här kan du antingen använda ett befintligt konto eller skapa ett nytt.

Om du vill använda ett befintligt konto markerar du det [!DNL Snowflake]-konto du vill ansluta till och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![Det befintliga kontogränssnittet i källarbetsflödet.](../../../../images/tutorials/create/snowflake/existing.png)

## Skapa ett nytt konto {#create}

Om du inte har något befintligt konto måste du skapa ett nytt konto genom att ange de autentiseringsuppgifter som motsvarar källan.

Om du vill skapa ett nytt konto väljer du **[!UICONTROL New account]** och anger sedan ett namn och kan lägga till en beskrivning för ditt konto.

### Anslut till Experience Platform på Azure {#azure}

Du kan ansluta ditt [!DNL Snowflake]-konto till Experience Platform på Azure med autentisering av kontonycklar eller autentisering med nyckelpar.

>[!BEGINTABS]

>[!TAB Autentisering av kontonyckel]

Om du vill använda kontonyckelautentisering väljer du **[!UICONTROL Account key authentication]**, anger anslutningssträngen i indataformuläret och väljer sedan **[!UICONTROL Connect to source]**.

![Autentiseringsgränssnittet för kontonyckeln.](../../../../images/tutorials/create/snowflake/account-key-auth.png)

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Konto | Ett kontonamn identifierar unikt ett konto inom organisationen. I det här fallet måste du unikt identifiera ett konto i olika [!DNL Snowflake]-organisationer. Om du vill göra det måste du lägga till ditt organisationsnamn i kontonamnet. Till exempel: `orgname-account_name`. Läs guiden om att [hämta din [!DNL Snowflake] kontoidentifierare](../../../../connectors/databases/snowflake.md#retrieve-your-account-identifier) om du vill ha mer information. Mer information finns i [[!DNL Snowflake] dokumentationen](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| Lagerställe | Lagerstället [!DNL Snowflake] hanterar frågekörningsprocessen för programmet. Varje [!DNL Snowflake]-lagerställe är oberoende av varandra och måste nås individuellt när data överförs till plattformen. |
| Databas | Databasen [!DNL Snowflake] innehåller de data som du vill ta med plattformen. |
| Användarnamn | Användarnamnet för kontot [!DNL Snowflake]. |
| Lösenord | Lösenordet för användarkontot [!DNL Snowflake]. |
| Roll | Standardrollen för åtkomstkontroll som ska användas i sessionen [!DNL Snowflake]. Rollen ska vara en befintlig roll som redan har tilldelats den angivna användaren. Standardrollen är `PUBLIC`. |
| Anslutningssträng | Anslutningssträngen som används för att ansluta till din [!DNL Snowflake]-instans. Anslutningssträngsmönstret för [!DNL Snowflake] är `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB Autentisering med nyckelpar]

Om du vill använda nyckelpars-autentisering väljer du **[!UICONTROL KeyPair authentication]**, anger värden för ditt konto, användarnamn, privat nyckel, lösenfras för privat nyckel, databas och lagerställe och väljer sedan **[!UICONTROL Connect to source]**.

![Autentiseringsgränssnittet för kontonyckelpar.](../../../../images/tutorials/create/snowflake/key-pair-auth.png)

Med autentisering med nyckelpar måste du generera ett 2 048-bitars RSA-nyckelpar och sedan ange följande värden när du skapar ett konto för [!DNL Snowflake]-källan.

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Konto | Ett kontonamn identifierar unikt ett konto inom organisationen. I det här fallet måste du unikt identifiera ett konto i olika [!DNL Snowflake]-organisationer. Om du vill göra det måste du lägga till ditt organisationsnamn i kontonamnet. Till exempel: `orgname-account_name`. Läs guiden om att [hämta din [!DNL Snowflake] kontoidentifierare](../../../../connectors/databases/snowflake.md#retrieve-your-account-identifier) om du vill ha mer information. Mer information finns i [[!DNL Snowflake] dokumentationen](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| Användarnamn | Användarnamnet för ditt [!DNL Snowflake]-konto. |
| Privat nyckel | Den [!DNL Base64-]kodade privata nyckeln för ditt [!DNL Snowflake]-konto. Du kan generera antingen krypterade eller okrypterade privata nycklar. Om du använder en krypterad privat nyckel måste du även ange en lösenfras för den privata nyckeln vid autentisering mot Experience Platform. Läs guiden om att [hämta din [!DNL Snowflake] privata nyckel](../../../../connectors/databases/snowflake.md) om du vill ha mer information. |
| Lösenfras för privat nyckel | Lösenfrasen för den privata nyckeln är ett extra säkerhetslager som du måste använda när du autentiserar med en krypterad privat nyckel. Du behöver inte ange lösenfrasen om du använder en okrypterad privat nyckel. |
| Databas | Databasen [!DNL Snowflake] som innehåller de data som du vill importera till Experience Platform. |
| Lagerställe | Lagerstället [!DNL Snowflake] hanterar frågekörningsprocessen för programmet. Varje [!DNL Snowflake]-lagerställe är oberoende av varandra och måste nås individuellt när data överförs till plattformen. |

Mer information om dessa värden finns i [det här Snowflake-dokumentet](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

### Anslut till Experience Platform på AWS {#aws}

>[!AVAILABILITY]
>
>Detta avsnitt gäller implementeringar av Experience Platform som körs på Amazon Web Services (AWS). Experience Platform som körs på AWS är för närvarande tillgängligt för ett begränsat antal kunder. Mer information om den Experience Platform-infrastruktur som stöds finns i [Experience Platform översikt över flera moln](../../../../../landing/multi-cloud.md).

Om du vill skapa ett nytt [!DNL Snowflake]-konto och ansluta till Experience Platform på AWS kontrollerar du att du befinner dig i en VA6-sandlåda och anger sedan de nödvändiga autentiseringsuppgifterna för autentisering.

![Det nya kontosteget i källarbetsflödet där du kan ansluta Snowflake till Experience Platform på AWS.](../../../../images/tutorials/create/snowflake/aws-auth.png)

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Värd | Den värd-URL som ditt [!DNL Snowflake]-konto ansluter till. |
| Port | Portnumret som används av [!DNL Snowflake] vid anslutning till en server via Internet. |
| Användarnamn | Användarnamnet som är associerat med ditt [!DNL Snowflake]-konto. |
| Lösenord | Lösenordet som är kopplat till ditt [!DNL Snowflake]-konto. |
| Databas | Databasen [!DNL Snowflake] från vilken data hämtas. |
| Schema | Namnet på schemat som är associerat med din [!DNL Snowflake]-databas. Du måste se till att användaren som du vill ge databasåtkomst till också har åtkomst till det här schemat. |
| Lagerställe | Det [!DNL Snowflake]-lagerställe som du använder. |

### Hoppa över förhandsgranskning av exempeldata {#skip-preview-of-sample-data}

Under dataurvalssteget kan du få en timeout när du importerar stora tabeller eller datafiler. Du kan hoppa över förhandsgranskning av data för att kringgå tidsgränsen och ändå visa ditt schema, om än utan exempeldata. Aktivera alternativet **[!UICONTROL Skip previewing sample data]** om du vill hoppa över förhandsgranskning av data.

Resten av arbetsflödet förblir detsamma. Den enda skillnaden är att om du hoppar över förhandsgranskning av data kan det förhindra att beräknade och obligatoriska fält valideras automatiskt under mappningssteget, och du måste då validera dessa fält manuellt under mappningen.

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt Snowflake-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till [!DNL Platform]](../../dataflow/databases.md).
