---
title: Aktivera målgrupper på konton för destinationer
type: Tutorial
description: Lär dig hur du aktiverar målgrupper för konton på destinationer
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="B2P Edition" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
exl-id: ad69d0a8-bf5b-42ac-97a3-401eadda62cd
source-git-commit: 4afb2c76f2022423e8f1fa29c91d02b43447ba90
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 0%

---

# Aktivera kontomålgrupper

>[!AVAILABILITY]
>
>Funktionen för att aktivera kontomålgrupper för mål är tillgänglig för företag som köper utgåvorna [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) och [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p) av Real-Time Customer Data Platform.

I den här artikeln förklaras det arbetsflöde som krävs för att exportera [kontomålgrupper](/help/segmentation/types/account-audiences.md) från Adobe Experience Platform till det önskade målet.

## Mål som stöds {#supported-destinations}

Gå till **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** och välj fliken **[!UICONTROL Catalog]**. Använd filtret **[!UICONTROL Data types]** och välj **[!UICONTROL Accounts]** för att se vilka mål som stöder aktivering av målgrupper. För närvarande är export av kontomålgrupper bara tillgängligt för vissa molnlagringsmål ([Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [ADLS Gen 2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [Azure Blob Storage](/help/destinations/catalog/cloud-storage/azure-blob.md), [Data Landing Zone](/help/destinations/catalog/cloud-storage/data-landing-zone.md) och [SFTP](/help/destinations/catalog/cloud-storage/sftp.md)) och [Demandbase](/help/destinations/catalog/advertising/demandbase.md) och [(Companies) LinkedIn Matching direktuppspelningsmål för ](/help/destinations/catalog/social/linkedin-b2b.md) .

![Destinationer som stöder målgrupper.](/help/destinations/assets/ui/activate-account-audiences/data-types-filter.png)

## Videoöversikt

I videon nedan finns en översikt över hur du skapar och aktiverar kontomålgrupper och vilka användningsfall som stöds när du aktiverar kontomålgrupper.

>[!VIDEO](https://video.tv.adobe.com/v/338252/?learn=on)

## Förhandskrav {#prerequisites}

* Du måste först importera [kontoprofiler](/help/rtcdp/accounts/account-profile-overview.md) och skapa [kontomålgrupper](/help/segmentation/types/account-audiences.md) innan du kan aktivera dem till underordnade mål.
* Om du vill aktivera kontomålgrupper för destinationer måste du ha anslutit till en destination. Om du inte redan har gjort det går du till [målkatalogen](../catalog/overview.md), bläddrar bland de mål som stöds och konfigurerar det mål som du vill använda. Mer information finns i självstudiekursen [Ansluta till mål](./connect-destination.md).

### Nödvändiga behörigheter {#permissions}

Om du vill aktivera kontomålgrupper behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Activate Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Bläddra i målkatalogen för att se till att du har de behörigheter som krävs för att aktivera målgrupper. Om ett mål har en **[!UICONTROL Activate]**-kontroll har du rätt behörighet.

## Välj mål {#select-destination}

Följ instruktionerna för att välja ett mål där du kan exportera datauppsättningar:

1. Gå till **[!UICONTROL Connections > Destinations]** och välj fliken **[!UICONTROL Catalog]**.

   ![Fliken Målkatalog med katalogkontrollen markerad.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. Välj **[!UICONTROL Activate]** på kortet som motsvarar målet som du vill exportera datauppsättningar till.

>[!TIP]
>
>Destinationerna som kan exportera kontomålar indikeras med en ikon i kortets övre högra hörn, som liknar målet som markeras nedan, eller så kan du använda datatypsfiltret för att endast visa destinationer som kan exportera kontomålar, vilket [visas högst upp på sidan](#supported-destinations).

![Målsida för Demandbase som kan exportera profilmålgrupper markerade.](/help/destinations/assets/ui/activate-account-audiences/demandbase-icon-activate-account-audiences.png)

1. Välj **[!UICONTROL Data type Accounts]**, följt av målanslutningen som du vill exportera datauppsättningar till, och välj sedan **[!UICONTROL Next]**.

>[!TIP]
> 
>Om du vill konfigurera ett nytt mål för att aktivera kontomaterial väljer du **[!UICONTROL Configure new destination]** för att aktivera arbetsflödet [Anslut till mål](/help/destinations/ui/connect-destination.md) och [välja konton som datatyp](/help/destinations/ui/connect-destination.md#segment-activation-or-dataset-exports).

![Arbetsflöde för målaktivering med kontokontroll markerat.](/help/destinations/assets/ui/activate-account-audiences/activate-account-audiences-highlighted.png)

1. Gå till nästa avsnitt för att [välja dina kontomaterial](#select-profile-audiences) för export.

## Välj era kontomålgrupper {#select-account-audiences}

Använd kryssrutorna till vänster om målgruppsnamnen för att välja de målgrupper som du vill exportera till målet och välj sedan **[!UICONTROL Next]**. Observera att endast *kontomålar* visas i den här vyn och att inga andra målgruppstyper visas.

![Arbetsflöde för dataexport med steget Välj målgrupper där du kan välja vilka kontomålgrupper som ska exporteras.](/help/destinations/assets/ui/activate-account-audiences/select-account-audiences.png)

## Schemaläggning och nästa steg

För resten av aktiveringsarbetsflödet för att exportera kontomaterial, läs självstudiekursen om hur du aktiverar data till filbaserade mål. Fortsätt från [schemalägg målgruppsexportsteget](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling). Om du aktiverar kontomålgrupper till målet **[!UICONTROL (Companies) LinkedIn Matched Audiences]**, läs självstudiekursen om hur du aktiverar direktuppspelningsmål. Fortsätt från [mappningssteget](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping).

>[!NOTE]
>
>Observera, att i schemaläggningssteget när du exporterar kontomålgrupper till molnlagringsmål, kan du bara exportera [fullständiga filer](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) och [inkrementella filer](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) _enligt ett dagligt schema_ i arbetsflödet för att aktivera kontomålgrupper. Export per timme stöds inte. Observera också att **[!UICONTROL After audience evaluation]** är den enda utvärderingstypen som stöds.

## Viktiga hänvisningar och kända begränsningar {#important-callouts-known-limitations}

Observera följande viktiga pratbubblor och kända begränsningar för den allmänna tillgänglighetsreleasen för funktionaliteten för att aktivera kontomålgrupper.

### Obligatoriska mappningspar i mappningssteget när kontomålgrupper aktiveras till målet **[!UICONTROL (Companies) LinkedIn Matched Audiences]** {#required-mappings}

Observera att följande två mappningspar är obligatoriska för att det ska gå att exportera data när kontomålgrupper aktiveras till målet **[!UICONTROL (Companies) LinkedIn Matched Audiences]**:

![LinkedIn-mappning av obligatoriska fält.](/help/destinations/assets/ui/activate-account-audiences/linkedin-mapping-required-fields.png)

| Source | Målfält |
|---------|----------|
| `accountName` | `companyName` |
| `accountKey.sourceKey` | `primaryId` (markera det här fältet i vyn **[!UICONTROL Select Identity namespace]** när du väljer **[!UICONTROL Target Field]**). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper för kontot till mål.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper för kontot till mål."){width="100" zoomable="yes"} |

### Tillämpning av datastyrning {#data-governance-enforcement}

Samtycke krävs på person- eller profilnivå för *kund- och potentiell publik*. Därför stöds för närvarande inte [utvärdering av principen för medgivande](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) vid aktivering av kontomålgrupper till mål. I granskningssteget i aktiveringsarbetsflödet kan du se en nedtonad kontroll för **[!UICONTROL View applicable consent policies]**.

![Granskningssteget i arbetsflödet för aktivering av målgrupper med efterlevnadskontrollen för samtycke är nedtonat.](/help/destinations/assets/ui/activate-account-audiences/consent-checks-greyed-out.png)

Andra mekanismer för datastyrning i Real-Time CDP, t.ex. [policykontroller för dataanvändning](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) och [attributbaserad åtkomstkontroll](/help/destinations/home.md#attribute-based-access), stöds.
