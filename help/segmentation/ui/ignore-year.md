---
solution: Experience Platform
title: Ignorera uppdatering av begränsning för årstid
description: Lär dig hur du löser ett problem med den ignorerade årstidsbegränsningen.
source-git-commit: d0bd7990f0d77cd5f8d30da735b89c188e13c780
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# Ignorera uppdatering av tidsbegränsning för år {#ignore-year}

>[!CONTEXTUALHELP]
>id="platform_audiences_segmentBuilder_ignoreYear"
>title="Ignorera årsuppdatering"
>abstract="Årets ignoreringsbegränsning har uppdaterats. Spara era målgrupper på nytt, tack."

I februari 2024-utgåvan av Adobe Experience Platform har ändringar gjorts i Adobe Experience Platform Segmentation Service, vilket löser ett problem med alternativet&quot;ignorera år&quot; när det gäller att skapa och utvärdera målgrupper.

Alternativet&quot;ignorera år&quot; är utformat för att ignorera årskomponenten för ett datum när målgruppsutvärderingar utförs. Du kan använda det här alternativet i situationer där tidsförhållandet mellan olika händelser är viktigt men det specifika året är oviktigt, till exempel ett födelsedatumfält.

Under skottår, t.ex. 2024, kunde det underliggande systemet emellertid inte hantera detta alternativ korrekt, vilket resulterade i felaktiga målgruppsutvärderingar. Om&quot;ignorera år&quot; aktiveras under ett skottår skulle därför målgruppsutvärderingen sakna en dag.

Om du skapade en målgrupp innan den här korrigeringen släpptes behöver du bara spara målgruppen på nytt i Segment Builder för att åtgärda problemet. Om du är osäker på om målgruppen påverkas av den här upplösningen kommer Segment Builder att fråga användaren om den befintliga målgruppen påverkas av problemet.
