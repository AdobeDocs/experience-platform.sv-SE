---
keywords: Experience Platform;home;popular topics;Analytics Data Connector;analytics;Analytics
solution: Experience Platform
title: Dataanslutning för Analytics
topic: overview
description: Det här dokumentet innehåller en översikt över Analytics och en beskrivning av användningsfall för Analytics-data.
translation-type: tm+mt
source-git-commit: 6934bfeee84f542558894bbd4ba5759891cd17f3
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 2%

---


# Analytics Data Connector

Med Adobe Experience Platform kan ni importera Adobe Analytics-data via Analytics Data Connector (ADC). ADC strömmar data som samlats in av [!DNL Analytics] till [!DNL Platform] i realtid och konverterar SCDS-formaterade [!DNL Analytics] data till [!DNL Experience Data Model] XDM-fält som kan användas av [!DNL Platform].

Det här dokumentet innehåller en översikt över [!DNL Analytics] och en beskrivning av användningsfall för [!DNL Analytics] data.

## Adobe Analytics- och Analytics-data

[!DNL Analytics] är en kraftfull motor som hjälper er att lära er mer om era kunder, hur de interagerar med era webbegenskaper, se var era utgifter för digital marknadsföring är effektiva och identifiera områden där det finns förbättringar. [!DNL Analytics] hanterar miljontals webbtransaktioner per år och med ADC kan ni enkelt utnyttja dessa omfattande beteendedata och berika dem [!DNL Real-time Customer Profile] på några minuter.

![](./images/analytics-data-experience-platform.png)

På en hög nivå samlas data in från olika digitala kanaler och från flera datacenter runt om i världen. [!DNL Analytics] När data har samlats in tillämpas VISTA-regler (Visitor Identification, Segmentation and Transformation Architecture) och bearbetningsregler för att forma inkommande data. När rådata har genomgått denna enkla bearbetning anses de vara klara att användas senast [!DNL Real-time Customer Profile]. I en process som är parallell med ovanstående är samma bearbetade data mikrobatchade och insamlade i plattformsdatauppsättningar för konsumtion av [!DNL Data Science Workspace], [!DNL Query Service]och andra dataidentifieringsprogram.

Mer information om bearbetningsregler finns i Översikt över [](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/processing-rules/processing-rules.html) Bearbetningsregler.

## Experience Data Model (XDM)

XDM är en öppet dokumenterad specifikation som innehåller gemensamma strukturer och definitioner för en tillämpning som ska användas för att kommunicera med tjänster i [!DNL Experience Platform].

Genom att följa XDM-standarder kan data integreras på ett enhetligt sätt, vilket gör det enklare att leverera data och samla in information.

Mer information om XDM finns i [XDM-systemöversikten](../../../xdm/home.md).

## Hur mappas fält från Adobe Analytics till XDM?

När en källanslutning upprättas för att hämta [!DNL Analytics] data till [!DNL Experience Platform] med [!DNL Platform] användargränssnittet mappas datafälten automatiskt och hämtas till [!DNL Real-time Customer Profile] inom några minuter. Instruktioner om hur du skapar en källanslutning med [!DNL Analytics] hjälp av [!DNL Platform] gränssnittet finns i självstudiekursen [för dataanslutning i Analytics](../../tutorials/ui/create/adobe-applications/analytics.md).

Detaljerad information om fältmappningen mellan [!DNL Analytics] och [!DNL Experience Platform]finns i [Adobe Analytics guide för fältmappning](./mapping/analytics.md) .

## Vilken fördröjning förväntas för Analytics Data on Platform?

| Analysdata | Förväntad svarstid |
| -------------- | ---------------- |
| Nya data till [!DNL Real-time Customer Profile] (A4T **är inte** aktiverat) | &lt; 2 minuter |
| Nya data till [!DNL Real-time Customer Profile] (A4T **är** aktiverat) | &lt; 15 minuter |
| Nya data till Data Lake | &lt; 45 minuter |
| Fyll i data i bakgrunden (13 månaders data eller 10 miljarder händelser, beroende på vilket som är lägst) | &lt; 4 veckor |

>[!NOTE]
>
>Svarstiden varierar beroende på kundens konfiguration, datavolymer och konsumentprogram. Om till exempel Analytics-implementeringen har konfigurerats med fördröjning `A4T` till pipeline kommer den att öka till 5-10 minuter.

## Primära identifierare i analysdata

Varje träff från datakopplingen för Analytics innehåller en primär identifierare som är beroende av om det finns ett ECID eller ett AAID. Om det finns ett ECID-id anges ECID som primär identifierare. Om det finns ett AAID-id anges AAID som primär.