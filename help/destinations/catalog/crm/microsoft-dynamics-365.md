---
keywords: crm;CRM;crm destination;Microsoft Dynamics 365;Microsoft Dynamics 365 crm destination
title: Microsoft Dynamics 365-anslutning
description: Med Microsoft Dynamics 365-destinationen kan du exportera dina kontodata och aktivera dem i Microsoft Dynamics 365 efter dina affärsbehov.
last-substantial-update: 2022-11-08T00:00:00Z
exl-id: 49bb5c95-f4b7-42e1-9aae-45143bbb1d73
source-git-commit: 29cf080f83adf0e7f8b3549104229e9f54c5b8d9
workflow-type: tm+mt
source-wordcount: '2106'
ht-degree: 0%

---

# [!DNL Microsoft Dynamics 365] anslutning

## Översikt {#overview}

[[!DNL Microsoft Dynamics 365]](https://dynamics.microsoft.com/en-us/) är en molnbaserad plattform för affärsapplikationer som kombinerar ERP (Enterprise Resource Planning) och CRM (Customer Relationship Management) med produktivitetsprogram och AI-verktyg, vilket ger smidigare och mer kontrollerad drift, bättre tillväxtpotential och minskade kostnader.

Detta [!DNL Adobe Experience Platform] [mål](/help/destinations/home.md) utnyttjar [[!DNL Contact Entity Reference API]](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1)som gör att ni kan uppdatera identiteter inom en viss målgrupp till [!DNL Dynamics 365].

[!DNL Dynamics 365] använder OAuth 2 med auktoriseringsbidrag som autentiseringsmekanism för att kommunicera med [!DNL Contact Entity Reference API]. Instruktioner för hur du autentiserar [!DNL Dynamics 365] -instansen är längre ned, i [Autentisera till mål](#authenticate) -avsnitt.

## Användningsfall {#use-cases}

Som marknadsförare kan ni leverera personaliserade upplevelser till era användare, baserat på attribut från deras Adobe Experience Platform-profiler. Ni kan bygga målgrupper utifrån era offlinedata och skicka dessa målgrupper till [!DNL Dynamics 365], som visas i användarnas flöden så snart som målgrupper och profiler uppdateras i Adobe Experience Platform.

## Förutsättningar {#prerequisites}

### Förutsättningar för Experience Platform {#prerequisites-in-experience-platform}

Innan du aktiverar data för [!DNL Dynamics 365] mål, du måste ha [schema](/help/xdm/schema/composition.md), a [datauppsättning](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)och [målgrupper](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html) som [!DNL Experience Platform].

Mer information finns i Adobe dokumentation [Schemafältgrupp för målgruppsmedlemskapsdetaljer](/help/xdm/field-groups/profile/segmentation.md) om ni behöver vägledning om målgruppsstatus.

### [!DNL Microsoft Dynamics 365] krav {#prerequisites-destination}

Observera följande krav i [!DNL Dynamics 365]för att exportera data från Platform till [!DNL Dynamics 365] konto:

#### Du måste ha en [!DNL Microsoft Dynamics 365] konto {#prerequisites-account}

Gå till [!DNL Dynamics 365] [testversion](https://dynamics.microsoft.com/en-us/dynamics-365-free-trial/) sida för att registrera och skapa ett konto, om du inte redan har ett.

#### Skapa fält i [!DNL Dynamics 365] {#prerequisites-custom-field}

Skapa ett anpassat typfält `Simple` med fältdatatyp som `Single Line of Text` vilket Experience Platform ska använda för att uppdatera målgruppsstatus inom [!DNL Dynamics 365].

Se [!DNL Dynamics 365] [Skapa eller redigera ett fält (attribut)](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1) dokumentation om du behöver ytterligare vägledning.

Skriv ned **[!UICONTROL Customization prefix]** av det anpassade fältet som du skapar i [!DNL Dynamics 365]. Du behöver det här prefixet under [Fyll i målinformation](#destination-details) steg. Se [Skapa och redigera fält](https://learn.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1#create-and-edit-fields) i [!DNL Dynamics 365] för mer information.
![Skärmbild för användargränssnittet i Dynamics 365 med anpassningsprefixet.](../../assets/catalog/crm/microsoft-dynamics-365/dynamics-365-customization-prefix.png)

Exempelinställningar i [!DNL Dynamics 365] visas nedan:
![Skärmbild för användargränssnittet i Dynamics 365 med anpassade fält.](../../assets/catalog/crm/microsoft-dynamics-365/dynamics-365-fields.png)

#### Registrera en program- och programanvändare i Azure Active Directory {#prerequisites-app-user}

Aktivera [!DNL Dynamics 365] för att få tillgång till resurser som du måste logga in med [!DNL Azure Account] till [[!DNL Azure Active Directory]](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#register-an-application-with-azure-ad-and-create-a-service-principal) och skapa följande:
* An [!DNL Azure Active Directory] program
* Tjänsthuvudman
* En programhemlighet

Du måste också [skapa en programanvändare](https://docs.microsoft.com/en-us/power-platform/admin/manage-application-users#create-an-application-user) in [!DNL Azure Active Directory] och associera det med det nya programmet.

#### Samla [!DNL Dynamics 365] autentiseringsuppgifter {#gather-credentials}

Anteckna nedanstående innan du autentiserar dig för [!DNL Dynamics 365] CRM-mål:

| Autentiseringsuppgifter | Beskrivning | Exempel |
| --- | --- | --- |
| `Client ID` | The [!DNL Dynamics 365] Klient-ID för din [!DNL Azure Active Directory] program. Se [[!DNL Dynamics 365] dokumentation](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#get-tenant-and-app-id-values-for-signing-in) för vägledning. | `ababbaba-abab-baba-acac-acacacacacac` |
| `Client Secret` | The [!DNL Dynamics 365] Klienthemlighet för [!DNL Azure Active Directory] program. Du använder alternativ 2 i [[!DNL Dynamics 365] dokumentation](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#authentication-two-options). | `abcde~abcdefghijklmnopqrstuvwxyz12345678` för vägledning. |
| `Tenant ID` | The [!DNL Dynamics 365] Klient-ID för din [!DNL Azure Active Directory] program. Se [[!DNL Dynamics 365] dokumentation](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#get-tenant-and-app-id-values-for-signing-in) för vägledning. | `1234567-aaaa-12ab-ba21-1234567890` |
| `Region` | Den Microsoft-region som är associerad med URL:en för miljön.<br> Se [[!DNL Dynamics 365] dokumentation](https://learn.microsoft.com/en-us/power-platform/admin/new-datacenter-regions) för vägledning. | Om din domän är som nedan måste du ange det markerade värdet för CRM-fältet i den nedrullningsbara väljaren när du autentiserar till [mål](#authenticate).<br> *org57771b33`crm`.dynamics.com*<br>  Ett exempel: Om ditt företag etableras i Nordamerika (NAM) skulle din URL vara `crm.dynamics.com` och du måste välja `crm`. Om ditt företag etableras i Kanada (CAN) är din URL `crm3.dynamics.com` och du måste välja `crm3`. |
| `Environment URL` | Se [[!DNL Dynamics 365] dokumentation](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/org-service/discover-url-organization-organization-service?view=op-9-1) för vägledning. | Om [!DNL Dynamics 365] domänen är som nedan, du behöver det markerade värdet.<br> *`org57771b33`.crm.dynamics.com* |

{style="table-layout:auto"}

## Guardrails {#guardrails}

The [Begäranden om gränser och tilldelningar](https://docs.microsoft.com/en-us/power-platform/admin/api-request-limits-allocations) sidinformation om [!DNL Dynamics 365] API-begränsningar som är kopplade till [!DNL Dynamics 365] licens. Du måste se till att dina data och din nyttolast är inom dessa begränsningar.

## Identiteter som stöds {#supported-identities}

[!DNL Dynamics 365] har stöd för uppdatering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/namespaces.md).

| Målidentitet | Exempel | Beskrivning | Överväganden |
|---|---|---|---|
| `contactid` | 7eb682f1-ca75-e511-80d4-00155d2a68d1 | Unik identifierare för en kontakt. | **Obligatoriskt**. Se [[!DNL Dynamics 365] dokumentation](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1) för mer information. |

{style="table-layout:auto"}

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs alla målgrupper som du kan exportera till det här målet.

Detta mål stöder aktivering av alla målgrupper som genererats via Experience Platform [Segmenteringstjänst](../../../segmentation/home.md).

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | <ul><li>Du exporterar alla medlemmar i en målgrupp tillsammans med de önskade schemafälten *(t.ex. e-postadress, telefonnummer, efternamn)*, enligt fältmappningen.</li><li> Varje målgruppsstatus i [!DNL Dynamics 365] uppdateras med motsvarande målgruppsstatus från Platform, baserat på **[!UICONTROL Mapping ID]** det värde som anges under [målgruppsplanering](#schedule-audience-export-example) steg.</li></ul> |
| Exportfrekvens | **[!UICONTROL Streaming]** | <ul><li>Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
>
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

Inom **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** sök efter [!DNL Dynamics 365]. Du kan även hitta den under **[!UICONTROL CRM]** kategori.

### Autentisera till mål {#authenticate}

Om du vill autentisera mot målet väljer du **[!UICONTROL Connect to destination]**.
![Skärmbild av användargränssnittet för plattformen som visar hur man autentiserar.](../../assets/catalog/crm/microsoft-dynamics-365/authenticate-destination.png)

Fyll i de obligatoriska fälten nedan. Se [Samla in Dynamics 365-autentiseringsuppgifter](#gather-credentials) för vägledning.
* **[!UICONTROL Client ID]**: [!DNL Dynamics 365] Klient-ID för din [!DNL Azure Active Directory] program.
* **[!UICONTROL Tenant ID]**: [!DNL Dynamics 365] Klient-ID för din [!DNL Azure Active Directory] program.
* **[!UICONTROL Client Secret]**: [!DNL Dynamics 365] Klienthemlighet för [!DNL Azure Active Directory] program.
* **[!UICONTROL Region]**: din [[!DNL Dynamics 365]](https://learn.microsoft.com/en-us/power-platform/admin/new-datacenter-regions) Region. Ett exempel: Om ditt företag etableras i Nordamerika (NAM) skulle din URL vara `crm.dynamics.com` och du måste välja `crm`. Om ditt företag etableras i Kanada (CAN) är din URL `crm3.dynamics.com` och du måste välja `crm3`.
* **[!UICONTROL Environment URL]**: din [!DNL Dynamics 365] Environment URL.

Om den angivna informationen är giltig visas en **[!UICONTROL Connected]** status med en grön bockmarkering. Du kan sedan gå vidare till nästa steg.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.
![Skärmbild för användargränssnittet för plattformen som visar målinformationen.](../../assets/catalog/crm/microsoft-dynamics-365/destination-details.png)

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Customization Prefix]**: `Customization prefix` av det anpassade fältet som du skapade i [!DNL Dynamics 365]. Se [Skapa och redigera fält](https://learn.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1#create-and-edit-fields) i [!DNL Dynamics 365] för mer information.

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

Så här skickar du målgruppsdata från Adobe Experience Platform till [!DNL Dynamics 365] mål måste du gå igenom fältmappningssteget. Mappningen består av att skapa en länk mellan XDM-schemafälten (Experience Data Model) i ditt plattformskonto och motsvarande motsvarigheter från målmålet. Mappa XDM-fälten korrekt till [!DNL Dynamics 365] målfält, följ dessa steg:

1. I **[!UICONTROL Mapping]** steg, välja **[!UICONTROL Add new mapping]**. En ny mappningsrad visas på skärmen.
   ![Exempel på skärmbild för användargränssnittet för plattformen för att lägga till ny mappning.](../../assets/catalog/crm/microsoft-dynamics-365/add-new-mapping.png)

1. I **[!UICONTROL Select source field]** väljer du **[!UICONTROL Select identity namespace]** kategori och välj `contactid`.
   ![Exempel på skärmbild för plattformsgränssnitt för källmappning.](../../assets/catalog/crm/microsoft-dynamics-365/source-mapping.png)

1. I **[!UICONTROL Select target field]** väljer du den typ av målfält som du vill mappa källfältet till.
   * **[!UICONTROL Select identity namespace]**: välj det här alternativet om du vill mappa källfältet till ett identitetsnamnområde från listan.
     ![Skärmbild av användargränssnittet för plattformen med målmappning för kontaktpersoner.](../../assets/catalog/crm/microsoft-dynamics-365/target-mapping-contactid.png)

   * Lägg till följande mappning mellan XDM-profilschemat och [!DNL Dynamics 365] instans: |XDM-profilschema|[!DNL Dynamics 365] Instans| Obligatorisk| |—|—|—| |`contactid`|`contactid`| Ja |

   * **[!UICONTROL Select custom attributes]**: välj det här alternativet om du vill mappa källfältet till ett anpassat attribut som du definierar i dialogrutan **[!UICONTROL Attribute name]** fält. Se [[!DNL Dynamics 365] dokumentation](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1#entity-properties) om du vill ha en omfattande lista över attribut som stöds.
     ![Skärmbild av användargränssnittet för plattformen med målmappning för e-post.](../../assets/catalog/crm/microsoft-dynamics-365/target-mapping-email.png)

     >[!IMPORTANT]
     >
     > * Målfältsnamn ska finnas i `lowercase`.
     > * Om du har ett källfält för datum- eller tidsstämpling som är mappat till en [!DNL Dynamics 365] [datum eller tidsstämpel](https://docs.microsoft.com/en-us/power-apps/developer/data-platform/webapi/reference/timestampdatemapping?view=dataverse-latest) ska du se till att det mappade värdet inte är tomt. Om värdet för det exporterade fältet är tomt kommer du att få ett *`Bad request reported while pushing events to the destination. Please contact the administrator and try again.`* felmeddelande och data kommer inte att uppdateras. Det här är en [!DNL Dynamics 365] begränsning.

   * Beroende på vilka värden du vill uppdatera lägger du till följande mappning mellan XDM-profilschemat och ditt [!DNL Dynamics 365] instans: |XDM-profilschema|[!DNL Dynamics 365] Instans| |—|—| |`person.name.firstName`|`firstname`| |`person.name.lastName`|`lastname`| |`personalEmail.address`|`emailaddress1`|

   * Ett exempel på hur du använder dessa mappningar visas nedan:
     ![Exempel på skärmbild för användargränssnittet för plattformen som visar målmappningar.](../../assets/catalog/crm/microsoft-dynamics-365/mappings.png)

### Schemalägg målgruppsexport och exempel {#schedule-audience-export-example}

I [[!UICONTROL Schedule audience export]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) steg i aktiveringsarbetsflödet måste du manuellt mappa Platform-målgrupper till det anpassade fältattributet i [!DNL Dynamics 365].

För att göra detta väljer du varje målgrupp och anger sedan motsvarande attribut för anpassade fält från [!DNL Dynamics 365] i **[!UICONTROL Mapping ID]** fält.

>[!IMPORTANT]
>
>Värdet som används för **[!UICONTROL Mapping ID]** ska exakt matcha namnet på det anpassade fältattributet som skapats i [!DNL Dynamics 365]. Se [[!DNL Dynamics 365] dokumentation](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1) om du behöver hjälp med att hitta anpassade fältattribut.

Ett exempel visas nedan:
![Exempel på skärmbild för användargränssnittet för plattformen som visar export av schemalagda målgrupper.](../../assets/catalog/crm/microsoft-dynamics-365/schedule-segment-export.png)

## Validera dataexport {#exported-data}

Följ stegen nedan för att verifiera att du har konfigurerat målet korrekt:

1. Välj **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** för att navigera till listan över destinationer.
   ![Skärmbild av användargränssnittet för plattformen med bläddringsmål.](../../assets/catalog/crm/microsoft-dynamics-365/browse-destinations.png)

1. Markera målet och validera att statusen är **[!UICONTROL enabled]**.
   ![Skärmbild av användargränssnittet för plattformen med körning av måldataflöde.](../../assets/catalog/crm/microsoft-dynamics-365/destination-dataflow-run.png)

1. Växla till **[!DNL Activation data]** väljer du ett målgruppsnamn.
   ![Skärmbild för användargränssnittet för plattformen visar aktiveringsdata för destinationer.](../../assets/catalog/crm/microsoft-dynamics-365/destinations-activation-data.png)

1. Övervaka målgruppssammanfattningen och se till att antalet profiler motsvarar antalet som skapas inom målgruppen.
   ![Exempel på skärmbild för användargränssnittet för plattformen som visar målgruppen.](../../assets/catalog/crm/microsoft-dynamics-365/segment.png)

1. Logga in på [!DNL Dynamics 365] webbplatsen och sedan navigera till [!DNL Customers] > [!DNL Contacts] och kontrollera om profilerna från målgruppen har lagts till. Du kan se att varje målgruppsstatus i [!DNL Dynamics 365] uppdaterades med motsvarande målgruppsstatus från Platform, baserat på **[!UICONTROL Mapping ID]** det värde som anges under [målgruppsplanering](#schedule-audience-export-example) steg.
   ![Skärmbild för användargränssnittet i Dynamics 365 som visar sidan Kontakter med uppdaterade målgruppsstatusar.](../../assets/catalog/crm/microsoft-dynamics-365/contacts.png)

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, se [Datastyrning - översikt](/help/data-governance/home.md).

## Fel och felsökning {#errors-and-troubleshooting}

### Okända fel påträffades när händelser skickades till målet {#unknown-errors}

Om du får följande felmeddelande när du kontrollerar ett dataflöde: `Bad request reported while pushing events to the destination. Please contact the administrator and try again.`

![Skärmbild för användargränssnittet för plattformen visar ett fel för felaktig begäran.](../../assets/catalog/crm/microsoft-dynamics-365/error.png)

Du kan åtgärda felet genom att kontrollera att **[!UICONTROL Mapping ID]** du angav i [!DNL Dynamics 365] för er plattformskrets är giltigt och finns inom [!DNL Dynamics 365].

## Ytterligare resurser {#additional-resources}

Ytterligare användbar information från [[!DNL Dynamics 365] dokumentation](https://docs.microsoft.com/en-us/dynamics365/) är under:
* [IOrganizationService.Update(Entity)-metod](https://docs.microsoft.com/en-us/dotnet/api/microsoft.xrm.sdk.iorganizationservice.update?view=dataverse-sdk-latest)
* [Uppdatera och ta bort tabellrader med webb-API](https://docs.microsoft.com/en-us/power-apps/developer/data-platform/webapi/update-delete-entities-using-web-api#basic-update)

### Changelog

I det här avsnittet beskrivs funktionaliteten och viktiga dokumentationsuppdateringar för den här målanslutningen.

+++ Visa ändringslogg

| Releasamånad | Uppdateringstyp | Beskrivning |
|---|---|---|
| Oktober 2023 | Dokumentation - uppdatering | Uppdaterad vägledning för att indikera alla målattributnamn ska vara i gemener i [Mappa överväganden och exempel](#mapping-considerations-example) steg. |
| Augusti 2023 | Funktioner och dokumentation | Stöd för [!DNL Dynamics 365] anpassade fältprefix för anpassade fält som inte skapades i standardlösningen i [!DNL Dynamics 365]. Ett nytt inmatningsfält, **[!UICONTROL Customization Prefix]**, har lagts till i [Fyll i målinformation](#destination-details) steg. (PLATIR-31602). |
| Nov 2022 | Inledande version | Ursprunglig målversion och dokumentationspublicering. |

{style="table-layout:auto"}

+++