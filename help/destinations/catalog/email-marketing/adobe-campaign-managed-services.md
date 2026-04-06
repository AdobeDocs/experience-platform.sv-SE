---
title: Adobe Campaign Managed Cloud Services
description: Adobe Campaign Managed Cloud Services är en plattform för att designa flerkanaliga kundupplevelser och en miljö för visuell kampanjsamordning, interaktionshantering i realtid och flerkanalsmarknadsföring.
exl-id: fe151ad3-c431-4b5a-b453-9d1d9aedf775
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '1721'
ht-degree: 0%

---

# [!DNL Adobe Campaign Managed Cloud Services]-anslutning {#adobe-campaign-managed-services}

>[!IMPORTANT]
>
>Integrationen fungerar med [[!DNL Adobe Campaign] version 8.4 eller senare](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/release-notes.html#release-8-4-1).

## Översikt {#overview}

[!DNL Adobe Campaign Managed Cloud Services] är en plattform för att utforma flerkanaliga kundupplevelser och en miljö för visuell kampanjsamordning, interaktionshantering i realtid och körning över flera kanaler. [Kom igång med Campaign](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html)

Använd Campaign för att

* Driv personalisering och engagemang genom en enda lättillgänglig bild av kunden,
* Integrera kanaler för e-post, mobiler, online och offline i kundresan,
* Automatisera leverans av meningsfulla och aktuella meddelanden och erbjudanden.

## Skyddsräcken {#guardrails}

Tänk på följande skyddsräcken när du använder anslutningen [!DNL Adobe Campaign Managed Cloud Services]:

* Du kan [aktivera](#activate) högst 25 målgrupper till det här målet.

  Du kan ändra den här gränsen genom att uppdatera värdet för alternativet **NmsCdp_Aep_Audience_List_Limit** i mappen **[!UICONTROL Administration]** > **[!UICONTROL Platform]** > **[!UICONTROL Options]** i Campaign Explorer. Det här skyddsutkastet begränsar det totala antalet Experience Platform-målgrupper som kan exporteras till en enda Campaign-instans för alla konfigurerade mål.

* För varje målgrupp kan du lägga till upp till 20 fält i [karta](#map) till [!DNL Adobe Campaign].

  Du kan ändra den här gränsen genom att uppdatera värdet för alternativet **NmsCdp_Aep_Destinations_Max_Columns** i mappen **[!UICONTROL Administration]** > **[!UICONTROL Platform]** > **[!UICONTROL Options]** i Campaign Explorer.

* Datalagring på Azure blob storage Data Landing Zone (DLZ): 7 dagar.
* Aktiveringsfrekvensen är minst 3 timmar.
* Den maximala filnamnslängd som stöds av anslutningen är 255 tecken. När du [konfigurerar det exporterade filnamnet](../../ui/activate-batch-profile-destinations.md#configure-file-names) kontrollerar du att filnamnet inte är längre än 255 tecken. Om du överskrider maxlängden för filnamn uppstår aktiveringsfel.
* Segment/målgrupper som innehåller specialtecken (t.ex. `&`) stöds inte när målgrupper exporteras till [!DNL Adobe Campaign].

## Användningsfall {#use-cases}

För att du bättre ska kunna förstå hur och när du ska använda [!DNL Adobe Campaign]-hanterarmålet finns det ett exempel på användning som [!DNL Adobe Experience Platform]-kunder kan lösa genom att använda det här målet.

* [!DNL Adobe Experience Platform] skapar en kundprofil som innehåller information som identitetsdiagram, beteendedata från analyser, sammanfogar offline- och onlinedata osv. Med den här integreringen kan du utöka segmenteringsfunktionerna som redan finns i [!DNL Adobe Campaign] med de [!DNL Adobe Experience Platform]-drivna målgrupperna, och du kan därför aktivera dessa data i Campaign.

  Ett sportklädföretag vill till exempel utnyttja de [!DNL Adobe Experience Platform]-baserade målgrupperna och aktivera dem med [!DNL Adobe Campaign] för att nå ut till sina kunder via de olika kanaler som stöds av [!DNL Adobe Campaign]. När meddelandena har skickats vill de förbättra kundprofilen i [!DNL Adobe Experience Platform] med upplevelsedata från [!DNL Adobe Campaign], till exempel skicka, öppna och klickningar.

  Resultatet är flerkanalskampanjer som är mer enhetliga över hela Adobe Experience Cloud-ekosystemet och en rik kundprofil som snabbt anpassar sig och lär sig.


* Förutom målgruppsaktivering i Campaign kan du utnyttja målet [!DNL Adobe Campaign Managed Services] för att ta in ytterligare profilattribut som är kopplade till en profil på [!DNL Adobe Experience Platform] och som har en synkroniseringsprocess på plats så att de uppdateras i databasen [!DNL Adobe Campaign].

  Anta att du hämtar värden för anmälan och avanmälan i [!DNL Adobe Experience Platform]. Med den här anslutningen kan du ta över dessa värden till [!DNL Adobe Campaign] och ha en synkroniseringsprocess på plats så att de uppdateras regelbundet.

  >[!NOTE]
  >
  >Synkronisering av profilattribut är tillgängligt för profiler som redan finns i databasen [!DNL Adobe Campaign].

[Läs mer om  [!DNL Adobe Campaign] integrering med [!DNL Adobe Experience Platform]](https://experienceleague.adobe.com/docs/campaign/campaign-v8/connect/ac-aep.html)

## Identiteter som stöds {#supported-identities}

*[!DNL Adobe Campaign Managed Cloud Services]* stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| external_id | Anpassade användar-ID:n | Välj den här målidentiteten när källidentiteten är ett anpassat namnutrymme. Vi rekommenderar att du använder den här identiteten och mappar den till det ID i Campaign-instansen som representerar kund (loyalty_ID, account_ID, customer_ID..) |
| ECID | EXPERIENCE CLOUD ID | Ett namnutrymme som representerar ECID. Detta namnområde kan också refereras till av följande alias: Adobe Marketing Cloud ID, [!DNL Adobe Experience Cloud] ID, [!DNL Adobe Experience Platform] ID. Mer information finns i följande dokument på [ECID](/help/identity-service/features/ecid.md). |
| email_lc_sha256 | E-postadresser som hashas med SHA256-algoritmen | Både oformaterad text och SHA256-hash-adresser stöds av [!DNL Adobe Experience Platform]. Om källfältet innehåller ohashade attribut bör du kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Experience Platform] automatiskt hash-kodar data vid aktiveringen. |
| phone_sha256 | Telefonnummer hashas med SHA256-algoritmen | Både oformaterad text och SHA256-hashade telefonnummer stöds av [!DNL Adobe Experience Platform]. Om källfältet innehåller ohashade attribut bör du kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Experience Platform] automatiskt hash-kodar data vid aktiveringen. |
| GAID | GOOGLE ADVERTISING ID | Välj målidentiteten för GAID när källidentiteten är ett GAID-namnområde. |
| IDFA | Apple ID för annonsörer | Välj IDFA-målidentitet när din källidentitet är ett IDFA-namnutrymme. |

{style="table-layout:auto"}

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilka typer av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
|---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Publiker som genererats via Experience Platform [segmenteringstjänst](../../../segmentation/home.md). |
| Alla andra målgrupper kommer | Nej | Den här kategorin omfattar alla målgrupper som kommer utanför målgrupper som genereras via [!DNL Segmentation Service]. Läs om de [olika målgruppernas ursprung](/help/segmentation/ui/audience-portal.md#customize). Några exempel är: <ul><li> anpassade uppladdningsgrupper [importerade](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer,</li><li> lookalike-målgrupper, </li><li> federerade målgrupper, </li><li> målgrupper som har genererats i andra Experience Platform-appar som [!DNL Adobe Journey Optimizer], </li><li> med mera. </li></ul> |

{style="table-layout:auto"}



Målgrupper som stöds av olika typer av målgruppsdata:

| Typ av målgruppsdata | Stöds | Beskrivning | Användningsfall |
|--------------------|-----------|-------------|-----------|
| [Målgrupper](/help/segmentation/types/people-audiences.md) | Ja | Baserat på kundprofiler kan ni inrikta er på specifika grupper av människor för marknadsföringskampanjer. | Ofta köpare, övergivna varukorgar |
| [Kontomålgrupper](/help/segmentation/types/account-audiences.md) | Nej | Rikta er till individer inom specifika organisationer för kontobaserade marknadsföringsstrategier. | B2B-marknadsföring |
| [Prospektera målgrupper](/help/segmentation/types/prospect-audiences.md) | Nej | Rikta er till individer som ännu inte är kunder men som delar egenskaper med er målgrupp. | Prospektera med data från tredje part |
| [Datauppsättningsexport](/help/catalog/datasets/overview.md) | Nej | Samlingar med strukturerade data lagrade i datasjön [!DNL Adobe Experience Platform]. | Arbetsflöden för rapportering, datavetenskap |

{style="table-layout:auto"}


## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla medlemmar i en målgrupp tillsammans med de önskade schemafälten (t.ex. e-postadress, telefonnummer, efternamn), som du har valt på skärmen Välj profilattribut i arbetsflödet för [målaktivering](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrekvens | **[!UICONTROL Batch]** | Batchdestinationer exporterar filer till efterföljande plattformar i steg om tre, sex, åtta, tolv eller tjugofyra timmar. Läs mer om [gruppfilsbaserade mål](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
>
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

![[!DNL Adobe Campaign Managed Cloud Services] målinformationsformulär med fält för Namn, Beskrivning, instansval, målmappning och synkroniseringstyp.](../../assets/catalog/email-marketing/adobe-campaign-managed-services/destination-details.png)

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Select instance]**: Din **[!DNL Campaign]**-marknadsföringsinstans.
* **[!UICONTROL Target mapping]**: Välj den målmappning som du använder i **[!DNL Adobe Campaign]** för att skicka leveranser. [Läs mer](https://experienceleague.adobe.com/docs/campaign/campaign-v8/profiles-and-audiences/add-profiles/target-mappings.html).
* **[!UICONTROL Select sync type]**:

   * **[!UICONTROL Audience sync]**: Använd det här alternativet om du vill skicka över [!DNL Adobe Experience Platform] målgrupper till [!DNL Adobe Campaign].
   * **[!UICONTROL Profile sync (Update only)]**: Använd det här alternativet om du vill hämta [!DNL Adobe Experience Platform] profilattribut till [!DNL Adobe Campaign] och ha en synkroniseringsprocess på plats så att de kan uppdateras regelbundet.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

### Styrningspolicy och verkställighetsåtgärder {#governance}

Välj de marknadsföringsåtgärder som gäller för de data som du vill exportera till målet. För [!DNL Adobe Campaign] rekommenderar vi att du väljer marknadsföringsåtgärden **[!UICONTROL Email Targeting]**.

Mer information om marknadsföringsåtgärder finns i översikten [över dataanvändningsprinciper](/help/data-governance/policies/overview.md).

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
>
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera målgruppsdata för att batchprofilera exportmål](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html) om du vill ha instruktioner om hur du aktiverar målgruppsdata till det här målet.

### Mappa attribut och identiteter {#map}

Välj XDM-fält som ska exporteras med profilerna och mappa dem till motsvarande [!DNL Adobe Campaign]-fält.[Läs mer om val av identitet och attribut för e-postmarknadsföringsmål](overview.md)

1. Välj källfält:

   * Välj en **identifierare** (till exempel e-postfältet) som källidentitet som unikt identifierar en profil i [!DNL Adobe Experience Platform] och [!DNL Adobe Campaign].

   * Markera alla andra **XDM-källprofilattribut** som ska exporteras till [!DNL Adobe Campaign].

   >[!NOTE]
   >
   >Fältet&quot;segmentMembershipStatus&quot; är en obligatorisk mappning som återspeglar statusen för segmentMembership. Det här fältet läggs till som standard och kan inte ändras eller tas bort.

1. Mappa varje fält med målfältet i [!DNL Adobe Campaign]. Tillgängliga målfält avgörs av den målmappning som valts när [målet ](#destination-details) skapades.

1. Identifiera obligatoriska attribut och dedupliceringsnycklar. Observera att värden i attribut som är markerade som&quot;Obligatorisk&quot; eller&quot;Avdupliceringsnyckel&quot; inte kan vara null.

   * [Obligatoriska attribut](../../ui/activate-batch-profile-destinations.md#mandatory-attributes) kontrollerar att alla profilposter innehåller de valda attributen. Till exempel innehåller alla exporterade profiler en e-postadress. Rekommendationen är att ställa in på obligatorisk både identitetsfältet och fältet som används som dedupliceringsnyckel.
   * [En dedupliceringsnyckel](../../ui/activate-batch-profile-destinations.md#mandatory-attributes) är en primärnyckel som fastställer identiteten som användarna vill att deras profiler ska dedupliceras med.

     >[!IMPORTANT]
     >
     >Kontrollera att namnet på dedupliceringsnyckelattributet matchar ett kolumnnamn för den valda målmappningen.

   ![Skärm för attributmappning som visar XDM-källfält mappade till [!DNL Adobe Campaign] målfält, med obligatoriska nyckelindikatorer och nyckelindikatorer för deduplicering.](../../assets/catalog/email-marketing/adobe-campaign-managed-services/mapping.png)

1. När mappningen har utförts kan du granska och slutföra målkonfigurationen för att börja skicka data till **[!DNL Campaign]**.
   [Lär dig hur du granskar och slutför målkonfigurationen](/help/destinations/destination-types.md#destination-types-and-categories).

## Exporterade data/Validera dataexport {#exported-data}

När ett mål har aktiverats kan du komma åt motsvarande jobb och exporterade data i Campaign.

### Övervaka dataexportjobb {#jobs}

Navigera till menyn **[!UICONTROL Administration]** > **[!UICONTROL Audit]** > **[!UICONTROL Audience load jobs]** om du vill övervaka alla exportjobb som har aktiverats från [!DNL Adobe Experience Platform].

![[!DNL Adobe Campaign] Målgruppsinläsningsjobb visar exportjobb som har aktiverats från [!DNL Adobe Experience Platform].](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-jobs.png)

### Få åtkomst till exporterade data {#data}

För **[!UICONTROL Audience sync]** kan du kontrollera den exporterade målgruppen genom att gå till menyn **[!UICONTROL Profile and target]** > **[!UICONTROL List]** > **[!UICONTROL AEP audiences]** .

![[!DNL Adobe Campaign] AEP målgruppslista visar exporterade målgrupper från Experience Platform som är tillgängliga under Profil och mål.](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-audiences.png)

För **[!UICONTROL Profile sync (Update only)]** uppdateras data automatiskt till Campaign-databasen för varje profil som målgruppen har aktiverat i målet.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Översikt över datastyrning](/help/data-governance/home.md).
