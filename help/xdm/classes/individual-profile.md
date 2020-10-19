---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;identityMap;identity map;Identity map;Schema design;map;Map;union schema;union
solution: Experience Platform
title: Klassen XDM Individuell profil
topic: overview
description: Det här dokumentet innehåller en översikt över klassen XDM Individual Profile.
translation-type: tm+mt
source-git-commit: b7b57c0b70b1af3a833f0386bc809bb92c9b50f8
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---


# [!DNL XDM Individual Profile] class

[!DNL XDM Individual Profile] är en XDM-standardklass som bildar en enda representation (eller&quot;profil&quot;) av både identifierade och delvis identifierade individers attribut och intressen.

Profilerna kan omfatta allt från anonyma beteendesignaler (t.ex. cookies i webbläsare) till välidentifierade profiler med detaljerad information som namn, födelsedatum, plats och e-postadress. När en profil växer blir den ett robust arkiv med personuppgifter, identiteter, kontaktuppgifter och kommunikationsinställningar för en individ. Mer högnivåinformation om användningen av den här klassen i plattformens ekosystem finns i [XDM-översikten](../home.md#data-behaviors).

Själva [!DNL XDM Individual Profile] klassen innehåller flera systemgenererade värden som fylls i automatiskt när data hämtas, medan alla andra fält måste läggas till med hjälp av [kompatibla blandningar](#mixins):

![](../images/classes/individual-profile.png)

| Egenskap | Beskrivning |
| --- | --- |
| `_repo` | Ett objekt som innehåller följande [!UICONTROL DateTime] fält: <ul><li>`createDate`: Datum och tid då resursen skapades i datalagret, till exempel när data först importerades.</li><li>`modifyDate`: Datum och tid då resursen senast ändrades.</li></ul> |
| `_id` | En unik systemgenererad strängidentifierare för posten. Det här fältet används för att spåra en enskild posts unika karaktär, förhindra dubblering av data och för att söka efter posten i underordnade tjänster. Eftersom det här fältet genereras av systemet bör det inte anges som ett explicit värde vid datainmatning.<br><br>Det är viktigt att särskilja att detta fält **inte** representerar en identitet som är relaterad till en enskild person, utan själva registreringen av uppgifter. Identitetsdata som relaterar till en person bör i stället begränsas till [identitetsfält](../schema/composition.md#identity) . |
| `createdByBatchID` | ID:t för den inkapslade batchen som gjorde att posten skapades. |
| `modifiedByBatchID` | ID:t för den senaste inkapslade batchen som gjorde att posten uppdaterades. |
| `repositoryCreatedBy` | ID för den användare som skapade posten. |
| `repositoryLastModifiedBy` | ID för den användare som senast ändrade posten. |

## Kompatibla blandningar {#mixins}

Adobe innehåller flera standardblandningar som kan användas med [!DNL XDM Individual Profile] klassen. Nedan följer en lista över de vanligaste blandningarna för klassen:

* [[!UICONTROL IdentityMap]](../mixins/profile/identitymap.md)
* [[!UICONTROL Profile person details]](../mixins/profile/person-details.md)
* [[!UICONTROL Profile personal details]](../mixins/profile/personal-details.md)
* [[!UICONTROL Profile work details]](../mixins/profile/work-details.md)
* [[!UICONTROL Profile segmentation]](../mixins/profile/segmentation.md)