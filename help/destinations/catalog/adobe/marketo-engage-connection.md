---
title: Marketo Engage Connection
description: Marketo Engage är den enda heltäckande CXM-lösningen (Customer Experience Management) för marknadsföring, reklam, analys och handel. Ni kan automatisera och hantera aktiviteter från CRM-ledhantering och kundengagemang till kontobaserad marknadsföring och intäktsattribuering.
source-git-commit: 88864353d4872d62258914d6490b90331692fa96
workflow-type: tm+mt
source-wordcount: '1836'
ht-degree: 0%

---


# Marketo Engage

## Översikt {#overview}

[!DNL Marketo Engage] är den enda heltäckande CXM-lösningen (Customer Experience Management) för marknadsföring, reklam, analys och handel. Ni kan automatisera och hantera aktiviteter från CRM-ledhantering och kundengagemang till kontobaserad marknadsföring och intäktsattribuering.

Använd det här målet för synkronisering i realtid av målgruppsdata och profilattribut mellan Adobe Experience Platform och Marketo Engage.

## Användningsfall {#use-cases}

För att du bättre ska kunna förstå hur och när du ska använda målet [!DNL Marketo Engage] finns det exempel på användning som Adobe Experience Platform-kunder kan lösa genom att använda det här målet.

### Användningsexempel för målgruppssynkronisering {#audience-sync-use-cases}

**Återanslut endast kända leads**

Marknadsföringsteamet vill köra en kampanj för att vinna tillbaka leads som inte har engagerat sig på mer än 90 dagar, men som redan finns i Marketo.

De kan aktivera målgrupperna till Marketo Engage och använda synkroniseringstypen **[!UICONTROL Audience Only]**.

### Användningsexempel för målgrupps- och profilsynkronisering {#audience-profile-sync-use-cases}

**Återanslut kända leads och uppdatera leads**

Marknadsföringsteamet vill lansera en ny engagemangskampanj för befintliga Marketo-kontakter som har visat intresse baserat på webbplatsbesök. De vill också uppdatera informationen om leads (t.ex. preferenser, demografisk information), men inte skapa några nya personer i Marketo.

De kan aktivera målgrupperna till Marketo Engage och använda synkroniseringstypen **[!UICONTROL Audience and Profile]** i kombination med åtgärden **[!UICONTROL Update existing persons only]** för att se till att de bara riktar sig till de målgrupper som redan finns i Marketo.

**Engagera igen och utöka räckvidden med fullständig profilsynkronisering**

Marknadsföringsteamet vill aktivera en intressanta produktpublik för en ny kampanj. Många av profilerna finns redan i Marketo, men vissa är nya och finns bara i Real-Time CDP. De vill se till att de uppdaterar de personerna i Marketo, men även skapa nya profiler.

De kan aktivera sina målgrupper i Marketo Engage och använda synkroniseringstypen **[!UICONTROL Audience and Profile]** i kombination med åtgärden **[!UICONTROL Update existing and create new persons]** för att se till att de har befintliga leads från Marketo som mål och skapa nya för de nya målgrupperna som exporteras från Real-Time CDP.

## Förhandskrav {#prerequisites}

