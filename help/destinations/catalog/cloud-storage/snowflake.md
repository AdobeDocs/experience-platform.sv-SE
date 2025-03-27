---
title: Snowflake
description: Exportera data till ditt Snowflake-konto med privata listor.
hide: true
hidefromtoc: true
badgeBeta: label="Beta" type="Informative"
source-git-commit: 2893356e36fde4759ffe76e01296fcb8811ab8e7
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 3%

---


# Snowflake {#snowflake-destination}

>[!IMPORTANT]
>
>Den här destinationsanslutningen är i betaversion och endast tillgänglig för vissa kunder. Kontakta din Adobe-representant om du vill få åtkomst.

## Översikt {#overview}

Exportera data till ditt Snowflake-konto med privata listor.

## Förhandskrav {#prerequisites}

Innan du konfigurerar din Snowflake-anslutning måste du kontrollera att följande krav uppfylls:

* Du har åtkomst till ett [!DNL Snowflake]-konto.
* Ditt Snowflake-konto prenumererar på privata listor. Du eller någon på ditt företag som har kontoadministratörsbehörighet för Snowflake kan konfigurera detta.

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilka typer av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Publiker som genererats via Experience Platform [segmenteringstjänst](../../../segmentation/home.md). |
| Anpassade överföringar | ✓ | Publikerna [importerade](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en målgrupp med identifierarna (namn, telefonnummer eller andra) som används i målet [!DNL Snowflake]. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Om du vill autentisera till målet väljer du **[!UICONTROL Connect to destination]**.

![Exempelbild som visar hur du autentiserar till målet](../../assets/catalog/cloud-storage/snowflake/authenticate-destination.png)

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

![Exempelbild som visar hur du fyller i information för ditt mål](../../assets/catalog/cloud-storage/snowflake/configure-destination-details.png)

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Snowflake Account ID]**: Ditt Snowflake-konto-ID. Exempel: `adobe-123456`.
* **[!UICONTROL Account acknowledgment]**: Växla på bekräftelsen för ditt konto-ID på Snowflake för att bekräfta att ditt konto-ID är korrekt och tillhör dig.

>[!IMPORTANT]
>
> Specialtecken som används i målnamnet och Experience Platform-sandlådans namn konverteras automatiskt till understreck (`_`) i Snowflake. Undvik förvirring genom att inte använda några specialtecken i mål- och sandlådans namn.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera profiler och målgrupper för att direktuppspela målgruppsexportdestinationer](/help/destinations/ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

### Mappningsattribut {#map}

Snowflake-målet stöder mappning av profilattribut till anpassade attribut.

![Bilden på användargränssnittet för plattformen visar mappningsskärmen för Snowflake-målet.](../../assets/catalog/cloud-storage/snowflake/mapping.png)

Målattributen skapas automatiskt i Snowflake med det attributnamn som du anger i fältet **[!UICONTROL Attribute name]**.

## Exporterade data/Validera dataexport {#exported-data}

Kontrollera ditt Snowflake-konto för att bekräfta att data exporterades korrekt.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Översikt över datastyrning](/help/data-governance/home.md).