---
title: Aktivera målgrupper på konton för destinationer
type: Tutorial
description: Lär dig hur du aktiverar målgrupper för konton på destinationer
badgeB2B: label="B2B Edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="B2P Edition" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
exl-id: ad69d0a8-bf5b-42ac-97a3-401eadda62cd
source-git-commit: 3c0b7c4eee7c790a8ffae95c05a8db6ba7c3b285
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 0%

---

# Aktivera kontomålgrupper

>[!AVAILABILITY]
>
>Funktionen för att aktivera målgrupper på konton är tillgänglig för företag som köper [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) och [Personligt arbete](/help/rtcdp/overview.md#rtcdp-b2p) utgåvor av Real-time Customer Data Platform.

I den här artikeln förklaras vilket arbetsflöde som krävs för att exportera [kontomålgrupper](/help/segmentation/ui/account-audiences.md) från Adobe Experience Platform till det mål du föredrar.

## Mål som stöds {#supported-destinations}

Gå till **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** och väljer **[!UICONTROL Catalog]** -fliken. Använd **[!UICONTROL Data types]** filtrera och markera **[!UICONTROL Accounts]** för att se vilka destinationer som stöder aktivering av målgrupper. För närvarande är export av kontomålgrupper bara tillgängligt för vissa molnlagringsmål ([Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [ADLS Gen 2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [Azure Blob Storage](/help/destinations/catalog/cloud-storage/azure-blob.md), [Datallandningszon](/help/destinations/catalog/cloud-storage/data-landing-zone.md)och [SFTP](/help/destinations/catalog/cloud-storage/sftp.md)) och [(Företag) LinkedIn Matched Auditions](/help/destinations/catalog/social/linkedin.md) mål.

![Destinationer som stöder målgrupper på konton.](/help/destinations/assets/ui/activate-account-audiences/data-types-filter.png)

## Förutsättningar {#prerequisites}

* Du måste först importera [kontoprofiler](/help/rtcdp/accounts/account-profile-overview.md) och skapa [kontomålgrupper](/help/segmentation/ui/account-audiences.md) innan du kan aktivera dem för nedladdningsdestinationer.
* Om du vill aktivera kontomålgrupper för destinationer måste du ha anslutit till en destination. Om du inte redan har gjort det går du till [målkatalog](../catalog/overview.md), bläddra bland de mål som stöds och konfigurera det mål som du vill använda. Läs självstudiekursen om användargränssnittet [ansluta till destinationer](./connect-destination.md) för mer information.

### Nödvändiga behörigheter {#permissions}

Om du vill aktivera kontomålgrupper behöver du **[!UICONTROL View Destinations]** och **[!UICONTROL Activate Destinations]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Bläddra i målkatalogen för att se till att du har de behörigheter som krävs för att aktivera målgrupper. Om ett mål har en **[!UICONTROL Activate]** har du rätt behörighet.

## Välj mål {#select-destination}

Följ instruktionerna för att välja ett mål där du kan exportera datauppsättningar:

1. Gå till **[!UICONTROL Connections > Destinations]** och väljer **[!UICONTROL Catalog]** -fliken.

   ![Fliken Målkatalog med katalogkontrollen markerad.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. Välj **[!UICONTROL Activate]** på kortet som motsvarar målet som du vill exportera datauppsättningar till.

>[!TIP]
>
>Destinationerna som kan exportera kontomatgrupper indikeras med en ikon i kortets övre högra hörn, liknande det mål som markeras nedan, eller så kan du använda datatypsfiltret för att endast visa destinationer som kan exportera kontomålar, som [visas längst upp på sidan](#supported-destinations).

![Amazon S3-målsida som kan exportera profilmålgrupper som är markerade.](/help/destinations/assets/ui/activate-account-audiences/amazon-s3-icon-activate-account-audiences.png)

1. Välj **[!UICONTROL Data type Accounts]**, följt av den målanslutning som du vill exportera datauppsättningar till och välj sedan **[!UICONTROL Next]**.

>[!TIP]
> 
>Om du vill konfigurera en ny destination för att aktivera kontomålar väljer du **[!UICONTROL Configure new destination]** för att aktivera [Anslut till mål](/help/destinations/ui/connect-destination.md) arbetsflöde och [välj konton som datatyp](/help/destinations/ui/connect-destination.md#segment-activation-or-dataset-exports).

![Arbetsflöde för målaktivering med kontokontroll markerad.](/help/destinations/assets/ui/activate-account-audiences/activate-account-audiences-highlighted.png)

1. Gå till nästa avsnitt för att [välj era kontomålgrupper](#select-profile-audiences) för export.

## Välj era kontomålgrupper {#select-account-audiences}

Använd kryssrutorna till vänster om målgruppsnamnen för att välja vilka målgrupper du vill exportera till målet och markera sedan **[!UICONTROL Next]**. Observera att endast *kontomålgrupper* visas i den här vyn och inga andra typer av målgrupper visas.

![Arbetsflöde för dataexport med steget Välj målgrupper där du kan välja vilka kontomålgrupper som ska exporteras.](/help/destinations/assets/ui/activate-account-audiences/select-account-audiences.png)

## Schemaläggning och nästa steg

För resten av aktiveringsarbetsflödet för att exportera kontomaterial, läs självstudiekursen om hur du aktiverar data till filbaserade mål. Fortsätt från [schemalägg exportsteg för målgrupp](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling). Om du aktiverar kontomålgrupper för **[!UICONTROL (Companies) LinkedIn Matched Audiences]** mål, läs självstudiekursen om hur du aktiverar direktuppspelningsmål. Fortsätt från [mappningssteg](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping).

>[!NOTE]
>
>Observera att i schemaläggningssteget vid export av kontomålgrupper till molnlagringsmål, kan du bara exportera via arbetsflödet för att aktivera kontomålgrupper [fullständiga filer](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) och [inkrementella filer](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) _enligt ett dagligt schema_. Export per timme stöds inte. Observera också att **[!UICONTROL After audience evaluation]** är den enda utvärderingstyp som stöds.

## Viktiga hänvisningar och kända begränsningar {#important-callouts-known-limitations}

Observera följande viktiga pratbubblor och kända begränsningar för den allmänna tillgänglighetsreleasen för funktionaliteten för att aktivera kontomålgrupper.

### Obligatoriska mappningspar i mappningssteget när kontomålgrupper aktiveras till **[!UICONTROL (Companies) LinkedIn Matched Audiences]** mål {#required-mappings}

När kontomålgrupper aktiveras för **[!UICONTROL (Companies) LinkedIn Matched Audiences]** mål, observera att följande två mappningspar är obligatoriska för att data ska kunna exporteras:

![LinkedIn-mappning av obligatoriska fält.](/help/destinations/assets/ui/activate-account-audiences/linkedin-mapping-required-fields.png)

| Källfält | Målfält |
|---------|----------|
| `accountName` | `companyName` |
| `accountKey.sourceKey` | `primaryId` (välj det här fältet i dialogrutan **[!UICONTROL Select Identity namespace]** vyn, när du väljer **[!UICONTROL Target Field]**). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper för konton till mål.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper för konton till mål."){width="100" zoomable="yes"} |

### Tillämpning av datastyrning {#data-governance-enforcement}

Godkännandet används på person- eller profilnivå för *målgrupper för kunder och potentiella kunder*. Därför bör  [utvärdering av godkännandepolicy](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) stöds för närvarande inte vid aktivering av kontomålgrupper till mål. I granskningssteget i aktiveringsarbetsflödet ser du en nedtonad kontroll för **[!UICONTROL View applicable consent policies]**.

![Granska steg i arbetsflödet för aktivering av målgrupper för konton med den obligatoriska kontrollen nedtonad.](/help/destinations/assets/ui/activate-account-audiences/consent-checks-greyed-out.png)

Andra datastyrningsmekanismer i Real-Time CDP, som [principkontroller för dataanvändning](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) och [attributbaserad åtkomstkontroll](/help/destinations/home.md#attribute-based-access) stöds.
