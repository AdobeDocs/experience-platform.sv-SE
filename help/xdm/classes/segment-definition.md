---
solution: Experience Platform
title: Segmentdefinitionsklass
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över segmentdefinitionsklassen i XDM (Experience Data Model).
exl-id: c0f7b04c-2266-4d08-89a1-67ba758a51a7
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 0%

---

# [!UICONTROL Segment definition] class

&quot;[!UICONTROL Segment definition]&quot; är en XDM-klass (Standard Experience Data Model) som hämtar information om en segmentdefinition. Klassen innehåller obligatoriska fält som ID och namn för ett segment, tillsammans med andra valfria attribut. Den här klassen bör användas om du infogar segmentdefinitioner från externa system i Adobe Experience Platform.

>[!NOTE]
>
>Den här klassen ska bara användas för att samla in information om själva segmentdefinitionerna. För att kunna samla in information om segmentmedlemskap i dina profildata bör du använda fältgruppen [Information om segmentmedlemskap](../field-groups/profile/segmentation.md) i ditt [!UICONTROL XDM Individual Profile]-schema.

![](../images/classes/segment-definition.png)

| Egenskap | Beskrivning |
| --- | --- |
| `_repo` | Ett objekt som innehåller följande [!UICONTROL DateTime]-fält: <ul><li>`createDate`: Datum och tid då resursen skapades i datalagret, till exempel när data först importerades.</li><li>`modifyDate`: Datum och tid då resursen senast ändrades.</li></ul> |
| `_id` | En unik systemgenererad strängidentifierare för posten. Det här fältet används för att spåra en enskild posts unika karaktär, förhindra dubblering av data och för att söka efter posten i underordnade tjänster.<br><br>Eftersom det här fältet genereras av systemet, anges inget explicit värde vid datainmatning. Du kan dock välja att ange egna unika ID-värden om du vill.<br><br>Det är viktigt att särskilja att detta fält inte  **ger** en identitet som är relaterad till en enskild person, utan snarare själva registreringen av uppgifter. Identitetsdata som relaterar till en person ska i stället begränsas till [identitetsfält](../schema/composition.md#identity). |
| `createdByBatchID` | ID:t för den inkapslade batchen som gjorde att posten skapades. |
| `description` | En beskrivning av segmentdefinitionen. |
| `identityMap` | Ett kartfält som innehåller en uppsättning namngivna identiteter för de personer som segmentet gäller för. Det här fältet uppdateras automatiskt av systemet när identitetsdata hämtas.<br /><br />Mer information om hur de används finns i avsnittet om identitetskartor i  [grunderna för ](../schema/composition.md#identityMap) schemakompositioner. |
| `modifiedByBatchID` | ID:t för den senaste inkapslade batchen som gjorde att posten uppdaterades. |
| `repositoryCreatedBy` | ID för den användare som skapade posten. |
| `repositoryLastModifiedBy` | ID för den användare som senast ändrade posten. |
| `segmentName` | **(Obligatoriskt)** Ett namn för segmentdefinitionen. |
| `segmentStatus` | Status för segmentet från det externa systemet. Följande värden accepteras: <ul><li>`ACTIVE`</li><li>`INACTIVE`</li><li>`DELETED`</li><li>`DRAFT`</li><li>`REVOKED`</li></ul> |
| `version` | Det senaste versionsnumret för segmentdefinitionen. |
