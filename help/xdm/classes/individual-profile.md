---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;individuell profil;fält;scheman;scheman;identityMap;identity map;identity map;Schema design;map;union schema;union schema
solution: Experience Platform
title: XDM-klass för enskild profil
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över klassen XDM Individual Profile.
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---

# [!DNL XDM Individual Profile] class

[!DNL XDM Individual Profile] är en XDM-klass (Experience Data Model) som utgör en enda representation (eller&quot;profil&quot;) av en enskild person. Klassen (och dess kompatibla blandningar) fångar in attributen och intressena hos både identifierade och delvis identifierade individer som interagerar med ert varumärke.

Profilerna kan omfatta allt från anonyma beteendesignaler (t.ex. cookies i webbläsare) till välidentifierade profiler med detaljerad information som namn, födelsedatum, plats och e-postadress. När en profil växer blir den ett robust arkiv med personuppgifter, identiteter, kontaktuppgifter och kommunikationsinställningar för en individ. Mer högnivåinformation om användning av den här klassen i plattformens ekosystem finns i [XDM-översikten](../home.md#data-behaviors).

Själva klassen [!DNL XDM Individual Profile] innehåller flera systemgenererade värden som fylls i automatiskt när data hämtas, medan alla andra fält måste läggas till med [kompatibla schemafältgrupper](#field-groups):

![](../images/classes/individual-profile.png)

| Egenskap | Beskrivning |
| --- | --- |
| `_repo` | Ett objekt som innehåller följande [!UICONTROL DateTime]-fält: <ul><li>`createDate`: Datum och tid då resursen skapades i datalagret, till exempel när data först importerades.</li><li>`modifyDate`: Datum och tid då resursen senast ändrades.</li></ul> |
| `_id` | En unik identifierare för posten. Det här fältet används för att spåra en enskild posts unika karaktär, förhindra dubblering av data och för att söka efter posten i underordnade tjänster.<br><br>Det är viktigt att särskilja att detta fält inte  **ger** en identitet som är relaterad till en enskild person, utan snarare själva registreringen av uppgifter. Identitetsdata som relaterar till en person ska i stället begränsas till [identitetsfält](../schema/composition.md#identity). |
| `createdByBatchID` | ID:t för den inkapslade batchen som gjorde att posten skapades. |
| `modifiedByBatchID` | ID:t för den senaste inkapslade batchen som gjorde att posten uppdaterades. |
| `personID` | En unik identifierare för den person som den här posten är relaterad till. Det här fältet representerar inte nödvändigtvis en identitet som relateras till personen, såvida det inte också är angivet som ett [identitetsfält](../schema/composition.md#identity). |
| `repositoryCreatedBy` | ID för den användare som skapade posten. |
| `repositoryLastModifiedBy` | ID för den användare som senast ändrade posten. |

{style=&quot;table-layout:auto&quot;}

## Kompatibla fältgrupper {#field-groups}

>[!NOTE]
>
>Namnen på flera fältgrupper har ändrats. Mer information finns i dokumentet om [uppdatering av fältgruppnamn](../field-groups/name-updates.md).

Adobe innehåller flera standardfältgrupper som kan användas med klassen [!DNL XDM Individual Profile]. Nedan följer en lista över några vanliga fältgrupper för klassen:

* [[!UICONTROL IdentityMap]](../field-groups/profile/identitymap.md)
* [[!UICONTROL Demographic Details]](../field-groups/profile/demographic-details.md)
* [[!UICONTROL Personal Contact Details]](../field-groups/profile/personal-contact-details.md)
* [[!UICONTROL Work Contact Details]](../field-groups/profile/work-contact-details.md)
* [[!UICONTROL Segment Membership Details]](../field-groups/profile/segmentation.md)

En fullständig lista över alla kompatibla fältgrupper för [!DNL XDM Individual Profile] finns i [XDM GitHub-repo](https://github.com/adobe/xdm/tree/master/components/mixins/profile).
