---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Självstudiekurser för datastyrning och sekretess
topic: tutorial
translation-type: tm+mt
source-git-commit: 5c5f6c4868e195aef76bacc0a1e5df3857647bde
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---


# [!DNL Data Governance] och [!DNL Privacy] Tutorials

[!DNL Data Usage Labeling and Enforcement] (DULE) är kärnmekanismen i Adobe Experience Platform [!DNL Data Governanc]e. DULE-funktioner gör att du kan använda dataanvändningsetiketter på datauppsättningar och fält, och kategorisera dem efter relaterade principer för dataanvändning. Innan du börjar med etiketter kan du läsa översikten [över](../data-governance/home.md) datastyrning för en mer robust introduktion till DULE-ramverket i [!DNL Platform].

Adobe Experience Platform [!DNL Privacy Service] har ett RESTful API och användargränssnitt som gör att du kan samordna förfrågningar om sekretess och regelefterlevnad i olika lösningar. Börja med att läsa översikten över [Privacy Servicen](../privacy-service/home.md)om du vill veta mer.

## Lägg till etiketter för dataanvändning

Med etiketter för dataanvändning kan du kategorisera datauppsättningar och fält enligt de användarprofiler som gäller för dessa data. Etiketter kan användas när som helst, vilket ger flexibilitet i hur du väljer att styra data. Bästa tillvägagångssätt uppmuntrar till etikettdata så snart de har importerats till [!DNL Experience Platform]eller så snart data blir tillgängliga för användning i [!DNL Platform]. Dataanvändningsetiketter som används på datauppsättningsnivå sprids till alla fält i datauppsättningen. Etiketter kan också användas direkt på enskilda fält (kolumnrubriker) i en datauppsättning, utan spridning. Mer information om hur du använder dataetiketter finns i översikten över [](../data-governance/labels/overview.md)dataanvändningsetiketter.

## Skapa dataanvändningsprofiler

Med DULE [!DNL Policy Service] API kan du skapa och hantera DULE-principer för att avgöra vilka marknadsföringsåtgärder som kan vidtas mot data som innehåller vissa DULE-etiketter. Du kommer igång genom att läsa översikten över [dataanvändningsprinciper](../data-governance/policies/overview.md).

## Använd principer för dataanvändning

När du har skapat DULE-etiketter (Data Usage Labeling and Enforcement) för dina data och skapat DULE-profiler för marknadsföringsåtgärder mot dessa etiketter, kan du använda DULE [!DNL Policy Service] API för att utvärdera om en marknadsföringsåtgärd som utförts på en datauppsättning, eller en godtycklig grupp med DULE-etiketter, utgör en policyöverträdelse. Du kan sedan konfigurera egna interna protokoll för att hantera policyöverträdelser baserat på API-svaret. Kom igång genom att gå till översikten över [policyefterlevnaden](../data-governance/enforcement/overview.md).

## Använd regelefterlevnad för ett målgruppssegment

Segment som är aktiverade för användning i [!DNL Real-time Customer Profile] innehåller ett ID för sammanfogningsprincip i segmentdefinitionen. Den här sammanfogningsprincipen innehåller information om vilka datauppsättningar som ska inkluderas i segmentet, som i sin tur innehåller tillämpliga dataanvändningsetiketter. Följ självstudiekursen för [regelefterlevnad för segment](../segmentation/tutorials/governance.md)om du vill få en mer detaljerad genomgång av hur dataanvändningen efterlevs för ett målgruppssegment.

## Get started with [!DNL Privacy Service]

[!DNL Privacy Service] har ett RESTful-API och användargränssnitt som gör att du kan hantera personuppgifter för dina registrerade (kunder) i alla Adobe Experience Cloud-program. [!DNL Privacy Service] har också en central mekanism för granskning och loggning som gör att du kan komma åt status och resultat för jobb som innefattar [!DNL Experience Cloud] program. Anvisningar om hur du skapar och övervakar [!DNL Privacy Service] jobb finns i [Privacy Servicens utvecklarguide](../privacy-service/api/getting-started.md) eller i användarhandboken [för](../privacy-service/ui/overview.md)Privacy Servicen.