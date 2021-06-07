---
solution: Experience Platform
title: Datamodell för detaljhandeln - ERD
topic-legacy: overview
description: Visa en datamodell (ERD) som beskriver en standardiserad datamodell för detaljhandeln som är kompatibel med Experience Data Model (XDM) för användning i Adobe Experience Platform.
exl-id: 40cbb243-668b-4280-815f-1f94a06b6b87
source-git-commit: 629f47b934c59fe875a54cb13962033122097538
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# [!UICONTROL Retail] ERD för branschdatamodell

Följande enhetsrelationsdiagram representerar en standardiserad datamodell för detaljhandeln. Den europeiska referensdosen presenteras avsiktligt på ett avnormaliserat sätt och med hänsyn till hur data lagras i Adobe Experience Platform.

Använd följande förklaring för att tolka denna ERD:

* Varje entitet som visas i är baserad på en underliggande [XDM-klass (Experience Data Model)](../composition.md#class).
* För en given entitet representerar varje rad som är markerad med **fet** en fältgrupp eller en datatyp, med de relevanta fält som anges nedan i oförändrad text.
* De viktigaste fälten för en viss enhet markeras med rött.
* Alla egenskaper som kan användas för att identifiera enskilda kunder markeras som&quot;identitet&quot;, med en av dessa egenskaper markerad som&quot;primär identitet&quot;.
* Enhetsrelationer markeras som icke-beroende eftersom cookie-baserade händelser ofta inte kan avgöra vem eller vilka personer som gjorde transaktionen.

![](../../images/industries/retail.png)

>[!NOTE]
>
>Experience Event-entiteten innehåller ett fält av typen &quot;_ID&quot;, som representerar det unika identifierarattributet (`_id`) som tillhandahålls av klassen XDM ExperienceEvent. Mer information om vad som förväntas för det här värdet finns i referensdokumentet på [XDM ExperienceEvent](../../classes/experienceevent.md).