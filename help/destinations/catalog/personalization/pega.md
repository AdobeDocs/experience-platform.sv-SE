---
title: Pega-anslutning för kundens beslutshubb
description: Använd Pega Customer Decision Hub-destinationen i Adobe Experience Platform för att skicka profilattribut och data om segmentmedlemskap till Pega Customer Decision Hub för beslut om nästa bästa åtgärd.
exl-id: 0546da5d-d50d-43ec-bbc2-9468a7db4d90
source-git-commit: ae00b113308354e98f4448d2544e2a6e475c384e
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 0%

---

# Pega-anslutning för kundens beslutshubb

## Översikt {#overview}

Använd [!DNL Pega Customer Decision Hub] mål i Adobe Experience Platform att skicka profilattribut och segmentmedlemskapsdata till [!DNL Pega Customer Decision Hub] för nästa bästa-åtgärd-beslut.

Profilsegmentsmedlemskap från Adobe Experience Platform, vid inläsning till [!DNL Pega Customer Decision Hub], kan användas som prediktor i adaptiva modeller och bidra till att leverera rätt kontextuella data och beteendedata för nästa bästa åtgärd-beslut.

>[!IMPORTANT]
>
>Den här dokumentationssidan skapades av Pegasystems. Kontakta Pega direkt för frågor eller uppdateringsförfrågningar [här](mailto:support@pega.com).

## Användningsfall

För att du bättre ska förstå hur och när du ska använda [!DNL Customer Decision Hub] mål, här är exempel på användningsområden som Adobe Experience Platform-kunder kan lösa genom att använda den här destinationen.

### Telekommunikation

En marknadsförare vill utnyttja insikter från datavetenskapens modellbaserade nästa bästa åtgärd som levereras av [!DNL Pega Customer Decision Hub] för kundengagemang. [!DNL Pega Customer Decision Hub] är starkt beroende av kundens avsikter - till exempel&quot;Interested_In_5G&quot;,&quot;Interested_in_Unlimited_Dataplan&quot; eller&quot;Interest_in_iPhone_accessers&quot;.

### Finansiella tjänster

En marknadsförare vill optimera erbjudandena för kunder som prenumererar på eller avbeställer nyhetsbrev om pensionsavtal eller pensionsavtal. Företag inom finanssektorn kan importera flera kund-ID:n från sina egna CRM till Adobe Experience Platform, bygga segment utifrån sina egna offlinedata och skicka profiler som anger och avslutar segmenten till [!DNL Pega Customer Decision Hub] för NBA-beslut (next-best-action) i utgående kanaler.

## Förutsättningar {#prerequisites}

Innan du kan använda det här målet för att exportera data från Adobe Experience Platform måste du uppfylla följande krav i [!DNL Pega Customer Decision Hub]:

