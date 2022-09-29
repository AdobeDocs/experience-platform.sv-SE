---
title: Adobe Campaign Managed Cloud Services-anslutning
description: Adobe Campaign Managed Cloud Services är en plattform för att designa flerkanaliga kundupplevelser och en miljö för visuell kampanjsamordning, interaktionshantering i realtid och flerkanalsmarknadsföring.
source-git-commit: 10dc6ac0f78237f8d6bea01d63d07e61662278df
workflow-type: tm+mt
source-wordcount: '1426'
ht-degree: 0%

---

# Adobe Campaign Managed Cloud Services-anslutning {#adobe-campaign-managed-services}

## Översikt {#overview}

Adobe Campaign Managed Cloud Services är en plattform för att designa flerkanaliga kundupplevelser och en miljö för visuell kampanjsamordning, interaktionshantering i realtid och flerkanalsmarknadsföring. [Kom igång med Campaign](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html)

Använd Campaign för att:
* Driv personalisering och engagemang genom en enda lättillgänglig bild av kunden,
* Integrera e-post, mobilkanaler, online- och offlinekanaler i kundresan,
* Automatisera leverans av meningsfulla och aktuella meddelanden och erbjudanden.

>[!IMPORTANT]
>
>Tänk på följande skyddsräcken när du använder Adobe Campaign Managed Cloud Services-anslutningen:
>
>* Högst 50 segment kan vara [aktiverad](#activate) för destinationen,
>* För varje segment kan du lägga till upp till 20 fält i [map](#map) till Adobe Campaign,
>* Datalagring på DLZ (Azure Blob Storage Data Landing Zone): 7 dagar,
>* Aktiveringsfrekvensen är minst 3 timmar.


## Användningsfall {#use-cases}

För att du bättre ska kunna förstå hur och när du ska använda Adobe Campaign Manage Service-målet finns ett exempel på användning som Adobe Experience Platform-kunder kan lösa genom att använda den här destinationen.

Adobe Experience Platform skapar en kundprofil som innehåller information som identitetsdiagram, beteendedata från analyser, sammanfogar offline- och onlinedata osv. Med den här integreringen kan ni utöka de segmenteringsfunktioner som redan finns i Adobe Campaign med de målgrupper som drivs av Adobe Experience Platform, och ni kan därför aktivera dessa data i Campaign.

Ett sportklädföretag vill t.ex. utnyttja de smarta segmenten som drivs av Adobe Experience Platform och aktivera dem med Adobe Campaign för att nå ut till sina kunder via de olika kanaler som stöds av Adobe Campaign.

När meddelandena har skickats vill de förbättra kundprofilen i Adobe Experience-plattformen med upplevelsedata från Adobe Campaign, till exempel skicka, öppna och klicka.

Resultatet är flerkanalskampanjer som är mer enhetliga över hela Adobe Experience Cloud-ekosystemet och en rik kundprofil som snabbt anpassar sig och lär sig.

[Läs mer om Adobe Campaign integrering med Adobe Experience Platform](https://experienceleague.adobe.com/docs/campaign/campaign-v8/connect/ac-aep.html)


## Förutsättningar {#prerequisites}

För att Campaign ska kunna hämta data från Adobe Experience Platform måste ni skapa ett Campaign API-projekt och be kundtjänst att lägga till det associerade klient-ID:t i en tillåtelselista.

>[!NOTE]
>
>Global information om hur du skapar ett API-projekt finns i [den här dokumentationen](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/set-up-developer-console-and-postman.html)

1. Logga in på [Adobe Developer Console](https://console.adobe.io/) och skapa ett nytt projekt.

1. Välj **[!UICONTROL Add API]** och välja **[!UICONTROL Adobe Campaign]**.

   ![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/create-api.png)

1. Skapa ett nyckelpar.

1. Välj `<Instance Name> - admin` produktprofil och välj **[!UICONTROL Save configured API]**.

1. Ditt API-projekt skapas. Anteckning nedåt **[!UICONTROL Client ID]** visas i ditt projekt. Kontakta Adobe kundtjänst och be dem lägga till ditt klient-ID i en tillåtelselista.

   ![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/client-id.png)

## Identiteter som stöds {#supported-identities}

*Adobe Campaign Managed Cloud Services* stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| external_id | Anpassade användar-ID:n | Välj den här målidentiteten när källidentiteten är ett anpassat namnutrymme. Vi rekommenderar att du använder den här identiteten och mappar den till det ID i Campaign-instansen som representerar kund (loyalty_ID, account_ID, customer_ID..) |
| ECID | Experience Cloud ID | Ett namnutrymme som representerar ECID. Detta namnutrymme kan även refereras till av följande alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Se följande dokument på [ECID](/help/identity-service/ecid.md) för mer information. |
| email_lc_sha256 | E-postadresser som hash-kodats med SHA256-algoritmen | Både oformaterad text och SHA256-hashade e-postadresser stöds av Adobe Experience Platform. När källfältet innehåller ohash-kodade attribut markerar du **[!UICONTROL Apply transformation]** alternativ, att ha [!DNL Platform] automatiskt hash-koda data vid aktiveringen. |
| phone_sha256 | Telefonnummer hashas med SHA256-algoritmen | Både oformaterad text och SHA256-hashade telefonnummer stöds av Adobe Experience Platform. När källfältet innehåller ohash-kodade attribut markerar du **[!UICONTROL Apply transformation]** alternativ, att ha [!DNL Platform] automatiskt hash-koda data vid aktiveringen. |
| GAID | Google Advertising ID | Välj målidentiteten för GAID när källidentiteten är ett GAID-namnområde. |
| IDFA | Apple ID för annonsörer | Välj IDFA-målidentitet när din källidentitet är ett IDFA-namnutrymme. |

{style=&quot;table-layout:auto&quot;}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla medlemmar i ett segment tillsammans med önskade schemafält (till exempel: e-postadress, telefonnummer, efternamn), som du har valt på skärmen Välj profilattribut i [arbetsflöde för målaktivering](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrekvens | **[!UICONTROL Batch]** | Batchdestinationer exporterar filer till efterföljande plattformar i steg om tre, sex, åtta, tolv eller tjugofyra timmar. Läs mer om [gruppfilsbaserade mål](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/destination-details.png)

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Select instance]**: Dina **[!DNL Campaign]** marknadsinstans.
* **[!UICONTROL Target mapping]**: Välj den målmappning som du använder i **[!DNL Adobe Campaign]** för att skicka leveranser. [Läs mer](https://experienceleague.adobe.com/docs/campaign/campaign-v8/profiles-and-audiences/add-profiles/target-mappings.html).

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om status för ditt dataflöde. Mer information om varningar finns i guiden om [prenumerera på destinationsvarningar med hjälp av användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

### Styrningspolicy och verkställighetsåtgärder {#governance}

Välj de marknadsföringsåtgärder som gäller för de data som du vill exportera till målet. För Adobe Campaign rekommenderar vi att du väljer **[!UICONTROL Email Targeting]** marknadsföringsåtgärder.

Mer information om marknadsföringsåtgärder finns i [dataanvändningsprinciper - översikt](/help/data-governance/policies/overview.md) sida.

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
> 
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Läs [Aktivera målgruppsdata för att batchprofilera exportmål](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html) för instruktioner om hur målgruppsdata aktiveras till det här målet.

### Mappa attribut och identiteter {#map}

Välj XDM-fält som ska exporteras med profilerna och mappa dem till motsvarande Adobe Campaign-fält.[Läs mer om val av identitet och attribut för e-postmarknadsföringsmål](overview.md)

1. Välj källfält:

   * Välj en **identifierare** (Exempel: e-postfältet) som källidentitet som unikt identifierar en profil i Adobe Experience Platform och Adobe Campaign.

   * Markera alla andra **XDM-källprofilattribut** som behöver exporteras till Adobe Campaign.
   >[!NOTE]
   >
   >Fältet&quot;segmentMembershipStatus&quot; är en obligatorisk mappning som återspeglar statusen för segmentMembership. Det här fältet läggs till som standard och kan inte ändras eller tas bort.

1. Mappa varje fält med målfältet i Adobe Campaign. Tillgängliga målfält bestäms av den valda målmappningen när [skapa målet](#destination-details).

1. Identifiera obligatoriska attribut och dedupliceringsnycklar. Observera att värden i attribut som är markerade som&quot;Obligatorisk&quot; eller&quot;Avdupliceringsnyckel&quot; inte kan vara null.

   * [Obligatoriska attribut](../../ui/activate-batch-profile-destinations.md#mandatory-attributes) se till att alla profilposter innehåller de valda attributen. Till exempel: alla exporterade profiler innehåller en e-postadress. Rekommendationen är att ställa in på obligatorisk både identitetsfältet och fältet som används som dedupliceringsnyckel.
   * [En dedupliceringsnyckel](../../ui/activate-batch-profile-destinations.md#mandatory-attributes) är en primärnyckel som bestämmer identiteten som användarna vill att deras profiler ska dedupliceras med.

      >[!IMPORTANT]
      >
      >Kontrollera att namnet på dedupliceringsnyckelattributet matchar ett kolumnnamn för den valda målmappningen.
   ![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/mapping.png)

1. När mappningen har utförts kan du granska och slutföra målkonfigurationen för att börja skicka data till **[!DNL Campaign]**.
   [Lär dig hur du granskar och slutför målkonfigurationen](/help/destinations/destination-types.md#review).

## Exporterade data/Validera dataexport {#exported-data}

När ett mål har aktiverats kan du komma åt motsvarande jobb och exporterade data i Campaign.

### Övervaka dataexportjobb {#jobs}

Navigera till **[!UICONTROL Administration]** > **[!UICONTROL Audit]** > **[!UICONTROL Audience load jobs]** för att övervaka alla exportjobb som aktiveras från Adobe Experience Platform.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-jobs.png)

### Få åtkomst till exporterade data {#data}

Navigera till **[!UICONTROL Profile and target]** > **[!UICONTROL List]** > **[!UICONTROL AEP audiences]** för att få åtkomst till målgrupper som skapats efter att ett mål har aktiverats.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-audiences.png)

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, läs [Datastyrning - översikt](/help/data-governance/home.md).
