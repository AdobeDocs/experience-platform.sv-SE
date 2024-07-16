---
solution: Experience Platform
title: Segmentdefinitionsklass
description: Läs mer om segmentdefinitionsklassen i Experience Data Model (XDM).
exl-id: c0f7b04c-2266-4d08-89a1-67ba758a51a7
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# klassen [!UICONTROL Segment definition]

[!UICONTROL Segment definition] är en XDM-klass (Experience Data Model) som används som standard och som hämtar information om en segmentdefinition. Klassen innehåller obligatoriska fält, t.ex. ID:t och namnet på en målgrupp, tillsammans med andra valfria attribut. Den här klassen bör användas om du infogar segmentdefinitioner från externa system i Adobe Experience Platform.

>[!NOTE]
>
>Den här klassen ska bara användas för att samla in information om själva segmentdefinitionerna. Om du vill samla in information om målgruppsmedlemskap i dina profildata bör du använda fältgruppen [Information om segmentmedlemskap](../field-groups/profile/segmentation.md) i ditt [!UICONTROL XDM Individual Profile]-schema.

![](../images/classes/segment-definition.png)

| Egenskap | Beskrivning |
| --- | --- |
| `_repo` | Ett objekt som innehåller följande [!UICONTROL DateTime] fält: <ul><li>`createDate`: Det datum och den tidpunkt då resursen skapades i datalagret, till exempel när data först importerades.</li><li>`modifyDate`: Datum och tid då resursen senast ändrades.</li></ul> |
| `_id` | En unik systemgenererad strängidentifierare för posten. Det här fältet används för att spåra en enskild posts unika karaktär, förhindra dubblering av data och för att söka efter posten i underordnade tjänster.<br><br>Eftersom det här fältet är systemgenererat anges inget explicit värde vid datainmatning. Du kan dock välja att ange egna unika ID-värden om du vill.<br><br>Det är viktigt att skilja på att det här fältet **inte** representerar en identitet som relateras till en enskild person, utan själva dataposten. Identitetsdata som relaterar till en person ska i stället begränsas till [identitetsfält](../schema/composition.md#identity). |
| `createdByBatchID` | ID:t för den inkapslade batchen som gjorde att posten skapades. |
| `description` | En beskrivning av segmentdefinitionen. |
| `identityMap` | Ett kartfält som innehåller en uppsättning namngivna identiteter för de personer som målgruppen gäller för. Mer information om hur de används finns i avsnittet om identitetskartor i [grunderna för schemakomposition](../schema/composition.md#identityMap). |
| `modifiedByBatchID` | ID:t för den senaste inkapslade batchen som gjorde att posten uppdaterades. |
| `repositoryCreatedBy` | ID för den användare som skapade posten. |
| `repositoryLastModifiedBy` | ID för den användare som senast ändrade posten. |
| `segmentName` | **(Obligatoriskt)** Ett namn för segmentdefinitionen. |
| `segmentStatus` | Status för målgruppen från det externa systemet. Följande värden accepteras: <ul><li>`ACTIVE`</li><li>`INACTIVE`</li><li>`DELETED`</li><li>`DRAFT`</li><li>`REVOKED`</li></ul> |
| `version` | Det senaste versionsnumret för segmentdefinitionen. |

{style="table-layout:auto"}