Användaren som ställer in målet måste ha behörigheten [Redigera person](https://experienceleague.adobe.com/sv/docs/marketo/using/product-docs/administration/users-and-roles/descriptions-of-role-permissions#access-database) i sin Marketo-instans och -partition.

## Identiteter som stöds {#supported-identities}

[!DNL Marketo Engage] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| `DedupeField` | Det fält som används för att identifiera och matcha befintliga leads i Marketo. | Under steget [mapping](#mapping) mappar du alla källfält (till exempel `Email` eller andra anpassade identifierare) som du vill använda som dedupliceringsfält till den här målidentiteten. För bästa resultat väljer du ett fält som är enhetligt tillgängligt och unikt i alla era kundprofiler. `ECID` stöds inte som dedupliceringsfält. |

{style="table-layout:auto"}

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilka typer av målgrupper du kan exportera till det här målet. De två tabellerna nedan visar vilka målgrupper som den här kopplingen stöder, per _målgruppsursprung_ och _profiltyper som ingår i målgruppen_:

| Målgruppsursprung | Stöds | Beskrivning |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Publiker som genererats via Experience Platform [segmenteringstjänst](../../../segmentation/home.md). |
| Alla andra målgrupper kommer | ✓ | Den här kategorin omfattar alla målgrupper som kommer utanför målgrupper som genereras via [!DNL Segmentation Service]. Läs om de [olika målgruppernas ursprung](/help/segmentation/ui/audience-portal.md#customize). Några exempel är: <ul><li> anpassade uppladdningsgrupper [importerade](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer,</li><li> lookalike-målgrupper, </li><li> federerade målgrupper, </li><li> målgrupper som genererats i andra Experience Platform-appar som Adobe Journey Optimizer, </li><li> med mera. </li></ul> <br> |

{style="table-layout:auto"}

Målgrupper som stöds av olika typer av målgruppsdata:

| Typ av målgruppsdata | Stöds | Beskrivning | Användningsfall |
|--------------------|-----------|-------------|-----------|
| [Målgrupper](/help/segmentation/types/people-audiences.md) | Ja | Baserat på kundprofiler kan ni inrikta er på specifika grupper av människor för marknadsföringskampanjer. | Ofta köpare, övergivna varukorgar |
| [Kontomålgrupper](/help/segmentation/types/account-audiences.md) | Nej | Rikta er till individer inom specifika organisationer för kontobaserade marknadsföringsstrategier. | B2B-marknadsföring |
| [Prospektera målgrupper](/help/segmentation/types/prospect-audiences.md) | Nej | Rikta er till individer som ännu inte är kunder men som delar egenskaper med er målgrupp. | Prospektera med data från tredje part |
| [Datauppsättningsexport](/help/catalog/datasets/overview.md) | Nej | Samlingar med strukturerade data som lagras i Adobe Experience Platform Data Lake. | Arbetsflöden för rapportering, datavetenskap |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en målgrupp med de identifierare (e-post, ECID) som används i målet [!DNL Marketo Engage]. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Leadmatchningsbeteende {#lead-matching}

Genom att förstå hur Marketo lead-matchning fungerar kan du välja rätt konfiguration för ditt användningsfall. Det matchande beteendet beror på de valda inställningarna för **[!UICONTROL Sync Type]** och **[!UICONTROL Person Action]**.

Marketo använder de **[!UICONTROL Marketo deduplication field]** du väljer för att matcha Experience Platform-profiler med befintliga Marketo-leads. Den matchande processen söker igenom alla partitioner i din Marketo-instans för att hitta befintliga leads. I tabellen nedan ser du hur leads skapas och uppdateras i din Marketo-instans beroende på vilken konfiguration du har valt.

| Synkroniseringstyp | Personåtgärd | Matchande beteende |
|-----------|---------------|-------------------|
| **[!UICONTROL Profile only]** | **[!UICONTROL Update existing and create new persons]** | <ul><li>Uppdaterar befintliga leads med nya profildata</li><li>Skapar nya leads i den valda partitionen för omatchade profiler</li></ul> |
| **[!UICONTROL Profile only]** | **[!UICONTROL Update existing persons only]** | <ul><li>Uppdaterar befintliga leads med nya profildata</li><li>Inga nya leads har skapats för omatchade profiler</li></ul> |
| **[!UICONTROL Audience only]** | N/A | <ul><li>Lägger till befintliga leads till målgruppslistor</li><li>Inga nya leads har skapats för omatchade profiler</li></ul> |
| **[!UICONTROL Audience and profile]** | **[!UICONTROL Update existing and create new persons]** | <ul><li>Uppdaterar befintliga leads med nya profildata</li><li>Lägger till befintliga leads till målgruppslistor</li><li>Skapar nya leads i den valda partitionen för omatchade profiler</li><li>Lägger till nya leads till målgruppslistor</li></ul> |
| **[!UICONTROL Audience and profile]** | **[!UICONTROL Update existing persons only]** | <ul><li>Uppdaterar befintliga leads med nya profildata</li><li>Lägger till befintliga leads till målgruppslistor</li><li>Inga nya leads har skapats för omatchade profiler</li></ul> |

{style="table-layout:auto"}

### Viktiga överväganden

* **Markering av dedupliceringsfält**: Välj ett fält som alltid är tillgängligt och unikt i alla kundprofiler (till exempel e-postadress, kund-ID)
* **Partitionshantering**: När du skapar nya leads placeras de i den valda partitionen (eller **[!UICONTROL Default]** partition om du inte valde en partition)
* **Duplicerad hantering**: Om flera Marketo-leads matchar samma profil uppdateras endast den senast uppdaterade lead
* **Matchning mellan partitioner**: Systemet söker igenom alla partitioner för att hitta befintliga leads, oavsett vilken partition du har valt för nya leads

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>* Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions).
>
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Om du vill autentisera till målet väljer du **[!UICONTROL Connect to destination]**.

![Skärmbild som visar hur du autentiserar till målet](../../assets/catalog/adobe/marketo-engage-connection/connect-destination.png)

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

![Exempelbild som visar hur du fyller i information för ditt mål](../../assets/catalog/adobe/marketo-engage-connection/destination-details.png)

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Munchkin ID]**: Markera [!DNL Marketo Munchkin ID] som du vill använda för det här målet.
* **[!UICONTROL Workspace ID]**: Välj ditt Marketo-arbetsyte-ID.
* **[!UICONTROL Sync type]**: Välj den synkroniseringstyp som du vill använda för det här målet:
   * **[!UICONTROL Audience and profile]**: Välj det här alternativet när du vill lägga till målgruppsmedlemmar i Marketo-listor och hålla deras profilinformation aktuell.
   * **[!UICONTROL Profile only]**: Välj det här alternativet om du vill att Marketo lead-profiler ska vara uppdaterade med den senaste informationen från Experience Platform.
   * **[!UICONTROL Audience only]**: Välj det här alternativet om du vill lägga till målgruppsmedlemmar i Marketo-listor utan att uppdatera deras profilinformation.
* **[!UICONTROL Partition]**: *Partitionsval är bara tillgängligt när du väljer **[!UICONTROL Profile only]**&#x200B;eller **[!UICONTROL Audience and profile]**&#x200B;synkroniseringstyper*. Välj ett partitions-ID för Marketo som är kopplat till den valda arbetsytan. På så sätt kan du ange vilken huvudpartition i Marketo som ska ta emot exporterade data. Om du inte väljer en viss partition skickas dina data till partitionen **[!UICONTROL Default]** i Marketo.
* **[!UICONTROL Marketo deduplication field]**: Markera det Marketo-fält för borttagning av dubbletter som du vill använda när du uppdaterar befintliga Marketo-leads. Den här väljaren visar de fält som du har markerat som dedupliceringsfält i Marketo. Om du vill att ett visst fält från Marketo ska visas som ett dedupliceringsfält måste du markera fältet som ett [sökbart fält](https://experienceleague.adobe.com/sv/docs/marketo-developer/marketo/rest/lead-database/lead-database) i Marketo.

  >[!NOTE]
  >
  >Marketo `Lead ID` och Experience Cloud ID:n (`ECID`) stöds inte för deduplicering.

* **[!UICONTROL Person Action]**: Välj den Marketo-åtgärd som du vill utföra när du exporterar data.
   * **[!UICONTROL Update existing and create new persons]**: Välj det här alternativet om du vill uppdatera befintliga Marketo-leads och skapa nya leads för målgruppsmedlemmar som inte redan är i Marketo. Nya leads skapas i den valda partitionen. Om du inte valde någon partition skapas nya leads i partitionen **[!UICONTROL Default]**.
   * **[!UICONTROL Update existing persons only]**: Välj det här alternativet om du bara vill uppdatera befintliga Marketo-leads utan att skapa nya. Om flera leads matchar samma profil uppdateras endast den senast uppdaterade Marketo-leadet med dina Experience Platform-data.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera profiler och målgrupper för att direktuppspela målgruppsexportdestinationer](/help/destinations/ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

### Obligatoriska mappningar {#required-mappings}

Under mappningssteget mappar du alla källfält (till exempel `email` eller andra anpassade identifierare) som du vill använda som dedupliceringsfält till `DedupeField`-målidentiteten. För bästa resultat väljer du ett fält som är enhetligt tillgängligt och unikt i alla era kundprofiler.

För att Marketo ska kunna skapa leads måste du också mappa följande obligatoriska målattribut:

* `firstName`: Förnamnet på leadet
* `lastName`: Leadens efternamn
* `email`: Leadens e-postadress

Om du använder `email` som ett dedupliceringsfält måste du också mappa attributen `firstName` och `lastName` enligt bilden nedan.

![Skärmbild som visar den nödvändiga mappningen när e-post används som dedupliceringsfält](../../assets/catalog/adobe/marketo-engage-connection/required-mapping-email-dedupe.png)

Om du använder ett annat dedupliceringsfält måste du manuellt mappa alla tre nödvändiga attribut (`firstName`, `lastName`, `email`) enligt bilden nedan.

![Skärmbild som visar den nödvändiga mappningen när inte e-post används som dedupliceringsfält](../../assets/catalog/adobe/marketo-engage-connection/required-mapping-email.png)

## Exporterade data/Validera dataexport {#exported-data}

När du har exporterat målgrupper till Marketo Engage bör du logga in på ditt Marketo-konto för att verifiera att målgrupperna har aktiverats som förväntat. Kontrollera de relevanta lead-partitionerna och arbetsytorna i Marketo för att bekräfta att målgruppsdata visas korrekt och att de avsedda åtgärderna (som att uppdatera eller skapa personer) har utförts.

Om du inte ser de data som förväntas granskar du mappnings- och exportinställningarna i Adobe Experience Platform och försöker exportera igen.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Översikt över datastyrning](/help/data-governance/home.md).
