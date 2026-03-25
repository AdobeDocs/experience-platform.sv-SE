---
title: Målgruppsanalys
description: Se vilka målgrupper kunderna är berättigade till i Customer Journey Analytics.
badgeLimitedAvailability: label="Begränsad tillgänglighet" type="Informative"
exl-id: 81437237-d746-4ce9-b938-7d2541f0ed32
hide: true
hidefromtoc: true
source-git-commit: 20427c4c8826905a77fac04d055d523b12a6f739
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 1%

---

# Målgruppsanalys

Använd målet [!UICONTROL Audience Analysis] för att berika [!DNL Adobe Experience Platform] målgruppsdata till [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html). Du kan välja vilka målgrupper du vill inkludera i de resulterande berikade data. Målgruppskvalifikationer är sedan tillgängliga som dimensioner i [Analysis Workspace](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/home.html) -rapportering.

>[!AVAILABILITY]
>
>Den här destinationen är i en begränsad testfas. Om du är intresserad av att använda den här destinationen kontaktar du ditt Adobe-kontoteam.

## Förutsättningar {#prerequisites}

Du måste ange följande innan du kan använda det här målet:

* Du måste etableras för att kunna använda målplatsen för målgruppsanalys. Om du ännu inte har etablerat dig för att använda det här målet kontaktar du ditt Adobe-kontoteam.
* Du måste vara etablerad för att kunna använda Customer Journey Analytics.
* Du måste ha minst en målgrupp skapad i [!DNL Adobe Experience Platform].

## Identiteter som stöds {#supported-identities}

Målgruppsanalys stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md). Experience Cloud ID (ECID) används vanligtvis.

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Välj målidentiteten för GAID när källidentiteten är ett GAID-namnområde. |
| IDFA | Apple ID för annonsörer | Välj IDFA-målidentitet när din källidentitet är ett IDFA-namnutrymme. |
| ECID | EXPERIENCE CLOUD ID | Ett namnutrymme som representerar ECID. Detta namnområde kan också refereras till av följande alias: Adobe Marketing Cloud ID, [!DNL Adobe Experience Cloud] ID, [!DNL Adobe Experience Platform] ID. Mer information finns i följande dokument på [ECID](/help/identity-service/features/ecid.md). |
| phone_sha256 | Telefonnummer hashas med SHA256-algoritmen | Både oformaterad text och SHA256-hashade telefonnummer stöds av [!DNL Adobe Experience Platform]. Om källfältet innehåller ohashade attribut bör du kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Experience Platform] automatiskt hash-kodar data vid aktiveringen. |
| email_lc_sha256 | E-postadresser som hashas med SHA256-algoritmen | Både oformaterad text och SHA256-hash-adresser stöds av [!DNL Adobe Experience Platform]. Om källfältet innehåller ohashade attribut bör du kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Experience Platform] automatiskt hash-kodar data vid aktiveringen. |
| extern_id | Anpassade användar-ID:n | Välj den här målidentiteten när källidentiteten är ett anpassat namnutrymme. |

{style="table-layout:auto"}

## Målgrupper {#supported-audiences}

Följande typer av målgrupper stöds när du använder det här målet:

| Målgruppsursprung | Stöds | Beskrivning |
|---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Publiker som genererats via Experience Platform [segmenteringstjänst](../../../segmentation/home.md). |
| Alla andra målgrupper kommer | Nej | Den här kategorin omfattar alla målgrupper som kommer utanför målgrupper som genereras via [!DNL Segmentation Service]. Läs om de [olika målgruppernas ursprung](/help/segmentation/ui/audience-portal.md#customize). Några exempel är: <ul><li> anpassade uppladdningsgrupper [importerade](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer,</li><li> lookalike-målgrupper, </li><li> federerade målgrupper, </li><li> målgrupper som har genererats i andra Experience Platform-appar som [!DNL Adobe Journey Optimizer], </li><li> med mera. </li></ul> |

{style="table-layout:auto"}



Målgrupper som stöds av olika typer av målgruppsdata:

| Typ av målgruppsdata | Stöds | Beskrivning | Användningsfall |
|--------------------|-----------|-------------|-----------|
| [Målgrupper](/help/segmentation/types/people-audiences.md) | Ja | Baserat på kundprofiler kan ni inrikta er på specifika grupper av människor för marknadsföringskampanjer. | Ofta köpare, övergivna varukorgar |
| [Kontomålgrupper](/help/segmentation/types/account-audiences.md) | Nej | Rikta er till individer inom specifika organisationer för kontobaserade marknadsföringsstrategier. | B2B-marknadsföring |
| [Prospektera målgrupper](/help/segmentation/types/prospect-audiences.md) | Nej | Rikta er till individer som ännu inte är kunder men som delar egenskaper med er målgrupp. | Prospektera med data från tredje part |
| [Datauppsättningsexport](/help/catalog/datasets/overview.md) | Nej | Samlingar med strukturerade data lagrade i datasjön [!DNL Adobe Experience Platform]. | Arbetsflöden för rapportering, datavetenskap |

{style="table-layout:auto"}


## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en målgrupp med de identifierare (namn, telefonnummer eller andra) som används i målplatsen för målgruppsanalys. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. När en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedåt till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Konfigurera nytt mål {#configure-destination}

>[!IMPORTANT]
>
>Om du vill skapa mål behöver du behörigheten **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill skapa det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md).

### Destinationsinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

* **[!UICONTROL Name]**: Målnamnet.
* **[!UICONTROL Description]**: Målbeskrivningen.
* **[!UICONTROL Datastream ID]**: Det dataström-ID som du vill utöka med kvalificerade målgrupper. Du kan hämta detta ID i [Datastreams-hanteraren](/help/datastreams/overview.md).
* **[!UICONTROL Integration alias]**: Integreringsalias.

### Aviseringar {#alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

* **[!UICONTROL Activation Skipped Rate Exceed]**: Meddela när aktiveringen har hoppat över ett tröskelvärde.

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

### Styrningspolicy och verkställighetsåtgärder {#governance-policy}

Med det här valfria avsnittet kan du definiera dina datastyrningsprinciper och se till att de data som används är kompatibla när målgrupper skickas och är aktiva.

Välj **[!UICONTROL Create]** när du är klar med valet av marknadsföringsåtgärder för målet.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
>
>För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

När målet har skapats kan du aktivera önskade målgrupper för målet.

1. Om du inte redan befinner dig på det mål du skapat kan du hitta det igen genom att gå till **[!UICONTROL Destinations]** > **[!UICONTROL Browse]**.
1. Välj **[!UICONTROL Activate audiences]**.
1. Välj vilka målgrupper du vill analysera kvalifikationer för. När du är klar väljer du **[!UICONTROL Next]**.
1. Granska målkonfigurationen och målgruppsinställningarna och välj sedan **[!UICONTROL Finish]**.

Du kan lägga till fler målgrupper att analysera i framtiden genom att gå tillbaka till sidan **[!UICONTROL Activate audiences]**. Du kan inte ta bort målgrupper när de har aktiverats.
