---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Självstudiekurser för datastyrning och sekretess
topic: tutorial
type: Tutorial
description: Det här dokumentet innehåller en översikt över de olika tillgängliga självstudiekurserna för Adobe Experience Platform Data Governance och Adobe Experience Platform Privacy Service.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---


# [!DNL Data Governance] och [!DNL Privacy] Tutorials

Med Adobe Experience Platform Data Governance kan du använda etiketter för dataanvändning på datauppsättningar och fält, kategorisera varje dataanvändning enligt relaterade policyer för dataanvändning och utvärdera om det finns policyöverträdelser när vissa åtgärder utförs på dessa datauppsättningar och/eller fält. Innan du börjar använda de självstudiekurser som listas i det här dokumentet, se [[!DNL Data Governance] översikten](../data-governance/home.md) för en mer robust introduktion till ramverket.

Adobe Experience Platform [!DNL Privacy Service] tillhandahåller ett RESTful API och användargränssnitt som gör att ni kan samordna förfrågningar om sekretess och regelefterlevnad i olika lösningar. Börja med att läsa översikten över [Privacy Servicen](../privacy-service/home.md)om du vill veta mer.

## Lägg till etiketter för dataanvändning

Med etiketter för dataanvändning kan du kategorisera datauppsättningar och fält enligt de användarprofiler som gäller för dessa data. Etiketter kan användas när som helst, vilket ger flexibilitet i hur du väljer att styra data. Bästa tillvägagångssätt uppmuntrar till etikettdata så snart de har importerats till [!DNL Experience Platform]eller så snart data blir tillgängliga för användning i [!DNL Platform]. Dataanvändningsetiketter som används på datauppsättningsnivå sprids till alla fält i datauppsättningen. Etiketter kan också användas direkt på enskilda fält (kolumnrubriker) i en datauppsättning, utan spridning. Mer information om hur du använder dataetiketter finns i översikten över [](../data-governance/labels/overview.md)dataanvändningsetiketter.

## Skapa dataanvändningsprofiler

Med [!DNL Policy Service] API kan ni skapa och hantera dataanvändningspolicyer för att avgöra vilka marknadsföringsåtgärder som kan vidtas mot data som innehåller vissa användningsetiketter. Du kommer igång genom att läsa översikten över [dataanvändningsprinciper](../data-governance/policies/overview.md).

## Använd principer för dataanvändning

När du har lagt till användningsetiketter för dina data, och har skapat policyer för marknadsföringsåtgärder mot dessa etiketter, kan du använda funktionen för [!DNL Policy Service API] att utvärdera om en marknadsföringsåtgärd utgör en policyöverträdelse när den utförs på en datauppsättning eller en godtycklig grupp med användningsetiketter. Du kan sedan konfigurera egna interna protokoll för att hantera policyöverträdelser baserat på API-svaret. Kom igång genom att gå till [översikt](../data-governance/enforcement/overview.md)över policyefterlevnaden.

## Använd regelefterlevnad för ett målgruppssegment

Segment som är aktiverade för användning i [!DNL Real-time Customer Profile] innehåller ett ID för sammanfogningsprincip i segmentdefinitionen. Den här sammanfogningsprincipen innehåller information om vilka datauppsättningar som ska inkluderas i segmentet, som i sin tur innehåller tillämpliga dataanvändningsetiketter. Följ självstudiekursen för [regelefterlevnad för segment](../segmentation/tutorials/governance.md)om du vill få en mer detaljerad genomgång av hur dataanvändningen efterlevs för ett målgruppssegment.

## Kom igång med [!DNL Privacy Service]

[!DNL Privacy Service] har ett RESTful-API och användargränssnitt som gör att du kan hantera personuppgifter för dina registrerade (kunder) i alla Adobe Experience Cloud-program. [!DNL Privacy Service] har också en central mekanism för granskning och loggning som gör att du kan komma åt status och resultat för jobb som innefattar [!DNL Experience Cloud] program. Anvisningar om hur du skapar och övervakar [!DNL Privacy Service] jobb finns i [Privacy Servicens utvecklarguide](../privacy-service/api/getting-started.md) eller i användarhandboken [för](../privacy-service/ui/overview.md)Privacy Servicen.