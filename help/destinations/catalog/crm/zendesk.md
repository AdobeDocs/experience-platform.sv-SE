---
title: Zendesk-anslutning
description: Med Zendesk-destinationen kan du exportera dina kontouppgifter och aktivera dem i Zendesk efter behov.
last-substantial-update: 2023-03-14T00:00:00Z
source-git-commit: 661ef040398a9e2ef8dd9cebdf7bd27d4268636b
workflow-type: tm+mt
source-wordcount: '1437'
ht-degree: 1%

---

# [!DNL Zendesk] anslutning

[[!DNL Zendesk]](https://www.zendesk.com) är en kundtjänstlösning och ett säljverktyg.

Detta [!DNL Adobe Experience Platform] [mål](/help/destinations/home.md) utnyttjar [[!DNL Zendesk] Kontakt-API](https://developer.zendesk.com/api-reference/sales-crm/resources/contacts/), till **skapa och uppdatera identiteter** inom en målgrupp som kontakter inom [!DNL Zendesk].

[!DNL Zendesk] använder lagervariabler som en autentiseringsmekanism för att kommunicera med [!DNL Zendesk] Kontakter-API. Instruktioner för hur du autentiserar [!DNL Zendesk] -instansen är längre ned, i [Autentisera till mål](#authenticate) -avsnitt.

## Användningsfall {#use-cases}

Kundtjänstavdelningen på en flerkanalig B2C-plattform vill säkerställa en sömlös och personaliserad upplevelse för sina kunder. Avdelningen kan bygga målgrupper utifrån sina egna offlinedata för att skapa nya användarprofiler eller uppdatera befintlig profilinformation från olika interaktioner (t.ex. köp, returer etc.) och skicka dessa från Adobe Experience Platform till [!DNL Zendesk]. Den uppdaterade informationen finns i [!DNL Zendesk] säkerställer att kundtjänstpersonalen har den senaste informationen om kunden omedelbart tillgänglig, vilket ger snabbare svar och lösningar.

## Förutsättningar {#prerequisites}

### Förutsättningar för Experience Platform {#prerequisites-in-experience-platform}

Innan du aktiverar data för [!DNL Zendesk] mål, du måste ha [schema](/help/xdm/schema/composition.md), a [datauppsättning](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)och [segment](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) som [!DNL Experience Platform].

Se Experience Platform dokumentation för [Schemafältgrupp för målgruppsmedlemskapsdetaljer](/help/xdm/field-groups/profile/segmentation.md) om ni behöver vägledning om målgruppsstatus.

### [!DNL Zendesk] krav {#prerequisites-destination}

För att kunna exportera data från Platform till [!DNL Zendesk] konto du behöver ha [!DNL Zendesk] konto.

#### Samla [!DNL Zendesk] autentiseringsuppgifter {#gather-credentials}

Anteckna nedanstående innan du autentiserar dig för [!DNL Zendesk] mål:

| Autentiseringsuppgifter | Beskrivning | Exempel |
| --- | --- | --- |
| `Bearer token` | Åtkomsttoken som du har skapat i din [!DNL Zendesk] konto. <br> Följ dokumentationen för att [generera en [!DNL Zendesk] åtkomsttoken](https://developer.zendesk.com/documentation/sales-crm/first-call/#1-generate-an-access-token) om du inte har någon. | `a0b1c2d3e4...v20w21x22y23z` |

## Guardrails {#guardrails}

The [Priser och prisgränser](https://developer.zendesk.com/api-reference/sales-crm/rate-limits/#pricing) sidinformation om [!DNL Zendesk] API-begränsningar som är kopplade till ditt konto. Du måste se till att dina data och din nyttolast är inom dessa begränsningar.

## Identiteter som stöds {#supported-identities}

[!DNL Zendesk] har stöd för uppdatering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/namespaces.md).

| Målidentitet | Exempel | Beskrivning | Obligatoriskt |
|---|---|---|---|
| `email` | `test@test.com` | Kontaktens e-postadress. | Ja |

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | <ul><li>Du exporterar alla medlemmar i ett segment tillsammans med de önskade schemafälten *(t.ex. e-postadress, telefonnummer, efternamn)*, enligt fältmappningen.</li><li> Varje segmentstatus i [!DNL Zendesk] uppdateras med motsvarande målgruppsstatus från Platform, baserat på **[!UICONTROL Mapping ID]** det värde som anges under [målgruppsplanering](#schedule-segment-export-example) steg.</li></ul> |
| Exportfrekvens | **[!UICONTROL Streaming]** | <ul><li>Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
>
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

Inom **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** sök efter [!DNL Zendesk]. Du kan även hitta den under **[!UICONTROL CRM]** kategori.

### Autentisera till mål {#authenticate}

Fyll i de obligatoriska fälten nedan. Se [Samla [!DNL Zendesk] autentiseringsuppgifter](#gather-credentials) för vägledning.
* **[!UICONTROL Bearer Token]**: Den åtkomsttoken som du har skapat i [!DNL Zendesk] konto.

Om du vill autentisera mot målet väljer du **[!UICONTROL Connect to destination]**.
![Skärmbild av användargränssnittet för plattformen som visar hur man autentiserar.](../../assets/catalog/crm/zendesk/authenticate-destination.png)

Om den angivna informationen är giltig visas en **[!UICONTROL Connected]** status med en grön bockmarkering. Du kan sedan gå vidare till nästa steg.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.
![Skärmbild för användargränssnittet för plattformen som visar målinformationen.](../../assets/catalog/crm/zendesk/destination-details.png)

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden på [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.
>* Exportera *identiteter* behöver du **[!UICONTROL View Identity Graph]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). <br> ![Markera det identitetsnamnutrymme som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera det identitetsnamnutrymme som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera profiler och målgrupper för att strömma målgruppernas exportdestinationer](/help/destinations/ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

### Mappa överväganden och exempel {#mapping-considerations-example}

Så här skickar du målgruppsdata från Adobe Experience Platform till [!DNL Zendesk] mål måste du gå igenom fältmappningssteget. Mappningen består av att skapa en länk mellan XDM-schemafälten (Experience Data Model) i ditt plattformskonto och motsvarande motsvarigheter från målmålet.

Attribut som anges i **[!UICONTROL Target field]** ska namnges exakt så som beskrivs i tabellen för attributmappningar eftersom dessa attribut kommer att utgöra begärandetexten.

Attribut som anges i **[!UICONTROL Source field]** inte följer någon sådan begränsning. Du kan mappa den baserat på dina behov, men om dataformatet inte är korrekt när det skickas till [!DNL Zendesk] det kommer att resultera i ett fel.

Mappa XDM-fälten korrekt till [!DNL Zendesk] målfält, följ dessa steg:

1. I **[!UICONTROL Mapping]** steg, välja **[!UICONTROL Add new mapping]**. En ny mappningsrad visas på skärmen.
1. I **[!UICONTROL Select source field]** väljer du **[!UICONTROL Select attributes]** och välj XDM-attributet eller välj **[!UICONTROL Select identity namespace]** och välj en identitet.
1. I **[!UICONTROL Select target field]** väljer du **[!UICONTROL Select identity namespace]** och välj en målidentitet, eller välj **[!UICONTROL Select attributes]** och välj ett av de schemaattribut som stöds.
   * Upprepa dessa steg om du vill lägga till följande obligatoriska mappningar, du kan även lägga till andra attribut som du vill uppdatera mellan XDM-profilschemat och ditt [!DNL Zendesk] instans: |Källfält|Målfält| Obligatoriskt| |—|—|—| |`xdm: person.name.lastName`|`xdm: last_name`| Ja | |`IdentityMap: Email`|`Identity: email`| Ja | |`xdm: person.name.firstName`|`xdm: first_name`| |

   * Ett exempel på hur du använder dessa mappningar visas nedan:
     ![Skärmbild för plattformsgränssnitt med attributmappningar.](../../assets/catalog/crm/zendesk/mappings.png)

>[!IMPORTANT]
>
>The `Attribute: last_name` och `Identity: email` målmappningar är obligatoriska för det här målet. Om mappningarna saknas ignoreras alla andra mappningar och skickas inte till [!DNL Zendesk].

När du är klar med mappningarna för målanslutningen väljer du **[!UICONTROL Next]**.

### Schemalägg målgruppsexport och exempel {#schedule-segment-export-example}

I [[!UICONTROL Schedule audience export]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) steg i aktiveringsarbetsflödet måste du manuellt mappa Platform-målgrupper till det anpassade fältattributet i [!DNL Zendesk].

Om du vill göra det markerar du varje segment och anger sedan motsvarande attribut för anpassade fält från [!DNL Zendesk] i **[!UICONTROL Mapping ID]** fält.

Ett exempel visas nedan:
![Exempel på skärmbild för användargränssnittet för plattformen som visar export av schemalagda målgrupper.](../../assets/catalog/crm/zendesk/schedule-segment-export.png)

## Validera dataexport {#exported-data}

Följ stegen nedan för att verifiera att du har konfigurerat målet korrekt:

1. Välj **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** och navigera till listan över destinationer.
1. Välj sedan målet och växla till **[!UICONTROL Activation data]** väljer du ett målgruppsnamn.
   ![Skärmbild för användargränssnittet för plattformen visar aktiveringsdata för destinationer.](../../assets/catalog/crm/zendesk/destinations-activation-data.png)

1. Övervaka målgruppssammanfattningen och kontrollera att antalet profiler motsvarar antalet inom segmentet.
   ![Exempel på skärmbild för plattformsgränssnitt som visar segment.](../../assets/catalog/crm/zendesk/segment.png)

1. Logga in på [!DNL Zendesk] webbplatsen och sedan navigera till **[!UICONTROL Contacts]** sida för att kontrollera om profilerna från målgruppen har lagts till. Den här listan kan konfigureras för att visa kolumner för de ytterligare fält som skapas med målgruppen**[!UICONTROL Mapping ID]** och målgruppsstatus.
   ![Skärmbilden Zendesk UI visar sidan Kontakter med de ytterligare fält som skapats med målgruppens namn.](../../assets/catalog/crm/zendesk/contacts.png)

1. Du kan även gå ned i en individ **[!UICONTROL Person]** sidan och kontrollera **[!UICONTROL Additional fields]** -sektion som visar målgruppsnamn och målgruppsstatus.
   ![Skärmbilden Zendesk UI som visar sidan Person med de extra fälten som visar målgruppens namn och målgruppens status.](../../assets/catalog/crm/zendesk/contact.png)

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, se [Datastyrning - översikt](/help/data-governance/home.md).

## Ytterligare resurser {#additional-resources}

Ytterligare användbar information från [!DNL Zendesk] dokumentationen nedan:
* [Ring ditt första samtal](https://developer.zendesk.com/documentation/sales-crm/first-call/)
* [Anpassade fält](https://developer.zendesk.com/api-reference/sales-crm/requests/#custom-fields)

### Changelog

I det här avsnittet beskrivs funktionaliteten och viktiga dokumentationsuppdateringar för den här målanslutningen.

+++ Visa ändringslogg

| Releasamånad | Uppdateringstyp | Beskrivning |
|---|---|---|
| April 2023 | Dokumentation - uppdatering | <ul><li>Vi uppdaterade [användningsfall](#use-cases) med ett tydligare exempel på när kunderna skulle kunna dra nytta av detta mål.</li> <li>Vi uppdaterade [mappning](#mapping-considerations-example) för att spegla de nödvändiga mappningarna. The `Attribute: last_name` och `Identity: email` målmappningar är obligatoriska för det här målet. Om mappningarna saknas ignoreras alla andra mappningar och skickas inte till [!DNL Zendesk].</li> <li>Vi uppdaterade [mappning](#mapping-considerations-example) med tydliga exempel på både obligatoriska och valfria mappningar.</li></ul> |
| Mars 2023 | Inledande version | Ursprunglig målversion och dokumentationspublicering. |

{style="table-layout:auto"}

+++