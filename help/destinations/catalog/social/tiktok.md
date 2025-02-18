---
title: TikTok
description: Bygg anpassade målgrupper på TikTok med era data för målinriktning med era annonskampanjer. Dessa målgrupper kan vara personer som besökt er webbplats eller interagerat med ert innehåll. Knuffa snabbt och säkert den önskade målgruppen från Adobe Experience Platform till TikTok med Adobe realtidsintegrering med TikTok Ads Manager.
last-substantial-update: 2023-03-20T00:00:00Z
exl-id: 7b12d17f-7d9a-4615-9830-92bffe3f6927
source-git-commit: 9a80a9b49b1983e8e488d11b114c02130b045686
workflow-type: tm+mt
source-wordcount: '1048'
ht-degree: 1%

---

# TikTok

## Översikt {#overview}

Bygg anpassade målgrupper på TikTok med era data för målinriktning med era annonskampanjer. Dessa målgrupper kan vara personer som besökt er webbplats eller interagerat med ert innehåll. Knuffa snabbt och säkert den önskade målgruppen från Adobe Experience Platform till TikTok med Adobe realtidsintegrering med TikTok Ads Manager. Mer information finns på [TikTok hjälpcenter för företag](https://ads.tiktok.com/help/article/audiences).

>[!IMPORTANT]
>
>Den här målanslutnings- och dokumentationssidan skapas och underhålls av TikTok team. Om du har frågor eller uppdateringsfrågor kontaktar du dem direkt på [https://ads.tiktok.com/help/](https://ads.tiktok.com/help/).

## Användningsfall {#use-cases}

För att du bättre ska förstå hur och när du ska använda TikTok-destinationen finns här ett exempel på hur Adobe Experience Platform-kunder kan använda produkten.

### Användningsfall {#use-case-1}

Ett sportklädvarumärke vill nå befintliga kunder via sina konton för sociala medier. Kläddervarumärket kan importera e-postadresser från sin egen CRM till Adobe Experience Platform, bygga målgrupper utifrån sina egna offlinedata och skicka dessa målgrupper till TikTok för att visa annonser i sina kunders sociala medier.

## Förhandskrav {#prerequisites}

Du måste ha [!DNL Admin] eller [!DNL Operator] åtkomst till det TikTok Ads Manager-konto som du vill skicka målgrupper till. Mer instruktioner finns på [TikTok Help Center](https://ads.tiktok.com/help/article/add-users-tiktok-business-center).

Innan du skickar data till ditt TikTok Ads Manager-konto måste du ge Adobe Experience Platform behörighet att komma åt ditt annonskonto för `Audience Management`. Den här behörigheten kan ges genom att [ange ditt ID för annonshanteraren](#authenticate) i Experience Platform-gränssnittet och bevilja behörigheten efter att ha omdirigerats till ditt TikTok Ads Manager-konto.

## Identiteter som stöds {#supported-identities}

TikTok stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Välj målidentiteten för GAID när källidentiteten är ett GAID-namnområde. |
| IDFA | Apple ID för annonsörer | Välj IDFA-målidentitet när din källidentitet är ett IDFA-namnutrymme. |
| Telefonnummer | Telefonnummer hashas med SHA256-algoritmen | Både oformaterad text och SHA256-hashade telefonnummer stöds av Adobe Experience Platform och måste vara i E.164-format. Om källfältet innehåller ohashade attribut bör du kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Platform] automatiskt hash-kodar data vid aktiveringen. |
| E-post | E-postadresser som hashas med SHA256-algoritmen | Både oformaterad text och SHA256-hashade e-postadresser stöds av Adobe Experience Platform. Om källfältet innehåller ohashade attribut bör du kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Platform] automatiskt hash-kodar data vid aktiveringen. |

{style="table-layout:auto"}

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilka typer av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Publiker som genererats via Experience Platform [segmenteringstjänst](../../../segmentation/home.md). |
| Anpassade överföringar | ✓ | Publikerna [importerade](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer. |
| [!DNL Federated Audience Composition] | ✓ | Publiker som importerats till Experience Platform via [Federated Audience Composition](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/audiences). |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en målgrupp med de identifierare (namn, telefonnummer eller andra) som används i TikTok-målet. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Om du vill autentisera till målet omdirigeras du till ditt [!DNL TikTok Ads Manager]-konto och godkänner att Adobe hanterar målgrupper åt dig.

![Val av TikTok-behörighet](/help/destinations/assets/catalog/social/tiktok/tiktok-authenticate-destination.png "Bild av TikTok-gränssnitt för val av behörigheter")

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

![Information om målanslutning](/help/destinations/assets/catalog/social/tiktok/tiktok-configure-destination-details.png "Bild av plattformsgränssnittet, med information om målanslutning som ska fyllas i")

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL TikTok Ads Manager ID]**: Din [!DNL TikTok Ads Manager ID]. Du kan hitta det här i ditt [!DNL TikTok Ads manager]-konto.

![TikTok Ads Manager ID](/help/destinations/assets/catalog/social/tiktok/tiktok-ads-manager-ID.png "Bild av gränssnittet för TikTok Ads Manager som visar hur du hämtar ID:t för TikTok Ads Manager ")

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera profiler och målgrupper för att direktuppspela målgruppsexportdestinationer](/help/destinations/ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

### Mappa identiteter {#map}

Nedan visas ett exempel på korrekt identitetsmappning när du exporterar målgrupper till TikTok Ads Manager.

Välja källfält:

* Välj en identifierare (till exempel:` Email_LC_SHA256`) som källidentitet som unikt identifierar en profil i Adobe Experience Platform och [!DNL TikTok Ads Manager].

Markera målfält:

* Välj e-postnamnområdet som målidentitet.

![Identitetsmappning](/help/destinations/assets/catalog/social/tiktok/tiktok-map-identity.png "Bild av plattformsgränssnittet, mappning av identiteter")

## Exporterade data {#exported-data}

Kontrollera ditt [!DNL TikTok Ads Manager]-konto (under **Assets > Publiker**) för att kontrollera om din Experience Platform-publik har exporterats korrekt. Publiken fylls i som en målgruppstyp: `Partner Audience`.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Översikt över datastyrning](/help/data-governance/home.md).

## Ytterligare resurser {#additional-resources}

Mer information finns på sidan [TikTok Help Center](https://ads.tiktok.com/help/article/audiences).
