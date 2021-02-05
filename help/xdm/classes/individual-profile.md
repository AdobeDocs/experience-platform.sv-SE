---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;individuell profil;fält;scheman;scheman;identityMap;identity map;identity map;Schema design;map;union schema;union schema
solution: Experience Platform
title: XDM-klass för enskild profil
topic: overview
description: Det här dokumentet innehåller en översikt över klassen XDM Individual Profile.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 0%

---


# [!DNL XDM Individual Profile] class

[!DNL XDM Individual Profile] är en XDM-standardklass som bildar en enda representation (eller&quot;profil&quot;) av både identifierade och delvis identifierade individers attribut och intressen.

Profilerna kan omfatta allt från anonyma beteendesignaler (t.ex. cookies i webbläsare) till välidentifierade profiler med detaljerad information som namn, födelsedatum, plats och e-postadress. När en profil växer blir den ett robust arkiv med personuppgifter, identiteter, kontaktuppgifter och kommunikationsinställningar för en individ. Mer högnivåinformation om användning av den här klassen i plattformens ekosystem finns i [XDM-översikten](../home.md#data-behaviors).

Själva [!DNL XDM Individual Profile]-klassen innehåller flera systemgenererade värden som fylls i automatiskt när data hämtas, medan alla andra fält måste läggas till med [kompatibla blandningar](#mixins):

![](../images/classes/individual-profile.png)

| Egenskap | Beskrivning |
| --- | --- |
| `_repo` | Ett objekt som innehåller följande [!UICONTROL DateTime]-fält: <ul><li>`createDate`: Datum och tid då resursen skapades i datalagret, till exempel när data först importerades.</li><li>`modifyDate`: Datum och tid då resursen senast ändrades.</li></ul> |
| `_id` | En unik systemgenererad strängidentifierare för posten. Det här fältet används för att spåra en enskild posts unika karaktär, förhindra dubblering av data och för att söka efter posten i underordnade tjänster. Eftersom det här fältet genereras av systemet bör det inte anges som ett explicit värde vid datainmatning.<br><br>Det är viktigt att särskilja att detta fält inte  **ger** en identitet som är relaterad till en enskild person, utan snarare själva registreringen av uppgifter. Identitetsdata som relaterar till en person ska i stället begränsas till [identitetsfält](../schema/composition.md#identity). |
| `createdByBatchID` | ID:t för den inkapslade batchen som gjorde att posten skapades. |
| `modifiedByBatchID` | ID:t för den senaste inkapslade batchen som gjorde att posten uppdaterades. |
| `repositoryCreatedBy` | ID för den användare som skapade posten. |
| `repositoryLastModifiedBy` | ID för den användare som senast ändrade posten. |

## Kompatibla blandningar {#mixins}

>[!NOTE]
>
>Namnen på flera blandningar har ändrats. Mer information finns i dokumentet om [uppdateringar av blandnamn](../mixins/name-updates.md).

Adobe innehåller flera standardblandningar som kan användas med klassen [!DNL XDM Individual Profile]. Nedan följer en lista över de vanligaste blandningarna för klassen:

* [[!UICONTROL IdentityMap]](../mixins/profile/identitymap.md)
* [[!UICONTROL Demographic Details]](../mixins/profile/person-details.md)
* [[!UICONTROL Personal Contact Details]](../mixins/profile/personal-details.md)
* [[!UICONTROL Work Contact Details]](../mixins/profile/work-details.md)
* [[!UICONTROL Segment Membership Details]](../mixins/profile/segmentation.md)