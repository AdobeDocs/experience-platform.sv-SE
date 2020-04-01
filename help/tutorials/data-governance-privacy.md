---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Självstudiekurser för datastyrning och sekretess
topic: tutorial
translation-type: tm+mt
source-git-commit: ee08f43400fa72abce95ed52aff879f954f4b4d6

---


# Självstudiekurser för datastyrning och sekretess

DULE (Data Usage Labeling and Enforcement) är huvudmekanismen i Adobe Experience Platform Data Governance. DULE-funktioner gör att du kan använda dataanvändningsetiketter på datauppsättningar och fält, och kategorisera dem efter relaterade principer för dataanvändning. Innan du börjar med etiketter bör du läsa översikten över [datastyrning](../data-governance/home.md) för att få en mer robust introduktion till DULE-ramverket inom plattformen.

Adobe Experience Platform Privacy Service tillhandahåller ett RESTful API och användargränssnitt som gör att ni kan samordna förfrågningar om sekretess och regelefterlevnad över olika lösningar. Om du vill veta mer kan du börja med att läsa översikten över [sekretesstjänsten](../privacy-service/home.md).

## Lägg till etiketter för dataanvändning

Med etiketter för dataanvändning kan du kategorisera datauppsättningar och fält enligt de användarprofiler som gäller för dessa data. Etiketter kan användas när som helst, vilket ger flexibilitet i hur du väljer att styra data. Bästa tillvägagångssätt uppmuntrar till märkning av data så snart de hämtas till Experience Platform, eller så snart data blir tillgängliga för användning i Platform. Dataanvändningsetiketter som används på datauppsättningsnivå sprids till alla fält i datauppsättningen. Etiketter kan också användas direkt på enskilda fält (kolumnrubriker) i en datauppsättning, utan spridning. Mer information om hur du använder dataetiketter finns i översikten över [](../data-governance/labels/overview.md)dataanvändningsetiketter.

## Skapa dataanvändningsprofiler

Med DULE Policy Service API kan du skapa och hantera DULE-principer för att avgöra vilka marknadsföringsåtgärder som kan vidtas mot data som innehåller vissa DULE-etiketter. Du kommer igång genom att läsa översikten över [dataanvändningsprinciper](../data-governance/policies/overview.md).

## Använd principer för dataanvändning

När du har skapat DULE-etiketter (Data Usage Labeling and Enforcement) för dina data och skapat DULE-profiler för marknadsföringsåtgärder mot dessa etiketter, kan du använda DULE Policy Service API för att utvärdera om en marknadsföringsåtgärd som utförts på en datauppsättning, eller en godtycklig grupp med DULE-etiketter, utgör en policyöverträdelse. Du kan sedan konfigurera egna interna protokoll för att hantera policyöverträdelser baserat på API-svaret. Kom igång genom att gå till översikten över [policyefterlevnaden](../data-governance/enforcement/overview.md).

## Använd regelefterlevnad för ett målgruppssegment

Segment som har aktiverats för användning i kundprofilen i realtid innehåller ett ID för sammanfogningsprincip i segmentdefinitionen. Den här sammanfogningsprincipen innehåller information om vilka datauppsättningar som ska inkluderas i segmentet, som i sin tur innehåller tillämpliga dataanvändningsetiketter. Följ självstudiekursen för [regelefterlevnad för segment](../segmentation/tutorials/governance.md)om du vill få en mer detaljerad genomgång av hur dataanvändningen efterlevs för ett målgruppssegment.

## Kom igång med Integritetstjänst

Integritetstjänsten tillhandahåller ett RESTful-API och användargränssnitt som gör att du kan hantera personuppgifter för dina registrerade (kunder) i alla Adobe Experience Cloud-program. Integritetstjänsten erbjuder även en central gransknings- och loggningsmekanism som gör att du kan komma åt status och resultat för jobb som innefattar Experience Cloud-program. Instruktioner som visar hur du skapar och övervakar sekretessjobb finns i utvecklarhandboken [för](../privacy-service/api/getting-started.md) sekretesstjänsten eller användarhandboken [för](../privacy-service/ui/overview.md)sekretesstjänsten.