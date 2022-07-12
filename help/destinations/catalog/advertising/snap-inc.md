---
title: (Beta) Snap Inc-anslutning
description: Lär dig hur du ansluter till Snapchat Ads Platform och exporterar målgruppssegment från Experience Platform.
source-git-commit: 734d66cc881ab1b691c13ef446331d0c51851cf9
workflow-type: tm+mt
source-wordcount: '988'
ht-degree: 1%

---


# (Beta) Snap Inc

## Översikt {#overview}

[Snapchat-annonser](https://forbusiness.snapchat.com/) är gjort för alla företag, oavsett storlek eller bransch. Bli en del av Snapchatters dagliga samtal med digitala annonser i helskärmsläge som inspirerar till åtgärder från de människor som betyder mest för er verksamhet.

>[!IMPORTANT]
>
>Dokumentationssidan skapades av *Snap Inc* team. Detta är för närvarande en betaprodukt och funktionaliteten kan komma att ändras. Om du har frågor eller uppdateringsfrågor kontaktar du dem direkt på *dev-support@snap.com*

## Användningsfall {#use-cases}

Med den här destinationen kan marknadsförare importera användarsegment som skapats i Experience Platform till Snapchat Ads och använda dem för att rikta sina annonser.

## Förutsättningar {#prerequisites}

Om du vill använda den här destinationen måste du ha ett Snapchat Ads-konto. I den här dokumentationen finns information om hur du skapar en:

[Kom igång med Snapchat Advertising](https://businesshelp.snapchat.com/s/article/overview?language=en_US)

## Begränsningar {#limitations}

* Snap Inc stöder inte flera identiteter för ett visst målgruppssegment. Mappa endast en identitet när du aktiverar ett segment.
* Snap Inc stöder inte namnbyte av segment. Om du vill byta namn på ett segment måste du inaktivera det, byta namn på det och sedan aktivera det.
* Det går inte att definiera en kvarhållningsperiod för ett målgruppssegments medlemmar. Alla medlemmar behåller sin livstid och kommer att finnas i segmentet tills de tas bort.

## Identiteter som stöds {#supported-identities}

The *Snap Inc* målet har stöd för aktivering av de identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/namespaces.md).

Alla identifierare som skickats till *Snap Inc* målet måste hash-kodas i SHA-256-format. Om du vill hash-koda identifierare av oformaterad text innan du skickar dem till målet, markerar du **[!UICONTROL Apply transformation]** när målidentifierare mappas för målet.

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
| GAID | SHA-256 hashas Google Advertising ID | Mappa Google Advertising ID:n till målidentitetsfältet *gala*. |
| IDFA | SHA-256 hashas Apple Advertising ID | Mappa Apple Advertising ID:n till målidentitetsfältet *idfa*. |

{style=&quot;table-layout:auto&quot;}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Segment export]** | Du exporterar alla medlemmar i ett segment (publik) med de identifierare (namn, telefonnummer eller andra) som används i *YOURDESTINATION* mål. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på segmentutvärdering skickar kopplingen uppdateringen nedåt till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Ansluta till Snap Inc {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

### Autentisera till mål {#authenticate}

Så här autentiserar du målet:

1. Hitta *Snap Inc* mål från Adobe Experience Platform målkatalog och välj **Konfigurera**.
2. Välj **[!UICONTROL Connect to destination]**. Du kommer att omdirigeras till följande skärm:
   ![Autentiseringsskärm 1](/help/destinations/assets/catalog/advertising/snapchat-ads/auth1.png)
3. Ange dina autentiseringsuppgifter för Snapchat och välj **Logga in**.
4. Du kommer att få se Snapchat-data som Adobe Experience Platform kan komma åt. Välj **Fortsätt** för att fortsätta med anslutningsprocessen.

![Autentiseringsskärm 2](/help/destinations/assets/catalog/advertising/snapchat-ads/auth2.png)

När du har valt Fortsätt väntar du tills du omdirigeras tillbaka till Adobe Experience Platform.

### Fyll i målinformation {#destination-details}

![Destinationsinformation](/help/destinations/assets/catalog/advertising/snapchat-ads/destinationdetails.png)

Om du vill konfigurera information för målet fyller du i de obligatoriska fälten och väljer **[!UICONTROL Next]**.

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Account ID]**: Det annonskonto-ID som är associerat med annonskontot som du vill importera dina segment till. Mer information finns i [den här dokumentationen om Snapchat Business Help Center](https://businesshelp.snapchat.com/s/article/biz-acct-id?language=en_US).

>[!IMPORTANT]
> 
>Om du anger ett felaktigt eller ogiltigt konto-ID för Snapchat-annonsen misslyckas segmentaktiveringen. Kontrollera att du har angett rätt ID för annonskonto.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om status för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med hjälp av användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
> 
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Läs [Aktivera profiler och segment för att direktuppspela segmentexportmål](/help/destinations/ui/activate-segment-streaming-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

## Validera dataexport {#exported-data}

Efter aktivering av segment till *Snap Inc* kommer du att kunna se segmenten i Snap Ads Managers [**Målgrupper** section](https://businesshelp.snapchat.com/s/article/audience-sharing). Så här navigerar du till det här avsnittet:

1. Logga in på [Snap Ads Manager](https://ads.snapchat.com/)
2. Välj **Målgrupper** på menyn längst upp till vänster på skärmen. De segment du har aktiverat i Adobe Experience Platform visas i målgruppsbiblioteket:

![Publiker](/help/destinations/assets/catalog/advertising/snapchat-ads/audiences.png)

Observera att när ett Adobe-segment först aktiveras för Snap Inc ser du det först som en tom publik. Detta beror på att Adobe Experience Platform inte exporterar medlemsdata till Snap Inc förrän segmentet utvärderas. Mer information om hur segment utvärderas i Experience Platform finns i [Översikt över segmenteringstjänsten](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=en#evaluate-segments).

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, se [Datastyrning - översikt](/help/data-governance/home.md).