---
title: Fältgrupp för partnerprospekt (exempel)
description: Läs mer om schemafältgruppen XDM (Partner Prospect Details) (Exempel).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 0%

---

# [!UICONTROL Partner Prospect Details (Sample)] fältgrupp

[!UICONTROL Partner Prospect Details (Sample)] är en standardgrupp för schemafält för [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). The [!UICONTROL Partner Prospect Details (Sample)] innehåller ett exempelramverk för olika detaljer relaterade till en potentiell kunders profil. Detta ramverk effektiviserar processen att organisera och hantera olika typer av information som rör potentiella kunder.

Den här fältgruppen utökar [Profilklass för enskild potentiell kund](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/prospect.html) inom ramen för en partner.

![Ett diagram över [!UICONTROL Partner Prospect Details (Sample)] fältgrupp.](../../images/field-groups/partner/partner-prospect-details-sample.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
|---------------------------------------|-----------------------------|-----------|--------------------------------------------------|
| [!UICONTROL ageRangeInHousehold] | `ageRangeInHousehold` | string | Åldersintervallet inom hushållet. |
| [!UICONTROL apparelAccessories] | `apparelAccessories` | string | Inställningar eller engagemang i kläder/tillbehör. |
| [!UICONTROL bicycling] | `bicycling` | string | Intresse eller engagemang i cykelverksamhet. |
| [!UICONTROL cableTv] | `cableTv` | string | Visar engagemang med kabel-tv. |
| [!UICONTROL domestics] | `domestics` | string | Inställningar eller engagemang i inhemska aktiviteter. |
| [!UICONTROL electronics] | `electronics` | string | Intresse eller engagemang i elektroniska enheter. |
| [!UICONTROL foodAndBeverage] | `foodAndBeverage` | string | Inställningar för eller inblandning i livsmedel/dryck. |
| [!UICONTROL footwear] | `footwear` | string | Intresse eller engagemang i skodon. |
| [!UICONTROL healthFoods] | `healthFoods` | string | Inställningar för eller engagemang i hälsolivsmedel. |
| [!UICONTROL hiking] | `hiking` | string | Intresse eller engagemang i vandrarnas aktiviteter. |
| [!UICONTROL householdId] | `householdId` | string | En unik identifierare för hushållet. |
| [!UICONTROL individualId] | `individualId` | string | En unik identifierare för den enskilda personen. |
| [!UICONTROL inferredCardHolder] | `inferredCardHolder` | string | Slutsatsen av att vara kortinnehavare. |
| [!UICONTROL inferredPremiumCardholder] | `inferredPremiumCardholder]` | string | Slutsatsen av att vara en betald kortinnehavare. |
| [!UICONTROL matchLevelFlag] | `matchLevelFlag` | string | En indikator för matchningsnivån. |
| [!UICONTROL BuyerRating] | `buyerRating` | string | Ett omdöme om köpbeteende. |
| [!UICONTROL DonorRating] | `donorRating` | string | En klassificering som rör donatorbeteende. |
| [!UICONTROL InvestmentRating] | `investmentRating` | string | Ett kreditbetyg som avser investeringsbeteenden. |
| [!UICONTROL ResponderRating] | `responderRating` | string | En klassificering som relateras till responderbeteende. |
| [!UICONTROL SpendingVelocity] | `spendingVelocity` | string | Utgiftens hastighet eller hastighet. |
| [!UICONTROL SpendingVolume] | `spendingVolume` | string | Utgiftsbelopp eller -volym. |
| [!UICONTROL recordId] | `recordId` | string | En unik identifierare för posten. |
| [!UICONTROL residenceId] | `residenceId` | string | En unik identifierare för hemvisten. |
| [!UICONTROL sailing] | `sailing` | string | Anger intresset för eller engagemanget i segelverksamhet. |
| [!UICONTROL seasonalHolidayProducts] | `seasonalHolidayProducts` | string | Anger preferenser eller engagemang för semesterprodukter. |
| [!UICONTROL skiing] | `skiing` | string | Anger intresset för eller engagemanget i skidaktiviteter. |
| [!UICONTROL tennis] | `tennis` | string | Anger intresse för eller engagemang i tennisaktiviteter. |
| [!UICONTROL tvShoppers] | `tvShoppers` | string | Anger engagemang med TV-shopping. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i [fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/partner-prospect/merkle/prospect-details-partner-sample.schema.json) på den offentliga XDM-databasen.
