---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;individuell profil;fält;scheman;scheman;identityMap;identity map;identity map;Schema design;map;union schema;union schema
solution: Experience Platform
title: XDM Individual Profile Class
topic-legacy: overview
description: This document provides an overview of the XDM Individual Profile class.
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
source-git-commit: 79fcc44ec5e08f63bfd5eed6e90d7538273f4dab
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---

# [!DNL XDM Individual Profile] class

[!DNL XDM Individual Profile] is a standard Experience Data Model (XDM) class which forms a singular representation (or &quot;profile&quot;) of an individual person. Klassen (och dess kompatibla fältgrupper) fångar in både identifierade och delvis identifierade individers attribut och intressen som interagerar med ert varumärke.

Profilerna kan omfatta allt från anonyma beteendesignaler (t.ex. cookies i webbläsare) till välidentifierade profiler med detaljerad information som namn, födelsedatum, plats och e-postadress. När en profil växer blir den ett robust arkiv med personuppgifter, identiteter, kontaktuppgifter och kommunikationsinställningar för en individ. Mer högnivåinformation om användning av den här klassen i plattformens ekosystem finns i [XDM-översikten](../home.md#data-behaviors).

Själva klassen [!DNL XDM Individual Profile] innehåller flera systemgenererade värden som fylls i automatiskt när data hämtas, medan alla andra fält måste läggas till med [kompatibla schemafältgrupper](#field-groups):

![](../images/classes/individual-profile.png)

| Egenskap | Beskrivning |
| --- | --- |
| `_repo` | An object containing the following [!UICONTROL DateTime] fields: <ul><li>`createDate`: Datum och tid då resursen skapades i datalagret, till exempel när data först importerades.</li><li>`modifyDate`: The date and time when the resource was last modified.</li></ul> |
| `_id` | A unique string identifier for the record. This field is used to track the uniqueness of an individual record, prevent duplication of data, and look up that record in downstream services. I vissa fall kan `_id` vara en [UID (Universally Unique Identifier)](https://tools.ietf.org/html/rfc4122) eller [GUID (Global Unique Identifier)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>Om du direktuppspelar data från en källanslutning eller direkt inmatning från en Parquet-fil, bör du generera det här värdet genom att sammanfoga en viss kombination av fält som gör posten unik, t.ex. ett primärt ID, en tidsstämpel, en posttyp o.s.v. The concatenated value must be a `uri-reference` formatted string, meaning any colon characters must be removed. Efteråt bör det sammanfogade värdet hashas med SHA-256 eller någon annan algoritm som du väljer.<br><br>Det är viktigt att särskilja att  **detta fält inte representerar en identitet som är relaterad till en enskild person**, utan själva dataposten. Identitetsdata som relaterar till en person ska i stället begränsas till [identitetsfält](../schema/composition.md#identity) som tillhandahålls av kompatibla fältgrupper. |
| `createdByBatchID` | ID:t för den inkapslade batchen som gjorde att posten skapades. |
| `modifiedByBatchID` | The ID of the last ingested batch that caused the record to be updated. |
| `personID` | En unik identifierare för den person som den här posten är relaterad till. Det här fältet representerar inte nödvändigtvis en identitet som relateras till personen, såvida det inte också är angivet som ett [identitetsfält](../schema/composition.md#identity). |
| `repositoryCreatedBy` | The ID of the user who created the record. |
| `repositoryLastModifiedBy` | The ID of the user who last modified the record. |

{style=&quot;table-layout:auto&quot;}

## Compatible field groups {#field-groups}

>[!NOTE]
>
>Namnen på flera fältgrupper har ändrats. See the document on [field group name updates](../field-groups/name-updates.md) for more information.

Adobe innehåller flera standardfältgrupper som kan användas med klassen [!DNL XDM Individual Profile]. The following is a list of some commonly used field groups for the class:

* [[!UICONTROL Demographic Details]](../field-groups/profile/demographic-details.md)
* [[!UICONTROL IdentityMap]](../field-groups/profile/identitymap.md)
* [[!UICONTROL Loyalty Details]](../field-groups/profile/loyalty-details.md)
* [[!UICONTROL Personal Contact Details]](../field-groups/profile/personal-contact-details.md)
* [[!UICONTROL Privacy/Personalization/Marketing Preferences (Consents)]](../field-groups/profile/consents.md)
* [[!UICONTROL Segment Membership Details]](../field-groups/profile/segmentation.md)
* [[!UICONTROL Work Contact Details]](../field-groups/profile/work-contact-details.md)

En fullständig lista över alla kompatibla fältgrupper för [!DNL XDM Individual Profile] finns i [XDM GitHub-repo](https://github.com/adobe/xdm/tree/master/components/fieldgroups/profile).
