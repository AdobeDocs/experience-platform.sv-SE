---
title: Talon.One Source Overview
description: Läs om Talon.En källa på Adobe Experience Platform
badge: Beta
hide: true
hidefromtoc: true
source-git-commit: 558a9d6ff3222acbf77edea0a82ef50725cd6203
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 1%

---

# [!DNL Talon.One]

>[!AVAILABILITY]
>
>Källorna [!DNL Talon.One] är i betaversion. Läs [villkoren](../../home.md#terms-and-conditions) i källresursöversikten om du vill ha mer information om hur du använder betatecknade källor.

Med [!DNL Talon.One] kan ni enkelt skapa, hantera och optimera personaliserade marknadsföringskampanjer som är skräddarsydda för era kunder. Använd den här kraftfulla plattformen för att köra rabatter, distribuera kuponger, starta hänvisningsprogram, konfigurera lojalitetsprogram och erbjuda spelanpassade incitament - allt från ett skalbart system som hjälper er att engagera och belöna er målgrupp.

Du kan använda [!DNL Talon.One]-källorna i Adobe Experience Platform-källkatalogen för att importera både batch- och direktuppspelade lojalitetsdata från ditt [!DNL Talon.One]-konto.

* [Talon.One Streaming Events](../../tutorials/ui/create/loyalty/talon-one-streaming.md)
* [Talon.One Batch Source Connector](../../tutorials/ui/create/loyalty/talon-one-batch.md)

>[!TIP]
>
>Förmånsdata avser slutanvändarnas lojalitetsprograminformation, t.ex. förmånspoäng, utnyttjade förmånspoäng, aktuell nivå, beviljade kuponger, hänvisningar och prestationer.

## Förhandskrav {#prerequisites}

Ange värden för följande autentiseringsuppgifter för att autentisera och ansluta [!DNL Talon.One Batch Source Connector].

| Autentiseringsuppgifter | Beskrivning | Exempel |
| --- | --- | --- |
| Domän | Den unika URL som är associerad med din [!DNL Talon.One]-programmiljö. Se till att du inte inkluderar protokollet eller sökvägen när du anger domänen. | `acmetalonone.us-east4` |
| Hanterings-API för [!DNL Talon.One] | Hanterings-API-nyckeln är en autentiseringsuppgift som används för att autentisera och auktorisera åtkomst till [!DNL Talon.One]s hanterings-API. Detta hanterar åtgärder som: <ul><li>Importerar kuponger</li><li>Hämtar kampanjdata</li><li>Hantera program och slutpunkter</li></ul> | `ManagementKey-v1 {YOUR_MANAGEMENT_KEY}` |

## Mappning {#mapping}

För att du lättare ska kunna mappa varje effektobjekt baserat på dess unika `effectType`-värde kan du använda dataprep `array_to_map` -funktionen. På så sätt kan du enkelt konvertera en osorterad array med effekter till nyckelvärdepar som passar dina behov. Se exemplet nedan för vägledning.

| Källa | Mål |
| ---- | --- |
| `array_to_map(data.effects, "effectType").addLoyaltyPoints.campaignId` | `_{TENANT_ID}.loyalty.pointsGained[0].promotionId` |
| `array_to_map(data.effects, "effectType").addLoyaltyPoints.props.value` | `_{TENANT_ID}.loyalty.pointsGained[0].value` |
| `array_to_map(data.effects, "effectType").deductLoyaltyPoints.campaignId` | `_{TENANT_ID}.loyalty.pointsRedemption[0].promotionId` |
| `array_to_map(data.effects, "effectType").acceptCoupon.campaignId` | `_{TENANT_ID}.loyalty.couponRedemption[0].campaignId` |
| `array_to_map(data.effects, "effectType").deductLoyaltyPoints.props.value` | `_{TENANT_ID}.loyalty.pointsRedemption[0].value` |
| `array_to_map(data.effects, "effectType").acceptCoupon.props.value` | `_{TENANT_ID}.loyalty.couponRedemption[0].id` |
| `array_to_map(data.effects, "effectType").setDiscount.campaignId` | `_{TENANT_ID}.loyalty.discounts[0].promotionId` |
| `array_to_map(data.effects, "effectType").setDiscount.props.value` | `_{TENANT_ID}.loyalty.discounts[0].value` |
| `data.created` | `timestamp` |
| `data.attributes.params.profileId` | `personID` |
| `data.attributes.integrationId` | `_id` |
| `data.attributes.params.cartItems[*].name` | `productListItems[*].name` |
| `data.attributes.params.cartItems[*].category` | `productListItems[*].productCategories[0].categoryID` |
| `data.attributes.params.cartItems[*].sku` | `productListItems[*].SKU` |

{style="table-layout:auto"}

## Nästa steg

Läs följande dokumentation om du vill veta hur du kan ansluta ditt [!DNL Talon.One]-konto till Experience Platform och importera både batch- och direktuppspelningslojalitetsdata.

* [Talon.One Streaming Events](../../tutorials/ui/create/loyalty/talon-one-streaming.md)
* [Talon.One Batch Source Connector](../../tutorials/ui/create/loyalty/talon-one-batch.md)