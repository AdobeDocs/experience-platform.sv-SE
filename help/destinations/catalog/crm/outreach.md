---
keywords: crm;CRM;crm destination;Utanför;Utanför crm-mål
title: Utdataanslutning
description: Med Outreach-destinationen kan du exportera dina kontodata och aktivera dem inom ramarna för ditt företags behov.
exl-id: 7433933d-7a4e-441d-8629-a09cb77d5220
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1683'
ht-degree: 0%

---

# [!DNL Outreach] anslutning

## Översikt {#overview}

[[!DNL Outreach]](https://www.outreach.io/) är en plattform för säljavdelning med de flesta interaktionsdata för B2B-köpare i världen och betydande investeringar i egna AI-tekniker för att omvandla säljdata till intelligens. [!DNL Outreach] hjälper organisationer att automatisera säljengagemanget och agera utifrån intäktsanalys för att förbättra sin effektivitet, förutsägbarhet och tillväxt.

Detta [!DNL Adobe Experience Platform] [mål](/help/destinations/home.md) utnyttjar [Resurs-API för datauppdatering](https://api.outreach.io/api/v2/docs#update-an-existing-resource), som gör det möjligt att uppdatera identiteter inom en målgrupp som motsvarar presumtiva kunder i [!DNL Outreach].

[!DNL Outreach] använder OAuth 2 med auktoriseringsbidrag som autentiseringsmekanism för att kommunicera med [!DNL Outreach] [!DNL Update Resource API]. Instruktioner för hur du autentiserar [!DNL Outreach] -instansen är längre ned, inom [Autentisera till mål](#authenticate) -avsnitt.

## Användningsfall {#use-cases}

Som marknadsförare kan ni leverera personaliserade upplevelser till era presumtiva kunder, baserat på attribut från deras Adobe Experience Platform-profiler. Ni kan bygga målgrupper utifrån era offlinedata och skicka dessa målgrupper till [!DNL Outreach], som visas i presumtiva kunder så snart som målgrupper och profiler uppdateras i Adobe Experience Platform.

## Förutsättningar {#prerequisites}

### Förutsättningar för Experience Platform {#prerequisites-in-experience-platform}

Innan du aktiverar data för [!DNL Outreach] mål, du måste ha [schema](/help/xdm/schema/composition.md), a [datauppsättning](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)och [segment](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) som [!DNL Experience Platform].

Mer information finns i Adobe dokumentation [Schemafältgrupp för målgruppsmedlemskapsdetaljer](/help/xdm/field-groups/profile/segmentation.md) om ni behöver vägledning om målgruppsstatus.

### Förutsättningar {#prerequisites-destination}

Observera följande krav i [!DNL Outreach]för att exportera data från Platform till [!DNL Outreach] konto:

#### Du måste ha ett Outlook-konto {#prerequisites-account}

Gå till [!DNL Outreach] [logga in](https://accounts.outreach.io/users/sign_in) sida för att registrera och skapa ett konto, om du inte redan har ett. Se även [!DNL Outreach] support [page](https://support.outreach.io/hc/en-us/articles/207238607-Claim-Your-Outreach-Account) för mer information.

Anteckna nedanstående innan du autentiserar dig för [!DNL Outreach] CRM-mål:

| Autentiseringsuppgifter | Beskrivning |
|---|---|
| E-post | Dina [!DNL Outreach] e-postadress |
| Lösenord | Dina [!DNL Outreach] lösenord |

#### Ställ in anpassade fältetiketter {#prerequisites-custom-fields}

[!DNL Outreach] stöder anpassade fält för [prospects](https://support.outreach.io/hc/en-us/articles/360001557554-Outreach-Prospect-Profile-Overview). Se [Så här lägger du till ett anpassat fält i Utdata](https://support.outreach.io/hc/en-us/articles/219124908-How-To-Add-a-Custom-Field-in-Outreach) för ytterligare vägledning. För att underlätta identifieringen rekommenderar vi att etiketterna uppdateras manuellt till motsvarande målgruppsnamn i stället för att standardvärdena behålls. Exempel:

[!DNL Outreach] inställningssida för potentiella kunder som visar anpassade fält.
![Skärmbild av gränssnittet som visar anpassade fält på inställningssidan visas.](../../assets/catalog/crm/outreach/outreach-custom-fields.png)

[!DNL Outreach] inställningssida för potentiella kunder som visar anpassade fält med *användarvänlig* etiketter som matchar målgruppsnamnen. Du kan visa målgruppsstatus på den potentiella kundens sida mot dessa etiketter.
![Skärmbild av gränssnittet som visar anpassade fält med tillhörande etiketter på inställningssidan visas.](../../assets/catalog/crm/outreach/outreach-custom-field-labels.png)

>[!NOTE]
>
> Etikettnamn är bara till för att underlätta identifiering. De används inte vid uppdatering av potentiella kunder.

## Guardrails

The [!DNL Outreach] API har en hastighetsgräns på 10 000 begäranden per timme och användare. Om du når den här gränsen får du en `429` svar med följande meddelande: `You have exceeded your permitted rate limit of 10,000; please try again at 2017-01-01T00:00:00.`.

Om du får det här meddelandet måste du uppdatera ditt exportschema för målgruppen så att det uppfyller tröskelvärdet.

Se [[!DNL Outreach] dokumentation](https://api.outreach.io/api/v2/docs#rate-limiting) om du vill ha mer information.

## Identiteter som stöds {#supported-identities}

[!DNL Outreach] har stöd för uppdatering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| `OutreachId` | <ul><li>[!DNL Outreach] identifierare. Detta är ett numeriskt värde som motsvarar profilen för potentiell kund.</li><li>ID:t måste matcha ID:t i [!DNL Outreach] URL för den potentiella kund som uppdateras.</li><li>Se [[!DNL Outreach] dokumentation](https://api.outreach.io/api/v2/docs#update-an-existing-resource) för mer information.</li></ul> | Obligatoriskt |

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | <ul><li> Du exporterar alla medlemmar i ett segment tillsammans med de önskade schemafälten *(t.ex. e-postadress, telefonnummer, efternamn)*, enligt fältmappningen.</li><li> Varje segmentstatus i [!DNL Outreach] uppdateras med motsvarande målgruppsstatus från Platform, baserat på [!UICONTROL Mapping ID] det värde som anges under [målgruppsplanering](#schedule-segment-export-example) steg.</li></ul> |
| Exportfrekvens | **[!UICONTROL Streaming]** | <ul><li> Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
> Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

Inom **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** sök efter [!DNL Outreach]. Du kan också hitta den under CRM-kategorin.

### Autentisera till mål {#authenticate}

Om du vill autentisera mot målet väljer du **[!UICONTROL Connect to destination]**.

![Skärmbild av användargränssnittet för plattformen som visar hur man autentiserar till Outreach.](../../assets/catalog/crm/outreach/authenticate-destination.png)

Du kommer att få se [!DNL Outreach] inloggningssida. Ange din e-postadress.

![Skärmbild av användargränssnittet som visar fältet som e-postindata för autentisering till utdataenheten.](../../assets/catalog/crm/outreach/authenticate-destination-login-email.png)

Ange sedan ditt lösenord.

![Skärmbild av användargränssnitt som visar fältet som inmatningslösenord för autentisering till utdataenhet.](../../assets/catalog/crm/outreach/authenticate-destination-login-password.png)

* **[!UICONTROL Username]**: din [!DNL Outreach] e-postadress till konto.
* **[!UICONTROL Password]**: din [!DNL Outreach] kontolösenord.

Om den angivna informationen är giltig visas en **Ansluten** status med en grön bockmarkering. Du kan sedan gå vidare till nästa steg.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.
![Skärmbild av användargränssnittet för plattformen som visar hur du fyller i detaljer för målplatsen för utdataenheten.](../../assets/catalog/crm/outreach/destination-details.png)

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

Läs [Aktivera profiler och målgrupper för att strömma målgruppernas exportdestinationer](../../ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

### Mappa överväganden och exempel {#mapping-considerations-example}

Så här skickar du målgruppsdata från Adobe Experience Platform till [!DNL Outreach] mål måste du gå igenom fältmappningssteget. Mappningen består av att skapa en länk mellan XDM-schemafälten (Experience Data Model) i ditt plattformskonto och motsvarande motsvarigheter från målmålet. Mappa XDM-fälten korrekt till [!DNL Outreach] målfält, följ dessa steg:

1. I [!UICONTROL Mapping] klicka **[!UICONTROL Add new mapping]**. En ny mappningsrad visas på skärmen.
   ![Skärmbild av användargränssnittet för plattformen som visar hur du lägger till ny mappning](../../assets/catalog/crm/outreach/add-new-mapping.png)

1. I [!UICONTROL Select source field] väljer du **[!UICONTROL Select identity namespace]** och lägg till mappningarna.
   ![Skärmbild för användargränssnittet för plattformen med källmappning](../../assets/catalog/crm/outreach/source-mapping.png)

1. I [!UICONTROL Select target field] väljer du den typ av målfält som du vill mappa källfältet till.
   * **[!UICONTROL Select identity namespace]**: välj det här alternativet om du vill mappa källfältet till ett identitetsnamnområde från listan.
     ![Skärmbild av användargränssnittet för plattformen som visar målmappning med OutreachId.](../../assets/catalog/crm/outreach/target-mapping.png)

   * Lägg till följande mappning mellan XDM-profilschemat och [!DNL Outreach] instans: |XDM-profilschema|[!DNL Outreach] Instans| Obligatorisk| |—|—|—| |`Oid`|`OutreachId`| Ja |

   * **[!UICONTROL Select custom attributes]**: välj det här alternativet om du vill mappa källfältet till ett anpassat attribut som du definierar i dialogrutan [!UICONTROL Attribute name] fält. Se [[!DNL Outreach] dokumentation om potentiella kunder](https://api.outreach.io/api/v2/docs#prospect) om du vill ha en omfattande lista över attribut som stöds.
     ![Skärmbild för plattformsgränssnitt som visar målmappning med hjälp av LastName.](../../assets/catalog/crm/outreach/target-mapping-lastname.png)

   * Beroende på vilka värden du vill uppdatera lägger du till följande mappning mellan XDM-profilschemat och ditt [!DNL Outreach] instans: |XDM-profilschema|[!DNL Outreach] Instans| |—|—| |`person.name.firstName`|`firstName`| |`person.name.lastName`|`lastName`|

   * Ett exempel på hur du använder dessa mappningar visas nedan:
     ![Exempel på skärmbild för användargränssnittet för plattformen som visar målmappningar.](../../assets/catalog/crm/outreach/mappings.png)

### Schemalägg målgruppsexport och exempel {#schedule-segment-export-example}

* När du utför [Schemalägg målgruppsexport](../../ui/activate-segment-streaming-destinations.md) steg du måste mappa plattformsmålgrupper manuellt till det anpassade fältattributet i [!DNL Outreach].

* Det gör du genom att markera varje segment och sedan ange motsvarande numeriska värde som motsvarar *Anpassat fält `N` Etikett* fält från [!DNL Outreach] i **[!UICONTROL Mapping ID]** fält.

  >[!IMPORTANT]
  >
  > * Det numeriska värdet *(`N`)* används inom [!UICONTROL Mapping ID] ska matcha det anpassade attributnyckelsuffixet med det numeriska värdet inom [!DNL Outreach]. Exempel: *Anpassat fält `N` Etikett*.
  > * Du behöver bara ange det numeriska värdet, inte hela etiketten för anpassade fält.
  > * [!DNL Outreach] har stöd för högst 150 anpassade etikettfält.
  > * Se [[!DNL Outreach] dokumentation om potentiella kunder](https://api.outreach.io/api/v2/docs#prospect) för mer information.

   * Exempel:

     | [!DNL Outreach] Fält | Plattformsmappnings-ID |
     |---|---|
     | Anpassat fält `4` Etikett | `4` |

     ![Skärmbild av användargränssnittet för plattformen visar ett exempel på mappnings-ID vid export av schemalagda målgrupper.](../../assets/catalog/crm/outreach/schedule-segment-export.png)

## Validera dataexport {#exported-data}

Följ stegen nedan för att verifiera att du har konfigurerat målet korrekt:

1. Välj **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** för att navigera till listan över destinationer.
   ![Skärmbild av användargränssnittet för plattformen med bläddringsmål.](../../assets/catalog/crm/outreach/browse-destinations.png)

1. Markera målet och validera att statusen är **[!UICONTROL enabled]**.
   ![Skärmbild för användargränssnittet för plattformen med körning av måldataflöde för det valda målet.](../../assets/catalog/crm/outreach/destination-dataflow-run.png)

1. Växla till **[!DNL Activation data]** väljer du ett målgruppsnamn.
   ![Skärmbild av användargränssnittet för plattformen med aktiveringsdata för destinationer.](../../assets/catalog/crm/outreach/destinations-activation-data.png)

1. Övervaka målgruppssammanfattningen och se till att antalet profiler motsvarar antalet som skapas inom segmentet.
   ![Skärmbild av plattformsgränssnitt med segmentsammanfattning.](../../assets/catalog/crm/outreach/segment.png)

1. Logga in på [!DNL Outreach] webbplatsen och sedan navigera till [!DNL Apps] > [!DNL Contacts] och kontrollera om profilerna från målgruppen har lagts till. Du kan se att varje målgruppsstatus i [!DNL Outreach] uppdaterades med motsvarande målgruppsstatus från Platform, baserat på [!UICONTROL Mapping ID] det värde som anges under [målgruppsplanering](#schedule-segment-export-example) steg.

![Skärmbild av gränssnittet för Outreach visar sidan för Outreach Prospects med de uppdaterade målgruppsstatusarna.](../../assets/catalog/crm/outreach/outreach-prospect.png)

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, se [Datastyrning - översikt](/help/data-governance/home.md).

## Fel och felsökning {#errors-and-troubleshooting}

När du kontrollerar ett dataflöde kan följande felmeddelande visas: `Bad request reported while pushing events to the destination. Please contact the administrator and try again.`

![Skärmbilden för användargränssnittet för plattformen visar ett fel för felaktig begäran.](../../assets/catalog/crm/outreach/error.png)

Du kan åtgärda felet genom att kontrollera att [!UICONTROL Mapping ID] du angav i Platform för [!DNL Outreach] målgruppen är giltig och finns i [!DNL Outreach].

## Ytterligare resurser {#additional-resources}

The [[!DNL Outreach] dokumentation](https://api.outreach.io/api/v2/docs/) har information om [Felsvar](https://api.outreach.io/api/v2/docs#error-responses) som du kan använda för att felsöka problem.
