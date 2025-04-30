---
title: (V2) Audience-anslutning för Pega CDH Realtime
description: Använd målplatsen Pega Customer Decision Hub Realtime Audience i Adobe Experience Platform för att skicka profilattribut och data om målgruppsmedlemskap till Pega Customer Decision Hub för beslut om nästa bästa åtgärd.
source-git-commit: cc18f5c9445e5d08565cd5ac4bcbdb11ccbc1a31
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# (V2) Audience-anslutning för Pega CDH Realtime

## Översikt {#overview}

Använd målet (V2) [!DNL Pega CDH Realtime Audience] i Adobe Experience Platform för att skicka profilattribut och målgruppsmedlemskapsdata till [!DNL Pega Customer Decision Hub] för nästa beslut om bästa åtgärd.

Profilmedlemskap från Adobe Experience Platform kan, när det läses in till [!DNL Pega Customer Decision Hub], användas som prediktor i adaptiva modeller och hjälpa till att leverera rätt kontextuella data och beteendedata för beslutsfattande i nästa steg.

>[!IMPORTANT]
>
>Målanslutningen och dokumentationssidan skapas och underhålls av Pegasystems. Om du har frågor eller uppdateringsfrågor kontaktar du Pega direkt [här](mailto:support@pega.com).

## Användningsfall {#use-cases}

För att du bättre ska kunna förstå hur och när du ska använda målet [!DNL Customer Decision Hub] finns det exempel på användning som Adobe Experience Platform-kunder kan lösa genom att använda det här målet.

### Telekommunikation {#telecommunications}

En marknadsförare vill utnyttja insikter från datavetenskapens modellbaserade nästa bästa åtgärd som levereras av [!DNL Pega Customer Decision Hub] för kundengagemang. [!DNL Pega Customer Decision Hub] är i hög grad beroende av kundens avsikter, till exempel&quot;Interested_In_5G&quot;,&quot;Interested_in_Unlimited_Dataplan&quot; eller&quot;Interest_in_iPhone_accessers&quot;, för att avgöra NBA-beslut (next-best-action) i utgående kanaler.

### Finansiella tjänster {#financial-services}

En marknadsförare vill optimera erbjudandena för kunder som prenumererar på eller avbeställer nyhetsbrev om pensionsavtal eller pensionsavtal. Företag inom finanssektorn kan importera flera kund-ID:n från sina egna CRM till Adobe Experience Platform, bygga målgrupper utifrån sina egna offlinedata och skicka profiler som kommer in i och lämnar målgrupperna till [!DNL Pega Customer Decision Hub] för NBA-beslut (next-best-action) i utgående kanaler.

## Förhandskrav {#prerequisites}

Innan du kan använda det här målet för att exportera data från Adobe Experience Platform måste du uppfylla följande krav i [!DNL Pega Customer Decision Hub]:

