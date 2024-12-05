---
title: (Företag) LinkedIn-anslutning
description: Använd den här destinationen för att aktivera dina kontomålgrupper för användningsfall inom Account-Based Marketing (ABM). Aktivera profiler för era LinkedIn-kampanjer för målgruppsanpassning, personalisering och nedtryckning, baserat på hashad-e-post.
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="B2P Edition" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
source-git-commit: e45c50a6447be4a60145eea6956d30d51166e675
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 2%

---

# (Företag) LinkedIn Matcha målgrupper {#companies-linkedin}

>[!AVAILABILITY]
>
>Funktionen för att aktivera kontomålgrupper för LinkedIn-destinationen (företag) är tillgänglig för företag som köper utgåvorna [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) och [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p) av Real-time Customer Data Platform.

Använd det här målet för att aktivera dina [kontomålgrupper](/help/segmentation/ui/account-audiences.md) för Account-Based Marketing-användningsfall (ABM). Annonsera relevanta personer och roller i dina målkonton via målet **[!UICONTROL (Companies) LinkedIn]** business-to-business. Gå till LinkedIn-dokumentationen och [läs mer om målinriktning för konton](https://business.linkedin.com/marketing-solutions/cx/21/10/ad-targeting/account-targeting) på LinkedIn-plattformen.

>[!TIP]
>
>För enskilda (eller företag-till-kund) användningsområden rekommenderar Adobe att du använder målet [LinkedIn Matched Audience](/help/destinations/catalog/social/linkedin.md).

![LinkedIn-kontomålet visas i användargränssnittet för Experience Platform.](/help/destinations/assets/catalog/social/linkedin-b2b/linkedin-b2b-destination.png)

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilken typ av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Publiker som genererats via Experience Platform [segmenteringstjänsten](../../../segmentation/home.md). |
| Anpassade överföringar | X | Publikerna [importerade](../../../segmentation/ui/overview.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-and-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
|--------------|-----------|---------------------------|
| Exporttyp | Målgruppsexport | Alla målgruppsmedlemmar exporteras med nyckelidentifierare som namn, telefonnummer med mera. |
| Frekvens | Direktuppspelning | &quot;Alltid på&quot; API-baserade anslutningar. Uppdateringar skickas nedströms omedelbart efter att profilen har ändrats. |

{style="table-layout:auto"}

## Förhandskrav {#prerequisites}

Kontrollera att du uppfyller kraven nedan för att kunna exportera kontomaterial till LinkedIn:

### Krav för linkedIn-konton {#LinkedIn-account-prerequisites}

Innan du kan använda målet [!UICONTROL (Companies) LinkedIn Matched Audience] måste du kontrollera att ditt [!DNL LinkedIn Campaign Manager]-konto har behörighetsnivån [!DNL Creative Manager] eller högre.

Mer information om hur du redigerar användarbehörigheter för [!DNL LinkedIn Campaign Manager] finns i [Lägg till, redigera och ta bort användarbehörigheter för Advertising-konton](https://www.linkedin.com/help/lms/answer/5753) i LinkedIn-dokumentationen.

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du behörigheten **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

1. Hitta [!DNL (Companies) LinkedIn Matched Audiences]-målet i målkatalogen och välj **[!UICONTROL Set Up]**.
2. Välj **[!UICONTROL Connect to destination]**.
   ![Autentisera till LinkedIn](/help/destinations/assets/catalog/social/linkedin-b2b/authenticate-linkedin-destination.png)
3. Ange dina LinkedIn-autentiseringsuppgifter och välj **Logga in**.

När du har slutfört inloggningsprocessen med LinkedIn kan du gå vidare till nästa steg.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Account ID]**: Din [!DNL LinkedIn Campaign Manager Account ID]. Du kan hitta det här ID:t i ditt [!DNL LinkedIn Campaign Manager]-konto.

Nu kan du aktivera kontomålgrupper för LinkedIn.

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