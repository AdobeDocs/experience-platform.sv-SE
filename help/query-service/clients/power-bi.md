---
keywords: Experience Platform;hem;populära ämnen;frågetjänst;Query Service;Power BI;power bi;connect to query service;
solution: Experience Platform
title: Anslut Power BI till frågetjänst
description: Det här dokumentet går igenom stegen för att ansluta Power BI med Adobe Experience Platform Query Service.
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: 26f0725f0f239707bd719ed46929648f8d557155
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 0%

---

# Anslut [!DNL Power BI] till frågetjänsten

Det här dokumentet innehåller stegen för att ansluta [!DNL Power BI] Desktop med Adobe Experience Platform Query Service.

## Komma igång

Den här guiden kräver att du redan har tillgång till skrivbordsappen [!DNL Power BI] och känner till hur du navigerar i gränssnittet. Om du vill hämta [!DNL Power BI] Desktop eller om du vill ha mer information läser du [officiell [!DNL Power BI] dokumentation](https://docs.microsoft.com/en-us/power-bi/).

>[!IMPORTANT]
>
> Skrivbordsprogrammet [!DNL Power BI] är **endast** tillgängligt på Windows-enheter.

Om du vill få de nödvändiga autentiseringsuppgifterna för att ansluta [!DNL Power BI] till Experience Platform måste du ha tillgång till arbetsytan Frågor i plattformsgränssnittet. Kontakta din organisationsadministratör om du inte har åtkomst till arbetsytan för frågor just nu.

När du har installerat [!DNL Power BI] måste du installera `Npgsql`, ett .NET-drivrutinspaket för PostgreSQL. Mer information om Npgsql finns i [Npgsql-dokumentationen](https://www.npgsql.org/doc/index.html).

>[!IMPORTANT]
>
>Du måste hämta v4.0.10 eller tidigare, eftersom nyare versioner orsakar fel.

Välj **[!DNL Will be installed on local hard drive]** under [!DNL Npgsql GAC Installation] på skärmen för anpassade inställningar.

För att säkerställa att Npgsql har installerats korrekt måste du starta om datorn innan du fortsätter till nästa steg.

## Anslut [!DNL Power BI] till frågetjänsten {#connect-power-bi}

Om du vill ansluta [!DNL Power BI] till frågetjänsten öppnar du [!DNL Power BI] och väljer **[!DNL Get Data]** i menyfliksområdet på den översta menyn. Ange sedan [!DNL PostgreSQL] i sökfältet för att begränsa listan med datakällor. Välj **[!DNL PostgreSQL database]** följt av **[!DNL Connect]** bland de resultat som visas.

Databasdialogrutan [!DNL PostgreSQL] visas och begär värden för servern och databasen. Ytterligare instruktioner om hur du [ansluter till en PostgreSQL-databas från Power Query Desktop](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-to-a-postgresql-database-from-power-query-desktop) finns i den officiella [!DNL PowerBI] -dokumentationen.

Dessa obligatoriska värden hämtas från dina Adobe Experience Platform-uppgifter. Om du vill hitta dina autentiseringsuppgifter loggar du in på plattformsgränssnittet och väljer **[!UICONTROL Queries]** i den vänstra navigeringen, följt av **[!UICONTROL Credentials]**. Mer information om hur du söker efter databasnamn, värd, port och inloggningsuppgifter finns i [referenshandboken](../ui/credentials.md).

>[!IMPORTANT]
>
>Som Power BI- eller Tableau-användare kan du ansluta Customer Journey Analytics till dina BI-verktyg från fliken med autentiseringsuppgifter för frågetjänsten. Instruktioner om hur du [ansluter dina BI-verktyg till Customer Journey Analytics](../ui/credentials.md#connect-to-customer-journey-analytics) finns i dokumentationen för autentiseringsuppgifter.

![Arbetsytan för frågor i Experience Platform med fliken Autentiseringsuppgifter och inloggningsuppgifterna som förfaller är markerade.](../images/clients/power-bi/query-service-credentials-page.png)

I fältet **[!DNL Server]** i dialogrutan [!DNL PostgreSQL database] anger du värdet för värden som finns i avsnittet för frågetjänsten [!UICONTROL Credentials]. Lägg till port `:80` i slutet av värdsträngen för produktion. Exempel: `made-up.platform-query.adobe.io:80`.

Fältet **[!DNL Database]** kan vara antingen&quot;all&quot; eller ett datamängdstabellnamn. Exempel: `prod:all`.

>[!IMPORTANT]
>
>Kapslade datastrukturer i BI-verktyg från tredje part kan förenklas för att förbättra användbarheten och minska den arbetsbelastning som krävs för att hämta, analysera, omvandla och rapportera data. Mer information om hur du aktiverar den här inställningen vid anslutning till en databas finns i dokumentationen för [`FLATTEN`-funktionen](../key-concepts/flatten-nested-data.md).

### Dataanslutningsläge {#data-connectivity-mode}

Sedan kan du välja din **[!DNL Data Connectivity mode]**. I dialogrutan [!DNL PostgreSQL database] väljer du **[!DNL Import]** följt av **[!DNL OK]** om du vill visa en lista över alla tillgängliga tabeller, eller välj **[!DNL DirectQuery]** om du vill fråga datakällan direkt utan att importera eller kopiera data direkt till [!DNL Power BI].

Läs avsnittet [Importera en tabell](#import) om du vill veta mer om läget **[!DNL Import]**. Om du vill veta mer om läget **[!DNL DirectQuery]** kan du läsa avsnittet [ställa frågor om en datauppsättning utan att importera data](#direct-query).

Välj **[!DNL OK]** när du har bekräftat databasinformationen.

### Autentisering {#authentication}

När du har bekräftat ditt dataanslutningsläge visas en fråga om ditt användarnamn, lösenord och programinställningar. Användarnamnet är i det här fallet ditt företags-ID och lösenordet är din autentiseringstoken. Båda finns på sidan med autentiseringsuppgifter för frågetjänsten.

Fyll i dessa uppgifter och välj sedan **[!DNL Connect]** för att fortsätta till nästa steg.

## Importera en tabell {#import}

Genom att välja **[!DNL Import]** [!DNL Data Connectivity mode] importeras hela datauppsättningen så att du kan använda de markerade tabellerna och kolumnerna i [!DNL Power BI]-skrivbordsprogrammet som de är.

>[!IMPORTANT]
>
>Om du vill se dataändringar som har gjorts sedan den första importen måste du uppdatera data i [!DNL Power BI] genom att importera den fullständiga datauppsättningen igen.

Om du vill importera en tabell anger du server- och databasinformationen [ enligt beskrivningen ovan](#connect-power-bi) och väljer **[!DNL Import]** [!DNL Data Connectivity mode] följt av **[!DNL OK]**. Dialogrutan [!DNL Navigator] visas med en lista över alla tillgängliga tabeller. Markera den tabell som du vill förhandsgranska, följt av **[!DNL Load]**, för att överföra datauppsättningen till Power BI. Tabellen importeras nu till [!DNL Power BI].

[Allmän information om att ansluta till data i PowerBi-datorprogrammet](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-quickstart-connect-to-data#connect-to-data) finns i den officiella dokumentationen.

### Importera tabeller med anpassad SQL

[!DNL Power BI] och andra verktyg från tredje part, som [!DNL Tableau], tillåter för närvarande inte användare att importera kapslade objekt, som XDM-objekt på plattformen. Om du vill ta hänsyn till detta kan du i [!DNL Power BI] använda anpassad SQL för att komma åt dessa kapslade fält och skapa en förenklad vy av data. [!DNL Power BI] läser sedan in den förenklade vyn av tidigare kapslade data som en normal tabell.

I dialogrutan [!DNL PostgreSQL database] väljer du **[!DNL Advanced options]** för att ange en anpassad SQL-fråga i avsnittet **[!DNL SQL statement]**. Den här anpassade frågan bör användas för att förenkla JSON-par med namn och värde till ett tabellformat. Den officiella dokumentationen innehåller även information om hur du [ansluter PowerBI med en SQL-sats i de avancerade alternativen](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-using-advanced-options).

När du har angett din anpassade fråga väljer du **[!DNL OK]** om du vill fortsätta ansluta databasen. Se avsnittet [autentisering](#authentication) ovan för vägledning om hur du ansluter en databas från den här delen av arbetsflödet.

När autentiseringen är klar visas en förhandsgranskning av de förenklade data som en tabell på kontrollpanelen för skrivbordet i [!DNL Power BI]. Servern och databasnamnet visas högst upp i dialogrutan. Välj **[!DNL Load]** för att slutföra importprocessen.

Visualiseringarna är nu tillgängliga för redigering och export från skrivbordsappen [!DNL Power BI].

## Fråga datauppsättningen utan att importera data {#direct-query}

**[!DNL DirectQuery]** [!DNL Data Connectivity mode] frågar datakällan direkt utan att importera eller kopiera data till skrivbordet i [!DNL Power BI]. I det här anslutningsläget kan du uppdatera alla visualiseringar med aktuella data via gränssnittet. Den tid som krävs för att skapa eller uppdatera visualiseringen varierar dock beroende på den underliggande datakällans prestanda.

Mer information om [användningen av [!DNL DirectQuery]](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-use-directquery) samt en omfattande diskussion om dess [anslutningsalternativ, användningsfall och begränsningar](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-directquery-about) finns i den officiella [!DNL PowerBI]-dokumentationen.

Om du vill använda denna/detta [!DNL Data Connectivity mode] väljer du **[!DNL DirectQuery]** och sedan **[!DNL Advanced options]** för att ange en anpassad SQL-fråga i avsnittet **[!DNL SQL statement]**. Kontrollera att **[!DNL Include relationship columns]** är markerat. När du har slutfört din fråga väljer du **[!DNL OK]** för att fortsätta.

En förhandsgranskning av frågan visas. Välj **[!DNL Load]** om du vill visa resultatet av frågan.

## Nästa steg

Genom att läsa det här dokumentet bör du nu förstå hur du ansluter till datorprogrammet [!DNL Power BI] och de olika dataanslutningslägena som är tillgängliga. Mer information om hur du skriver och kör frågor finns i [vägledningen för frågekörning](../best-practices/writing-queries.md).
