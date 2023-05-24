---
title: TikTok-anslutning
description: Bygg anpassade målgrupper på TikTok med era data för målinriktning med era annonskampanjer. Dessa målgrupper kan vara personer som besökt er webbplats eller interagerat med ert innehåll. Knuffa snabbt och säkert det önskade segmentet från Adobe Experience Platform till TikTok med Adobe realtidsintegrering med TikTok Ads Manager.
last-substantial-update: 2023-03-20T00:00:00Z
exl-id: 7b12d17f-7d9a-4615-9830-92bffe3f6927
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 1%

---

# TikTok-anslutning

## Översikt {#overview}

Bygg anpassade målgrupper på TikTok med era data för målinriktning med era annonskampanjer. Dessa målgrupper kan vara personer som besökt er webbplats eller interagerat med ert innehåll. Knuffa snabbt och säkert det önskade segmentet från Adobe Experience Platform till TikTok med Adobe realtidsintegrering med TikTok Ads Manager. Besök [TikTok hjälpcenter för företag](https://ads.tiktok.com/help/article/audiences?lang=en) för mer information.

>[!IMPORTANT]
>
>Dokumentationssidan har skapats av TikTok team. Om du har frågor eller uppdateringsfrågor kontaktar du dem direkt på [https://ads.tiktok.com/help/](https://ads.tiktok.com/help/).

## Användningsfall {#use-cases}

För att du bättre ska förstå hur och när du ska använda TikTok-destinationen finns här ett exempel på hur Adobe Experience Platform-kunder kan använda produkten.

### Användningsfall {#use-case-1}

Ett sportklädmärke vill nå befintliga kunder via sina konton för sociala medier. Kläddervarumärket kan importera e-postadresser från sin egen CRM till Adobe Experience Platform, bygga segment utifrån sina egna offlinedata och skicka dessa segment till TikTok för att visa annonser i sina kunders sociala medier.

## Förutsättningar {#prerequisites}

Innan du skickar data till [!DNL TikTok Ads Manager] måste du ge Adobe Experience Platform tillåtelse att komma åt ditt annonskonto för `Audience Management`. Du kan ge tillstånd genom att ange ditt annonser-ID i Experience Platform och efter omdirigeringen för att bevilja tillstånd. Du hittar fler instruktioner i [TikTok API-dokumentation](https://ads.tiktok.com/marketing_api/docs?id=1738373141733378).

## Identiteter som stöds {#supported-identities}

TikTok stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| GAID | Google Advertising ID | Välj målidentiteten för GAID när källidentiteten är ett GAID-namnområde. |
| IDFA | Apple ID för annonsörer | Välj IDFA-målidentitet när din källidentitet är ett IDFA-namnutrymme. |
| Telefonnummer | Telefonnummer hashas med SHA256-algoritmen | Både oformaterad text och SHA256-hashade telefonnummer stöds av Adobe Experience Platform och måste vara i E.164-format. När källfältet innehåller ohash-kodade attribut markerar du **[!UICONTROL Apply transformation]** alternativ, att ha [!DNL Platform] automatiskt hash-koda data vid aktiveringen. |
| E-post | E-postadresser som hash-kodats med SHA256-algoritmen | Både oformaterad text och SHA256-hashade e-postadresser stöds av Adobe Experience Platform. När källfältet innehåller ohash-kodade attribut markerar du **[!UICONTROL Apply transformation]** alternativ, att ha [!DNL Platform] automatiskt hash-koda data vid aktiveringen. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Segment export]** | Du exporterar alla medlemmar i ett segment (publik) med de identifierare (namn, telefonnummer eller andra) som används i TikTok-målet. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på segmentutvärdering skickar kopplingen uppdateringen nedåt till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

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

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om status för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med hjälp av användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
> 
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Läs [Aktivera profiler och segment för att direktuppspela segmentexportmål](/help/destinations/ui/activate-segment-streaming-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

### Mappa identiteter {#map}

Nedan visas ett exempel på korrekt identitetsmappning när du exporterar segment till TikTok Ads Manager.

Välja källfält:

* Välj en identifierare (till exempel:` Email_LC_SHA256`) som källidentitet som unikt identifierar en profil i Adobe Experience Platform och [!DNL TikTok Ads Manager].

Markera målfält:

* Välj e-postnamnområdet som målidentitet.

![Identitetsmappning](/help/destinations/assets/catalog/social/tiktok/tiktok-map-identity.png "Bild av plattformens användargränssnitt, mappning av identiteter")

## Exporterade data {#exported-data}

Kontrollera [!DNL TikTok Ads Manager] konto (under **Resurser > Publiker**) för att verifiera om ditt Experience Platform-segment exporterades. Publiken fylls i som en målgruppstyp: `Partner Audience`.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, läs [Datastyrning - översikt](/help/data-governance/home.md).

## Ytterligare resurser {#additional-resources}

Se [TikTok Help Center page](https://ads.tiktok.com/help/article/audiences?lang=en) för ytterligare information.
