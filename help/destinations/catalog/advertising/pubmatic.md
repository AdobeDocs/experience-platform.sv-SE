---
title: PubMatic Connect
description: PubMatic maximerar kundvärdet genom att leverera framtidens programstyrda digitala marknadsföringskedja. PubMatic Connect kombinerar plattformsteknik och dedikerad tjänst för att förbättra hur lager och data paketeras och hanteras.
last-substantial-update: 2023-12-14T00:00:00Z
exl-id: 21e07d2c-9a6a-4cfa-a4b8-7ca48613956c
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---

# Mål för PubMatic Connect {#pubmatic-connect}

## Översikt {#overview}

Använd [!DNL PubMatic Connect] för att maximera kundens värde genom att leverera framtidens programstyrda leveranskedja för digital marknadsföring. [!DNL PubMatic Connect] kombinerar plattformsteknik och dedikerad tjänst för att förbättra hur lager och data paketeras och överförs.

Använd det här målet för att skicka målgruppsdata till [!DNL PubMatic Connect] plattform.

>[!IMPORTANT]
>
>Målanslutnings- och dokumentationssidan skapas och underhålls av [!DNL PubMatic] team. Om du har frågor eller uppdateringsfrågor kan du kontakta dem direkt på `support@pubmatic.com`.

## Användningsfall {#use-cases}

För att du bättre ska förstå hur och när du ska använda [!DNL PubMatic Connect] mål, här är ett exempel på användning som Adobe Experience Platform-kunder kan lösa genom att använda den här destinationen.

### Rikta användarna mot mobiler, webben och CTV-plattformar {#targeting}

Utgivare eller dataleverantörer vill skicka målgrupper från Adobe Experience Platform till [!DNL PubMatic Connect] målgruppsanpassning för användare på mobil-, webb- och CTV-plattformar med ett stort antal identifierare.

## Förhandskrav {#prerequisites}

Tala med [!DNL PubMatic] Account Manager för att säkerställa att ditt konto är korrekt konfigurerat och har stöd för att introducera målgruppssegment. De ser också till att du har all information som behövs för att använda destinationen och för att ge dig support under installationen.

## Identiteter som stöds {#supported-identities}

[!DNL PubMatic Connect] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
| --------------- | ------ | --- |
| GAID | GOOGLE ADVERTISING ID | Välj målidentiteten för GAID när källidentiteten är ett GAID-namnområde. |
| IDFA | Apple ID för annonsörer | Välj IDFA-målidentitet när din källidentitet är ett IDFA-namnutrymme. |
| extern_id | Anpassade användar-ID:n | Välj den här målidentiteten när källidentiteten är ett anpassat namnutrymme. |

{style="table-layout:auto"}

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilken typ av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
| --- | --------- | ------ |
| [!DNL Segmentation Service] | ✓ | Målgrupper som skapats genom Experience Platform [Segmenteringstjänst](../../../segmentation/home.md). |
| Anpassade överföringar | ✓ | Målgrupper [importerad](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
| --- | --- | --- |
| Exporttyp | **[!UICONTROL Segment export]** | Du exporterar alla medlemmar i ett segment (publik) med de identifierare (namn, telefonnummer eller andra) som används i PubMatic Connect-målet. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. När en profil uppdateras i Experience Platform baserat på segmentutvärdering, skickar kopplingen uppdateringen nedåt till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
>
> Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för målkonfiguration fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Om du vill autentisera mot målet fyller du i de obligatoriska fälten och väljer **[!UICONTROL Connect to destination]**.

![Hur man autentiserar](../../assets/catalog/advertising/pubmatic/authenticate-destination.png)

- **[!UICONTROL Bearer token]**: Fyll i bearer-token för att autentisera mot målet.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

![Destinationsinformation](../../assets/catalog/advertising/pubmatic/destination-details.png)

- **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
- **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
- **[!UICONTROL Data partner ID]**: Det ID för datapartner som är konfigurerat i din [!DNL PubMatic] konto för den här integreringen.
- **[!UICONTROL Default country code]**: Standardlandskoden som ska användas för alla identiteter om ingen anges i profilen.
- **[!UICONTROL Account ID]**: din [!DNL PubMatic Connect] konto-ID.
- **[!UICONTROL Account type]**: Kontotypen för din [!DNL PubMatic] plattform. Tala med [!DNL PubMatic] kontoansvarig om du har några frågor att välja på. De tillgängliga alternativen är:
   - [!UICONTROL PUBLISHER]
   - [!UICONTROL DEMAND_PARTNER]
   - [!UICONTROL BUYER]

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden på [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
>
> - För att aktivera data behöver du **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.
>
> - Exportera _identiteter_ behöver du **[!UICONTROL View Identity Graph]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). <br> ![Markera det identitetsnamnutrymme som är markerat i arbetsflödet för att aktivera målgrupper till mål.](../../assets/overview/export-identities-to-destination.png "Markera det identitetsnamnutrymme som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera profiler och segment för att direktuppspela segmentexportmål](/help/destinations/ui/activate-segment-streaming-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

### Mappa attribut och identiteter {#map}

Välja källfält:

- Välj en identifierare (vanligtvis namnutrymmen som IDFA eller ett anpassat ID-namnutrymme).

Markera målfält:

- Tala med [!DNL PubMatic] Kontohanteraren för att få information om vilken UID-typ som ska vara korrekt under det här steget.
- Välj [!DNL PubMatic UID] typnummer som matchar den identifierare som du valde i det första steget.

![Mappa attribut och identiteter](../..//assets/catalog/advertising/pubmatic/export-identities-to-destination.png)

## Exporterade data/Validera dataexport {#exported-data}

The [!DNL PubMatic] Med användargränssnittet kan du kontrollera om data har skickats korrekt och att segmenten är tillgängliga. Det kan ta upp till 24 timmar efter att data har skickats för [!DNL PubMatic] Gränssnittet ska uppdateras.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, läs [Datastyrning - översikt](/help/data-governance/home.md).
