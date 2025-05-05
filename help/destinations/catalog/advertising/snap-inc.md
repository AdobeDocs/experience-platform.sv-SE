---
title: Snap Inc-anslutning
description: Lär dig hur du ansluter till Snapchat Ads Platform och exporterar dina målgrupper från Experience Platform.
exl-id: 1f0f2dc0-5f3d-424b-9b22-b1a14ac30039
source-git-commit: 9a80a9b49b1983e8e488d11b114c02130b045686
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 0%

---

# Snap Inc-anslutning

## Översikt {#overview}

[Snapchat-annonser](https://forbusiness.snapchat.com/) är gjorda för alla företag, oavsett storlek eller bransch. Bli en del av Snapchatters dagliga samtal med digitala annonser i helskärmsläge som inspirerar till åtgärder från de människor som betyder mest för er verksamhet.

>[!IMPORTANT]
>
>Målanslutningen och dokumentationssidan skapas och underhålls av *Snap Inc* -teamet. Om du har frågor eller uppdateringsfrågor kontaktar du dem direkt på *dev-support@snap.com*

## Användningsfall {#use-cases}

Med den här destinationen kan marknadsförare importera användarmålgrupper som skapats i Experience Platform till Snapchat Ads och använda dem för att rikta sina annonser.

## Förhandskrav {#prerequisites}

Om du vill använda den här destinationen måste du ha ett Snapchat Ads-konto. I den här dokumentationen finns information om hur du skapar en:

[Kom igång med Snapchat Advertising](https://businesshelp.snapchat.com/s/article/overview?language=en_US)

## Begränsningar {#limitations}

* Snap Inc stöder inte flera identiteter för ett visst målgruppssegment. Mappa endast en identitet när du aktiverar ett segment.
* Snap Inc stöder inte namnbyte av segment. Om du vill byta namn på ett segment måste du inaktivera det, byta namn på det och sedan aktivera det.
* Det går inte att definiera en kvarhållningsperiod för ett målgruppssegments medlemmar. Alla medlemmar har livstidsbehållning och kommer att finnas i målgruppen tills de tas bort.

## Identiteter som stöds {#supported-identities}

Målet *Snap Inc* stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

Alla identifierare som skickas till *Snap Inc*-målet måste hash-kodas i SHA-256-format. Om du vill hash-koda identifierare för oformaterad text innan du skickar dem till målet, markerar du alternativet **[!UICONTROL Apply transformation]** när du mappar målidentifierare för målet.

>[!WARNING]
> 
> Ej hash-kodade identifierare accepteras inte av Snap Inc-målet och om de skickas kan det orsaka fel.


>[!IMPORTANT]
> 
> Snap Inc-målet stöder inte flera identiteter. Välj bara en identitet.

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| E-postadress | SHA-256 hash-e-postadress | Mappa e-postadresser till målidentitetsfältet *emailAddress*. |
| Telefonnummer | SHA-256 hash-telefonnummer | Mappa e-postadresser till målidentitetsfältet *phoneNumber*. |
| GAID | SHA-256 hashas Google Advertising ID | Mappa Google Advertising ID:n till målidentitetsfältet *gaid*. |
| IDFA | SHA-256 hashas Apple Advertising ID | Mappa Apple Advertising ID:n till målidentitetsfältet *idfa*. |

{style="table-layout:auto"}

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilka typer av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Publiker som genererats via Experience Platform [segmenteringstjänst](../../../segmentation/home.md). |
| Anpassade överföringar | ✓ | Publikerna [importerade](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer. |
| [!DNL Federated Audience Composition] | ✓ | Publiker som importerats till Experience Platform via [Federated Audience Composition](https://experienceleague.adobe.com/sv/docs/federated-audience-composition/using/start/audiences). |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en målgrupp med de identifierare (namn, telefonnummer eller andra) som används i Snap Inc-målet. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Ansluta till Snap Inc {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

### Autentisera till mål {#authenticate}

Så här autentiserar du målet:

1. Hitta *Snap Inc*-målet från Adobe Experience Platform målkatalog och välj **Konfigurera**.
2. Välj **[!UICONTROL Connect to destination]**.  Du kommer att omdirigeras till följande skärm:
   ![Autentiseringsskärm 1](/help/destinations/assets/catalog/advertising/snapchat-ads/auth1.png)
3. Ange dina autentiseringsuppgifter för Snapchat och välj **Logga in**.
4. Du kommer att få se Snapchat-data som Adobe Experience Platform kan komma åt. Välj **Fortsätt** om du vill fortsätta med anslutningsprocessen.

![Auth Screen 2](/help/destinations/assets/catalog/advertising/snapchat-ads/auth2.png)

När du har valt Fortsätt väntar du tills du omdirigeras tillbaka till Adobe Experience Platform.

### Fyll i målinformation {#destination-details}

![Målinformation](/help/destinations/assets/catalog/advertising/snapchat-ads/destinationdetails.png)

Om du vill konfigurera information för målet fyller du i de obligatoriska fälten och väljer **[!UICONTROL Next]**.

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Account ID]**: Det annonskonto-ID som är associerat med annonskontot som du vill importera dina målgrupper till. Mer information om hur du hittar detta finns i [den här dokumentationen på Snapchat Business Help Center](https://businesshelp.snapchat.com/s/article/biz-acct-id?language=en_US).

>[!IMPORTANT]
> 
>Om du anger ett felaktigt eller ogiltigt konto-ID för Snapchat-annons kommer målgruppsaktiveringen att misslyckas. Kontrollera att du har angett rätt ID för annonskonto.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera profiler och målgrupper för att direktuppspela målgruppsexportdestinationer](/help/destinations/ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

## Validera dataexport {#exported-data}

När du har aktiverat målgrupper för *Snap Inc* kan du se målgrupperna i Snap Ads Managers [**målgrupper** ](https://businesshelp.snapchat.com/s/article/audience-sharing) . Så här navigerar du till det här avsnittet:

1. Logga in i [hanteraren för ögonblicksbilder](https://ads.snapchat.com/)
2. Välj **Publiker** på menyn längst upp till vänster på skärmen. Du ser vilka målgrupper du har aktiverat i Adobe Experience Platform i målgruppsbiblioteket:

![Publiker](/help/destinations/assets/catalog/advertising/snapchat-ads/audiences.png)

Observera att när en Adobe-publik först aktiveras för Snap Inc ser du den först som en tom publik. Detta beror på att Adobe Experience Platform inte exporterar medlemsdata till Snap Inc förrän målgruppen utvärderas. Mer information om hur målgrupper utvärderas i Experience Platform finns i [Översikt över segmenteringstjänsten](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=sv-SE#evaluate-segments).

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Datastyrningsöversikten](/help/data-governance/home.md).
