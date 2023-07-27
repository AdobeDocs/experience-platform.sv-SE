---
title: Klassen XDM Individual Prospect Profile
description: Det här dokumentet innehåller en översikt över klassen XDM Individual Prospect Profile i Experience Data Model (XDM).
badgeBeta: label="Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 83f01c58e21bc42a53e2e7a08bd7a60ef90b41e6
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# [!UICONTROL XDM Individual Prospect Profile] class

>[!IMPORTANT]
>
>The [!UICONTROL XDM Individual Prospect Profile] klassen finns i betaversionen och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

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
| `partnerID` | [!UICONTROL String] | Vanligtvis är det en unik pseudonym identifierare som identifierar en enskild potentiell kund. Läs dokumentationen om [identitetstyper](../../identity-service/namespaces.md#identity-types) om du vill veta mer om partner-ID och andra identitetstyper som finns i Adobe Experience Platform. |
| `repositoryCreatedBy` | [!UICONTROL String] | ID för den användare som skapade posten. |
| `repositoryLastModifiedBy` | [!UICONTROL String] | ID för den användare som senast ändrade posten. När posten skapas `modifiedByUser` värdet anges som `createdByUser` värde. |

{style="table-layout:auto"}
