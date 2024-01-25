---
title: Adobe Advertising Cloud DSP
description: Adobe Advertising Cloud DSP är en integrerad målgrupp för Adobe Real-time Customer Data Platform, vilket gör att ni kan dela autentiserade förstahandsmålgrupper med godkända annonsörer och användare för kampanjaktivering.
exl-id: 11ff7797-a9c6-4334-b843-ae9df9a48e54
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 0%

---

# Adobe Advertising Cloud DSP

## Översikt {#overview}

Adobe Advertising Cloud [!DNL Demand-Side Platform] (DSP) kan ni dela autentiserade förstapartsmålgrupper med godkända annonsörer och användare för kampanjaktivering med DSP. Mer information om Real-Time CDP integrering med DSP finns i [Aktivera autentiserade målgrupper från målgruppskällor](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-about.html).

>[!IMPORTANT]
>
>Den här sidan skapades av DSP team. Om du har frågor eller uppdateringsfrågor kontaktar du Advertising Cloud support direkt på `adcloud_support@adobe.com`.

## Användningsfall {#use-cases}

För att du bättre ska förstå hur och när du ska använda Advertising Cloud DSP-destinationen finns exempel på användningsområden som Adobe Experience Platform-kunder kan lösa genom att använda den här destinationen.

### Användning av varumärken för annonsering

En webbutik vill återannonsera sina värdefulla kunder genom en webbannonskampanj utan att använda cookies för målinriktning. Återförsäljaren delar en målgrupp bestående av de hashas-ID:n som tillhör dess värdefulla kunder från dess Adobe Real-time Customer Data Platform-konto (Real-Time CDP) till dess DSP. DSP konverterar sedan hash-kodade e-post-ID:n till autentiserade [!DNL RampIDs] genom ett partnerskap mellan DSP och LiveRamp. Resultatet [!DNL RampIDs] kan användas i en webbannonskampanj för att rikta sig till målgruppen.

### Användningsexempel

En mediebyrå med ett DSP konto kör en återannonskampanj för sina kunders räkning, ett ledande varumärke inom turismbranschen. Varumärket vill rikta om alla sina gäster det senaste året med ett nytt kampanjerbjudande. Varumärket är värd för all gästinformation i [!DNL Real-Time CDP]. Varumärket kan dela en målgrupp som består av gästernas hash-kodade e-post-ID:n [!DNL Real-Time CDP] konto hos mediebyråens DSP för att omdirigera gästerna via en mediekampanj.

## Förutsättningar {#prerequisites}

* DSP på konto- och kampanjnivå för att möjliggöra målgruppsdelning med [!DNL LiveRamp RampID]som översätter kunddata till [!DNL RampIDs] för att skapa målgruppssegment. Ditt DSP-kontoteam kommer att utföra den här konfigurationen. [!DNL RampID] via ett partnerskap mellan DSP och [!DNL LiveRamp]och du behöver inte en egen [!DNL LiveRamp] medlemskap för att använda det.
* Experience Cloud organisation-ID för Experience Platform-kontot. Du kan hitta ditt ID på din [!DNL Real-Time CDP] användarprofilsida.
* A [[!DNL Real-Time CDP] källa i DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html) för att ta emot målgrupper för kampanjaktivering. Din DSP skapar källan med ditt Experience Cloud organisation-ID.
* Källnyckeln för DSP eller annonsören, som genereras när en [[!DNL Real-Time CDP] källan skapas i DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). Ditt DSP kommer att dela nyckeln med dig. Du kommer att använda det i Experience Platform för att skapa en målanslutning till Advertising Cloud DSP-målet, som [förklaras nedan](#authenticate).
* Kunddata som består av e-post eller hashad e-post.

## Identiteter som stöds {#supported-identities}

Adobe Advertising Cloud DSP-målet stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| email_lc_sha256 | E-postadresser som hashas med SHA256-algoritmen | Experience Platform har stöd för både oformaterad text och SHA256-hashed-e-postadresser. När källfältet innehåller ohash-kodade attribut markerar du **[!UICONTROL Apply transformation]** att Experience Platform automatiskt ska hash-koda data vid aktiveringen. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

I följande tabell finns information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en målgrupp med de identifierare (e-post eller hashad e-post) som används i Advertising Cloud DSP-målet. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. När en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutaren uppdateringen nedströms till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions) för Experience Platform. Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

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

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden på [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.
>* Exportera *identiteter* behöver du **[!UICONTROL View Identity Graph]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). <br> ![Markera det identitetsnamnutrymme som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera det identitetsnamnutrymme som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera profiler och målgrupper för att strömma målgruppernas exportdestinationer](/help/destinations/ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

## Validera dataexport {#exported-data}

Kontrollera följande om du vill verifiera att datapubliken delats med Advertising Cloud:

* Dataflödet i [!DNL Real-Time CDP] målet har slutförts.

* I DSP är målgruppen tillgänglig när du skapar eller redigerar en målgrupp från [!UICONTROL Audiences] > [!UICONTROL All Audiences] eller från [!UICONTROL Audience Targeting] i placeringsinställningarna. Publiken ska vara synlig i [!UICONTROL Adobe Segments] under [!UICONTROL Real-Time CDP] mapp.

![Real-Time CDP målgrupper DSP målgruppsinställningar](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, se [Datastyrning - översikt](/help/data-governance/home.md).
