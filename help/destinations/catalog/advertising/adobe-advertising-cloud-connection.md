---
title: Adobe Advertising Cloud DSP-anslutning
description: Adobe Advertising Cloud DSP är ett integrerat mål för [!DNL Adobe Real-time Customer Data Profile]så att ni kan dela autentiserade förstahandssegment med godkända annonsörer och användare för kampanjaktivering.
exl-id: 11ff7797-a9c6-4334-b843-ae9df9a48e54
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '988'
ht-degree: 0%

---

# Adobe Advertising Cloud DSP-anslutning

## Översikt {#overview}

Adobe Advertising Cloud [!DNL Demand-Side Platform] (DSP) kan ni dela autentiserade förstapartssegment med godkända annonsörer och användare för kampanjaktivering med DSP. Mer information om Real-Time CDP integrering med DSP finns i [Om aktivering av autentiserade segment från målgruppskällor](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-about.html).

>[!IMPORTANT]
>
>Den här sidan skapades av DSP team. Kontakta Advertising Cloud support på `adcloud_support@adobe.com`.

## Användningsfall {#use-cases}

För att du bättre ska förstå hur och när du ska använda Advertising Cloud DSP-destinationen finns exempel på användningsområden som Adobe Experience Platform-kunder kan lösa genom att använda den här destinationen.

### Användning av varumärken för annonsering

En webbutik vill återannonsera sina värdefulla kunder genom en webbannonskampanj utan att använda cookies för målinriktning. Återförsäljaren delar ett segment som består av det hashas-baserade e-post-ID:t för dess värdefulla kunder från dess [!DNL Real-Time CDP] till DSP konto. DSP konverterar sedan hash-kodade e-post-ID:n till autentiserade [!DNL RampIDs] genom ett partnerskap mellan DSP och LiveRamp. Resultatet [!DNL RampIDs] kan användas i en webbannonskampanj för att rikta sig till målgruppen.

### Användningsexempel

En mediebyrå med ett DSP konto kör en återannonskampanj för sina kunders räkning, ett ledande varumärke inom turismbranschen. Varumärket vill rikta om alla sina gäster det senaste året med ett nytt kampanjerbjudande. Varumärket är värd för all gästinformation i [!DNL Real-Time CDP]. Varumärket kan dela ett segment som består av gästernas hash-kodade e-post-ID:n från dess [!DNL Real-Time CDP] konto hos mediebyråens DSP för att omdirigera gästerna via en mediekampanj.

## Förutsättningar {#prerequisites}

* DSP på konto- och kampanjnivå för att aktivera segmentdelning med [!DNL LiveRamp RampID]som översätter kunddata till [!DNL RampIDs] för att skapa målgruppssegment. Ditt DSP kommer att utföra den här konfigurationen.
* Experience Cloud organisation-ID för Experience Platform-kontot. Du kan hitta ditt ID på din [!DNL Real-Time CDP] användarprofilsida.
* A [[!DNL Real-Time CDP] källa i DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html) för att få segment för kampanjaktivering. Din DSP skapar källan med ditt Experience Cloud organisation-ID.
* Källnyckeln för DSP eller annonsören, som genereras när en [[!DNL Real-Time CDP] källan skapas i DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). Ditt DSP kommer att dela nyckeln med dig. Du kommer att använda det i Experience Platform för att skapa en målanslutning till Advertising Cloud DSP-målet, som [förklaras nedan](#authenticate).
* Kunddata som består av e-post eller hash-kodade e-postmeddelanden.

## Identiteter som stöds {#supported-identities}

Adobe Advertising Cloud DSP-målet stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| email_lc_sha256 | E-postadresser som hash-kodats med SHA256-algoritmen | Experience Platform har stöd för både oformaterad text och SHA256-hashed-e-postadresser. När källfältet innehåller ohash-kodade attribut markerar du **[!UICONTROL Apply transformation]** att Experience Platform automatiskt ska hash-koda data vid aktiveringen. |

{style=&quot;table-layout:auto&quot;}

## Exportera typ och frekvens {#export-type-frequency}

I följande tabell finns information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Segment export]** | Du exporterar alla medlemmar i ett segment (målgrupp) med de identifierare (e-post eller hashade e-post) som används i Advertising Cloud DSP-målet. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. När en profil uppdateras i Experience Platform baserat på segmentutvärdering, skickar kopplingen uppdateringen nedåt till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions) för Experience Platform. Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Följ instruktionerna för att ansluta till målet [skapa en målanslutning](/help/destinations/ui/connect-destination.md) med användargränssnittet i Experience Platform. I arbetsflödet för målkonfiguration fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Om du vill ansluta till målet anger du följande parameter i [!UICONTROL Connection type] och sedan markera **[!UICONTROL Connect to destination]**.:

* **[!UICONTROL Account or Advertiser Key]**: Detta [!UICONTROL Source Key] genereras när en [[!DNL Real-Time CDP] källan skapas i DSP användargränssnitt](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). Ditt DSP-kontoteam delar nyckeln med dig när de har skapat källan.

![Fält för anslutningstyp](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.

![Målinformationsfält](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om status för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med hjälp av användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
> 
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Läs [Aktivera profiler och segment för att direktuppspela segmentexportmål](/help/destinations/ui/activate-segment-streaming-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

## Validera dataexport {#exported-data}

Kontrollera följande om du vill verifiera att datasegmentet delades med Advertising Cloud:

* Dataflödet i [!DNL Real-Time CDP] målet har slutförts.

* I DSP är segmentet tillgängligt när du skapar eller redigerar en målgrupp från [!UICONTROL Audiences] > [!UICONTROL All Audiences] eller från [!UICONTROL Audience Targeting] i placeringsinställningarna. Segmentet ska vara synligt i [!UICONTROL Adobe Segments] under [!UICONTROL Real-Time CDP] mapp.

![Real-Time CDP segment DSP målgruppsinställningar](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, se [Datastyrning - översikt](/help/data-governance/home.md).
