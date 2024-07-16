---
solution: Experience Platform
title: Ignorera uppdatering av begränsning för årstid
description: Lär dig hur du löser ett problem med den ignorerade årstidsbegränsningen.
exl-id: 44bb8817-e32d-4806-ad4e-b1840313e768
source-git-commit: 006950092f69d378b064c795b117166343e5d8f2
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---

# Ignorera uppdatering av tidsbegränsning för år {#ignore-year}

>[!CONTEXTUALHELP]
>id="platform_audiences_segmentBuilder_ignoreYear"
>title="Ignorera årsuppdatering"
>abstract="Årets ignoreringsbegränsning har uppdaterats. Spara era målgrupper på nytt, tack."

>[!IMPORTANT]
>
>Du kan bara använda tidsbegränsningen&quot;ignorera år&quot; i en segmentdefinition som utvärderats med **gruppsegmentering**. Om du lägger till tidsbegränsningen&quot;ignorera år&quot; i din segmentdefinition blir den resulterande målgruppen **oanvändbar** för direktuppspelning eller kantsegmentering.

I februari 2024-utgåvan av Adobe Experience Platform har ändringar gjorts i Adobe Experience Platform Segmentation Service, vilket löser ett problem med alternativet&quot;ignorera år&quot; när det gäller att skapa och utvärdera målgrupper.

Alternativet&quot;ignorera år&quot; är utformat för att ignorera årskomponenten för ett datum när målgruppsutvärderingar utförs. Du kan använda det här alternativet i situationer där tidsförhållandet mellan olika händelser är viktigt men det specifika året är oviktigt, till exempel ett födelsedatumfält.

Under skottår, t.ex. 2024, kunde det underliggande systemet emellertid inte hantera detta alternativ korrekt, vilket resulterade i felaktiga målgruppsutvärderingar. Om&quot;ignorera år&quot; aktiveras under ett skottår skulle därför målgruppsutvärderingen sakna en dag.

Om du skapade en målgrupp innan den här korrigeringen släpptes behöver du bara spara målgruppen på nytt i Segment Builder för att åtgärda problemet. Om du är osäker på om målgruppen påverkas av den här upplösningen kommer Segment Builder att fråga användaren om den befintliga målgruppen påverkas av problemet.
