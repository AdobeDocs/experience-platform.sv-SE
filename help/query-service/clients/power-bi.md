---
keywords: Experience Platform;hem;populära ämnen;frågetjänst;Query Service;Power BI;power bi;connect to query service;
solution: Experience Platform
title: Anslut Power BI till frågetjänst
topic-legacy: connect
description: Det här dokumentet går igenom stegen för att ansluta Power BI med Adobe Experience Platform Query Service.
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: 0c20b19c4c34b29c46964d5d87a8646c61055b06
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 1%

---

# Anslut Power BI till frågetjänst

Det här dokumentet beskriver hur du ansluter Power BI Desktop till Adobe Experience Platform Query Service.

## Komma igång

Den här guiden kräver att du redan har tillgång till datorprogrammet Power BI och känner till hur du navigerar i gränssnittet. Om du vill hämta Power BI Desktop eller om du vill ha mer information kan du läsa [officiell Power BI](https://docs.microsoft.com/en-us/power-bi/).

>[!IMPORTANT]
>
> Power BI är **endast** som är tillgängliga på Windows-enheter.

Om du vill ha de autentiseringsuppgifter som krävs för att ansluta Power BI till Experience Platform måste du ha tillgång till arbetsytan Frågor i plattformsgränssnittet. Kontakta IMS-organisationens administratör om du inte har tillgång till arbetsytan Frågor.

När du har installerat Power BI måste du installera `Npgsql`, ett .NET-drivrutinspaket för PostgreSQL. Mer information om Npgsql finns i [Npgsql-dokumentation](https://www.npgsql.org/doc/index.html).

>[!IMPORTANT]
>
>Du måste hämta v4.0.10 eller tidigare, eftersom nyare versioner orsakar fel.

Under &quot;[!DNL Npgsql GAC Installation]&quot; på skärmen för anpassade inställningar väljer du **[!DNL Will be installed on local hard drive]**.

För att säkerställa att Npgsql har installerats korrekt måste du starta om datorn innan du fortsätter till nästa steg.

## Anslut Power BI till frågetjänst {#connect-power-bi}

Om du vill ansluta Power BI till frågetjänsten öppnar du Power BI och väljer **[!DNL Get Data]** i menyfliksområdet på den översta menyn.

![](../images/clients/power-bi/open-power-bi.png)

Ange PostgreSQL i sökfältet om du vill begränsa listan med datakällor. Under resultaten som visas väljer du **[!DNL PostgreSQL database]**, följt av **[!DNL Connect]**.

![](../images/clients/power-bi/get-data.png)

Dialogrutan PostgreSQl-databas öppnas och värden för servern och databasen efterfrågas. Dessa värden hämtas från dina Adobe Experience Platform-uppgifter. Logga in på användargränssnittet för plattformen och välj **[!UICONTROL Queries]** från vänster navigering, följt av **[!UICONTROL Credentials]**. Mer information om hur du hittar databasnamn, värd, port och inloggningsuppgifter finns i [inloggningsguide](../ui/credentials.md).

![Instrumentpanelen för inloggningsuppgifter med autentiseringsuppgifter är markerad i Experience Platform.](../images/clients/power-bi/query-service-credentials-page.png)

För **[!DNL Server]** i Power BI anger du värdet för värddatorn som finns i avsnittet med autentiseringsuppgifter för frågetjänsten. Lägg till port för produktion `:80` till slutet av värdsträngen. Exempel, `made-up.platform-query.adobe.io:80`.

The **[!DNL Database]** -fältet kan vara antingen&quot;all&quot; eller ett datamängdstabellnamn. Exempel, `prod:all`.

>[!IMPORTANT]
>
>Kapslade datastrukturer i BI-verktyg från tredje part kan förenklas för att förbättra användbarheten och minska den arbetsbelastning som krävs för att hämta, analysera, omvandla och rapportera data. Läs dokumentationen på[`FLATTEN` funktion](../best-practices/flatten-nested-data.md) för instruktioner om hur du aktiverar den här inställningen vid anslutning till en databas.

![Power BI-kontrollpanelen med server- och databasindatafälten markerade.](../images/clients/power-bi/postgresql-database-dialog.png)

### Dataanslutningsläge

Nu kan du välja **[!DNL Data Connectivity mode]**. Välj **[!DNL Import]** följt av **[!DNL OK]** om du vill visa en lista över alla tillgängliga tabeller, eller väljer **[!DNL DirectQuery]** för att fråga datakällan direkt utan att importera eller kopiera data direkt till Power BI.

Mer information om **[!DNL Import]** mode, please read the section on [importera en tabell](#import). Mer information om **[!DNL DirectQuery]** mode, please read the section on [fråga en datauppsättning utan att importera data](#direct-query).

Välj **[!DNL OK]** när du har bekräftat databasinformationen.

![](../images/clients/power-bi/connectivity-mode.png)

### Autentisering

En fråga om ditt användarnamn, lösenord och programinställningar visas. Användarnamnet är i det här fallet ditt företags-ID och lösenordet är din autentiseringstoken. Båda finns på sidan med autentiseringsuppgifter för frågetjänsten.

Fyll i dessa uppgifter och välj **[!DNL Connect]** för att fortsätta till nästa steg.

![](../images/clients/power-bi/import-mode.png)

## Importera en tabell {#import}

Genom att välja **[!DNL Import]** [!DNL Data Connectivity mode]importeras hela datauppsättningen, vilket gör att du kan använda de markerade tabellerna och kolumnerna i Power BI-datorprogrammet i befintligt skick.

>[!IMPORTANT]
>
>Om du vill se dataändringar som har gjorts sedan den första importen måste du uppdatera data i Power BIET genom att importera hela datauppsättningen igen.

Om du vill importera en tabell anger du server- och databasinformation [enligt ovan](#connect-power-bi) och väljer **[!DNL Import]** [!DNL Data Connectivity mode], följt av **[!DNL OK]**. En dialogruta med en lista över alla tillgängliga tabeller visas. Markera tabellen som du vill förhandsgranska, följt av **[!DNL Load]** för att föra in datauppsättningen i Power BI.

![](../images/clients/power-bi/preview-table.png)

Tabellen importeras nu till Power BI.

![](../images/clients/power-bi/import-table.png)

### Importera tabeller med anpassad SQL

Power BI och andra tredjepartsverktyg som Tableau tillåter för närvarande inte användare att importera kapslade objekt, som XDM-objekt i Platform. Med Power BI kan du använda anpassad SQL för att komma åt dessa kapslade fält och skapa en förenklad vy av data. Power BI läser sedan in den förenklade vyn av tidigare kapslade data som en normal tabell.

I PostgreSQL-databasdrivrutinen väljer du **[!DNL Advanced options]** för att ange en anpassad SQL-fråga i **[!DNL SQL statement]** -avsnitt. Den här anpassade frågan bör användas för att förenkla JSON-par med namn och värde till ett tabellformat.

![Avancerade alternativ för att skapa en anpassad SQL-sats i dataanslutningsläget.](../images/clients/power-bi/custom-sql-statement.png)

När du har angett en egen fråga väljer du **[!DNL OK]** för att fortsätta ansluta databasen. Se [autentisering](#authentication) om du vill ha vägledning om hur du ansluter en databas från den här delen av arbetsflödet ovan.

När autentiseringen är klar visas en förhandsgranskning av de förenklade data som en tabell på kontrollpanelen för Power BI Desktop. Servern och databasnamnet visas högst upp i dialogrutan. Välj **[!DNL Load]** för att slutföra importprocessen.

![Den förenklade importerade tabellen på kontrollpanelen för Power BI.](../images/clients/power-bi/imported-table-preview.png)

Visualiseringarna är nu tillgängliga för redigering och export från Power BI-datorprogrammet.

## Fråga datauppsättningen utan att importera data {#direct-query}

The **[!DNL DirectQuery]** [!DNL Data Connectivity mode] Frågar datakällan direkt utan att importera eller kopiera data till Power BI Desktop. I det här anslutningsläget kan du uppdatera alla visualiseringar med aktuella data via gränssnittet. Den tid som krävs för att skapa eller uppdatera visualiseringen varierar dock beroende på den underliggande datakällans prestanda.

Om du vill använda [!DNL Data Connectivity mode]väljer du **[!DNL DirectQuery]** växla sedan **[!DNL Advanced options]** för att ange en anpassad SQL-fråga i **[!DNL SQL statement]** -avsnitt. Kontrollera att **[!DNL Include relationship columns]** är markerat. När du har slutfört frågan väljer du **[!DNL OK]** för att fortsätta.

![](../images/clients/power-bi/direct-query-mode.png)

En förhandsgranskning av frågan visas. Välj **[!DNL Load]** för att se resultatet av frågan.

![](../images/clients/power-bi/preview-direct-query.png)

## Nästa steg

Genom att läsa det här dokumentet bör du nu förstå hur du ansluter till Power BI-datorprogrammet och de olika dataanslutningslägena som är tillgängliga. Mer information om hur du skriver och kör frågor finns i [riktlinjer för frågekörning](../best-practices/writing-queries.md).
