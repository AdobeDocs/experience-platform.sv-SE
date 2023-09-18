---
title: (Beta) Trade Desk - CRM-anslutning
description: Aktivera profiler på ert Trade Desk-konto för målgruppsanpassning och undertryckning baserat på CRM-data.
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: 661ef040398a9e2ef8dd9cebdf7bd27d4268636b
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 0%

---

# (Beta) [!DNL Trade Desk] - CRM-anslutning

>[!IMPORTANT]
>
>[!DNL The Trade Desk - CRM] målet i Platform är för närvarande i betaversion. Dokumentationen och funktionaliteten kan komma att ändras.
>
>I och med lanseringen av EUID (European Unified ID) ser du nu två [!DNL The Trade Desk - CRM] destinationer i [målkatalog](/help/destinations/catalog/overview.md).
>* Om du hämtar data i EU ska du använda **[!DNL The Trade Desk - CRM (EU)]** mål.
>* Om du hämtar data i APAC- eller NAMER-regionerna använder du **[!DNL The Trade Desk - CRM (NAMER & APAC)]** mål.
>
>Båda destinationerna i Experience Platform är för närvarande betaversioner. Målanslutningen och dokumentationssidan skapas och underhålls av *[!DNL Trade Desk]* team. Om du har frågor eller uppdateringsfrågor kontaktar du [!DNL Trade Desk] kan dokumentationen och funktionaliteten ändras.

## Översikt {#overview}

Det här dokumentet är utformat för att hjälpa dig att aktivera profiler för [!DNL Trade Desk] för målgruppsanpassning och undertryckande baserat på CRM-data.

[!DNL The Trade Desk(TTD)] hanterar inte direkt den överförda filen med e-postadresser och inte heller [!DNL The Trade Desk] lagra e-postmeddelanden i Raw-format.

>[!TIP]
>
>Använd [!DNL The Trade Desk] CRM-mål för CRM-datamappning, t.ex. e-postadress eller hash-adress. Använd [Annan destination för Trade Desk](/help/destinations/catalog/advertising/tradedesk.md) i Adobe Experience Platform-katalogen för cookies och mappningar av enhets-ID.

## Förutsättningar {#prerequisites}

Innan du kan aktivera målgrupper för [!DNL The Trade Desk]måste du kontakta [!DNL The Trade Desk] kontoansvarig för att signera CRM-introduktionskontraktet. [!DNL The Trade Desk] ger sedan tillstånd och delar ditt annonsörs-ID för att konfigurera ditt mål.

## Krav för ID-matchning {#id-matching-requirements}

Beroende på vilken typ av ID som du importerar till Adobe Experience Platform måste du följa deras motsvarande krav. Läs [Översikt över namnområde för identitet](/help/identity-service/namespaces.md) för mer information.

## Identiteter som stöds {#supported-identities}

[!DNL The Trade Desk] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/namespaces.md).

