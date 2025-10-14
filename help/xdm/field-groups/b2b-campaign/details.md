---
title: XDM Business Campaign Details Schema Field Group
description: Läs mer om schemafältgruppen XDM Business Campaign Details.
exl-id: 3ef6c0b9-cba1-449e-8868-46446c00465f
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---

# Schemafältgruppen [!UICONTROL XDM Business Campaign Details]

[!UICONTROL XDM Business Campaign Details] är en standardschemafältgrupp för klassen [[!UICONTROL XDM Business Campaign] &#x200B;](../../classes/b2b/business-campaign.md) som samlar in detaljerad information om en företagskampanj.

![Strukturen för fältgruppen XDM Business Campaign Details så som den visas i användargränssnittet](../../images/field-groups/b2b/business-campaign-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `actualCost` | [[!UICONTROL Currency]](../../data-types/currency.md) | Representerar den verkliga kostnaden för affärskampanjen. |
| `budgetedCost` | [[!UICONTROL Currency]](../../data-types/currency.md) | Representerar den budgeterade kostnaden för affärskampanjen. |
| `expectedRevenue` | [[!UICONTROL Currency]](../../data-types/currency.md) | Representerar de intäkter som affärskampanjen förväntas generera. |
| `parentCampaignKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Det sammansatta ID:t för en överordnad kampanj, om tillämpligt. |
| `campaignEndDate` | [!UICONTROL DateTime] | En ISO 8601-tidsstämpel som anger när kampanjen avslutades eller kommer att avslutas. |
| `campaignProgressionName` | [!UICONTROL String] | Kampanjens progressionsnamn. |
| `campaignStartDate` | [!UICONTROL DateTime] | En ISO 8601-tidsstämpel som anger när kampanjen startades eller kommer att starta. |
| `campaignStatus` | [!UICONTROL String] | Kampanjens aktuella status. |
| `channelName` | [!UICONTROL String] | Namnet på kanalen som är associerad med kampanjen. |
| `expectedResponse` | [!UICONTROL String] | Det förväntade svaret för kampanjen. |
| `integrationPartnerName` | [!UICONTROL String] | Namnet på den partner som har integrerats med kampanjen. |
| `isActive` | [!UICONTROL Boolean] | Anger om kampanjen är aktiv. |
| `isDeleted` | [!UICONTROL Boolean] | Anger om kampanjen har tagits bort i Marketo Engage.<br><br>När du använder [Marketo-källkopplingen](../../../sources/connectors/adobe-applications/marketo/marketo.md) återspeglas alla poster som tas bort i Marketo automatiskt i kundprofilen i realtid. Poster som rör dessa profiler kan dock fortfarande finnas kvar i datasjön. Genom att ställa in `isDeleted` på `true` kan du använda fältet för att filtrera bort vilka poster som har tagits bort från dina källor när du frågar i datasjön. |
| `lastActivityDate` | [!UICONTROL DateTime] | En ISO 8601-tidsstämpel för den senaste aktiviteten som är associerad med kampanjen. |
| `timeZone` | [!UICONTROL String] | Tidszonen som kampanjen körs i. |
| `timeZoneDelivery` | [!UICONTROL String] | Den leveranstidszon som kampanjen körs i. |
| `timeZoneName` | [!UICONTROL String] | Namnet på den tidszon som kampanjen körs i. |
| `webinarHistorySyncDate` | [!UICONTROL DateTime] | En ISO 8601-tidsstämpel för den senaste webbseminariehistoriksynkroniseringen för kampanjen. |
| `webinarHistorySyncStatus` | [!UICONTROL String] | Status för webbinariets historiksynkronisering för kampanjen. |
| `webinarSessionDescription` | [!UICONTROL String] | En beskrivning av det webbinarium som är associerat med kampanjen. |
| `webinarSessionName` | [!UICONTROL String] | Ett namn på det webbinarium som är associerat med kampanjen. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i [den offentliga XDM-databasen](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign/campaign-details.schema.json).
