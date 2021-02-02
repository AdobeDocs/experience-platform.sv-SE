---
keywords: Experience Platform;hem;populära ämnen;frågetjänst;Query Service;Power BI;power bi;connect to query service;
solution: Experience Platform
title: Anslut till Power BI
topic: connect
description: Det här dokumentet går igenom stegen för att ansluta Power BI med Adobe Experience Platform Query Service.
translation-type: tm+mt
source-git-commit: eac93f3465fa6ce4af7a6aa783cf5f8fb4ac9b9b
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---


# [!DNL Power BI]

Det här dokumentet beskriver hur du ansluter Power BI till Adobe Experience Platform Query Service.

>[!NOTE]
>
> Den här handboken förutsätter att du redan har tillgång till [!DNL Power BI] och är bekant med hur du navigerar i dess gränssnitt. Mer information om [!DNL Power BI] finns i [officiell [!DNL Power BI] dokumentation](https://docs.looker.com/).
>
> Dessutom är Power BI **endast** tillgängligt på Windows-enheter.

## Konfigurera [!DNL Power BI]

När du har installerat Power BI måste du installera `Npgsql`, ett .NET-drivrutinspaket för PostgreSQL. Mer information om Npgsql finns i [Npgsql-dokumentationen](https://www.npgsql.org/doc/index.html).

>[!IMPORTANT]
>
>Du måste hämta v4.0.10 eller tidigare, eftersom nyare versioner orsakar fel.

Välj **[!DNL Will be installed on local hard drive]** under [!DNL Npgsql GAC Installation] på den anpassade installationsskärmen.

För att säkerställa att npgsql har installerats korrekt startar du om datorn innan du fortsätter till nästa steg.

## Anslut [!DNL Power BI] till [!DNL Query Service]

Om du vill ansluta [!DNL Power BI] till [!DNL Query Service] öppnar du [!DNL Power BI] och väljer **[!DNL Get Data]** i menyfliksområdet på den översta menyn.

![](../images/clients/power-bi/open-power-bi.png)

Välj **[!DNL PostgreSQL database]** följt av **[!DNL Connect]**.

![](../images/clients/power-bi/get-data.png)

Nu kan du ange värden för servern och databasen. Mer information om hur du hittar databasnamn, värd, port och inloggningsuppgifter finns på sidan [inloggningsuppgifter på Platform](https://platform.adobe.com/query/configuration). Logga in på [!DNL Platform] och välj **[!UICONTROL Queries]** följt av **[!UICONTROL Credentials]** för att hitta dina inloggningsuppgifter.

**[!DNL Server]** är värddatorn som finns under anslutningsinformationen. För produktion lägger du till porten `:80` i slutet av värdsträngen. **[!DNL Database]** kan vara antingen&quot;all&quot; eller ett datamängdstabellnamn.

Dessutom kan du välja din **[!DNL Data Connectivity mode]**. Välj **[!DNL Import]** om du vill visa en lista över alla tillgängliga tabeller, eller välj **[!DNL DirectQuery]** om du vill skapa en fråga direkt.

Läs avsnittet [förhandsgranska och importera en tabell](#preview) om du vill veta mer om **[!DNL Import]**-läget. Mer information om läget **[!DNL DirectQuery]** finns i avsnittet [skapa SQL-satser](#create). Välj **[!DNL OK]** när du har bekräftat databasinformationen.

![](../images/clients/power-bi/connectivity-mode.png)

En fråga om ditt användarnamn, lösenord och programinställningar visas. Fyll i dessa uppgifter och välj sedan **[!DNL Connect]** för att fortsätta till nästa steg.

![](../images/clients/power-bi/import-mode.png)

## Förhandsgranska och importera en tabell {#preview}

Om du har valt **[!DNL Import]**-läge visas en dialogruta med en lista över alla tillgängliga tabeller. Markera den tabell som du vill förhandsgranska, följt av **[!DNL Load]** för att hämta datauppsättningen till [!DNL Power BI].

![](../images/clients/power-bi/preview-table.png)

Tabellen importeras nu till Power BI.

![](../images/clients/power-bi/import-table.png)

## Skapa SQL-satser {#create}

Om du har valt **[!DNL DirectQuery]**-läge måste du fylla i avsnittet Avancerade alternativ med den SQL-fråga som du vill skapa.

Under **[!DNL SQL statement]** infogar du den SQL-fråga som du vill skapa. Kontrollera att kryssrutan **[!DNL Include relationship columns]** är markerad. När du har skrivit frågan väljer du **[!DNL OK]** för att fortsätta.

![](../images/clients/power-bi/direct-query-mode.png)

En förhandsgranskning av frågan visas. Välj **[!DNL Load]** om du vill visa resultatet av frågan.

![](../images/clients/power-bi/preview-direct-query.png)

## Nästa steg

Nu när du är ansluten till [!DNL Query Service] kan du använda [!DNL Power BI] för att skriva frågor. Mer information om hur du skriver och kör frågor finns i guiden [kör frågor](../best-practices/writing-queries.md).