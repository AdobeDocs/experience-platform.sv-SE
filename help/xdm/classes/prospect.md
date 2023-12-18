---
title: Klassen XDM Individual Prospect Profile
description: Läs mer om klassen XDM Individual Prospect Profile i Experience Data Model (XDM).
exl-id: 10fd9d16-4123-4ad4-971f-b715231ee6a9
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# [!UICONTROL XDM Individual Prospect Profile] class

I Experience Data Model (XDM) är [!UICONTROL XDM Individual Prospect Profile] klassen samlar in profiler för potentiella kunder som vanligen kommer från datapartners för att kunna användas vid kundvärvning.

![Schemagrafiken för klassen XDM Prospect.](../images/classes/individual-prospect-profile.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `_repo` | Objekt | Med den här klassen kan ni infoga profiler för potentiella kunder som har hämtats från dataleverantörer för att hantera kundvärvningsfall. |
| `_repo.createDate` | [!UICONTROL DateTime] | Serverdatum och -tid när resursen skapades i databasen. Skapandetiden kan vara när en resursfil först överförs eller när en katalog skapas av servern som överordnad till en ny resurs. Egenskapen datetime ska följa ISO 8601-standarden. Ett exempel på det här formatet är &quot;2004-10-23T12:00:00-06:00&quot;. |
| `_repo.modifyDate` | [!UICONTROL DateTime] | Serverdatum och -tid när resursen senast ändrades i databasen, till exempel när en ny version av en resurs överförs eller en katalogs underordnade resurs läggs till eller tas bort. Egenskapen datetime ska följa ISO 8601-standarden. Ett exempelformulär är &quot;2004-10-23T12:00:00-06:00&quot;. |
| `_id` | [!UICONTROL String] | En unik systemgenererad strängidentifierare för posten. Det här fältet används för att spåra en enskild posts unika karaktär, förhindra dubblering av data och för att söka efter posten i underordnade tjänster.<br><br>Eftersom det här fältet genereras av systemet, ger det inget explicit värde vid datainmatning. Du kan dock välja att ange egna unika ID-värden om du vill. |
| `createdByBatchID` | [!UICONTROL String] | ID:t för den inkapslade batchen som gjorde att posten skapades. |
| `modifiedByBatchID` | [!UICONTROL String] | ID:t för den senaste inkapslade batchen som gjorde att posten uppdaterades. |
| `partnerID` | [!UICONTROL String] | Vanligtvis är det en unik pseudonym identifierare som identifierar en enskild potentiell kund. Läs dokumentationen om [identitetstyper](../../identity-service/namespaces.md#identity-type) om du vill veta mer om partner-ID och andra identitetstyper som finns i Adobe Experience Platform. |
| `repositoryCreatedBy` | [!UICONTROL String] | ID för den användare som skapade posten. |
| `repositoryLastModifiedBy` | [!UICONTROL String] | ID för den användare som senast ändrade posten. När posten skapas `modifiedByUser` värdet anges som `createdByUser` värde. |

{style="table-layout:auto"}
