---
title: Demandbase-anslutning
description: Använd den här destinationen för att aktivera dina kontomålgrupper för användningsfall inom Account-Based Marketing (ABM). Annonsera till relevanta personas och roller i dina målgruppskonton via DemandBases B2B Demand Side Platform (DSP). Målgruppskonton kan också berikas med tredjepartsdata från Demandbase, för andra användningsfall i senare led av marknadsförings- och säljprocessen.
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=sv-SE#rtcdp-editions newtab=true"
badgeB2P: label="B2P Edition" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=sv-SE#rtcdp-editions newtab=true"
last-substantial-update: 2024-09-30T00:00:00Z
exl-id: a84609a2-f1d3-4998-9db4-ad59c0a0b631
source-git-commit: 39012e2308af57af7c9193bdc4894f8f2e358606
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 14%

---

# Demandbase-anslutning {#demandbase}

>[!AVAILABILITY]
>
>Funktionen för att aktivera kontomålgrupper för Demandbase-målet är tillgänglig för företag som köper utgåvorna [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) och [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p) av Real-Time Customer Data Platform.

Aktivera profiler för dina Demandbase-kampanjer för målgruppsanpassning, personalisering och nedtryckning, baserat på [målgrupper](/help/segmentation/types/account-audiences.md) .

## Användningsfall {#use-case}

Använd den här destinationen för att aktivera dina kontomålgrupper för användningsfall inom Account-Based Marketing (ABM). Annonsera till relevanta personas och roller i dina målgruppskonton via DemandBases B2B Demand Side Platform (DSP). Målgruppskonton kan också berikas med tredjepartsdata från Demandbase, för andra användningsfall i senare led av marknadsförings- och säljprocessen.

Använd till exempel Demandbase:s reklamtekniker DSP för att inrikta dig på specifika personer eller roller inom nyckelkonton för ledande generering av leads, eller skapa och utöka inköpsgrupper. Använd Demandbase-målet för att utforska andra användningsfall för att effektivt rikta in dina konton.

Med den här integreringen kan ni också personalisera webbplatsupplevelsen med kontosökning i realtid för att optimera engagemanget.

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilken typ av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Publiker som genererats via Experience Platform [segmenteringstjänst](../../../segmentation/home.md). |
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

Om du vill exportera kontomaterial till Demandbase behöver du följande:

1. Ett Demandbase-konto.
2. En API-token för Demandbase. Du kan generera en API-token med användaren i Demandbase. Om du vill generera en token går du till [Min profil > API-token](https://web.demandbase.com/o/ad/at) när du har loggat in på ditt Demandbase-konto.

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du behörigheten **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Fyll i de obligatoriska fälten och välj **[!UICONTROL Connect to destination]** om du vill autentisera mot målet.

![Lägg till innehavartoken](/help/destinations/assets/catalog/advertising/demandbase/add-bearer-token.png)

* **[!UICONTROL Bearer token]**: Fyll i bearer-token för att autentisera mot målet. Visa [förutsättningarna](#prerequisites) om du vill ha information om hur du hämtar token.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

![Lägg till information om målanslutningen](/help/destinations/assets/catalog/advertising/demandbase/name-and-description.png)

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Entity type]**: Välj **[!UICONTROL Account]** som entitetstyp.

Nu kan ni aktivera era målgrupper i Demandbase.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera kontomålgrupper](/help/destinations/ui/activate-account-audiences.md) om du vill ha instruktioner om hur du aktiverar kontomålgrupper till det här målet.

### Obligatoriska mappningar {#mandatory-mappings}

När du aktiverar målgrupper till målet [!DNL Demandbase] måste du konfigurera följande obligatoriska fältmappningar i mappningssteget:

| Source | Målfält | Beskrivning |
|--------------|--------------|-------------|
| `xdm: accountName` | `xdm: accountName` | Namnet på kontot |
| `xdm: accountOrganization.domain` | `xdm: accountEmailDomain` | Kontoorganisationens e-postdomän |
| `xdm: accountKey.sourceKey` | `Identity: primaryId` | Den primära identifieraren för kontot |

![Demandbase-mappningar](/help/destinations/assets/catalog/advertising/demandbase/demandbase-mapping.png)

Dessa mappningar krävs för att målet ska fungera korrekt och måste konfigureras innan du kan fortsätta med aktiveringsarbetsflödet.

## Ytterligare kommentarer och viktiga bildtexter {#additional-notes}

* Om en kontomålgrupp med samma namn aktiverades tidigare för Demandbase kan du inte aktivera den igen via ett annat dataflöde till Demandbase-målet.
* Om du har exporterat målgrupper till Demandbase och exporterna är framgångsrika i Experience Platform, men inte alla data når Demandbase, kan du ha råkat ut för API-strypning på Demandbase-sidan. Nå ut till dem för klargöranden.