* Konfigurera [Integrationskomponent för Adobe Experience Platform-profil och segmentmedlemskap](https://docs.pega.com/component/customer-decision-hub/adobe-experience-platform-profile-and-segment-membership-integration-component) i [!DNL Pega Customer Decision Hub] -instans.
* Konfigurera OAuth 2.0 [Klientregistrering med klientautentiseringsuppgifter](https://docs.pega.com/security/87/creating-and-configuring-oauth-20-client-registration) Typ av bidrag i din [!DNL Pega Customer Decision Hub] -instans.
* Konfigurera [dataflöde vid körning i realtid](https://docs.pega.com/decision-management/87/creating-real-time-run-data-flows) för Adobe segmentmedlemskapets dataflöde i [!DNL Pega Customer Decision Hub] -instans.

## Identiteter som stöds {#supported-identities}

[!DNL Pega Customer Decision Hub] har stöd för aktivering av anpassade användar-ID:n som beskrivs i tabellen nedan. Mer information finns i [identiteter](/help/identity-service/namespaces.md).

| Målidentitet | Beskrivning |
|---|---|
| *CustomerID* | Vanlig användaridentifierare som unikt identifierar en profil i [!DNL Pega Customer Decision Hub] och Adobe Experience Platform |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Exportera alla medlemmar i ett segment med identifierare (*CustomerID*), attribut (efternamn, förnamn, plats osv.) och segmentmedlemskapsdata. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform, baserat på segmentutvärdering, skickar kopplingen uppdateringen nedåt till målplattformen. Mer information finns i [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

#### Autentisering med OAuth 2-klientautentiseringsuppgifter {#oauth-2-client-credentials-authentication}

![Bild av gränssnittsskärmen där du kan ansluta till Pega CDH-målet med hjälp av OAuth 2 med autentisering av klientautentiseringsuppgifter](../../assets/catalog/personalization/pega/pega-api-authentication-oauth2-client-credentials.png)

Fyll i fälten nedan och välj **[!UICONTROL Connect to destination]**:

* **[!UICONTROL Access Token URL]**: URL:en för OAuth 2-åtkomsttoken på din [!DNL Pega Customer Decision Hub] -instans.
* **[!UICONTROL Client ID]**: The OAuth 2 [!DNL client ID] som du har skapat i [!DNL Pega Customer Decision Hub] -instans.
* **[!UICONTROL Client Secret]**: The OAuth 2 [!DNL client secret] som du har skapat i [!DNL Pega Customer Decision Hub] -instans.

### Fyll i målinformation {#destination-details}

När autentiseringsanslutningen till [!DNL Pega Customer Decision Hub]Ange följande information för destinationen:

![Bild av gränssnittsskärmen som visar slutförda fält för målinformationen för Pega CDH](../../assets/catalog/personalization/pega/pega-connect-destination.png)

Om du vill konfigurera information för målet fyller du i de obligatoriska fälten och väljer **[!UICONTROL Next]**.

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Host Name]**: Värdnamnet för Pega-kundens beslutshubben som profilen exporteras till som json-data.

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
> 
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Se [Aktivera målgruppsdata till exportmål för direktuppspelningsprofiler](../../ui/activate-streaming-profile-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

### Målattribut {#attributes}

I [[!UICONTROL Select attributes]](../../ui/activate-streaming-profile-destinations.md#select-attributes) Adobe rekommenderar att du väljer en unik identifierare från [union](../../../profile/home.md#profile-fragments-and-union-schemas). Välj den unika identifieraren och eventuella andra XDM-fält som du vill exportera till målet.

### Mappningsexempel: aktivera profiluppdateringar i [!DNL Pega Customer Decision Hub] {#mapping-example}

Nedan visas ett exempel på korrekt identitetsmappning när profiler exporteras till [!DNL Pega Customer Decision Hub].

Välja källfält:

* Välj en identifierare (till exempel: CustomerID) som källidentitet som unikt identifierar en profil i Adobe Experience Platform och [!DNL Pega Customer Decision Hub].
* Välj ändringar i XDM-källprofilsattribut som behöver exporteras och uppdateras i [!DNL Pega Customer Decision Hub].

Markera målfält:

* Välj `CustomerID` namespace som target identity.
* Markera attributnamn för målprofil som måste mappas till motsvarande XDM-källprofilattribut.

![Identitetsmappning](../../assets/catalog/personalization/pega/pega-source-destination-mapping.png)

## Exporterade data/Validera dataexport {#exported-data}

En lyckad uppdatering av ett segmentmedlemskap för en profil skulle infoga segmentidentifieraren, namnet och statusvärdena i Pegas Marketing Segment-medlemskapets datalager. Medlemskapsinformationen är kopplad till en kund med hjälp av kundprofildesignern i [!DNL Pega Customer Decision Hub], vilket visas nedan.
![Bild av användargränssnittsskärmen där du kan associera Adobe-segmentmedlemskapsdata till kunden med hjälp av kundprofildesignern](../../assets/catalog/personalization/pega/pega-profile-designer-associate.png)

Segmentmedlemskapsdata används i Pega Designer Engagement policies för nästa bästa åtgärd, vilket visas nedan.
![Bild av gränssnittsskärmen där du kan lägga till fält för segmentmedlemskap som villkor i Pegas interaktionsregler för Designer för nästa bästa åtgärd](../../assets/catalog/personalization/pega/pega-profile-designer-engagment.png)

Datafälten för medlemskap i kundsegment läggs till som prediktorer i adaptiva modeller, vilket visas nedan.
![Bild av gränssnittsskärmen där du kan lägga till segmentmedlemsfält som prediktorer i adaptiva modeller med Predication Studio](../../assets/catalog/personalization/pega/pega-profile-designer-adaptivemodel.png)

## Ytterligare resurser {#additional-resources}

Se [Konfigurera en OAuth 2.0-klientregistrering](https://docs.pega.com/security/87/creating-and-configuring-oauth-20-client-registration) in [!DNL Pega Customer Decision Hub].

Se [Skapa en körning i realtid för dataflöden](https://docs.pega.com/decision-management/87/creating-real-time-run-data-flows) in [!DNL Pega Customer Decision Hub].

Se [Hantera kundposter i kundprofildesignern](https://docs.pega.com/whats-new-pega-platform/manage-customer-records-customer-profile-designer-86).

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, se [Datastyrning - översikt](/help/data-governance/home.md).
