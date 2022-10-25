---
keywords: Experience Platform;hemmabruk;populära ämnen;
title: (Beta) Adobe Workfront Source
description: Adobe Workfront är en arbetsstyrningsapplikation för marknadsföring som hjälper er att hantera hela arbetscykeln på ett och samma ställe. Workfront innehåller rapporterings- och analysverktyg som ni kan använda för att bättre förstå och optimera arbetsflödet i organisationen.
source-git-commit: 1af0863766e29c599e02f2a553d237bc62f455d2
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# (Beta) Adobe Workfront-källa

>[!NOTE]
>
>Adobe Workfront-källan är i betaversion. Se [Översikt över källor](../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder beta-märkta anslutningar.

Adobe Workfront är en arbetsstyrningsapplikation för marknadsföring som hjälper er att hantera hela arbetscykeln på ett och samma ställe. Workfront innehåller rapporterings- och analysverktyg som ni kan använda för att bättre förstå och optimera arbetsflödet i organisationen.

Tack vare Workfront-integreringen med Adobe Experience Platform källkatalog kan du överföra dina Workfront-data till Experience Platform och använda följande exempel:

* Kombinera arbetsposter med data från tredje part.
* Använd historik- och tidsserieanalyser på arbetsregister.
* Få åtkomst till arbetsregister via verktyg från andra leverantörer som [!DNL PowerBI].
* Fråga arbetsdata med standard-SQL.

Följande arbetsposter och deras motsvarande attribut kan tas med i Experience Platform via Workfront-källan:

* Portfolio
* Program
* Projekt
* Uppgift
* Verksamhetsuppgift (problem)
* Användare

Workfront-källan strömmar alla nya uppdateringar av dessa attribut och säkerhetskopierar upp till ett års historiska ändringshändelser. När era Workfront-data finns i en plattformsdatauppsättning kan ni använda [Frågetjänst](../../../query-service/home.md) och andra verktyg för att ytterligare analysera eller förena dina arbetsrelaterade data med andra datauppsättningar efter behov.

## Ansluta Workfront till plattformen med användargränssnittet

Detaljerade anvisningar om hur du får med dina Workfront-data till Platform finns i handboken [skapa en källanslutning för att överföra dina Workfront-data till plattformen](../../tutorials/ui/create/adobe-applications/workfront.md).