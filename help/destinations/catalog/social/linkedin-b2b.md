---
title: (Företag) LinkedIn-anslutning
description: Använd den här destinationen för att aktivera dina kontomålgrupper för användningsfall inom Account-Based Marketing (ABM). Aktivera profiler för era LinkedIn-kampanjer för målgruppsanpassning, personalisering och nedtryckning, baserat på hash-kodade e-postmeddelanden.
exl-id: 68d2cca3-952b-49d0-8ea2-e776a233b752
source-git-commit: d946d3dbb09c1fe0163fba3a892b4c0f1b331f87
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 2%

---

# (Företag) LinkedIn Match Audiences-anslutning {#companies-linkedin}

>[!AVAILABILITY]
>
>Funktionen för att aktivera kontomålgrupper för LinkedIn-destinationen (Companies) är tillgänglig för företag som köper [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b)- och [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p)-utgåvorna av [!DNL Real-Time Customer Data Platform].

Använd det här målet för att aktivera dina [kontomålgrupper](/help/segmentation/types/account-audiences.md) för Account-Based Marketing-användningsfall (ABM). Annonsera relevanta personer och roller i dina målkonton via målet **[!UICONTROL (Companies) LinkedIn]** business-to-business. Besök LinkedIn-dokumentationen för att [lära dig mer om målinriktning för konton](https://business.linkedin.com/marketing-solutions/cx/21/10/ad-targeting/account-targeting) på LinkedIn-plattformen.

>[!TIP]
>
>För enskilda (eller företag-till-kund) användningsområden rekommenderar Adobe att du använder målet [LinkedIn Matched Audience](/help/destinations/catalog/social/linkedin.md).

![LinkedIn-kontomålet visas i Experience Platform-gränssnittet.](/help/destinations/assets/catalog/social/linkedin-b2b/linkedin-b2b-destination.png)

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilken typ av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
|---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Publiker som genererats via Experience Platform [segmenteringstjänst](../../../segmentation/home.md). |
| Alla andra målgrupper kommer | Ja | Den här kategorin omfattar alla målgrupper som kommer utanför målgrupper som genereras via [!DNL Segmentation Service]. Läs om de [olika målgruppernas ursprung](/help/segmentation/ui/audience-portal.md#customize). Några exempel är: <ul><li> anpassade uppladdningsgrupper [importerade](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer,</li><li> lookalike-målgrupper, </li><li> federerade målgrupper, </li><li> målgrupper som har genererats i andra Experience Platform-appar som [!DNL Adobe Journey Optimizer], </li><li> med mera. </li></ul> |

{style="table-layout:auto"}



Målgrupper som stöds av olika typer av målgruppsdata:

| Typ av målgruppsdata | Stöds | Beskrivning | Användningsfall |
|--------------------|-----------|-------------|-----------|
| [Målgrupper](/help/segmentation/types/people-audiences.md) | Ja | Baserat på kundprofiler kan ni inrikta er på specifika grupper av människor för marknadsföringskampanjer. | Ofta köpare, övergivna varukorgar |
| [Kontomålgrupper](/help/segmentation/types/account-audiences.md) | Ja | Rikta er till individer inom specifika organisationer för kontobaserade marknadsföringsstrategier. | B2B-marknadsföring |
| [Prospektera målgrupper](/help/segmentation/types/prospect-audiences.md) | Nej | Rikta er till individer som ännu inte är kunder men som delar egenskaper med er målgrupp. | Prospektera med data från tredje part |
| [Datauppsättningsexport](/help/catalog/datasets/overview.md) | Nej | Samlingar med strukturerade data lagrade i datasjön [!DNL Adobe Experience Platform]. | Arbetsflöden för rapportering, datavetenskap |

{style="table-layout:auto"}


## Exportera typ och frekvens {#export-type-and-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
|--------------|-----------|---------------------------|
| Exporttyp | Målgruppsexport | Alla målgruppsmedlemmar exporteras med nyckelidentifierare som namn, telefonnummer med mera. |
| Frekvens | Direktuppspelning | &quot;Alltid på&quot; API-baserade anslutningar. Uppdateringar skickas nedströms omedelbart efter att profilen har ändrats. |

{style="table-layout:auto"}

## Förutsättningar {#prerequisites}

Kontrollera att du uppfyller kraven nedan för att exportera kontomaterial till LinkedIn:

### Krav för LinkedIn-konto {#LinkedIn-account-prerequisites}

Innan du kan använda målet [!UICONTROL (Companies) LinkedIn Matched Audience] måste du kontrollera att ditt [!DNL LinkedIn Campaign Manager]-konto har behörighetsnivån [!DNL Creative Manager] eller högre.

Mer information om hur du redigerar användarbehörigheter för [!DNL LinkedIn Campaign Manager] finns i [Lägg till, redigera och ta bort användarbehörigheter för Advertising-konton](https://www.linkedin.com/help/lms/answer/5753) i dokumentationen för LinkedIn.

## Anslut till målet {#connect}

>[!IMPORTANT]
>
>Om du vill ansluta till målet behöver du behörigheten **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

1. Hitta [!DNL (Companies) LinkedIn Matched Audiences]-målet i målkatalogen och välj **[!UICONTROL Set Up]**.
2. Välj **[!UICONTROL Connect to destination]**.
   ![Autentisera till LinkedIn](/help/destinations/assets/catalog/social/linkedin-b2b/authenticate-linkedin-destination.png)
3. Ange dina inloggningsuppgifter för LinkedIn och välj **Logga in**.

När du har slutfört inloggningsprocessen med LinkedIn kan du gå vidare till nästa steg.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Account ID]**: Din [!DNL LinkedIn Campaign Manager Account ID]. Du kan hitta det här ID:t i ditt [!DNL LinkedIn Campaign Manager]-konto.

Nu kan du aktivera kontomaterial för LinkedIn.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
>
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper för kontot till mål.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper för kontot till mål."){width="100" zoomable="yes"}

Läs [Aktivera kontomålgrupper](/help/destinations/ui/activate-account-audiences.md) om du vill ha instruktioner om hur du aktiverar kontomålgrupper till det här målet.

## Obligatoriska mappningspar i mappningssteget när kontomålgrupper aktiveras till målet **[!UICONTROL (Companies) LinkedIn Matched Audiences]** {#required-mappings}

Observera att följande två mappningspar är obligatoriska för att det ska gå att exportera data när kontomålgrupper aktiveras till målet **[!UICONTROL (Companies) LinkedIn Matched Audiences]**:

![LinkedIn-mappning av obligatoriska fält.](/help/destinations/assets/ui/activate-account-audiences/linkedin-mapping-required-fields.png)

| Source | Målfält |
|---------|----------|
| `accountName` | `companyName` |
| `accountKey.sourceKey` | `primaryId` (markera det här fältet i vyn **[!UICONTROL Select Identity namespace]** när du väljer **[!UICONTROL Target Field]**). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper för kontot till mål.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper för kontot till mål."){width="100" zoomable="yes"} |

{style="table-layout:auto"}

## Exporterade data {#exported-data}

En lyckad aktivering innebär att en anpassad [!DNL LinkedIn]-målgrupp skapas programmatiskt i [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login). Målgruppsmedlemskapet justeras eftersom användarna är kvalificerade eller diskvalificerade för de aktiverade målgrupperna.
