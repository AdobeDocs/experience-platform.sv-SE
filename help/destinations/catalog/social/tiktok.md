---
title: TikTok
description: Bygg anpassade målgrupper på TikTok med era data för målinriktning med era annonskampanjer. Dessa målgrupper kan vara personer som besökt er webbplats eller interagerat med ert innehåll. Knuffa snabbt och säkert den önskade målgruppen från Adobe Experience Platform till TikTok med hjälp av Adobe realtidsintegrering med TikTok Ads Manager.
last-substantial-update: 2023-03-20T00:00:00Z
exl-id: 7b12d17f-7d9a-4615-9830-92bffe3f6927
source-git-commit: d9d31013d93e0e9e4e291a63840869e73d30ef01
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 1%

---

# TikTok

## Översikt {#overview}

Bygg anpassade målgrupper på TikTok med era data för målinriktning med era annonskampanjer. Dessa målgrupper kan vara personer som besökt er webbplats eller interagerat med ert innehåll. Knuffa snabbt och säkert den önskade målgruppen från Adobe Experience Platform till TikTok med hjälp av Adobe realtidsintegrering med TikTok Ads Manager. Besök [TikTok hjälpcenter för företag](https://ads.tiktok.com/help/article/audiences?lang=en) för mer information.

>[!IMPORTANT]
>
>Den här målanslutnings- och dokumentationssidan skapas och underhålls av TikTok team. Om du har frågor eller uppdateringsfrågor kontaktar du dem direkt på [https://ads.tiktok.com/help/](https://ads.tiktok.com/help/).

## Användningsfall {#use-cases}

För att du bättre ska förstå hur och när du ska använda TikTok-destinationen finns här ett exempel på hur Adobe Experience Platform-kunder kan använda produkten.

### Användningsfall {#use-case-1}

Ett sportklädvarumärke vill nå befintliga kunder via sina konton för sociala medier. Kläddervarumärket kan importera e-postadresser från sin egen CRM till Adobe Experience Platform, bygga målgrupper utifrån sina egna offlinedata och skicka dessa målgrupper till TikTok för att visa annonser i sina kunders sociala medier.

## Förutsättningar {#prerequisites}

Du måste ha [!DNL Admin] eller [!DNL Operator] åtkomst till det TikTok Ads Manager-konto som du vill skicka målgrupper till. Fler instruktioner finns på [TikTok Help Center](https://ads.tiktok.com/help/article/add-users-tiktok-business-center?lang=en).

Innan du skickar data till ditt TikTok Ads Manager-konto måste du ge Adobe Experience Platform behörighet att komma åt ditt Ad-konto för `Audience Management`. Den här behörigheten kan ges av [ange ditt ID för annonshanteraren](#authenticate) i användargränssnittet i Experience Platform och ger tillstånd efter att ha omdirigerats till ditt TikTok Ads Manager-konto.

## Identiteter som stöds {#supported-identities}

TikTok stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| GAID | Google Advertising ID | Välj målidentiteten för GAID när källidentiteten är ett GAID-namnområde. |
| IDFA | Apple ID för annonsörer | Välj IDFA-målidentitet när din källidentitet är ett IDFA-namnutrymme. |
| Telefonnummer | Telefonnummer hashas med SHA256-algoritmen | Både oformaterad text och SHA256-hashade telefonnummer stöds av Adobe Experience Platform och måste vara i E.164-format. När källfältet innehåller ohash-kodade attribut markerar du **[!UICONTROL Apply transformation]** alternativ, att ha [!DNL Platform] automatiskt hash-koda data vid aktiveringen. |
| E-post | E-postadresser som hashas med SHA256-algoritmen | Både oformaterad text och SHA256-hashade e-postadresser stöds av Adobe Experience Platform. När källfältet innehåller ohash-kodade attribut markerar du **[!UICONTROL Apply transformation]** alternativ, att ha [!DNL Platform] automatiskt hash-koda data vid aktiveringen. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en målgrupp med de identifierare (namn, telefonnummer eller andra) som används i TikTok-målet. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Om du vill autentisera till målet omdirigeras du till ditt [!DNL TikTok Ads Manager] redovisa för och auktorisera Adobe att hantera målgrupper för era räkning.

![TikTok behörighetsval](/help/destinations/assets/catalog/social/tiktok/tiktok-authenticate-destination.png "Bild av TikTok-gränssnitt för att välja behörigheter")

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

![Information om målanslutning](/help/destinations/assets/catalog/social/tiktok/tiktok-configure-destination-details.png "Bild av plattformsgränssnittet, med information om målanslutning som ska fyllas i")

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL TikTok Ads Manager ID]**: Din [!DNL TikTok Ads Manager ID]. Du hittar den här i [!DNL TikTok Ads manager] konto.

![TikTok Ads Manager-ID](/help/destinations/assets/catalog/social/tiktok/tiktok-ads-manager-ID.png "Bild av användargränssnittet för TikTok Ads Manager som visar hur du hämtar ID:t för TikTok Ads Manager")

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden på [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>För att aktivera data behöver du **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Läs [Aktivera profiler och målgrupper för att strömma målgruppernas exportdestinationer](/help/destinations/ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

### Mappa identiteter {#map}

Nedan visas ett exempel på korrekt identitetsmappning när du exporterar målgrupper till TikTok Ads Manager.

Välja källfält:

* Välj en identifierare (till exempel:` Email_LC_SHA256`) som källidentitet som unikt identifierar en profil i Adobe Experience Platform och [!DNL TikTok Ads Manager].

Markera målfält:

* Välj e-postnamnområdet som målidentitet.

![Identitetsmappning](/help/destinations/assets/catalog/social/tiktok/tiktok-map-identity.png "Bild av plattformens användargränssnitt, mappning av identiteter")

## Exporterade data {#exported-data}

Kontrollera [!DNL TikTok Ads Manager] konto (under **Resurser > Publiker**) för att bekräfta om din Experience Platform-publik har exporterats. Publiken fylls i som en målgruppstyp: `Partner Audience`.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, läs [Datastyrning - översikt](/help/data-governance/home.md).

## Ytterligare resurser {#additional-resources}

Läs mer i [TikTok Help Center page](https://ads.tiktok.com/help/article/audiences?lang=en) om du vill ha mer information.
