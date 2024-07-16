---
title: (Beta) Trade Desk - CRM-anslutning
description: Aktivera profiler på ert Trade Desk-konto för målgruppsanpassning och undertryckning baserat på CRM-data.
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 0%

---

# (Beta) [!DNL Trade Desk] - CRM-anslutningen

>[!IMPORTANT]
>
>[!DNL The Trade Desk - CRM]-målet i Platform är för närvarande i betaversion. Dokumentationen och funktionaliteten kan komma att ändras.
>
>I och med lanseringen av EUID (European Unified ID) ser du nu två [!DNL The Trade Desk - CRM] mål i [målkatalogen](/help/destinations/catalog/overview.md).
>* Använd målet **[!DNL The Trade Desk - CRM (EU)]** om du hämtar data i EU.
>* Använd målet **[!DNL The Trade Desk - CRM (NAMER & APAC)]** om du hämtar data i APAC- eller NAMER-regionerna.
>
>Båda destinationerna i Experience Platform är för närvarande betaversioner. Målanslutningen och dokumentationssidan skapas och underhålls av *[!DNL Trade Desk]*-teamet. Om du har frågor eller uppdateringsfrågor kontaktar du din [!DNL Trade Desk]-representant. Dokumentationen och funktionen kan komma att ändras.

## Översikt {#overview}

Det här dokumentet är utformat för att hjälpa dig att aktivera profiler för ditt [!DNL Trade Desk]-konto för målgruppsanpassning och inaktivering baserat på CRM-data.

[!DNL The Trade Desk(TTD)] hanterar inte direkt den överförda filen med e-postadresser och [!DNL The Trade Desk] lagrar inte heller dina ohashade e-postmeddelanden.

>[!TIP]
>
>Använd [!DNL The Trade Desk] CRM-mål för CRM-datamappning, till exempel e-post eller hash-e-postadress. Använd det [andra målet för Trade Desk](/help/destinations/catalog/advertising/tradedesk.md) i Adobe Experience Platform-katalogen för cookies och mappningar av enhets-ID.

## Förhandskrav {#prerequisites}

Innan du kan aktivera målgrupper för [!DNL The Trade Desk] måste du kontakta din [!DNL The Trade Desk]-kontohanterare för att signera CRM-introduktionskontraktet. [!DNL The Trade Desk] ger sedan tillstånd och delar ditt annonsörs-ID för att konfigurera ditt mål.

## Krav för ID-matchning {#id-matching-requirements}

Beroende på vilken typ av ID som du importerar till Adobe Experience Platform måste du följa deras motsvarande krav. Mer information finns i [Översikt över identitetsnamnet](/help/identity-service/features/namespaces.md).

## Identiteter som stöds {#supported-identities}

[!DNL The Trade Desk] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

Både oformaterad text och SHA256-hashade e-postadresser stöds av Adobe Experience Platform. Följ instruktionerna i avsnittet Krav för ID-matchning och använd lämpliga namnutrymmen för oformaterad text respektive hashade e-postadresser.

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| E-post | E-postadresser (klartext) | Ange `email` som målidentitet när din källidentitet är ett e-postnamnområde eller attribut. |
| Email_LC_SHA256 | E-postadresser måste hash-kodas med SHA256 och nedsänkt. Du kan inte ändra den här inställningen senare. | Ange `hashed_email` som målidentitet när din källidentitet är ett Email_LC_SHA256-namnutrymme eller -attribut. |

{style="table-layout:auto"}

## Krav för e-posthashning {#hashing-requirements}

Du kan hash-koda e-postadresser innan du importerar dem till Adobe Experience Platform eller använda obearbetade e-postadresser.

Läs [översikten över gruppimporten](/help/ingestion/batch-ingestion/overview.md) om du vill veta mer om hur du kan importera e-postadresser i Experience Platform.

Om du väljer att hash-koda e-postadresserna själv måste du se till att uppfylla följande krav:

* Ta bort inledande och avslutande blanksteg.
* Konvertera alla ASCII-tecken till gemener.
* Ta bort följande tecken från användarnamnsdelen i e-postadressen i `gmail.com`:
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