* Konfigurera integrationskomponenten [Adobe Experience Platform Profile och Audience Membership](https://docs.pega.com/bundle/components/page/customer-decision-hub/components/adobe-membership-component.html) i din [!DNL Pega Customer Decision Hub]-instans.
* Konfigurera OAuth 2.0 [klientregistrering med typen Klientautentiseringsuppgifter](https://docs.pega.com/bundle/platform/page/platform/security/configure-oauth-2-client-registration.html) i din [!DNL Pega Customer Decision Hub]-instans.
* Konfigurera [dataflödet för körning i realtid](https://docs.pega.com/bundle/platform/page/platform/decision-management/data-flow-run-real-time-create.html) för dataflödet för Adobe-målgruppsmedlemskap i din [!DNL Pega Customer Decision Hub]-instans.

## Identiteter som stöds {#supported-identities}

[!DNL Pega Customer Decision Hub] stöder aktivering av anpassade användar-ID:n som beskrivs i tabellen nedan. Mer information finns i [identiteter](/help/identity-service/features/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| `CustomerID` | Kund-ID | En vanlig användaridentifierare som unikt identifierar en profil i [!DNL Pega Customer Decision Hub] och Adobe Experience Platform. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Exportera alla medlemmar i en målgrupp med ID (*CustomerID*), attribut (efternamn, förnamn, plats osv.) och data för målgruppsmedlemskap. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform, baserat på målgruppsutvärdering, skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Mer information finns i [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

#### Autentisering med OAuth 2-klientautentiseringsuppgifter {#oauth-2-client-credentials-authentication}

![Bild av gränssnittsskärmen där du kan ansluta till Pega CDH-målet med OAuth 2 med autentisering av klientautentiseringsuppgifter](../../assets/catalog/personalization/pega/pega-api-authentication-oauth2-client-credentials.png)

Fyll i fälten nedan och välj **[!UICONTROL Connect to destination]**:

* **[!UICONTROL Access Token URL]**: Åtkomsttoken-URL:en för OAuth 2 på din [!DNL Pega Customer Decision Hub]-instans.
* **[!UICONTROL Client ID]**: OAuth 2 [!DNL client ID] som du genererade i din [!DNL Pega Customer Decision Hub]-instans.
* **[!UICONTROL Client Secret]**: OAuth 2 [!DNL client secret] som du genererade i din [!DNL Pega Customer Decision Hub]-instans.

### Fyll i målinformation {#destination-details}

När du har upprättat autentiseringsanslutningen till [!DNL Pega Customer Decision Hub] anger du följande information för målet:

![Bild av gränssnittsskärmen som visar slutförda fält för målinformationen för Pega CDH ](../../assets/catalog/personalization/pega/pega-connect-destination-v2.png)

Om du vill konfigurera information för målet fyller du i de obligatoriska fälten och väljer **[!UICONTROL Next]**.

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Pega CDH Host Name]**: Värdnamn för Pega-kunds beslutshubben som profilen exporteras till som JSON-data.
* **[!UICONTROL Application alias]**: Det programalias som du konfigurerade för ditt Kundbesluts-hubbkonto. Mer information finns i [Lägga till ett program-URL-alias](https://docs.pega.com/bundle/platform/page/platform/user-experience/adding-application-url-alias.html) i din [!DNL Pega Customer Decision Hub]-instans.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Se [Aktivera målgruppsdata för att direktuppspela profilexportmål](../../ui/activate-streaming-profile-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

### Mappning {#mapping}

I steget [!UICONTROL Mapping] väljer du en unik identifierare från ditt unionsschema och alla andra XDM-fält som du vill exportera till målet.

### Mappningsexempel: aktiverar profiluppdateringar i [!DNL Pega Customer Decision Hub] {#mapping-example}

Nedan visas ett exempel på korrekt identitetsmappning när profiler exporteras till [!DNL Pega Customer Decision Hub].

* Välj en källidentitet som unikt identifierar en profil i Adobe Experience Platform och [!DNL Pega Customer Decision Hub]. Till exempel: `CustomerID`.
* Välj de målprofilattribut som du vill mappa de valda källprofilattributen till.

![Identitetsmappning](../../assets/catalog/personalization/pega/pega-source-destination-mapping.png)

## Exporterade data/Validera dataexport {#exported-data}

En lyckad uppdatering av ett målgruppsmedlemskap för en profil skulle infoga målgruppsidentifieraren, namnet och statusvärdena i Pegas medlemskapsdatabas för marknadsföringspubliker. Medlemskapsinformationen är kopplad till en kund med Designer för kundprofil i [!DNL Pega Customer Decision Hub], vilket visas nedan.
![Bild av användargränssnittsskärmen där du kan koppla Adobe-målgruppsmedlemskapsdata till kunden med hjälp av Designer för kundprofil](../../assets/catalog/personalization/pega/pega-profile-designer-associate.png)

Målgruppsmedlemskapsdata används i Pega Next-Best-Action Designer Engagement policies för nästa bästa åtgärd, vilket visas nedan.
![Bild av användargränssnittsskärmen där du kan lägga till fält för målgruppsmedlemskap som villkor i Villkor för användarprofiler för Pega Designer för nästa bästa åtgärd](../../assets/catalog/personalization/pega/pega-profile-designer-engagment.png)

Datafälten för kundens målgruppsmedlemskap läggs till som prediktorer i adaptiva modeller, vilket visas nedan.
![Bild av gränssnittsskärmen där du kan lägga till fält för målgruppsmedlemskap som prediktorer i adaptiva modeller med Predication Studio](../../assets/catalog/personalization/pega/pega-profile-designer-adaptivemodel.png)

## Ytterligare resurser {#additional-resources}

Mer information finns i följande [!DNL Pega]-dokumentation:
* [Konfigurerar en OAuth 2.0-klientregistrering](https://docs.pega.com/bundle/platform/page/platform/security/configure-oauth-2-client-registration.html)
* [Skapa en körning i realtid för dataflöden](https://docs.pega.com/bundle/platform/page/platform/decision-management/data-flow-run-real-time-create.html)
* [Hantera kundposter i kundprofilen Designer](https://docs.pega.com/bundle/customer-decision-hub/page/customer-decision-hub/implement/profile-designer-data-management.html)

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Datastyrningsöversikten](/help/data-governance/home.md).