Både oformaterad text och SHA256-hashade e-postadresser stöds av Adobe Experience Platform. Följ instruktionerna i avsnittet Krav för ID-matchning och använd lämpliga namnutrymmen för oformaterad text respektive hashade e-postadresser.

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| E-post | E-postadresser (klartext) | Indata `email` som målidentitet när din källidentitet är ett e-postnamnutrymme eller attribut. |
| Email_LC_SHA256 | E-postadresser måste hash-kodas med SHA256 och nedsänkt. Var noga med att följa [e-postnormalisering](https://github.com/UnifiedID2/uid2docs/tree/main/api#email-address-normalization) regler krävs. Du kan inte ändra den här inställningen senare. | Indata `hashed_email` som målidentitet när källidentiteten är ett Email_LC_SHA256-namnutrymme eller -attribut. |

{style="table-layout:auto"}

## Krav för e-posthashning {#hashing-requirements}

Du kan hash-koda e-postadresser innan du importerar dem till Adobe Experience Platform eller använda obearbetade e-postadresser.

Om du vill veta mer om att importera e-postadresser i Experience Platform läser du [batchvis hantering - översikt](/help/ingestion/batch-ingestion/overview.md).

Om du väljer att hash-koda e-postadresserna själv måste du se till att uppfylla följande krav:

* Ta bort inledande och avslutande blanksteg.
* Konvertera alla ASCII-tecken till gemener.
* I `gmail.com` e-postadresser, ta bort följande tecken från e-postadressens användarnamn:
   * Perioden (. (ASCII-kod 46). Till exempel normalisera `jane.doe@gmail.com` till `janedoe@gmail.com`.
   * Plustecknet (+ (ASCII-kod 43)) och alla efterföljande tecken. Till exempel normalisera `janedoe+home@gmail.com` till `janedoe@gmail.com`.

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en målgrupp med de identifierare (e-post eller hashad e-post) som används i Trade Desk-målet. |
| Exportfrekvens | **[!UICONTROL Daily Batch]** | När en profil uppdateras i Experience Platform baserat på målgruppsutvärdering uppdateras profilen (identiteterna) en gång om dagen nedströms till målplattformen. Läs mer om [batchexport](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

### Autentisera till mål {#authenticate}

[!DNL The Trade Desk] CRM-målet är en daglig batchfilöverföring och kräver ingen autentisering av användaren.

### Fyll i målinformation {#fill-in-details}

Innan du kan skicka, eller aktivera, målgruppsdata till ett mål måste du skapa en anslutning till din egen målplattform. while [konfigurera](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en) Om du vill ange destinationen måste du ange följande information:

* **[!UICONTROL Account Type]**: Välj **[!UICONTROL Existing Account]** alternativ.
* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Advertiser ID]**: din [!DNL Trade Desk Advertiser ID], som antingen kan delas av dina [!DNL Trade Desk] Kontohanteraren eller finns under [!DNL Advertiser Preferences] i [!DNL Trade Desk] Gränssnitt.

![Skärmbild av användargränssnittet för plattformen som visar hur du fyller i målinformation.](/help/destinations/assets/catalog/advertising/tradedesk/configuredestination2.png)

När du ansluter till målet är det helt valfritt att ange en datastyrningsprincip. Granska Experience Platform [datastyrningsöversikt](/help/data-governance/policies/overview.md) för mer information.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.
>* Exportera *identiteter* behöver du **[!UICONTROL View Identity Graph]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). <br> ![Markera det identitetsnamnutrymme som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera det identitetsnamnutrymme som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [aktivera målgruppsdata till exportmål för batchprofiler](/help/destinations/ui/activate-batch-profile-destinations.md) för instruktioner om hur du aktiverar målgrupper till ett mål.

I **[!UICONTROL Scheduling]** kan du konfigurera schemat och filnamnen för varje publik som du exporterar. Det är obligatoriskt att konfigurera schemat, men det är valfritt att konfigurera filnamnet.

![Skärmbild för plattformsgränssnitt för att schemalägga målgruppsaktivering.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment1.png)

>[!NOTE]
>
>Alla målgrupper aktiverade för [!DNL The Trade Desk] CRM-målet ställs automatiskt in på en daglig frekvens och fullständig filexport.

![Skärmbild för plattformsgränssnitt för att schemalägga målgruppsaktivering.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment2.png)

I **[!UICONTROL Mapping]** måste du välja attribut eller identitetsnamnutrymmen i källkolumnen och mappa till målkolumnen.

![Skärmbild av användargränssnittet för plattformen för att kartlägga målgruppsaktivering.](/help/destinations/assets/catalog/advertising/tradedesk/mappingsegment1.png)

Nedan visas ett exempel på korrekt identitetsmappning när målgrupper aktiveras för [!DNL The Trade Desk] CRM-mål.

>[!IMPORTANT]
>
> [!DNL The Trade Desk] CRM-destinationen accepterar inte oformaterade och streckade e-postadresser som identiteter i samma aktiveringsflöde. Skapa separata aktiveringsflöden för oformaterade och streckade e-postadresser.

Välja källfält:

* Välj `Email` namnutrymmet eller attributet som källidentitet om du använder den oformaterade e-postadressen vid datainmatning.
* Välj `Email_LC_SHA256` namnutrymmet eller attributet som källidentitet om du hash-kodade kundens e-postadresser när data hämtas till Platform.

Markera målfält:

* Indata  `email` som målidentitet när källnamnutrymmet eller attributet är `Email`.
* Indata  `hashed_email` som målidentitet när källnamnutrymmet eller attributet är `Email_LC_SHA256`.

## Validera dataexport {#validate}

Validera att data exporteras korrekt från Experience Platform och till [!DNL The Trade Desk]hittar du målgrupperna under dataplattan Adobe 1PD i [!DNL The Trade Desk] Datahanteringsplattform (DMP). Här följer stegen för att hitta motsvarande ID i [!DNL Trade Desk] Gränssnitt:

1. Klicka först på **[!UICONTROL Data]** Flikar och granska **[!UICONTROL First-Party]**.
2. Bläddra nedåt på sidan, under **[!UICONTROL Imported Data]** hittar du **[!UICONTROL Adobe 1PD Tile]**.
3. Klicka på**[!UICONTROL Adobe 1PD]** så listas alla målgrupper som är aktiverade för [!DNL Trade Desk] mål för annonsören. Du kan också använda sökfunktionen.
4. Segment-ID # från Experience Platform visas som segmentnamn i [!DNL Trade Desk] Gränssnitt.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, se [Datastyrning - översikt](/help/data-governance/home.md).