CRM-målet [!DNL The Trade Desk] är en daglig batchfilöverföring och kräver ingen autentisering av användaren.

### Fyll i målinformation {#fill-in-details}

Innan du kan skicka, eller aktivera, målgruppsdata till ett mål måste du skapa en anslutning till din egen målplattform. När [konfigurerar](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html) för det här målet måste du ange följande information:

* **[!UICONTROL Account Type]**: Välj alternativet **[!UICONTROL Existing Account]**.
* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Advertiser ID]**: din [!DNL Trade Desk Advertiser ID], som antingen kan delas av din [!DNL Trade Desk]-kontohanterare eller hittas under [!DNL Advertiser Preferences] i [!DNL Trade Desk]-gränssnittet.

![Skärmbild för plattformsgränssnitt som visar hur du fyller i målinformation.](/help/destinations/assets/catalog/advertising/tradedesk/configuredestination2.png)

När du ansluter till målet är det helt valfritt att ange en datastyrningsprincip. Mer information finns i Experience Platform [översikten över datastyrning](/help/data-governance/policies/overview.md).

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera målgruppsdata för exportmål för gruppprofiler](/help/destinations/ui/activate-batch-profile-destinations.md) om du vill ha instruktioner om hur du aktiverar målgrupper till ett mål.

På sidan **[!UICONTROL Scheduling]** kan du konfigurera schemat och filnamnen för varje målgrupp som du exporterar. Det är obligatoriskt att konfigurera schemat, men det är valfritt att konfigurera filnamnet.

![Skärmbild för plattformsgränssnitt för att schemalägga målgruppsaktivering.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment1.png)

>[!NOTE]
>
>Alla målgrupper som är aktiverade på [!DNL The Trade Desk] CRM-målet ställs automatiskt in på en daglig frekvens och fullständig filexport.

![Skärmbild för plattformsgränssnitt för att schemalägga målgruppsaktivering.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment2.png)

På sidan **[!UICONTROL Mapping]** måste du välja attribut eller identitetsnamnutrymmen från källkolumnen och mappa till målkolumnen.

![Skärmbild av plattformsgränssnitt för att mappa målgruppsaktivering.](/help/destinations/assets/catalog/advertising/tradedesk/mappingsegment1.png)

Nedan visas ett exempel på korrekt identitetsmappning när målgrupper aktiveras till CRM-målet [!DNL The Trade Desk].

>[!IMPORTANT]
>
> CRM-destinationen [!DNL The Trade Desk] accepterar inte oformaterade och streckade e-postadresser som identiteter i samma aktiveringsflöde. Skapa separata aktiveringsflöden för oformaterade och streckade e-postadresser.

Välja källfält:

* Välj namnutrymmet eller attributet `Email` som källidentitet om du använder den oformaterade e-postadressen vid datahämtning.
* Välj namnutrymmet eller attributet `Email_LC_SHA256` som källidentitet om du hashas i kundens e-postadresser vid datahämtning på plattformen.

Markera målfält:

* Ange `email` som målidentitet när källnamnområdet eller källattributet är `Email`.
* Ange `hashed_email` som målidentitet när källnamnområdet eller källattributet är `Email_LC_SHA256`.

## Validera dataexport {#validate}

Om du vill verifiera att data exporteras korrekt från Experience Platform och till [!DNL The Trade Desk] kan du hitta målgrupperna under datapanelen för Adobe 1PD i [!DNL The Trade Desk] Data Management Platform (DMP). Så här söker du efter motsvarande ID i användargränssnittet för [!DNL Trade Desk]:

1. Klicka först på fliken **[!UICONTROL Data]** och granska **[!UICONTROL First-Party]**.
2. Bläddra nedåt på sidan, under **[!UICONTROL Imported Data]**, hittar du **[!UICONTROL Adobe 1PD Tile]**.
3. Klicka på rutan**[!UICONTROL Adobe 1PD]** så listas alla målgrupper som är aktiverade för din annonsörs [!DNL Trade Desk] -mål. Du kan också använda sökfunktionen.
4. Segment-ID # från Experience Platform visas som segmentnamn i användargränssnittet för [!DNL Trade Desk].

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Datastyrningsöversikten](/help/data-governance/home.md).
