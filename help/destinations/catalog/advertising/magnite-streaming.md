---
title: Målanslutning för direktuppspelning i realtid av Magnite
description: Använd den här destinationen för att leverera Adobe CDP-målgrupper till Magnite Streaming-plattformen i realtid.
badgeBeta: label="Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: c61907768f6d3cfdae3d07291bb25ff4a5229a89
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 0%

---


# (Beta) Magnite Streaming: Målanslutning i realtid

## Översikt {#overview}

The [!DNL Magnite Streaming: Real-Time] och Magnite Streaming: Batch-mål i Adobe Experience Platform hjälper er att kartlägga och exportera målgrupper för målgruppsanpassning och aktivering på plattformen Magnite Streaming.

Aktivera målgrupper för [!DNL Magnite Streaming] är en tvåstegsprocess som kräver att du använder både Magnite Streaming: Real-Time och Magnite Streaming: Batch-mål.

Så här aktiverar du målgrupper för [!DNL Magnite Streaming]måste du:

* Aktivera målgrupperna på [!DNL Magnite Streaming: Real-Time] mål, vilket visas på den här sidan.
* Aktivera samma målgrupp på Magnite Streaming: Batch-mål. The [!DNL Magnite Streaming: Batch] mål är en obligatorisk komponent. Det gick inte att aktivera målgruppen på [!DNL Magnite Streaming] Batchmålet resulterar i en misslyckad integrering och dina målgrupper kommer inte att aktiveras.

Obs! När du använder Real-Time-målet [!DNL Magnite: Streaming] kommer att ta emot målgrupper i realtid, men vi kan bara lagra målgrupper i realtid tillfälligt på vår plattform, och de kommer att tas bort från vårt system inom några dagar. Om du vill använda Magnite: Streaming Real-Time-målet kommer du därför att *även* behöver använda Magnite Streaming: Batch-mål - varje målgrupp som du aktiverar till Real-Time-målet måste du också aktivera till Batch-målet.

>[!IMPORTANT]
>
>Den här målanslutningen är i betaversion och endast tillgänglig för vissa kunder. Kontakta din Adobe-representant om du vill ha åtkomst.
>
>Målanslutnings- och dokumentationssidan skapas och underhålls av [!DNL Magnite] team. Om du har frågor eller uppdateringsfrågor kontaktar du dem direkt på `adobe-tech@magnite.com`.

## Användningsfall {#use-cases}

För att du bättre ska förstå hur och när du ska använda [!DNL Magnite Streaming: Real-Time] mål, här är ett exempel på användning som Adobe Experience Platform-kunder kan lösa genom att använda den här destinationen.

### Aktivering och målinriktning {#activation-and-targeting}

Tack vare integreringen med Magnite kan kunderna skicka sina CDP-målgrupper från Adobe Experience Platform till Magnite för annonsriktad marknadsföring. Målgrupper kan väljas i Magnite för både positiv målinriktning och negativ målinriktning (undertryckning).

## Förhandskrav {#prerequisites}

