---
title: Målanslutning för Magnite Real-Time
description: Använd den här destinationen för att leverera Adobe CDP-målgrupper till Magnite Streaming-plattformen i realtid.
last-substantial-update: 2024-11-18T00:00:00Z
exl-id: 4e08a14b-6800-41e1-95a5-826a6241144d
source-git-commit: da05db9376893bdbe8f0aa291f19a507e4a73d4f
workflow-type: tm+mt
source-wordcount: '1278'
ht-degree: 0%

---

# Magnite: Målanslutning i realtid

## Översikt {#overview}

Destinationerna [!DNL Magnite: Real-Time] och [Magnite: Batch](/help/destinations/catalog/advertising/magnite-batch.md) i Adobe Experience Platform hjälper dig att mappa och exportera målgrupper för målinriktning och aktivering på plattformen Magnite Streaming.

Att aktivera målgrupper för plattformen [!DNL Magnite Streaming] är en tvåstegsprocess som kräver att du använder både Magnite: Real-Time och Magnite: Batch-mål.

Om du vill aktivera dina målgrupper till [!DNL Magnite Streaming] måste du:

* Aktivera målgrupperna på målet [!DNL Magnite: Real-Time], vilket visas på den här sidan.
* Aktivera samma målgrupp på Magnite: Batch-målet. Målet [!DNL Magnite: Batch] är en obligatorisk komponent. Om målgruppen inte aktiveras på gruppmålet [!DNL Magnite Streaming] kommer det att leda till en misslyckad integrering och dina målgrupper kommer inte att aktiveras.

Obs! När du använder Real-Time-målet kommer [!DNL Magnite Streaming] att ta emot målgrupper i realtid, men Magnite kan bara lagra målgrupper i realtid tillfälligt på sin plattform, och de kommer att tas bort från systemet inom några dagar. Därför måste du, om du vill använda Magniten: Real-Time-målet, *även* använda Magniten: Batch-målet - varje målgrupp som du aktiverar till Real-Time-målet måste du även aktivera till Batch-målet.

>[!IMPORTANT]
>
>Målanslutningen och dokumentationssidan skapas och underhålls av [!DNL Magnite]-teamet. Om du har frågor eller uppdateringsfrågor kontaktar du dem direkt på `adobe-tech@magnite.com`.

## Användningsfall {#use-cases}

För att du bättre ska kunna förstå hur och när du ska använda målet [!DNL Magnite: Real-Time] finns det ett exempel på användning som Adobe Experience Platform-kunder kan lösa genom att använda det här målet.

### Aktivering och målinriktning {#activation-and-targeting}

Tack vare integreringen med Magnite kan kunderna skicka sina CDP-målgrupper från Adobe Experience Platform till Magnite för annonsriktad marknadsföring. Målgrupper kan väljas i Magnite för både positiv målinriktning och negativ målinriktning (undertryckning).

## Förhandskrav {#prerequisites}

