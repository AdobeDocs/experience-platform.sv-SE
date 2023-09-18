---
title: Salesforce Marketing Cloud Account Engagement
description: Lär dig hur du använder Salesforce Marketing Cloud Account Engagement (tidigare Pardot)-målet för att exportera dina kontodata och aktivera dem i Salesforce Marketing Cloud Account Engagement för dina affärsbehov.
last-substantial-update: 2023-04-14T00:00:00Z
exl-id: fca9d4f4-8717-4bfa-9992-5164ba98bea4
source-git-commit: 8e37ff057ec0fb750bc7b4b6f566f732d9fe5d68
workflow-type: tm+mt
source-wordcount: '1568'
ht-degree: 1%

---

# [!DNL Salesforce Marketing Cloud Account Engagement] anslutning

Använd [[!DNL Salesforce Marketing Cloud Account Engagement]](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) *(tidigare känt som [!DNL Pardot])* mål för att fånga, spåra, poängsätta och betygsätta leads. Ni kan också utforma huvudspår för alla faser av pipeline för riktade målgrupper och kundgrupper via e-postdroppkampanjer och lead-hantering med näring, poängsättning och kampanjsegmentering.

Jämfört med [!DNL Salesforce Marketing Cloud Engagement] som är mer inriktad på **B2C** marknadsföring, [!DNL Marketing Cloud Account Engagement] är idealiskt för **B2B** använda ärenden som berör flera avdelningar och beslutsfattare och som kräver längre försäljnings- och beslutscykler. Dessutom ligger ni närmare och är bättre integrerade med CRM för att fatta lämpliga beslut om försäljning och marknadsföring. *Observera att Experience Platform också har anslutningar för [!DNL Salesforce Marketing Cloud Engagement]kan du kontrollera dem på [[!DNL Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) och [[!DNL (API) Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md) sidor.*

Detta [!DNL Adobe Experience Platform] [mål](/help/destinations/home.md) utnyttjar [[!DNL Salesforce Account Engagement API > Prospect Upsert by Email]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#prospect-upsert-by-email) slutpunkt, till **lägga till eller uppdatera dina leads** efter att ha aktiverat dem i en ny [!DNL Marketing Cloud Account Engagement] segment.

[!DNL Marketing Cloud Account Engagement] använder protokollet OAuth 2 med Authorization Code för att autentisera [!DNL Account Engagement] API. Instruktioner för hur du autentiserar [!DNL Marketing Cloud Account Engagement] -instansen är längre ned, i [Autentisera till mål](#authenticate) -avsnitt.

## Användningsfall {#use-cases}

För att du bättre ska förstå hur och när du ska använda [!DNL Marketing Cloud Account Engagement] mål, här är ett exempel på användning som Adobe Experience Platform-kunder kan lösa genom att använda den här destinationen.

### Skicka e-post till kontakter för marknadsföringskampanjer {#use-case-send-emails}

Marknadsföringsavdelningen på en onlineplattform vill sända en e-postbaserad marknadsföringskampanj till en välstrukturerad publik av B2B-leads. Plattformens marknadsföringsteam kan lägga till nya leads eller uppdatera befintlig lead-information via Adobe Experience Platform, bygga målgrupper utifrån sina egna offlinedata och skicka dessa målgrupper till [!DNL Marketing Cloud Account Engagement]som sedan kan användas för att skicka marknadsföringskampanjens e-post.

## Förutsättningar {#prerequisites}

I avsnitten nedan finns information om alla krav som du måste ställa in i Experience Platform och [!DNL Salesforce] och för information som du behöver samla in innan du arbetar med [!DNL Marketing Cloud Account Engagement] mål.

### Förutsättningar i Experience Platform {#prerequisites-in-experience-platform}

Innan du aktiverar data för [!DNL Marketing Cloud Account Engagement] mål, du måste ha [schema](/help/xdm/schema/composition.md), a [datauppsättning](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)och [segment](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) som [!DNL Experience Platform].

### Krav [!DNL Marketing Cloud Account Engagement] {#prerequisites-destination}

Observera följande krav för att kunna exportera data från Platform till [!DNL Marketing Cloud Account Engagement] konto:

#### Du måste ha en [!DNL Marketing Cloud Account Engagement] konto {#prerequisites-account}

A [!DNL Marketing Cloud Account Engagement] konto med en prenumeration på [Marketing Cloud-kontoengagemang](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) produkten är obligatorisk för att fortsätta.

Dina [!DNL Salesforce] kontot ska ha [!DNL Salesforce] `Account Engagement Administrator role`. Detta krävs för att [skapa anpassade fält för potentiell kund](https://help.salesforce.com/s/articleView?id=sf.pardot_fields_create_custom_field.htm&amp;type=5).

Slutligen bör ditt konto även kunna komma åt [[!DNL Account Engagement Lightning App]](https://help.salesforce.com/s/articleView?id=sf.pardot_lightning_enable.htm&amp;type=5).

Nå ut till [[!DNL Salesforce] Support](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10) eller [!DNL Salesforce] kontoadministratören om du inte har något konto eller om kontot saknas [!DNL Marketing Cloud Account Engagement] prenumerationen eller [!DNL Account Engagement Administrator role].

#### Samla [!DNL Marketing Cloud Account Engagement] autentiseringsuppgifter {#gather-credentials}

Anteckna nedanstående innan du autentiserar dig för [!DNL Marketing Cloud Account Engagement] mål.

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `Username` | Dina [!DNL Marketing Cloud Account Engagement] användarnamn för konto. |
| `Password` | Dina [!DNL Marketing Cloud Account Engagement] kontolösenord. |
| `Account Engagement Business Unit ID` | Om du vill hitta affärsenhets-ID för kontoengagemang använder du Inställningar i [!DNL Salesforce]. I installationsprogrammet anger du *Konfiguration av affärsenhet* i rutan Snabbsökning. Affärsenhets-ID för ditt kontoengagemang börjar med `0Uv` och är 18 tecken långt. Om du inte kan komma åt information om affärsenhetens inställningar frågar du [!DNL Salesforce] Kontoadministratör för att ge dig `Account Engagement Business Unit ID`. Om du behöver ytterligare vägledning, se [[!DNL Salesforce] Autentisering](https://developer.salesforce.com/docs/marketing/pardot/guide/authentication) stödsida. |

{style="table-layout:auto"}

### Guardrails {#guardrails}

Se [!DNL Marketing Cloud Account Engagement] [hastighetsbegränsningar](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html#rate-limits) som närmare anger de gränser som er plan innebär och som även skulle gälla för Experience Platform-avrättningarna.

>[!IMPORTANT]
>
>Om [!DNL Salesforce] kontoadministratören har begränsat åtkomsten till betrodda IP-intervall, du måste kontakta dem för att få [IP-adresser för Experience Platform](/help/destinations/catalog/streaming/ip-address-allow-list.md) tillåtslista. Se [!DNL Salesforce] [Begränsa åtkomst till betrodda IP-intervall för ett anslutet program](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) dokumentation om du behöver ytterligare vägledning.

## Identiteter som stöds {#supported-identities}

[!DNL Marketing Cloud Account Engagement] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| E-post | E-postadress för potentiell kund | Obligatoriskt |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | <ul><li>Du exporterar alla medlemmar i ett segment tillsammans med de önskade schemafälten *(t.ex. e-postadress, telefonnummer, efternamn)*, enligt fältmappningen.</li><li> För varje vald publik i Platform [!DNL Salesforce Marketing Cloud Account Engagement] segmentets status uppdateras med målgruppsstatus från Platform.</li></ul> |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
>
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

Inom **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**, sök efter [!DNL Salesforce Marketing Cloud Account Engagement]. Du kan även hitta den under **[!UICONTROL Email marketing]** kategori.

### Autentisera till mål {#authenticate}

Om du vill autentisera mot målet väljer du **[!UICONTROL Connect to destination]**. Du kommer att navigeras till [!DNL Salesforce] inloggningssida. Ange [!DNL Marketing Cloud Account Engagement] kontoinloggningsuppgifter och välj [!DNL Log In].

![Skärmbild av användargränssnittet för plattformen som visar hur du autentiserar till Marketing Cloud Account Engagement.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/authenticate-destination.png)

Nästa, Välj [!UICONTROL Allow] i efterföljande fönster för att ge behörighet till **Adobe Experience Platform** app för att få tillgång till [!DNL Salesforce Marketing Cloud Account Engagement] konto. *Du behöver bara göra detta en gång*.

![Salesforce-appens bekräftelsepopup för skärmavbild för att ge Experience Platform-appen åtkomst till Marketing Cloud Account Engagement.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/allow-app.png)

Om den angivna informationen är giltig visas ett meddelande: *Du har anslutit till Salesforce Marketing Cloud Account Engagement-kontot* meddelande och **[!UICONTROL Connected]** status med en grön bockmarkering kan du fortsätta till nästa steg.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt. Se [Samla [!DNL Marketing Cloud Account Engagement] autentiseringsuppgifter](#gather-credentials) för vägledning.

![Skärmbild för användargränssnittet för plattformen som visar målinformationen.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/destination-details.png)

| Fält | Beskrivning |
| --- | --- |
| **[!UICONTROL Name]** | Ett namn som du känner igen det här målet med i framtiden. |
| **[!UICONTROL Description]** | En beskrivning som hjälper dig att identifiera det här målet i framtiden. |
| **[!UICONTROL Account Engagement Business Unit ID]** | Din [!DNL Salesforce] `Account Engagement Business Unit ID`. |

{style="table-layout:auto"}

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

Så här skickar du målgruppsdata från Adobe Experience Platform till [!DNL Marketing Cloud Account Engagement] mål måste du gå igenom fältmappningssteget. Mappningen består av att skapa en länk mellan XDM-schemafälten (Experience Data Model) i ditt plattformskonto och motsvarande motsvarigheter från målmålet.

Mappa XDM-fälten korrekt till [!DNL Marketing Cloud Account Engagement] målfält, följ stegen nedan.

1. I **[!UICONTROL Mapping]** steg, välja **[!UICONTROL Add new mapping]**. En ny mappningsrad visas på skärmen.
1. I **[!UICONTROL Select source field]** väljer du **[!UICONTROL Select attributes]** och välj XDM-attributet eller välj **[!UICONTROL Select identity namespace]** och välj en identitet.
1. I **[!UICONTROL Select target field]** väljer du **[!UICONTROL Select identity namespace]** och välj en identitet eller välj **[!UICONTROL Select custom attributes]** -kategori och ange i listan över [[!DNL Prospect API fields]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#fields) från tillgängligt schema.

   * Upprepa de här stegen för att lägga till mappningar mellan XDM-profilschemat och [!DNL Marketing Cloud Account Engagement]: | Källfält | Målfält | Obligatoriskt | | — | — | — | |`IdentityMap: Email`|`Identity: email`| Ja | |`xdm: MailingAddress.city`|`xdm: city`| | |`xdm: person.name.firstName`|`Attribute: firstName`| |

   * Ett exempel med mappningarna ovan visas nedan:
     ![Exempel på skärmbild för användargränssnittet för plattformen som visar målmappningar.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/mappings.png)

När du har angett mappningarna för målanslutningen väljer du **[!UICONTROL Next]**.

## Validera dataexport {#exported-data}

Följ stegen nedan för att verifiera att du har konfigurerat målet korrekt:

1. Navigera till en av de valda målgrupperna. Klicka på fliken **[!DNL Activation data]**.  The **[!UICONTROL Mapping ID]** kolumnen visar namnet på det anpassade fält som genereras i [!DNL Marketing Cloud Account Engagement Prospects] sida.
   ![Exempel på skärmbild för plattformsgränssnitt som visar mappnings-ID för ett valt segment.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/selected-segment-mapping-id.png)

1. Logga in på [[!DNL Salesforce]](https://login.salesforce.com/) webbplats. Navigera sedan till **[!DNL Account Engagement]** > **[!DNL Prospects]** > **[!DNL Pardot Prospects]** och kontrollera om målgruppens potentiella kunder har lagts till/uppdaterats. Du kan även använda [[!DNL Salesforce Pardot]](https://pi.pardot.com/) och få tillgång till **[!DNL Prospects]** sida.
   ![Salesforce-användargränssnittet visar sidan Prospects.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospects.png)

1. Om du vill kontrollera om potentiella kunder har uppdaterats markerar du en potentiell kund och kontrollerar om fältet för anpassad potentiell kund har uppdaterats med Experience Platform-målgruppsstatus.
   ![Användargränssnittet i Salesforce som visar den valda sidan för potentiell kund uppdateras det anpassade fältet för potentiell kund med målgruppens status.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospect.png)

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, se [Datastyrning - översikt](/help/data-governance/home.md).

## Ytterligare resurser {#additional-resources}

* [!DNL Marketing Cloud Account Engagement] [API-dokumentation](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html).
