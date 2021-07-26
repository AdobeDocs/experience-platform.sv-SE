---
solution: Experience Platform
title: ERD för datamodell för finanssektorn
topic-legacy: overview
description: Visa ett enhetsrelationsdiagram (ERD) som beskriver en standardiserad datamodell för banksektorn, finanssektorn och försäkringssektorn (BFSI). Den här datamodellen är kompatibel med Experience Data Model (XDM) för användning i Adobe Experience Platform.
exl-id: 2e8f6b2a-10e7-4394-b45f-c03db0f25400
source-git-commit: 38fa2345cb87e50bd4c8788996f03939fb199cf9
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---

# [!UICONTROL Financial services] ERD för branschdatamodell

Följande företagsrelationsdiagram representerar en standardiserad datamodell för banksektorn, finanssektorn och försäkringssektorn. Den europeiska referensdosen presenteras avsiktligt på ett avnormaliserat sätt och med hänsyn till hur data lagras i Adobe Experience Platform.

>[!NOTE]
>
>Den rekommenderade referensmetoden är en rekommendation för hur du ska modellera dina data för det här användningsexemplet. Om du vill använda den här datamodellen i Platform måste du själv skapa de rekommenderade scheman och deras relationer. Mer information finns i guiderna för att hantera [scheman](../../ui/resources/schemas.md) och [relationer](../../tutorials/relationship-ui.md) i användargränssnittet.

Använd följande förklaring för att tolka denna ERD:

* Varje entitet som visas i är baserad på en underliggande [XDM-klass (Experience Data Model)](../composition.md#class).
* För en given entitet representerar varje rad som är markerad med **fet** en fältgrupp eller en datatyp, med de relevanta fält som anges nedan i oförändrad text.
* De viktigaste fälten för en viss enhet markeras med rött.
* Alla egenskaper som kan användas för att identifiera enskilda kunder markeras som&quot;identitet&quot;, med en av dessa egenskaper markerad som&quot;primär identitet&quot;.
* Enhetsrelationer markeras som icke-beroende eftersom cookie-baserade händelser ofta inte kan avgöra vem eller vilka personer som gjorde transaktionen.

![](../../images/industries/financial.png)

>[!NOTE]
>
>Experience Event-entiteten innehåller ett fält av typen &quot;_ID&quot;, som representerar det unika identifierarattributet (`_id`) som tillhandahålls av klassen XDM ExperienceEvent. Mer information om vad som förväntas för det här värdet finns i referensdokumentet på [XDM ExperienceEvent](../../classes/experienceevent.md).