---
title: (API) Oraclena Eloqua-anslutning
description: Med API-Oraclet Eloqua kan du exportera dina kontouppgifter och aktivera dem i Oracle Eloqua efter dina affärsbehov.
last-substantial-update: 2023-03-14T00:00:00Z
source-git-commit: 3197eddcf9fef2870589fdf9f09276a333f30cd1
workflow-type: tm+mt
source-wordcount: '1431'
ht-degree: 0%

---

# [!DNL (API) Oracle Eloqua] anslutning

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) gör det möjligt för marknadsförare att planera och genomföra kampanjer samtidigt som de levererar en personaliserad kundupplevelse till sina presumtiva kunder. Tack vare integrerad hantering av leads och enkel kampanjframtagning kan marknadsförarna engagera rätt målgrupp vid rätt tidpunkt i köparens resa och på ett elegant sätt skala nå målgrupper över olika kanaler, inklusive e-post, webbannonsering, video och mobiler. Säljarna kan sluta fler avtal snabbare och öka avkastningen på marknadsföringen genom realtidsinsikter.

Detta [!DNL Adobe Experience Platform] [mål](/help/destinations/home.md) utnyttjar [Uppdatera en kontakt](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-id-put.html) åtgärd från [!DNL Oracle Eloqua] REST API, som gör att du kan uppdatera identiteter inom ett segment till [!DNL Oracle Eloqua].

[!DNL Oracle Eloqua] använder [Grundläggande autentisering](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html) att kommunicera med [!DNL Oracle Eloqua] REST API. Instruktioner för hur du autentiserar [!DNL Oracle Eloqua] -instansen är längre ned, i [Autentisera till mål](#authenticate) -avsnitt.

## Användningsfall {#use-cases}

Som marknadsförare kan ni leverera personaliserade upplevelser till era användare, baserat på attribut från deras Adobe Experience Platform-profiler. Du kan skapa segment utifrån offlinedata och skicka dessa segment till [!DNL Oracle Eloqua], som visas i användarnas flöden så snart segment och profiler uppdateras i Adobe Experience Platform.

## Förutsättningar {#prerequisites}

### Krav för Experience Platform {#prerequisites-in-experience-platform}

Innan du aktiverar data för [!DNL Oracle Eloqua] mål, du måste ha en [schema](/help/xdm/schema/composition.md), a [datauppsättning](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)och [segment](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) skapad i [!DNL Experience Platform].

Se dokumentationen för Experience Platform för [Schemafältgrupp för detaljer om segmentmedlemskap](/help/xdm/field-groups/profile/segmentation.md) om du behöver vägledning om segmentstatus.

### [!DNL Oracle Eloqua] krav {#prerequisites-destination}

För att kunna exportera data från Platform till [!DNL Oracle Eloqua] konto du behöver ha [!DNL Oracle Eloqua] konto.

#### Samla [!DNL Oracle Eloqua] autentiseringsuppgifter {#gather-credentials}

Anteckna vad som står nedan innan du autentiserar dig för [!DNL Oracle Eloqua] mål:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `Username` | Användarnamnet för [!DNL Oracle Eloqua] konto. |
| `Password` | Lösenordet för [!DNL Oracle Eloqua] konto. |

## Guardrails {#guardrails}

>[!NOTE]
>
>* [!DNL Oracle Eloqua] anpassade kontaktfält skapas automatiskt med namnen på de segment som markerats under **[!UICONTROL Select segments]** steg.


* [!DNL Oracle Eloqua] har en maxgräns på 250 anpassade kontaktfält.
* Innan du exporterar nya segment ser du till att antalet plattformssegment och antalet befintliga segment inom [!DNL Oracle Eloqua] inte överskrider denna gräns.
* Om denna gräns överskrids kommer ett fel att uppstå i Experience Platform. Det beror på att [!DNL Oracle Eloqua] API:t kan inte validera begäran och svarar med en - *400: Ett valideringsfel uppstod* - felmeddelande som beskriver problemet.
* Om du har nått gränsen ovan måste du ta bort befintliga mappningar från målet och ta bort motsvarande anpassade kontaktfält i [!DNL Oracle Eloqua] innan du kan exportera fler segment.

* Se [Oraclet Eloqua skapar kontaktfält](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/ContactFields/Tasks/CreatingContactFields.htm) sida för information om ytterligare begränsningar.

## Identiteter som stöds {#supported-identities}

[!DNL Oracle Eloqua] har stöd för uppdatering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/namespaces.md).

