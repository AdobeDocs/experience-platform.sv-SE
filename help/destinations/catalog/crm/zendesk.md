---
title: Zendesk-anslutning
description: Med Zendesk-destinationen kan du exportera dina kontouppgifter och aktivera dem i Zendesk efter behov.
last-substantial-update: 2023-03-14T00:00:00Z
exl-id: e7fcbbf4-5d6c-4abb-96cb-ea5b67a88711
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1408'
ht-degree: 1%

---

# [!DNL Zendesk]-anslutning

[[!DNL Zendesk]](https://www.zendesk.com) är en kundtjänstlösning och ett säljverktyg.

Det här [!DNL Adobe Experience Platform] [målet](/help/destinations/home.md) använder [[!DNL Zendesk] kontakt-API](https://developer.zendesk.com/api-reference/sales-crm/resources/contacts/) för att **skapa och uppdatera identiteter** inom en målgrupp som kontakter inom [!DNL Zendesk].

[!DNL Zendesk] använder innehavartoken som en autentiseringsmekanism för att kommunicera med [!DNL Zendesk] Contacts API. Instruktioner för autentisering till din [!DNL Zendesk]-instans finns längre ned i avsnittet [Autentisera till mål](#authenticate).

## Användningsfall {#use-cases}

Kundtjänstavdelningen på en flerkanalig B2C-plattform vill säkerställa en sömlös och personaliserad upplevelse för sina kunder. Avdelningen kan skapa målgrupper utifrån sina egna offlinedata för att skapa nya användarprofiler eller uppdatera befintlig profilinformation från olika interaktioner (t.ex. köp, returer osv.) och skicka dessa målgrupper från Adobe Experience Platform till [!DNL Zendesk]. Genom att ha den uppdaterade informationen i [!DNL Zendesk] kan kundtjänstagenten få den senaste informationen om kunden omedelbart tillgänglig, vilket ger snabbare svar och lösningar.

## Förhandskrav {#prerequisites}

### Krav för Experience Platform {#prerequisites-in-experience-platform}

Innan du aktiverar data till målet [!DNL Zendesk] måste du ha ett [schema](/help/xdm/schema/composition.md), en [datamängd](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) och [segment](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) som skapats i [!DNL Experience Platform].

Se Experience Platform-dokumentationen för schemafältgruppen [Information om målgruppsmedlemskap](/help/xdm/field-groups/profile/segmentation.md) om du behöver vägledning om målgruppsstatus.

### Krav för [!DNL Zendesk] {#prerequisites-destination}

Om du vill exportera data från Experience Platform till ditt [!DNL Zendesk]-konto måste du ha ett [!DNL Zendesk]-konto.

#### Samla in inloggningsuppgifter för [!DNL Zendesk] {#gather-credentials}

Observera objekten nedan innan du autentiserar till målet [!DNL Zendesk]:

| Autentiseringsuppgifter | Beskrivning | Exempel |
| --- | --- | --- |
| `Bearer token` | Åtkomsttoken som du har skapat i ditt [!DNL Zendesk]-konto. <br> Följ dokumentationen för att [generera en [!DNL Zendesk] åtkomsttoken](https://developer.zendesk.com/documentation/sales-crm/first-call/#1-generate-an-access-token) om du inte har någon. | `a0b1c2d3e4...v20w21x22y23z` |

## Guardrails {#guardrails}

Sidan [Pris- och prisgränser](https://developer.zendesk.com/api-reference/sales-crm/rate-limits/#pricing) innehåller information om de [!DNL Zendesk] API-gränser som är kopplade till ditt konto. Du måste se till att dina data och din nyttolast är inom dessa begränsningar.

## Identiteter som stöds {#supported-identities}

[!DNL Zendesk] har stöd för uppdatering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Målidentitet | Exempel | Beskrivning | Obligatoriskt |
|---|---|---|---|
| `email` | `test@test.com` | Kontaktens e-postadress. | Ja |

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | <ul><li>Du exporterar alla medlemmar i ett segment, tillsammans med de önskade schemafälten *(till exempel e-postadress, telefonnummer, efternamn)*, enligt fältmappningen.</li><li> Varje segmentstatus i [!DNL Zendesk] uppdateras med motsvarande målgruppsstatus från Experience Platform, baserat på det **[!UICONTROL Mapping ID]**-värde som angavs under [målgruppsplaneringssteget](#schedule-segment-export-example).</li></ul> |
| Exportfrekvens | **[!UICONTROL Streaming]** | <ul><li>Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
>
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

I **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** söker du efter [!DNL Zendesk]. Du kan också hitta den under kategorin **[!UICONTROL CRM]**.

### Autentisera till mål {#authenticate}

Fyll i de obligatoriska fälten nedan. Mer information finns i avsnittet [Samla [!DNL Zendesk] inloggningsuppgifter](#gather-credentials).
* **[!UICONTROL Bearer Token]**: Den åtkomsttoken som du har genererat i ditt [!DNL Zendesk]-konto.

Om du vill autentisera till målet väljer du **[!UICONTROL Connect to destination]**.
![Experience Platform UI, bild som visar hur du autentiserar.](../../assets/catalog/crm/zendesk/authenticate-destination.png)

Om den angivna informationen är giltig visas statusen **[!UICONTROL Connected]** med en grön bockmarkering. Du kan sedan gå vidare till nästa steg.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.
![Experience Platform UI-skärmbild med målinformation.](../../assets/catalog/crm/zendesk/destination-details.png)

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera profiler och målgrupper för att direktuppspela målgruppsexportdestinationer](/help/destinations/ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

### Mappa överväganden och exempel {#mapping-considerations-example}

Om du vill skicka målgruppsdata från Adobe Experience Platform till målet [!DNL Zendesk] måste du gå igenom fältmappningssteget. Mappningen består av att skapa en länk mellan XDM-schemafälten (Experience Data Model) i ditt Experience Platform-konto och deras motsvarande motsvarigheter från målmålet.

Attribut som anges i **[!UICONTROL Target field]** ska namnges exakt så som beskrivs i tabellen för attributmappningar eftersom dessa attribut kommer att utgöra begärandetexten.

Attribut som anges i **[!UICONTROL Source field]** följer inte någon sådan begränsning. Du kan mappa den baserat på dina behov, men om dataformatet inte är korrekt när det skickas till [!DNL Zendesk] resulterar det i ett fel.

Följ de här stegen för att mappa dina XDM-fält korrekt till målfälten för [!DNL Zendesk]:

1. Välj **[!UICONTROL Add new mapping]** i steget **[!UICONTROL Mapping]**. En ny mappningsrad visas på skärmen.
1. Välj kategorin **[!UICONTROL Select attributes]** i fönstret **[!UICONTROL Select source field]** och markera XDM-attributet eller välj **[!UICONTROL Select identity namespace]** och välj en identitet.
1. I fönstret **[!UICONTROL Select target field]** väljer du kategorin **[!UICONTROL Select identity namespace]** och väljer en målidentitet, eller väljer kategorin **[!UICONTROL Select attributes]** och väljer ett av de schemaattribut som stöds.

   * Upprepa dessa steg om du vill lägga till följande obligatoriska mappningar, du kan även lägga till andra attribut som du vill uppdatera mellan XDM-profilschemat och din [!DNL Zendesk]-instans:

     | Source Field | Målfält | Obligatoriskt |
     |---|---|---|
     | `xdm: person.name.lastName` | `xdm: last_name` | Ja |
     | `IdentityMap: Email` | `Identity: email` | Ja |
     | `xdm: person.name.firstName` | `xdm: first_name` | |

   * Ett exempel på hur du använder dessa mappningar visas nedan:
     ![Exempel på skärmbild i Experience Platform UI med attributmappningar.](../../assets/catalog/crm/zendesk/mappings.png)

>[!IMPORTANT]
>
>Målmappningarna `Attribute: last_name` och `Identity: email` är obligatoriska för det här målet. Om dessa mappningar saknas ignoreras alla andra mappningar och skickas inte till [!DNL Zendesk].

Välj **[!UICONTROL Next]** när du är klar med mappningarna för målanslutningen.

### Schemalägg målgruppsexport och exempel {#schedule-segment-export-example}

I steget [[!UICONTROL Schedule audience export]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) i aktiveringsarbetsflödet måste du manuellt mappa Experience Platform-målgrupper till det anpassade fältattributet i [!DNL Zendesk].

Om du vill göra det markerar du varje segment och anger sedan motsvarande anpassade fältattribut från [!DNL Zendesk] i fältet **[!UICONTROL Mapping ID]**.

Ett exempel visas nedan:
![Exempel på skärmbild i Experience Platform som visar export av schemalagda målgrupper.](../../assets/catalog/crm/zendesk/schedule-segment-export.png)

## Validera dataexport {#exported-data}

Följ stegen nedan för att verifiera att du har konfigurerat målet korrekt:

1. Välj **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** och navigera till listan med mål.
1. Välj sedan målet, växla till fliken **[!UICONTROL Activation data]** och välj sedan ett målgruppsnamn.
   ![Exempel på skärmbild i Experience Platform UI som visar aktiveringsdata för destinationer.](../../assets/catalog/crm/zendesk/destinations-activation-data.png)

1. Övervaka målgruppssammanfattningen och kontrollera att antalet profiler motsvarar antalet inom segmentet.
   ![Exempel på skärmbild i Experience Platform UI som visar segment.](../../assets/catalog/crm/zendesk/segment.png)

1. Logga in på webbplatsen [!DNL Zendesk] och navigera sedan till sidan **[!UICONTROL Contacts]** för att kontrollera om profilerna från målgruppen har lagts till. Den här listan kan konfigureras för att visa kolumner för de ytterligare fält som har skapats med målgruppsstatus**[!UICONTROL Mapping ID]** och målgruppsstatus.
   ![Skärmbild från användargränssnittet i Zendesk som visar sidan Kontakter med de ytterligare fält som har skapats med målgruppens namn.](../../assets/catalog/crm/zendesk/contacts.png)

1. Du kan även gå ned på en enskild **[!UICONTROL Person]**-sida och kontrollera avsnittet **[!UICONTROL Additional fields]** som visar målgruppsnamnet och målgruppsstatus.
   ![Skärmbild av användargränssnittet i Zendesk som visar sidan Person med avsnittet med ytterligare fält som visar målgruppens namn och målgruppens status.](../../assets/catalog/crm/zendesk/contact.png)

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Datastyrningsöversikten](/help/data-governance/home.md).

## Ytterligare resurser {#additional-resources}

Ytterligare användbar information från dokumentationen för [!DNL Zendesk] finns nedan:
* [Gör ditt första samtal](https://developer.zendesk.com/documentation/sales-crm/first-call/)
* [Anpassade fält](https://developer.zendesk.com/api-reference/sales-crm/requests/#custom-fields)

### Changelog

I det här avsnittet beskrivs funktionaliteten och viktiga dokumentationsuppdateringar för den här målanslutningen.

+++ Visa ändringslogg

| Releasamånad | Uppdateringstyp | Beskrivning |
|---|---|---|
| April 2023 | Uppdatering av dokumentation | <ul><li>Vi uppdaterade avsnittet [use-cases](#use-cases) med ett tydligare exempel på när kunder skulle kunna dra nytta av det här målet.</li> <li>Avsnittet [mapping](#mapping-considerations-example) har uppdaterats så att rätt mappningar återspeglas. Målmappningarna `Attribute: last_name` och `Identity: email` är obligatoriska för det här målet. Om dessa mappningar saknas ignoreras alla andra mappningar och skickas inte till [!DNL Zendesk].</li> <li>Vi uppdaterade avsnittet [mapping](#mapping-considerations-example) med tydliga exempel på både obligatoriska och valfria mappningar.</li></ul> |
| Mars 2023 | Inledande version | Ursprunglig målversion och dokumentationspublicering. |

{style="table-layout:auto"}

+++
