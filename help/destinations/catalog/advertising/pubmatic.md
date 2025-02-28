---
title: PubMatic Connect
description: PubMatic maximerar kundvärdet genom att leverera framtidens programstyrda digitala marknadsföringskedja. PubMatic Connect kombinerar plattformsteknik och dedikerad tjänst för att förbättra hur lager och data paketeras och hanteras.
last-substantial-update: 2025-02-12T00:00:00Z
exl-id: 21e07d2c-9a6a-4cfa-a4b8-7ca48613956c
source-git-commit: 2041c06e660e24f63d4c44adc0e8f3082bb007ae
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 0%

---


# Mål för PubMatic Connect {#pubmatic-connect}

## Översikt {#overview}

Använd [!DNL PubMatic Connect] för att maximera kundens värde genom att leverera framtidens programbaserade leveranskedja för digital marknadsföring. [!DNL PubMatic Connect] kombinerar plattformsteknik och dedikerad tjänst för att förbättra hur lager och data paketeras och överförs.

Det finns två tillgängliga mål som gör att du kan skicka målgruppsdata till PubMatic Connect-plattformen. De skiljer sig något när det gäller funktionalitet:

1. PubMatic Connect

   Under den initiala aktiveringen registreras målgrupperna automatiskt i PubMatic-plattformen och det interna Adobe Experience Platform-id:t används för mappning.

2. PubMatic Connect (Custom Audience ID Mapping)

   På den här platsen kan du välja att manuellt lägga till ett mappnings-ID under aktiveringsarbetsflödet. Använd det här målet när data ska skickas till befintliga målgrupper i PubMatic-plattformen eller om ett anpassat &#39;Source Audience ID&#39; krävs.

![Visa sida vid sida om de två PubMatic-anslutningarna i målkatalogen.](/help/destinations/assets/catalog/advertising/pubmatic/two-pubmatic-connectors-side-by-side.png)

>[!IMPORTANT]
>
> Målanslutningen och dokumentationssidan skapas och underhålls av [!DNL PubMatic]-teamet. Om du har frågor eller uppdateringsförfrågningar kontaktar du dem direkt på `support@pubmatic.com`.

## Användningsfall {#use-cases}

För att du bättre ska kunna förstå hur och när du ska använda målet [!DNL PubMatic Connect] finns det ett exempel på användning som Adobe Experience Platform-kunder kan lösa genom att använda det här målet.

### Rikta användarna mot mobiler, webben och CTV-plattformar {#targeting}

Utgivare eller dataleverantörer vill skicka målgrupper från Adobe Experience Platform till [!DNL PubMatic Connect] för målanvändare på mobil-, webb- och CTV-plattformar med ett stort antal identifierare.

## Förhandskrav {#prerequisites}

Tala med din kontohanterare för [!DNL PubMatic] för att kontrollera att ditt konto är korrekt konfigurerat och har stöd för introduktion av målgruppssegment. De ser också till att du har all information som behövs för att använda destinationen och för att ge dig support under installationen.

## Identiteter som stöds {#supported-identities}

[!DNL PubMatic Connect] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
| --------------- | ------------------------ | ------------------------------------------------------------------------------- |
| GAID | GOOGLE ADVERTISING ID | Välj målidentiteten för GAID när källidentiteten är ett GAID-namnområde. |
| IDFA | Apple ID för annonsörer | Välj IDFA-målidentitet när din källidentitet är ett IDFA-namnutrymme. |
| extern_id | Anpassade användar-ID:n | Välj den här målidentiteten när källidentiteten är ett anpassat namnutrymme. |

{style="table-layout:auto"}

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilken typ av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
| --------------------------- | --------- | -------------------------------------------------------------------------------------------------------------------------- |
| [!DNL Segmentation Service] | ✓ | Publiker som genererats via Experience Platform [segmenteringstjänst](../../../segmentation/home.md). |
| Anpassade överföringar | ✓ | Publikerna [importerade](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
| ---------------- | ------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Exporttyp | **[!UICONTROL Segment export]** | Du exporterar alla medlemmar i ett segment (publik) med de identifierare (namn, telefonnummer eller andra) som används i PubMatic Connect-målet. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. När en profil uppdateras i Experience Platform baserat på segmentutvärdering, skickar kopplingen uppdateringen nedåt till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
>
> Om du vill ansluta till målet måste du ha **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för målkonfiguration fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Fyll i de obligatoriska fälten och välj **[!UICONTROL Connect to destination]** om du vill autentisera mot målet.

![Autentisera](../../assets/catalog/advertising/pubmatic/authenticate-destination.png)

- **[!UICONTROL Bearer token]**: Fyll i bearer-token för att autentisera mot målet.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

![Målinformation](../../assets/catalog/advertising/pubmatic/destination-details.png)

- **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
- **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
- **[!UICONTROL Data partner ID]**: Det ID för datapartner som har konfigurerats i ditt [!DNL PubMatic]-konto för den här integreringen.
- **[!UICONTROL Default country code]**: Standardlandskoden som ska användas för alla identiteter om ingen anges i profilen.
- **[!UICONTROL Account ID]**: Ditt konto-ID för [!DNL PubMatic Connect].
- **[!UICONTROL Account type]**: Kontotypen för ditt [!DNL PubMatic]-plattformskonto. Tala med din [!DNL PubMatic]-kontoansvarige om du har några frågor att välja på. De tillgängliga alternativen är:
   - [!UICONTROL PUBLISHER]
   - [!UICONTROL DEMAND_PARTNER]
   - [!UICONTROL BUYER]

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
>
> - För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>
> - Om du vill exportera _identiteter_ måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](../../assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera profiler och segment för att direktuppspela segmentexportmål](/help/destinations/ui/activate-segment-streaming-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

### Mappa attribut och identiteter {#map}

Välja källfält:

- Välj en identifierare (vanligtvis namnutrymmen som IDFA eller ett anpassat ID-namnutrymme).

Markera målfält:

- Tala med din kontohanterare för [!DNL PubMatic] för att få information om vilken UID-typ som ska vara korrekt under det här steget.
- Välj det [!DNL PubMatic UID]-typnummer som matchar den identifierare som du valde i det första steget.

![Mappa attribut och identiteter](../..//assets/catalog/advertising/pubmatic/export-identities-to-destination.png)

### Målgruppsplanering

Om du använder målet PubMatic Connect (Custom Audience ID Mapping) måste du ange ett mappnings-ID för varje målgrupp som motsvarar &quot;Source Audience ID&quot; i PubMatic-plattformen.

![Målgruppsplanering](../..//assets/catalog/advertising/pubmatic/audience-scheduling-mapping-id.png)

## Exporterade data/Validera dataexport {#exported-data}

Med användargränssnittet i [!DNL PubMatic] kan du kontrollera om data har skickats korrekt och om segmenten är tillgängliga. Det kan ta upp till 24 timmar efter att data har skickats för att [!DNL PubMatic]-gränssnittet ska uppdateras.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Översikt över datastyrning](/help/data-governance/home.md).
