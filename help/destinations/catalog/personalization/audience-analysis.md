---
title: Målgruppsanalys
description: Se vilka målgrupper kunderna är berättigade till i Customer Journey Analytics.
badgeLimitedAvailability: label="Begränsad tillgänglighet" type="Informative"
exl-id: 81437237-d746-4ce9-b938-7d2541f0ed32
hide: true
hidefromtoc: true
source-git-commit: 4bd94c292a13a80405a3d726295ebd6eaf86aaaa
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 0%

---

# Målgruppsanalys

Med målet [!UICONTROL Audience Analysis] kan du berika Adobe Experience Platform målgruppsdata till [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html). Du kan välja vilka målgrupper du vill inkludera i de resulterande berikade data. Målgruppskvalifikationer är sedan tillgängliga som dimensioner i [Analysis Workspace](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/home.html) -rapportering.

>[!AVAILABILITY]
>
>Den här destinationen är i en begränsad testfas. Om du är intresserad av att använda den här destinationen kontaktar du ditt Adobe-kontoteam.

## Förhandskrav

Du måste ange följande innan du kan använda det här målet:

* Du måste etableras för att kunna använda målplatsen för målgruppsanalys. Om du ännu inte har etablerat dig för att använda det här målet kontaktar du ditt Adobe-kontoteam.
* Du måste vara etablerad för att kunna använda Customer Journey Analytics.
* Du måste ha minst en målgrupp som skapats i Adobe Experience Platform.

## Identiteter som stöds

Målgruppsanalys stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md). Experience Cloud ID (ECID) används vanligtvis.

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Välj målidentiteten för GAID när källidentiteten är ett GAID-namnområde. |
| IDFA | Apple ID för annonsörer | Välj IDFA-målidentitet när din källidentitet är ett IDFA-namnutrymme. |
| ECID | EXPERIENCE CLOUD ID | Ett namnutrymme som representerar ECID. Detta namnutrymme kan även refereras av följande alias:&quot;Adobe Marketing Cloud ID&quot;,&quot;Adobe Experience Cloud ID&quot;,&quot;Adobe Experience Platform ID&quot;. Mer information finns i följande dokument på [ECID](/help/identity-service/features/ecid.md). |
| phone_sha256 | Telefonnummer hashas med SHA256-algoritmen | Både oformaterad text och SHA256-hashade telefonnummer stöds av Adobe Experience Platform. Om källfältet innehåller ohashade attribut bör du kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Experience Platform] automatiskt hash-kodar data vid aktiveringen. |
| email_lc_sha256 | E-postadresser som hashas med SHA256-algoritmen | Både oformaterad text och SHA256-hashade e-postadresser stöds av Adobe Experience Platform. Om källfältet innehåller ohashade attribut bör du kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Experience Platform] automatiskt hash-kodar data vid aktiveringen. |
| extern_id | Anpassade användar-ID:n | Välj den här målidentiteten när källidentiteten är ett anpassat namnutrymme. |

{style="table-layout:auto"}

## Målgrupper

Följande typer av målgrupper stöds när du använder det här målet:

| Målgruppsursprung | Stöds | Beskrivning |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Publiker som genererats via Experience Platform [segmenteringstjänst](../../../segmentation/home.md). |
| Anpassade överföringar | ✓ | Publikerna [importerade](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en målgrupp med de identifierare (namn, telefonnummer eller andra) som används i målplatsen för målgruppsanalys. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. När en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedåt till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Konfigurera nytt mål

>[!IMPORTANT]
> 
>Om du vill skapa mål behöver du behörigheten **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill skapa det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md).

### Destinationsinformation

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

* **[!UICONTROL Name]**: Målnamnet.
* **[!UICONTROL Description]**: Målbeskrivningen.
* **[!UICONTROL Datastream ID]**: Det dataström-ID som du vill utöka med kvalificerade målgrupper. Du kan hämta detta ID i [Datastreams-hanteraren](/help/datastreams/overview.md).
* **[!UICONTROL Integration alias]**: Integreringsalias.

### Aviseringar

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

* **[!UICONTROL Activation Skipped Rate Exceed]**: Meddela när aktiveringen har hoppat över ett tröskelvärde.

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

### Styrningspolicy och verkställighetsåtgärder

I det här valfria avsnittet kan du definiera dina datastyrningsprinciper och se till att de data som används är kompatibla när målgrupper skickas och är aktiva.

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
