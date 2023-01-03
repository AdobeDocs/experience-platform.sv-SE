---
title: XDM Business Campaign-medlemsinformationsschemagrupp
description: Det här dokumentet innehåller en översikt över schemafältgruppen XDM Business Campaign Member Details.
exl-id: 597629c8-7f41-4c1c-95b6-aed5e16cee72
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---

# [!UICONTROL XDM Business Campaign Member Details] schemafältgrupp

[!UICONTROL XDM Business Campaign Member Details] är en standardgrupp för schemafält för [[!UICONTROL XDM Business Campaign Members] class](../../classes/b2b/business-campaign-members.md), som innehåller detaljerad information om en företagskampanj.

![Strukturen för fältgruppen XDM Business Campaign-medlemsinformation så som den visas i användargränssnittet](../../images/field-groups/b2b/business-campaign-member-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `acquiredByCampaignKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Det sammansatta ID:t för kampanjen som förvärvade den här kampanjmedlemmen. |
| `acquiredByCampaignID` | [!UICONTROL String] | En strängidentifierare för kampanjen som förvärvade den här kampanjmedlemmen. |
| `firstRespondedDate` | [!UICONTROL DateTime] | En ISO 8601-tidsstämpel som anger när personen först svarade på kampanjen. |
| `hasReachedSuccess` | [!UICONTROL Boolean] | Anger om kampanjmedlemmen har resulterat i en lyckad konvertering. |
| `hasResponded` | [!UICONTROL Boolean] | Anger om kampanjmedlemmen har svarat på kampanjen. |
| `isDeleted` | [!UICONTROL Boolean] | Anger om den här kampanjmedlemmen har tagits bort i Marketo Engage.<br><br>När du använder [Marketo källanslutning](../../../sources/connectors/adobe-applications/marketo/marketo.md), återspeglas alla poster som tas bort i Marketo automatiskt i kundprofilen i realtid. Poster som rör dessa profiler kan dock fortfarande finnas kvar i datasjön. Efter inställning `isDeleted` till `true`kan du använda fältet för att filtrera bort vilka poster som har tagits bort från dina källor när du frågar efter datasjön. |
| `isExhausted` | [!UICONTROL Boolean] | Anger om kampanjmedlemmen har uttömt alla kampanjinteraktioner. |
| `lastStatus` | [!UICONTROL String] | Den senaste statusen för kampanjmedlemmen. |
| `memberStatus` | [!UICONTROL String] | Aktuell status för kampanjmedlemmen. |
| `memberStatusReason` | [!UICONTROL String] | Orsaken till kampanjmedlemmens aktuella status. |
| `membershipDate` | [!UICONTROL DateTime] | Orsaken till kampanjmedlemmens aktuella status. |
| `nurtureCadence` | [!UICONTROL String] | Tidsgränsen för kampanjrelaterad information som ska presenteras för kampanjmedlemmen. |
| `nurtureTrackName` | [!UICONTROL String] | Namnet på det vårdprogram som kampanjmedlemmen omfattas av. |
| `reachedSuccessDate` | [!UICONTROL DateTime] | En ISO 8601-tidsstämpel för när en lyckad konvertering gjordes för kampanjmedlemmen. |
| `webinarConfirmationUrl` | [!UICONTROL String] | Webbinariets bekräftelse-URL för kampanjmedlemmen. |
| `webinarRegistrationID` | [!UICONTROL String] | Registrerings-ID för webbinariet för kampanjmedlemmen. |

{style=&quot;table-layout:auto&quot;}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign-member/campaign-member-details.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign-member/campaign-member-details.schema.json)
