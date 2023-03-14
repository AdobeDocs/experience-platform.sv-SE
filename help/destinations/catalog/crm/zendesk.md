---
title: Zendesk-anslutning
description: Med Zendesk-destinationen kan du exportera dina kontouppgifter och aktivera dem i Zendesk efter behov.
source-git-commit: 6a54926e47fb2364475dbf71593de97b642163d5
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 0%

---

# [!DNL Zendesk] anslutning

[[!DNL Zendesk]](https://www.zendesk.com) är en kundtjänstlösning och ett säljverktyg.

Detta [!DNL Adobe Experience Platform] [mål](/help/destinations/home.md) utnyttjar [[!DNL Zendesk] Kontakt-API](https://developer.zendesk.com/api-reference/sales-crm/resources/contacts/), för att skapa och uppdatera identiteter inom ett segment som kontakter inom [!DNL Zendesk].

[!DNL Zendesk] använder lagervariabler som en autentiseringsmekanism för att kommunicera med [!DNL Zendesk] Kontakter-API. Instruktioner för hur du autentiserar [!DNL Zendesk] -instansen är längre ned, i [Autentisera till mål](#authenticate) -avsnitt.

## Användningsfall {#use-cases}

Som marknadsförare kan ni leverera personaliserade upplevelser till era användare, baserat på attribut från deras Adobe Experience Platform-profiler. Du kan skapa segment utifrån offlinedata och skicka dessa segment till [!DNL Zendesk], som visas i användarnas flöden så snart segment och profiler uppdateras i Adobe Experience Platform.

## Förutsättningar {#prerequisites}

### Krav för Experience Platform {#prerequisites-in-experience-platform}

Innan du aktiverar data för [!DNL Zendesk] mål, du måste ha en [schema](/help/xdm/schema/composition.md), a [datauppsättning](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)och [segment](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) skapad i [!DNL Experience Platform].

Se Experience Platform dokumentation för [Schemafältgrupp för detaljer om segmentmedlemskap](/help/xdm/field-groups/profile/segmentation.md) om du behöver vägledning om segmentstatus.

### [!DNL Zendesk] krav {#prerequisites-destination}

För att kunna exportera data från Platform till [!DNL Zendesk] konto du behöver ha [!DNL Zendesk] konto.

#### Samla [!DNL Zendesk] autentiseringsuppgifter {#gather-credentials}

Anteckna vad som står nedan innan du autentiserar dig för [!DNL Zendesk] mål:

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
| Exporttyp | **[!UICONTROL Profile-based]** | <ul><li>Du exporterar alla medlemmar i ett segment tillsammans med de önskade schemafälten *(till exempel: e-postadress, telefonnummer, efternamn)*, enligt fältmappningen.</li><li> Varje segmentstatus i [!DNL Zendesk] uppdateras med motsvarande segmentstatus från Platform, baserat på **[!UICONTROL Mapping ID]** det värde som anges under [segmentplanering](#schedule-segment-export-example) steg.</li></ul> |
| Exportfrekvens | **[!UICONTROL Streaming]** | <ul><li>Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på segmentutvärdering skickar kopplingen uppdateringen nedåt till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
>
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

Inom **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** sök efter [!DNL Zendesk]. Du kan även hitta den under **[!UICONTROL CRM]** kategori.

### Autentisera till mål {#authenticate}

Fyll i de obligatoriska fälten nedan. Se [Samla [!DNL Zendesk] autentiseringsuppgifter](#gather-credentials) för vägledning.
* **[!UICONTROL Bearer Token]**: Åtkomsttoken som du har skapat i din [!DNL Zendesk] konto.

Om du vill autentisera mot målet väljer du **[!UICONTROL Connect to destination]**.
![Skärmbild av användargränssnittet för plattformen som visar hur man autentiserar.](../../assets/catalog/crm/zendesk/authenticate-destination.png)

Om den angivna informationen är giltig visas en **[!UICONTROL Connected]** status med grön bockmarkering. Du kan sedan gå vidare till nästa steg.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.
![Skärmbild för användargränssnittet för plattformen som visar målinformationen.](../../assets/catalog/crm/zendesk/destination-details.png)

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om status för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med hjälp av användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
>
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Läs [Aktivera profiler och segment för att direktuppspela segmentexportmål](/help/destinations/ui/activate-segment-streaming-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

### Mappa överväganden och exempel {#mapping-considerations-example}

Så här skickar du målgruppsdata från Adobe Experience Platform till [!DNL Zendesk] mål måste du gå igenom fältmappningssteget. Mappningen består av att skapa en länk mellan XDM-schemafälten (Experience Data Model) i ditt plattformskonto och motsvarande motsvarigheter från målmålet.

Attribut som anges i **[!UICONTROL Target field]** ska namnges exakt så som beskrivs i tabellen för attributmappningar eftersom dessa attribut kommer att utgöra begärandetexten.

Attribut som anges i **[!UICONTROL Source field]** inte följer någon sådan begränsning. Du kan mappa den baserat på dina behov, men om dataformatet inte är korrekt när det skickas till [!DNL Zendesk] det resulterar i ett fel.

Koppla XDM-fälten till [!DNL Zendesk] målfält, följ dessa steg:

1. I **[!UICONTROL Mapping]** steg, välja **[!UICONTROL Add new mapping]**. En ny mappningsrad visas på skärmen.
1. I **[!UICONTROL Select source field]** väljer du **[!UICONTROL Select attributes]** och välj XDM-attributet eller välj **[!UICONTROL Select identity namespace]** och välj en identitet.
1. I **[!UICONTROL Select target field]** väljer du **[!UICONTROL Select identity namespace]** och välj en identitet eller välj **[!UICONTROL Select custom attributes]** och välj ett attribut efter behov.
   * Upprepa dessa steg för att lägga till följande mappningar mellan XDM-profilschemat och ditt [!DNL Zendesk] instans: |Källfält|Målfält| Obligatoriskt| |—|—|—| |`xdm: person.name.lastName`|`Attribute: last_name` <br>eller `Attribute: name`| Ja | |`IdentityMap: Email`|`Identity: email`| Ja |

   * Ett exempel på hur du använder dessa mappningar visas nedan:
      ![Skärmbild för plattformsgränssnitt med attributmappningar.](../../assets/catalog/crm/zendesk/mappings.png)

      >[!IMPORTANT]
      >
      >Både målfältsmappningar är obligatoriska och obligatoriska för [!DNL Zendesk] till jobbet.
      >
      >Mappningen för *Efternamn* eller *Namn* krävs annars [!DNL Zendesk] API svarar inte med något fel och alla attributvärden som skickas ignoreras.

När du är klar med mappningarna för målanslutningen väljer du **[!UICONTROL Next]**.

### Schemalägg segmentexport och exempel {#schedule-segment-export-example}

I [[!UICONTROL Schedule segment export]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) steg i aktiveringsarbetsflödet måste du manuellt mappa plattformssegment till det anpassade fältattributet i [!DNL Zendesk].

Om du vill göra det markerar du varje segment och anger sedan motsvarande attribut för anpassade fält från [!DNL Zendesk] i **[!UICONTROL Mapping ID]** fält.

Ett exempel visas nedan:
![Exempel på skärmbild för användargränssnittet för plattformen som visar export av Schedule-segment.](../../assets/catalog/crm/zendesk/schedule-segment-export.png)

## Validera dataexport {#exported-data}

Följ stegen nedan för att verifiera att du har konfigurerat målet korrekt:

1. Välj **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** och navigera till listan över destinationer.
1. Välj sedan målet och växla till **[!UICONTROL Activation data]** väljer du ett segmentnamn.
   ![Skärmbild för användargränssnittet för plattformen visar aktiveringsdata för destinationer.](../../assets/catalog/crm/zendesk/destinations-activation-data.png)

1. Övervaka segmentsammanfattningen och kontrollera att antalet profiler motsvarar antalet inom segmentet.
   ![Exempel på skärmbild för plattformsgränssnitt som visar segment.](../../assets/catalog/crm/zendesk/segment.png)

1. Logga in på [!DNL Zendesk] webbplatsen och sedan navigera till **[!UICONTROL Contacts]** sida för att kontrollera om profilerna från segmentet har lagts till. Den här listan kan konfigureras för att visa kolumner för de ytterligare fält som skapas med segmentet **[!UICONTROL Mapping ID]** och segmentstatus.
   ![Skärmbilden Zendesk UI visar sidan Kontakter med de ytterligare fält som skapats med segmentnamnet.](../../assets/catalog/crm/zendesk/contacts.png)

1. Du kan även gå ned i en individ **[!UICONTROL Person]** sidan och kontrollera **[!UICONTROL Additional fields]** där segmentnamnet och segmentstatusvärdena visas.
   ![Skärmbilden Zendesk UI som visar sidan Person med avsnittet med ytterligare fält som visar segmentnamnet och segmentstatusvärdena.](../../assets/catalog/crm/zendesk/contact.png)

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, se [Datastyrning - översikt](/help/data-governance/home.md).

## Ytterligare resurser {#additional-resources}

Ytterligare användbar information från [!DNL Zendesk] dokumentationen nedan:
* [Ring ditt första samtal](https://developer.zendesk.com/documentation/sales-crm/first-call/)
* [Anpassade fält](https://developer.zendesk.com/api-reference/sales-crm/requests/#custom-fields)