| Målidentitet | Exempel | Beskrivning | Obligatoriskt |
|---|---|---|---|
| `EloquaId` | `111111` | Unik identifierare för kontakten. | Ja |

## Anslut till målet {#connect}

>[!IMPORTANT]
>
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

Inom **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** sök efter [!DNL (API) Oracle Eloqua]. Du kan även hitta den under **[!UICONTROL Email Marketing]** kategori.

### Autentisera till mål {#authenticate}

Fyll i de obligatoriska fälten nedan. Se [Samla [!DNL Oracle Eloqua] autentiseringsuppgifter](#gather-credentials) för vägledning.
* **[!UICONTROL Password]**: Lösenordet för [!DNL Oracle Eloqua] konto.
* **[!UICONTROL Username]**: Användarnamnet för [!DNL Oracle Eloqua] konto.

Om du vill autentisera mot målet väljer du **[!UICONTROL Connect to destination]**.
![Skärmbild av användargränssnittet för plattformen som visar hur man autentiserar.](../../assets/catalog/email-marketing/oracle-eloqua-api/authenticate-destination.png)

Om den angivna informationen är giltig visas en **[!UICONTROL Connected]** status med grön bockmarkering. Du kan sedan gå vidare till nästa steg.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.
![Skärmbild för användargränssnittet för plattformen som visar målinformationen.](../../assets/catalog/email-marketing/oracle-eloqua-api/destination-details.png)

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

Så här skickar du målgruppsdata från Adobe Experience Platform till [!DNL Oracle Eloqua] mål måste du gå igenom fältmappningssteget. Mappningen består av att skapa en länk mellan XDM-schemafälten (Experience Data Model) i ditt plattformskonto och motsvarande motsvarigheter från målmålet.

`EloquaID` måste uppdatera attribut som motsvarar identiteten. The `emailAddress` är också nödvändigt eftersom API utan detta orsakar ett fel enligt nedan:

```json
{
   "type":"ObjectValidationError",
   "container":{
      "type":"ObjectKey",
      "objectType":"Contact"
   },
   "property":"emailAddress",
   "requirement":{
      "type":"EmailAddressRequirement"
   },
   "value":"<null>"
}
```

Attribut som anges i **[!UICONTROL Target field]** ska namnges exakt så som beskrivs i tabellen för attributmappningar eftersom dessa attribut kommer att bilda begärandetexten.

Attribut som anges i **[!UICONTROL Source field]** inte följer någon sådan begränsning. Du kan mappa den baserat på dina behov, men om dataformatet inte är korrekt när det skickas till [!DNL Oracle Eloqua] det resulterar i ett fel.

Du kan till exempel mappa **[!UICONTROL Source field]** identity namespace `contact key`, `ABC ID` osv. till **[!UICONTROL Target field]** : `EloquaID` efter att ha säkerställt att ID-värdena överensstämmer med det format som accepteras av [!DNL Oracle Eloqua].

Koppla XDM-fälten till [!DNL Oracle Eloqua] målfält, följ dessa steg:

1. I **[!UICONTROL Mapping]** steg, välja **[!UICONTROL Add new mapping]**. En ny mappningsrad visas på skärmen.
1. I **[!UICONTROL Select source field]** väljer du **[!UICONTROL Select attributes]** och välj XDM-attributet eller välj **[!UICONTROL Select identity namespace]** och välj en identitet.
1. I **[!UICONTROL Select target field]** väljer du **[!UICONTROL Select identity namespace]** och välj en identitet eller välj **[!UICONTROL Select custom attributes]** och välj ett attribut efter behov.
   * Upprepa dessa steg för att lägga till följande mappningar mellan XDM-profilschemat och ditt [!DNL Oracle Eloqua] instans: |Källfält|Målfält| Obligatoriskt| |—|—|—| |`xdm: personalEmail.address`|`Attribute: emailAddress`| Ja | |`IdentityMap: Eid`|`Identity: EloquaId`| Ja |

   * Ett exempel på hur du använder dessa mappningar visas nedan:
      ![Skärmbild för plattformsgränssnitt med attributmappningar.](../../assets/catalog/email-marketing/oracle-eloqua-api/mappings.png)

      >[!IMPORTANT]
      >
      >Båda `emailAddress` och `EloquaId` Målattributsmappningar är obligatoriska.

När du är klar med mappningarna för målanslutningen väljer du **[!UICONTROL Next]**.

>[!NOTE]
>
>Målet lägger automatiskt till en unik identifierare till de valda segmentnamnen vid varje körning när kontaktfältsinformationen skickas till [!DNL Oracle Eloqua]. Detta garanterar att de kontaktfältsnamn som motsvarar dina segmentnamn inte överlappar varandra. Se [Validera dataexport](#exported-data) skärmbild av ett avsnitt [!DNL Oracle Eloqua] Kontaktinformation med anpassat kontaktfält som skapats med segmentnamnen.

## Validera dataexport {#exported-data}

Följ stegen nedan för att verifiera att du har konfigurerat målet korrekt:

1. Välj **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** och navigera till listan över destinationer.
1. Välj sedan målet och växla till **[!UICONTROL Activation data]** väljer du ett segmentnamn.
   ![Skärmbild för användargränssnittet för plattformen visar aktiveringsdata för destinationer.](../../assets/catalog/email-marketing/oracle-eloqua-api/destinations-activation-data.png)

1. Övervaka segmentsammanfattningen och kontrollera att antalet profiler motsvarar antalet inom segmentet.
   ![Exempel på skärmbild för plattformsgränssnitt som visar segment.](../../assets/catalog/email-marketing/oracle-eloqua-api/segment.png)

1. Logga in på [!DNL Oracle Eloqua] webbplatsen och sedan navigera till **[!UICONTROL Contacts Overview]** sida för att kontrollera om profilerna från segmentet har lagts till. Om du vill se segmentets status går du ned till en **[!UICONTROL Contact Detail]** och kontrollera om kontaktfältet med det valda segmentnamnet som prefix har skapats.

![Skärmbilden Oracle Eloqua UI som visar kontaktinformationssidan med ett anpassat kontaktfält som skapats med segmentnamnet.](../../assets/catalog/email-marketing/oracle-eloqua-api/contact.png)

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, se [Datastyrning - översikt](/help/data-governance/home.md).

## Fel och felsökning {#errors-and-troubleshooting}

När du skapar målet kan du få något av följande felmeddelanden: `400: There was a validation error` eller `400 BAD_REQUEST`. Detta inträffar när du överskrider gränsen på 250 anpassade kontaktfält, vilket beskrivs i [skyddsräcken](#guardrails) -avsnitt. Kontrollera att du inte överskrider gränsen för anpassade kontaktfält i [!DNL Oracle Eloqua].
![Skärmbild för användargränssnittet för plattformen visar ett fel.](../../assets/catalog/email-marketing/oracle-eloqua-api/error.png)

Se [[!DNL Oracle Eloqua] HTTP-statuskoder](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPStatusCodes.html) och [[!DNL Oracle Eloqua] Valideringsfel](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPValidationErrors.html) sidor med en omfattande lista över status- och felkoder med förklaringar.

## Ytterligare resurser {#additional-resources}

Ytterligare användbar information från [!DNL Oracle ELoqua] dokumentationen nedan:
* [Oracle Eloqua Marketing Automation](https://docs.oracle.com/en/cloud/saas/marketing/eloqua.html)
* [REST API för tjänsten Oracle Eloqua Marketing Cloud](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/rest-endpoints.html)