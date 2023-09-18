---
keywords: mobil;mål för mobilengagemang;LINE;LINE mobile engagement destination
title: LINJEanslutning
description: Med LINE-destinationen kan ni lägga till profiler till era plattformar och leverera personaliserade upplevelser till anslutna användare.
last-substantial-update: 2022-11-08T00:00:00Z
exl-id: 9981798a-61f2-4a09-9a33-57e63eb36d43
source-git-commit: 05e996f9e33e0d8be3d15a9ab3baaaf6d8152b5a
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 0%

---

# [!DNL LINE] anslutning

## Översikt {#overview}

[[!DNL LINE]](https://line.me/en/) är en populär kommunikationsplattform som knyter samman människor, tjänster och information och har växt från en chattapp till ett nav för underhållning, sociala aktiviteter och dagliga aktiviteter.

Detta [!DNL Adobe Experience Platform] [mål](/help/destinations/home.md) utnyttjar [[!DNL LINE] MeddelandeAPI](https://developers.line.biz/en/reference/messaging-api/). Du kan aktivera profiler från dina Experience Platform-målgrupper som anslutningar inom [!DNL LINE] för era behov.

[!DNL LINE] använder Bearer Tokens som autentiseringsmekanism för att kommunicera med [!DNL LINE] MeddelandeAPI. Instruktioner för hur du autentiserar [!DNL LINE] -instansen är längre ned, inom [Autentisera till mål](#authenticate) -avsnitt.

## Användningsfall {#use-cases}

Som marknadsförare kan ni inrikta er på användare i en mobil engagemangsdestination med inbyggda målgrupper [!DNL Adobe Experience Platform]. Dessutom kan ni leverera personaliserade upplevelser till dem utifrån deras attribut [!DNL Adobe Experience Platform] profiler så snart som målgrupper och profiler uppdateras i [!DNL Adobe Experience Platform].

## Förutsättningar {#prerequisites}

### [!DNL LINE] krav {#prerequisites-destination}

Observera följande krav i [!DNL LINE]för att exportera data från Platform till [!DNL LINE] konto:

#### Du måste ha en [!DNL LINE] konto {#prerequisites-account}

Du måste registrera dig och skapa en [!DNL LINE] om du inte redan har ett konto. Skapa ett konto:

1. Navigera till [!DNL LINE] [kontoinloggning](https://account.line.biz/login?redirectUri=https%3A%2F%2Fmanager.line.biz%2F) page
2. Välj **[!UICONTROL Create an account]**.

#### Samla [!DNL LINE channel access token (long-lived)] från [!DNL LINE] utvecklarkonsol {#gather-credentials}

Så här tillåter du att plattformen får åtkomst [!DNL LINE] behöver du *[!DNL Channel access token (long-lived)]* från önskat [!DNL LINE] *MeddelandeAPI* kanal.

1. Logga in med [!DNL LINE] konto till [[!DNL LINE] Utvecklarkonsol](https://developers.line.biz/console).
1. Gå sedan till *[!DNL Providers]* väljer du *[!DNL Provider]* av intresse och slutligen välja *MeddelandeAPI* för att komma åt inställningarna. Om du använder utvecklarkonsolen för första gången följer du [[!DNL LINE] dokumentation](https://developers.line.biz/en/docs/messaging-api/getting-started/) för att slutföra de steg som krävs för att skapa en leverantör.
1. Till sist navigerar du till ***[!DNL Channel access token]*** och kopiera ***[!DNL Channel access token (long-lived)]*** värde som krävs inom [Autentisera till mål](#authenticate) steg.

| Autentiseringsuppgifter | Beskrivning | Exempel |
| --- | --- | --- |
| `[!DNL Channel access token (long-lived)]` | Din [!DNL LINE Channel access token (long-lived)]. | `aaa2112XSMWqLXR7..........nyilFU=` |

Se [[!DNL LINE] dokumentation](https://developers.line.biz/en/docs/messaging-api/getting-started/) om du vill ha hjälp med att skapa en kanal eller lägga till en kanal i en befintlig [!DNL LINE] via [!DNL LINE] utvecklarkonsol.

## Identiteter som stöds {#supported-identities}

[!DNL LINE] stöder uppdatering och export av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/namespaces.md).

| Målidentitet | Beskrivning |
|---|---|
| ID för annonsörer (IFA) | Markera ID:t för annonsörer (IFA:n) som mål-ID när källidentiteten är IFA *(Apple ID för annonsörer)* eller GAID *(Google Advertising ID), namnutrymmen. |
| Användar-ID för RAD | Välj användar-ID-målidentiteten när källidentiteterna är LINE-användar-ID:n. |

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla medlemmar i en målgrupp med identifierarna (namn, telefonnummer eller andra) som används i [!DNL LINE] mål. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
>
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

Inom **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** sök efter [!DNL LINE]. Du kan även hitta den under **[!UICONTROL Mobile engagement]** kategori.

### Autentisera till mål {#authenticate}

Om du vill autentisera mot målet väljer du **[!UICONTROL Connect to destination]**.
![Skärmbild av användargränssnittet för plattformen som visar hur man autentiserar.](../../assets/catalog/mobile-engagement/line/authenticate-destination.png)

Fyll i de obligatoriska fälten nedan.
* **[!UICONTROL Bearer token]**: din [!DNL LINE Channel access token (long-lived)] från [!DNL LINE] utvecklarkonsol. Se [samla in autentiseringsuppgifter](#gather-credentials) -avsnitt.

Om den angivna informationen är giltig visas en **[!UICONTROL Connected]** status med en grön bockmarkering. Du kan sedan gå vidare till nästa steg.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.
![Skärmbild för användargränssnittet för plattformen som visar målinformationen.](../../assets/catalog/mobile-engagement/line/destination-details.png)

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Audience Type]**: Välj **[!UICONTROL ID for Advertisers(IFAs)]** om de identiteter du vill exportera är av typen *ID för annonsörer (IFA)*. Välj **[!UICONTROL LINE user IDs]** om de identiteter du vill exportera är av typen *Användar-ID för RAD*. Se [Identiteter som stöds](#supported-identities) för mer information om identitetstyperna.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden på [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.
>* Exportera *identiteter* behöver du **[!UICONTROL View Identity Graph]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). <br> ![Markera det identitetsnamnutrymme som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera det identitetsnamnutrymme som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera profiler och målgrupper för att strömma målgruppernas exportdestinationer](/help/destinations/ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

### Mappa attribut och identiteter {#map}

Så här skickar du målgruppsdata från Adobe Experience Platform till [!DNL LINE] mål måste du gå igenom fältmappningssteget. Mappningen består av att skapa en länk mellan XDM-schemafälten (Experience Data Model) i ditt plattformskonto och motsvarande motsvarigheter från målmålet. Mappa XDM-fälten korrekt till [!DNL LINE] målfält, följ dessa steg:

Beroende på din källidentitet måste följande namnrymder för målidentitet mappas: | Målidentitet | Källfält | Målfält | | — | — | — | | ID för annonsörer (IFA) | `IDFA` eller `GAID` | `LineId` | | Användar-ID:n för RAD | `UserID` | `LineId` |

Om dina målidentiteter är *Användar-ID:n för RAD* nedan:
![Skärmbild av användargränssnitt för plattform som visar målmappningen när LINE-användar-ID används för målidentiteter.](../../assets/catalog/mobile-engagement/line/mappings-userid.png)

Om din målidentitet är *ID för annonsörer (IFA)* nedan:
![Skärmbild av användargränssnitt för plattform som visar målmappningen när ID för annonsörer (IFA) används för målidentiteter.](../../assets/catalog/mobile-engagement/line/mappings-idfa.png)

## Validera dataexport {#exported-data}

Vid en lyckad dataexport från Experience Platform [!DNL LINE] målgruppen skapar en ny målgrupp inom [!DNL LINE] med det valda målgruppsnamnet.

Följ stegen nedan för att verifiera att du har konfigurerat målet korrekt:

1. I [!DNL LINE]loggar du in på [Manager-konsol](https://manager.line.biz/).

1. Navigera sedan till **[!UICONTROL Data Controls]** > **[!UICONTROL Audiences]** och kontrollera namnet som matchar den valda publiken i **[!UICONTROL Audience name]** kolumn.

1. Den uppdaterade volymen matchar antalet i segmentet.

1. The *Typ* kolumn kommer att innehålla **[!UICONTROL UserID]** om de identiteter du exporterade är av typen *Användar-ID*. På samma sätt är *Typ* kolumn kommer att innehålla **[!UICONTROL Mobile ad Id]** om de identiteter du exporterade är av typen *IDFA*.

Exempelinställningar i [!DNL LINE] visas nedan:
![Skärmbilden LINE UI visar målgruppsvolymen.](../../assets/catalog/mobile-engagement/line/audience-volume.png)

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, se [Datastyrning - översikt](/help/data-governance/home.md).