Om du vill använda [!DNL Magnite]-destinationerna i Adobe Experience Platform måste du först ha ett [!DNL Magnite Streaming]-konto. Om du har ett [!DNL Magnite Streaming]-konto kan du kontakta din [!DNL Magnite]-kontohanterare för att få inloggningsuppgifter för att få åtkomst till [!DNL Magnite's]-mål.
Om du inte har något [!DNL Magnite Streaming]-konto kan du kontakta adobe-tech@magnite.com

## Identiteter som stöds {#supported-identities}

Målet [!DNL Magnite: Real-Time] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|-------------------|--------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| device_id | En unik identifierare för en enhet eller identitet. Vi godkänner alla enhets-ID och förstaparts-ID oavsett typ. | Identitetstyper som stöds av Magnite är bland annat PPUID, GAID, IDFA och TV-enhets-ID. |

{style="table-layout:auto"}

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilken typ av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
|-----------------------------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Publiker som genererats via Experience Platform [segmenteringstjänsten](../../../segmentation/home.md). |
| Anpassade överföringar | ✓ | Publikerna [importerade](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
|------------------|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Exporttyp | **[!UICONTROL Segment export]** | Du exporterar alla medlemmar i ett segment (publik) med identifierarna (namn, telefonnummer eller andra) som används i målet [!DNL Magnite: Real-Time]. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på segmentutvärdering skickar kopplingen uppdateringen nedåt till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
>
>Om du vill ansluta till målet behöver du behörigheten **[!UICONTROL View destinations]** och **[!UICONTROL Manage destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Fyll i de obligatoriska fälten och välj **[!UICONTROL Connect to destination]** om du vill autentisera mot målet.

![autentiseringsfält för målkonfiguration har inte fyllts i](../../assets/catalog/advertising/magnite/destination-realtime-config-auth-unfilled.png)

* **[!UICONTROL Username]**: Användarnamnet som du fick från [!DNL Magnite].
* **[!UICONTROL Password]**: Lösenordet som du får från [!DNL Magnite].

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Your company name]**: Ditt kund-/företagsnamn. Endast [!DNL Magnite Streaming]-klienter som stöds är tillgängliga för markering.

>[!NOTE]
>
>Företagsnamnet måste vara en sträng som matchar namnet på den Amazon S3-leveransgrupp som du har konfigurerat med Magnite och som har konfigurerats i steget [Autentisera till mål](#authenticate). Tecknen som stöds är a-z, A-Z, 0-9, - eller_ (understreck).

![autentiseringsfält för målkonfiguration har fyllts i](../../assets/catalog/advertising/magnite/destination-realtime-config-auth-filled.png)

När du är klar väljer du knappen **[!UICONTROL Create]**.

![Frivillig policy och tvångsåtgärder för styrning](../../assets/catalog/advertising/magnite/destination-realtime-config-grouping-policy.png)

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
>
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View destinations]**, **[!UICONTROL Activate destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera profiler och segment för att direktuppspela segmentexportmål](/help/destinations/ui/activate-segment-streaming-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

När målanslutningen har skapats kan du fortsätta till målgruppsaktiveringsflödet. I följande avsnitt beskrivs hur du aktiverar målgrupper med hjälp av målet för realtid.

### Mappa attribut och identiteter {#map}

Nästa steg är att mappa källidentifierare till identifieraren för Magnite device_id.

* Du kan lägga till så många mappningar du behöver genom att välja **[!UICONTROL Add new mapping]**.

I det här exemplet med Real-Time-målet visas en rad som innehåller en allmän käll-ID för deviceId som är mappad till målfältet för Magnite device_id. Välj [!UICONTROL Next] när du är med mappningarna.

![Mappa önskade datafält till fältet device_ID](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-field-mapping.png)

Var noga med att ange mappnings-ID:n till alla aktiverade målgrupper, eller ange NONE om det inte finns något mappnings-ID.

![Ange mappnings-ID:n till alla aktiverade målgrupper, eller ange NONE om det inte finns något mappnings-ID](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-mappingid.png)

Du måste nu konfigurera ett startdatum (obligatoriskt), ett slutdatum (valfritt) och ett mappnings-ID för varje målgrupp.

**Mappnings-ID**

* Använd fältet **[!UICONTROL Mapping ID]** när en målgrupp har ett befintligt segment-ID som tidigare är känt av Magnite.

* Om du vill lägga till en **[!UICONTROL Mapping ID]** till en målgrupp markerar du varje målgruppsrad individuellt och anger data i den högra kolumnen (se bilden ovan). Om du inte vill lägga till ett mappnings-ID anger du INGEN i fältet Mappnings-ID.

Välj **[!UICONTROL Next]** och slutför aktiveringsflödet.

![Välj nästa och slutför aktiveringsflödet.](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-review.png)

## Exporterade data/Validera dataexport {#exported-data}

När era målgrupper har överförts kan ni validera att era målgrupper har skapats och överförts på rätt sätt med följande steg:

<!--

* In 95% of cases, audiences will be delivered to Magnite Streaming in under 10 minutes. The actual receipt and processing of the events within Magnite Streaming depends on the shared data volume.

-->

* Målgrupper efter importen förväntas visas om [!DNL Magnite Streaming] inom några minuter och kan tillämpas på ett avtal. Du kan bekräfta detta genom att leta upp det segment-ID som delades under aktiveringsstegen i Adobe Experience Platform.

## Aktivera samma målgrupper via målet [!DNL Magnite: Batch]

Publiker som delas med [!DNL Magnite Streaming] med Real-Time-målet måste också delas med Magnite: Batch-målet. När segmentnamnen i användargränssnittet för [!DNL Magnite Streaming] är korrekt konfigurerade uppdateras de som används i Adobe Experience Platform-uppdateringen efter den dagliga uppdateringen.

Slutligen, om ett batchmål inte har konfigurerats för din integrering, ställer du in det nu via Magnite: Batch-måldokumentet.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Översikt över datastyrning](/help/data-governance/home.md).

## Ytterligare resurser {#additional-resources}

Mer information finns på [Magnite Help Center](https://help.magnite.com/help).