Använd [!DNL Magnite] mål i Adobe Experience Platform måste du först ha [!DNL Magnite Streaming] konto. Om du har en [!DNL Magnite Streaming] konto, kontakta [!DNL Magnite] kontohanterare som ska ges autentiseringsuppgifter för åtkomst [!DNL Magnite's] destinationer.
Om du inte har en [!DNL Magnite Streaming] konto, kontakta adobe-tech@magnite.com

## Identiteter som stöds {#supported-identities}

The [!DNL Magnite Streaming: Real-Time] målet har stöd för aktivering av de identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|-------------------|--------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| device_id | En unik identifierare för en enhet eller identitet. Vi godkänner alla enhets-ID och förstaparts-ID oavsett typ. | Identitetstyper som stöds är bland annat PPUID, GAID, IDFA och TV-enhets-ID. |

{style="table-layout:auto"}

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilken typ av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
|-----------------------------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Målgrupper som skapats genom Experience Platform [Segmenteringstjänst](../../../segmentation/home.md). |
| Anpassade överföringar | ✓ | Målgrupper [importerad](../../../segmentation/ui/overview.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
|------------------|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Exporttyp | **[!UICONTROL Segment export]** | Du exporterar alla medlemmar i ett segment (publik) med de identifierare (namn, telefonnummer eller andra) som används i [!DNL Magnite Streaming: Real-Time] mål. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på segmentutvärdering skickar kopplingen uppdateringen nedåt till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
>
>Om du vill ansluta till målet behöver du **[!UICONTROL View destinations]** och **[!UICONTROL Manage destinations]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Om du vill autentisera mot målet fyller du i de obligatoriska fälten och väljer **[!UICONTROL Connect to destination]**.

![autentiseringsfält för målkonfiguration har inte fyllts i](../../assets/catalog/advertising/magnite/destination-realtime-config-auth-unfilled.png)

* **[!UICONTROL Username]**: Det användarnamn som du får från [!DNL Magnite].
* **[!UICONTROL Password]**: Lösenordet som du får från [!DNL Magnite].

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Name of your source partner]**: Ditt kund-/företagsnamn. Endast stöds [!DNL Magnite Streaming] klienter är tillgängliga för val.

![autentiseringsfält för målkonfiguration har fyllts i](../../assets/catalog/advertising/magnite/destination-realtime-config-auth-filled.png)

När du är klar väljer du **[!UICONTROL Create]** -knappen.

![Frivillig styrningspolicy och verkställighetsåtgärder](../../assets/catalog/advertising/magnite/destination-realtime-config-grouping-policy.png)

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden på [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
>
>* För att aktivera data behöver du **[!UICONTROL View destinations]**, **[!UICONTROL Activate destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.
>* Exportera *identiteter* behöver du **[!UICONTROL View Identity Graph]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). <br> ![Markera det identitetsnamnutrymme som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera det identitetsnamnutrymme som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera profiler och segment för att direktuppspela segmentexportmål](/help/destinations/ui/activate-segment-streaming-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

När målanslutningen har skapats kan du fortsätta till målgruppsaktiveringsflödet. I följande avsnitt beskrivs hur du aktiverar målgrupper med hjälp av målet för realtid.

### Mappa attribut och identiteter {#map}

Nästa steg är att mappa källidentifierare till identifieraren för Magnite device_id.

* Du kan lägga till så många mappningar du behöver genom att välja **[!UICONTROL Add new mapping]**.

I det här exemplet med Real-Time-målet visas en rad som innehåller en allmän käll-ID för deviceId som är mappad till målfältet för Magnite device_id. När du är med mappningarna väljer du [!UICONTROL Next].

![Mappa önskade datafält till fältet device_ID](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-field-mapping.png)

Var noga med att ange mappnings-ID:n till alla aktiverade målgrupper, eller ange NONE om det inte finns något mappnings-ID.

![Var noga med att ange mappnings-ID:n till alla aktiverade målgrupper, eller ange NONE om det inte finns något mappnings-ID](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-mappingid.png)

Du måste nu konfigurera ett startdatum (obligatoriskt), ett slutdatum (valfritt) och ett mappnings-ID för varje målgrupp.

**Mappnings-ID**

* Använd **[!UICONTROL Mapping ID]** när en målgrupp har ett befintligt segment-ID som tidigare är känt för Magnite.

* Lägga till en **[!UICONTROL Mapping ID]** för en målgrupp markerar du varje målgruppsrad individuellt och anger data i den högra kolumnen (se bilden ovan). Om du inte vill lägga till ett mappnings-ID anger du INGEN i fältet Mappnings-ID.

Välj **[!UICONTROL Next]** och slutföra aktiveringsflödet.

![Välj nästa och slutför aktiveringsflödet.](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-review.png)

## Exporterade data/Validera dataexport {#exported-data}

När era målgrupper har överförts kan ni validera att era målgrupper har skapats och överförts på rätt sätt med följande steg:

<!--

* In 95% of cases, audiences will be delivered to Magnite Streaming in under 10 minutes. The actual receipt and processing of the events within Magnite Streaming depends on the shared data volume.

-->

* Post-import, målgrupper förväntas finnas i [!DNL Magnite Streaming] inom några minuter och kan tillämpas på ett avtal. Du kan bekräfta detta genom att leta upp det segment-ID som delades under aktiveringsstegen i Adobe Experience Platform.

## Aktivera samma målgrupper via [!DNL Magnite Streaming: Batch]mål

Målgrupper delade med [!DNL Magnite Streaming] med Real-Time-målet måste också delas med Magnite Streaming: Batch-målet. När segmentnamnen är korrekt konfigurerade finns de i [!DNL Magnite Streaming] Gränssnittet uppdateras för att återspegla de som används i Adobe Experience Platform post-day-uppdateringen.

Slutligen, om ett batchmål inte har konfigurerats för din integrering, ställer du in det nu via Magnite Streaming: Batch-måldokument.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, läs [Datastyrning - översikt](/help/data-governance/home.md).

## Ytterligare resurser {#additional-resources}

Ytterligare hjälpdokumentation finns på [Magnite Help Center](https://help.magnite.com/help).
