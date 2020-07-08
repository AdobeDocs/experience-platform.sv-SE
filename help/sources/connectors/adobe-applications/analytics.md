---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Analytics dataanslutning
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 2%

---


# Analytics Data Connector

Med Adobe Experience Platform kan du importera Adobe Analytics-data via Analytics Data Connector (ADC). ADC strömmar data som samlats in av Adobe Analytics till Platform i realtid och konverterar SCDS-formaterade Analytics-data till XDM-fält (Experience Data Model) för användning i Platform.

I det här dokumentet finns en översikt över Adobe Analytics och en beskrivning av användningsfall för Analytics-data.

## Adobe Analytics- och Analytics-data

Adobe Analytics är en kraftfull motor som hjälper er att lära er mer om era kunder, hur de interagerar med era webbegenskaper, se var era utgifter för digital marknadsföring är effektiva och identifiera områden där det finns förbättringar. Adobe Analytics hanterar miljontals webbtransaktioner per år och med ADC kan ni enkelt utnyttja dessa omfattande beteendedata och berika kundprofilen i realtid på bara några minuter.

![](./images/analytics-data-experience-platform.png)

På en hög nivå samlar Adobe Analytics in data från olika digitala kanaler och datacenter världen över. När data har samlats in tillämpas VISTA-regler (Visitor Identification, Segmentation and Transformation Architecture) och bearbetningsregler för att forma inkommande data. När rådata har genomgått den här enkla bearbetningen anses de sedan vara klara att användas av kundprofilen i realtid. I en process som är parallell med ovanstående är samma bearbetade data mikrobatchade och insamlade i Platform datamängder för konsumtion av Data Science Workspace, Query Service och andra dataidentifieringsprogram.

Mer information om bearbetningsregler finns i Översikt över [](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/processing-rules/processing-rules.html) Bearbetningsregler.

## Experience Data Model (XDM)

XDM är en offentligt dokumenterad specifikation som innehåller gemensamma strukturer och definitioner för en tillämpning som ska användas för att kommunicera med tjänster på Adobe Experience Platform.

Genom att följa XDM-standarder kan data integreras på ett enhetligt sätt, vilket gör det enklare att leverera data och samla in information.

Mer information om XDM finns i [XDM-systemöversikten](../../../xdm/home.md).

## Hur mappas fält från Adobe Analytics till XDM?

När en källanslutning upprättas för att överföra Analytics-data till Experience Platform med Platform användargränssnitt mappas datafälten automatiskt och hämtas in i kundprofilen i realtid inom några minuter. Instruktioner om hur du skapar en källanslutning med Adobe Analytics med Platform-gränssnittet finns i [Analytics självstudiekurs](../../tutorials/ui/create/adobe-applications/analytics.md)för dataanslutning.

Mer information om fältmappning mellan Analytics och Experience Platform finns i [Adobe Analytics](./mapping/analytics.md) guide.

## Vilken fördröjning förväntas för Analytics Data på Platform?

| Analytics Data | Förväntad svarstid |
| -------------- | ---------------- |
| Nya data i kundprofilen i realtid (A4T **är inte** aktiverat) | &lt; 2 minuter |
| Nya data i kundprofilen i realtid (A4T **är** aktiverat) | &lt; 15 minuter |
| Nya data till Data Lake | &lt; 45 minuter |
| Fyll i data i bakgrunden (13 månaders data eller 10 miljarder händelser, beroende på vilket som är lägst) | &lt; 4 veckor |

>[!NOTE]
>
>Svarstiden varierar beroende på kundens konfiguration, datavolymer och konsumentprogram. Om till exempel Analytics-implementeringen är konfigurerad med fördröjning `A4T` till pipeline kommer den att öka till 5-10 minuter.