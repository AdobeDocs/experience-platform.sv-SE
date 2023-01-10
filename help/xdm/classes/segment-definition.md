---
solution: Experience Platform
title: Segmentdefinitionsklass
description: Det här dokumentet innehåller en översikt över segmentdefinitionsklassen i XDM (Experience Data Model).
exl-id: c0f7b04c-2266-4d08-89a1-67ba758a51a7
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# [!UICONTROL Segment definition] class

&quot;[!UICONTROL Segment definition]&quot; är en XDM-klass (Experience Data Model) som hämtar information om en segmentdefinition. Klassen innehåller obligatoriska fält som ID och namn för ett segment, tillsammans med andra valfria attribut. Den här klassen bör användas om du infogar segmentdefinitioner från externa system i Adobe Experience Platform.

>[!NOTE]
>
>Den här klassen ska bara användas för att samla in information om själva segmentdefinitionerna. Om du vill samla in information om ett segmentmedlemskap i dina profildata använder du [Fältgrupp för information om segmentmedlemskap](../field-groups/profile/segmentation.md) i [!UICONTROL XDM Individual Profile] schema.

![](../images/classes/segment-definition.png)

| Egenskap | Beskrivning |
| --- | --- |
| `_repo` | Ett objekt som innehåller följande [!UICONTROL DateTime] fält: <ul><li>`createDate`: Datum och tid då resursen skapades i datalagret, till exempel när data först importerades.</li><li>`modifyDate`: Datum och tid då resursen senast ändrades.</li></ul> |
| `_id` | En unik systemgenererad strängidentifierare för posten. Det här fältet används för att spåra en enskild posts unika karaktär, förhindra dubblering av data och för att söka efter posten i underordnade tjänster.<br><br>Eftersom det här fältet genereras av systemet, anges inget explicit värde vid datainmatning. Du kan dock välja att ange egna unika ID-värden om du vill.<br><br>Det är viktigt att särskilja att detta fält **inte** representerar en identitet som är relaterad till en enskild person, i stället för själva registreringen av uppgifter. Identitetsuppgifter som rör en person bör begränsas till [identitetsfält](../schema/composition.md#identity) i stället. |
| `createdByBatchID` | ID:t för den inkapslade batchen som gjorde att posten skapades. |
| `description` | En beskrivning av segmentdefinitionen. |
| `identityMap` | Ett kartfält som innehåller en uppsättning namngivna identiteter för de personer som segmentet gäller för. Se avsnittet om identitetskartor i [grunderna för schemakomposition](../schema/composition.md#identityMap) om du vill ha mer information om deras användningsfall. |
| `modifiedByBatchID` | ID:t för den senaste inkapslade batchen som gjorde att posten uppdaterades. |
| `repositoryCreatedBy` | ID för den användare som skapade posten. |
| `repositoryLastModifiedBy` | ID för den användare som senast ändrade posten. |
| `segmentName` | **(Obligatoriskt)** Ett namn för segmentdefinitionen. |
| `segmentStatus` | Status för segmentet från det externa systemet. Följande värden accepteras: <ul><li>`ACTIVE`</li><li>`INACTIVE`</li><li>`DELETED`</li><li>`DRAFT`</li><li>`REVOKED`</li></ul> |
| `version` | Det senaste versionsnumret för segmentdefinitionen. |

{style=&quot;table-layout:auto&quot;}
