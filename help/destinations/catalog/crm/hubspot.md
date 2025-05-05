---
title: HubSpot-anslutning
description: Med HubSpot-målet kan du hantera kontaktposter i ditt HubSpot-konto.
last-substantial-update: 2023-09-28T00:00:00Z
exl-id: e2114bde-b7c3-43da-9f3a-919322000ef4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 0%

---

# [!DNL HubSpot]-anslutning

[[!DNL HubSpot]](https://www.hubspot.com) är en CRM-plattform med all programvara, alla integreringar och resurser du behöver för att koppla samman marknadsföring, försäljning, innehållshantering och kundtjänst. Ni kan koppla samman data, team och kunder på en och samma CRM-plattform.

Det här [!DNL Adobe Experience Platform] [målet](/help/destinations/home.md) använder [[!DNL HubSpot] kontakt-API](https://developers.hubspot.com/docs/api/crm/contacts) för att uppdatera kontakter inom [!DNL HubSpot] från en befintlig Experience Platform-målgrupp efter aktivering.

Instruktioner för autentisering till din [!DNL HubSpot]-instans finns längre ned i avsnittet [Autentisera till mål](#authenticate).

## Användningsfall {#use-cases}

För att du bättre ska kunna förstå hur och när du ska använda målet [!DNL HubSpot] finns det ett exempel på användning som Adobe Experience Platform-kunder kan lösa genom att använda det här målet.

[!DNL HubSpot] kontakter lagrar information om de personer som interagerar med ditt företag. Ditt team använder de kontakter som finns i [!DNL HubSpot] för att skapa Experience Platform-målgrupper. När dessa målgrupper har skickats till [!DNL HubSpot] uppdateras deras information och varje kontakt tilldelas en egenskap med dess värde som målgruppsnamn som anger vilken målgrupp kontakten tillhör.

## Förhandskrav {#prerequisites}

I avsnitten nedan finns information om eventuella krav som du måste ställa in i Experience Platform och [!DNL HubSpot] och om information som du måste samla in innan du kan arbeta med målet för [!DNL HubSpot].

### Krav för Experience Platform {#prerequisites-in-experience-platform}

Innan du aktiverar data till målet [!DNL HubSpot] måste du ha ett [schema](/help/xdm/schema/composition.md), en [datamängd](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=sv-SE) och [målgrupper](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html?lang=sv-SE) som skapats i [!DNL Experience Platform].

Se Experience Platform-dokumentationen för schemafältgruppen [Information om målgruppsmedlemskap](/help/xdm/field-groups/profile/segmentation.md) om du behöver vägledning om målgruppsstatus.

### Krav för målet [!DNL HubSpot] {#prerequisites-destination}

Observera följande krav för att kunna exportera data från Experience Platform till ditt [!DNL HubSpot]-konto:

#### Du måste ha ett [!DNL HubSpot]-konto {#prerequisites-account}

Om du vill exportera data från Experience Platform till ditt [!DNL Hubspot]-konto måste du ha ett [!DNL HubSpot]-konto. Om du inte redan har en kan du gå till sidan [Konfigurera ditt HubSpot-konto](https://knowledge.hubspot.com/get-started/set-up-your-account) och följa anvisningarna för att registrera och skapa ditt konto.

#### Samla in åtkomsttoken för det privata programmet [!DNL HubSpot] {#gather-credentials}

Du behöver din [!DNL HubSpot] `Access token` för att [!DNL HubSpot]-destinationen ska kunna göra API-anrop via din privata [!DNL HubSpot]-app i ditt [!DNL HubSpot]-konto. `Access token` fungerar som `Bearer token` när du [autentiserar målet](#authenticate).

Om du inte har någon privat app följer du dokumentationen för att [skapa en privat app i [!DNL HubSpot]](https://developers.hubspot.com/docs/api/private-apps).

>[!IMPORTANT]
>
> Det privata programmet bör tilldelas följande omfång:
> `crm.objects.contacts.write`, `crm.objects.contacts.read`
> `crm.schemas.contacts.write`, `crm.schemas.contacts.read`

| Autentiseringsuppgifter | Beskrivning | Exempel |
| --- | --- | --- |
| `Bearer token` | `Access token` för din privata [!DNL HubSpot]-app. <br>Om du vill hämta din [!DNL HubSpot] `Access token` följer du [!DNL HubSpot]-dokumentationen för att [göra API-anrop med din apps åtkomsttoken](https://developers.hubspot.com/docs/api/private-apps#make-api-calls-with-your-app-s-access-token). | `pat-na1-11223344-abcde-12345-9876-1234a1b23456` |

## Guardrails {#guardrails}

[!DNL HubSpot] privata appar omfattas av [tariffgränser](https://developers.hubspot.com/docs/api/usage-details). Antalet samtal som din privata app kan ringa baseras på din [!DNL HubSpot]-kontoprenumeration och om du har köpt API-tillägget. Se även [Andra gränser](https://developers.hubspot.com/docs/api/usage-details#other-limits).

## Identiteter som stöds {#supported-identities}

[!DNL HubSpot] har stöd för uppdatering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Målidentitet | Exempel | Beskrivning | Överväganden |
|---|---|---|---|
| `email` | `test@test.com` | Kontaktens e-postadress. | Obligatoriskt |

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs alla målgrupper som du kan exportera till det här målet.

Det här målet stöder aktivering av alla målgrupper som genereras via Experience Platform [segmenteringstjänst](../../../segmentation/home.md).

Detta mål stöder även aktivering av målgrupperna som beskrivs i tabellen nedan.

| Målgruppstyp | Beskrivning |
|---------|----------|
| Anpassade överföringar | Publikerna [importerade](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | <ul><li>Du exporterar alla medlemmar i en målgrupp tillsammans med de önskade schemafälten *(till exempel e-postadress, telefonnummer, efternamn)*, enligt fältmappningen.</li><li> Dessutom skapas en ny egenskap i [!DNL HubSpot] med målgruppsnamnet och dess värde är med motsvarande målgruppsstatus från Experience Platform, för var och en av de valda målgrupperna.</li></ul> |
| Exportfrekvens | **[!UICONTROL Streaming]** | <ul><li>Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
>
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

I **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** söker du efter [!DNL HubSpot]. Du kan också hitta den under kategorin **[!UICONTROL CRM]**.

### Autentisera till mål {#authenticate}

Fyll i de obligatoriska fälten nedan. Mer information finns i avsnittet [Samla in  [!DNL HubSpot] åtkomsttoken för privata appar](#gather-credentials).
* **[!UICONTROL Bearer token]**: Åtkomsttoken för din privata [!DNL HubSpot]-app.

Om du vill autentisera till målet väljer du **[!UICONTROL Connect to destination]**.
![Experience Platform UI, bild som visar hur du autentiserar.](../../assets/catalog/crm/hubspot/authenticate-destination.png)

Om den angivna informationen är giltig visas statusen **[!UICONTROL Connected]** med en grön bockmarkering. Du kan sedan gå vidare till nästa steg.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.
![Experience Platform UI-skärmbild med målinformation.](../../assets/catalog/crm/hubspot/destination-details.png)

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
>
>För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Läs [Aktivera profiler och målgrupper för att direktuppspela målgruppsexportdestinationer](/help/destinations/ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

### Mappa attribut och identiteter {#map}

Om du vill skicka målgruppsdata från Adobe Experience Platform till målet [!DNL HubSpot] måste du gå igenom fältmappningssteget. Mappningen består av att skapa en länk mellan XDM-schemafälten (Experience Data Model) i ditt Experience Platform-konto och deras motsvarande motsvarigheter från målmålet.

Följ stegen nedan för att mappa dina XDM-fält korrekt till målfälten för [!DNL HubSpot]:

#### Mappar identiteten `Email`

Identiteten `Email` är en obligatorisk mappning för det här målet. Följ stegen nedan för att mappa den:
1. Välj **[!UICONTROL Add new mapping]** i steget **[!UICONTROL Mapping]**. Nu kan du se en ny mappningsrad på skärmen.
   ![Experience Platform UI, skärmbild med knappen Lägg till ny mappning markerad.](../../assets/catalog/crm/hubspot/mapping-add-new-mapping.png)
1. I fönstret **[!UICONTROL Select source field]** väljer du **[!UICONTROL Select identity namespace]** och väljer en identitet.
   ![Experience Platform UI, skärmbild där e-post väljs som ett källattribut att mappa som identitet.](../../assets/catalog/crm/hubspot/mapping-select-source-identity.png)
1. I fönstret **[!UICONTROL Select target field]** väljer du **[!UICONTROL Select attributes]** och sedan `email`.
   ![Experience Platform UI, skärmbild som markerar e-post som ett målattribut att mappa som identitet.](../../assets/catalog/crm/hubspot/mapping-select-target-identity.png)

| Source Field | Målfält | Obligatoriskt |
| --- | --- | --- |
| `IdentityMap: Email` | `Identity: email` | Ja |

Ett exempel med identitetsmappning visas nedan:
![Exempel på skärmbild i Experience Platform UI med mappning av e-postidentitet.](../../assets/catalog/crm/hubspot/mapping-identities.png)

#### Mappa **valfria** attribut

Om du vill lägga till andra attribut som du vill uppdatera mellan XDM-profilschemat och ditt [!DNL HubSpot]-konto upprepar du stegen nedan:
1. Välj **[!UICONTROL Add new mapping]** i steget **[!UICONTROL Mapping]**. Nu kan du se en ny mappningsrad på skärmen.
   ![Experience Platform UI, skärmbild med knappen Lägg till ny mappning markerad.](../../assets/catalog/crm/hubspot/mapping-add-new-mapping.png)
1. I fönstret **[!UICONTROL Select source field]** väljer du kategorin **[!UICONTROL Select attributes]** och väljer XDM-attributet.
   ![Experience Platform UI, skärmbild som väljer Förnamn som källattribut.](../../assets/catalog/crm/hubspot/mapping-select-source-attribute.png)
1. Välj kategorin **[!UICONTROL Select attributes]** i fönstret **[!UICONTROL Select target field]** och välj i listan över attribut som fylls i automatiskt från ditt [!DNL HubSpot]-konto. Målet använder API:t [[!DNL HubSpot] Properties](https://developers.hubspot.com/docs/api/crm/properties) för att hämta den här informationen. Både [!DNL HubSpot] [standardegenskaper](https://knowledge.hubspot.com/contacts/hubspots-default-contact-properties) och eventuella anpassade egenskaper hämtas för markering som målfält.
   ![Experience Platform UI, skärmbild som väljer Förnamn som målattribut.](../../assets/catalog/crm/hubspot/mapping-select-target-attribute.png)

Några tillgängliga mappningar mellan ditt XDM-profilschema och [!DNL Hubspot] visas nedan:

| Source Field | Målfält |
| --- | --- |
| `xdm: person.name.firstName` | `Attribute: firstname` |
| `xdm: person.name.lastName` | `Attribute: lastname` |
| `xdm: workAddress.street1` | `Attribute: address` |
| `xdm: workAddress.city` | `Attribute: city` |
| `xdm: workAddress.country` | `Attribute: country` |

Ett exempel som använder dessa attributmappningar visas nedan:
![Exempel på skärmbild i Experience Platform UI med attributmappningar.](../../assets/catalog/crm/hubspot/mapping-attributes.png)

Välj **[!UICONTROL Next]** när du är klar med mappningarna för målanslutningen.

## Validera dataexport {#exported-data}

Följ stegen nedan för att verifiera att du har konfigurerat målet korrekt:

1. Logga in på webbplatsen [!DNL HubSpot] och navigera sedan till sidan **[!UICONTROL Contacts]** för att kontrollera målgruppsstatus. Den här listan kan konfigureras för att visa kolumner för anpassade egenskaper som har skapats med målgruppens namn och deras värde är målgruppsstatus.
   ![HubSpot UI, skärmbild som visar sidan Kontakter med kolumnrubriker som visar målgruppsnamnet och cellernas målgruppsstatus](../../assets/catalog/crm/hubspot/contacts.png)

1. Du kan även gå ned på en enskild **[!UICONTROL Person]**-sida och navigera till egenskaperna som visar målgruppens namn och målgruppens status.
   ![HubSpot UI-skärmbild som visar kontaktsidan med anpassade egenskaper som visar målgruppens namn och målgruppens status.](../../assets/catalog/crm/hubspot/contact.png)

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Datastyrningsöversikten](/help/data-governance/home.md).

## Ytterligare resurser {#additional-resources}

Ytterligare användbar information från dokumentationen för [!DNL HubSpot] finns nedan:
* [Autentiseringsmetoder på HubSpot](https://developers.hubspot.com/docs/api/intro-to-auth)
* [!DNL HubSpot] API-referenser för API:erna [Kontakter](https://developers.hubspot.com/docs/api/crm/contacts) och [Egenskaper](https://developers.hubspot.com/docs/api/crm/properties).

### Changelog

I det här avsnittet beskrivs funktionaliteten och viktiga dokumentationsuppdateringar för den här målanslutningen.

+++ Visa ändringslogg

| Releasamånad | Uppdateringstyp | Beskrivning |
|---|---|---|
| September 2023 | Inledande version | Ursprunglig målversion och dokumentationspublicering. |

{style="table-layout:auto"}

+++
