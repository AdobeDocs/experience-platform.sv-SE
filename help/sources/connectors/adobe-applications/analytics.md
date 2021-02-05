---
keywords: Experience Platform;hem;populära ämnen;Analytics Data Connector;analytics;Analytics
solution: Experience Platform
title: Adobe Analytics Source Connector for Report-Suite Data
topic: overview
description: Det här dokumentet innehåller en översikt över Analytics och en beskrivning av användningsfall för Analytics-data.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 1%

---


# Adobe Analytics Connector for report-suite data

Med Adobe Experience Platform kan ni importera Adobe Analytics-data via Analytics Data Connector (ADC). ADC strömmar data som samlats in av [!DNL Analytics] till [!DNL Platform] i realtid och konverterar SCDS-formaterade [!DNL Analytics]-data till [!DNL Experience Data Model]-fält (XDM) för konsumtion av [!DNL Platform].

Det här dokumentet ger en översikt över [!DNL Analytics] och beskriver användningsfall för [!DNL Analytics]-data.

## Adobe Analytics- och Analytics-data

[!DNL Analytics] är en kraftfull motor som hjälper er att lära er mer om era kunder, hur de interagerar med era webbegenskaper, se var era utgifter för digital marknadsföring är effektiva och identifiera områden där det finns förbättringar. [!DNL Analytics] hanterar miljontals webbtransaktioner per år och med ADC kan ni enkelt utnyttja dessa omfattande beteendedata och berika dem  [!DNL Real-time Customer Profile] på några minuter.

![](./images/analytics-data-experience-platform.png)

På en hög nivå samlar [!DNL Analytics] in data från olika digitala kanaler och från flera datacenter runt om i världen. När data har samlats in tillämpas VISTA-regler (Visitor Identification, Segmentation and Transformation Architecture) och bearbetningsregler för att forma inkommande data. När rådata har genomgått den här enkla bearbetningen anses de vara klara att användas senast [!DNL Real-time Customer Profile]. I en process som är parallell med ovanstående är samma bearbetade data mikrobatchade och insamlade i plattformsdatauppsättningar för konsumtion av [!DNL Data Science Workspace], [!DNL Query Service] och andra program för dataidentifiering.

Mer information om bearbetningsregler finns i [Översikt över bearbetningsregler](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/processing-rules/processing-rules.html).

## Experience Data Model (XDM)

XDM är en öppet dokumenterad specifikation som innehåller gemensamma strukturer och definitioner för ett program som ska användas för att kommunicera med tjänster på [!DNL Experience Platform].

Genom att följa XDM-standarder kan data integreras på ett enhetligt sätt, vilket gör det enklare att leverera data och samla in information.

Mer information om XDM finns i [XDM-systemöversikt](../../../xdm/home.md).

## Hur mappas fält från Adobe Analytics till XDM?

När en källanslutning upprättas för att överföra [!DNL Analytics]-data till [!DNL Experience Platform] med [!DNL Platform]-användargränssnittet mappas datafälten automatiskt och hämtas till [!DNL Real-time Customer Profile] på några minuter. Instruktioner om hur du skapar en källanslutning med [!DNL Analytics] med hjälp av användargränssnittet i [!DNL Platform] finns i självstudiekursen [Analytics data connector](../../tutorials/ui/create/adobe-applications/analytics.md).

Mer information om fältmappning mellan [!DNL Analytics] och [!DNL Experience Platform] finns i handboken [Adobe Analytics field mapping](./mapping/analytics.md).

## Vilken fördröjning förväntas för Analytics Data on Platform?

| Analysdata | Förväntad svarstid |
| -------------- | ---------------- |
| Nya data till [!DNL Real-time Customer Profile] (A4T **är inte** aktiverat) | &lt; 2=&quot;&quot; minutes=&quot;&quot;> |
| Nya data till [!DNL Real-time Customer Profile] (A4T **är** aktiverat) | &lt; 15=&quot;&quot; minutes=&quot;&quot;> |
| Nya data till Data Lake | &lt; 45=&quot;&quot; minutes=&quot;&quot;> |
| Fyll i data i bakgrunden (13 månaders data eller 10 miljarder händelser, beroende på vilket som är lägst) | &lt; 4=&quot;&quot; weeks=&quot;&quot;> |

>[!NOTE]
>
>Svarstiden varierar beroende på kundens konfiguration, datavolymer och konsumentprogram. Om till exempel Analytics-implementeringen är konfigurerad med `A4T` kommer fördröjningen till Pipeline att öka till 5-10 minuter.

## Primära identifierare i analysdata

Varje träff från datakopplingen för Analytics innehåller en primär identifierare som är beroende av om det finns ett ECID eller ett AAID. Om det finns ett ECID-id anges ECID som primär identifierare. Om det finns ett AAID-id anges AAID som primär.