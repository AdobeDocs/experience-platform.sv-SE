---
title: (Beta) Trade Desk - CRM-anslutning
description: Aktivera profiler på ert Trade Desk-konto för målgruppsanpassning och undertryckning baserat på CRM-data.
source-git-commit: 69bf43f86ab3369ad0c7febcb69ec41d3bcac8bb
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 1%

---


# (Beta) [!DNL Trade Desk] - CRM-anslutning

>[!IMPORTANT]
>
> [!DNL The Trade Desk - CRM] målet i Platform är för närvarande i betaversion. Dokumentationen och funktionerna kan komma att ändras.

## Översikt {#overview}

>[!IMPORTANT]
>
> Dokumentationssidan skapades av *[!DNL Trade Desk]* team. Om du har frågor eller uppdateringsfrågor kontaktar du [!DNL Trade Desk] -representant.

Det här dokumentet är utformat för att hjälpa dig att aktivera profiler för [!DNL Trade Desk] för målgruppsanpassning och undertryckande baserat på CRM-data.

>[!TIP]
>
>Använd [!DNL The Trade Desk] CRM-mål för CRM-datamappning, t.ex. e-postadress eller hashad e-postadress. Använd [Annan destination för Trade Desk](/help/destinations/catalog/advertising/tradedesk.md) i Adobe Experience Platform-katalogen för cookies och mappningar av enhets-ID.

[!DNL The Trade Desk] (TTD) hanterar inte alltid den överförda filen med e-postadresser och inte heller [!DNL The Trade Desk] lagra e-postmeddelanden i Raw-format.

## Förutsättningar {#prerequisites}

Innan du kan aktivera segment till [!DNL The Trade Desk]måste du kontakta [!DNL The Trade Desk] kontoansvarig för att signera CRM-introduktionskontraktet. [!DNL The Trade Desk] ger sedan tillstånd och delar ditt annonsörs-ID för att konfigurera ditt mål.

## Krav för ID-matchning (#id-matching-requirements)

Beroende på vilken typ av ID som du importerar till Adobe Experience Platform måste du följa deras motsvarande krav. Läs [Översikt över namnområde för identitet](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=sv) för mer information.

## Identiteter som stöds {#supported-identities}

[!DNL The Trade Desk] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/namespaces.md).

Både oformaterad text och SHA256-hashade e-postadresser stöds av Adobe Experience Platform. Följ instruktionerna i avsnittet Krav för ID-matchning och använd lämpliga namnutrymmen för oformaterad text respektive hashade e-postadresser.

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| E-post | E-postadresser (klartext) | Välj `Email` mål-ID när din källidentitet är ett e-postnamnutrymme eller attribut. |
| Email_LC_SHA256 | E-postadresser måste hash-kodas med SHA256 och nedsänkt. Var noga med att följa [e-postnormalisering](https://github.com/UnifiedID2/uid2docs/tree/main/api#email-address-normalization) regler krävs. Du kan inte ändra den här inställningen senare. | Välj `Email_LC_SHA256` target-identitet när din källidentitet är ett Email_LC_SHA256-namnutrymme eller -attribut. |

{style=&quot;table-layout:auto&quot;}

## Krav för hashning via e-post (#hashing-requirements)

Du kan hash-koda e-postadresser innan du importerar dem till Adobe Experience Platform eller använda obearbetade e-postadresser.

Om du vill veta mer om hur du importerar e-postadresser i Experience Platform kan du läsa [batchvis hantering - översikt](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/overview.html?lang=en).

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
| Exporttyp | **[!UICONTROL Segment export]** | Du exporterar alla medlemmar i ett segment (målgrupp) med de identifierare (e-post eller hashade e-post) som används i Trade Desk-målet. |
| Exportfrekvens | **[!UICONTROL Daily Batch]** | När en profil uppdateras i Experience Platform baserat på segmentutvärdering uppdateras profilen (identiteterna) en gång om dagen nedströms till målplattformen. Läs mer om [batchöverföringar](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=en#file-based). |

{style=&quot;table-layout:auto&quot;}

## Anslut till målet {#connect}

### Autentisera till mål (#authenticate)

[!DNL The Trade Desk] CRM-målet är en daglig batchfilöverföring och kräver ingen autentisering av användaren.

### Fyll i målinformation (#fill-in-details)

Innan du kan skicka, eller aktivera, målgruppsdata till ett mål måste du skapa en anslutning till din egen målplattform. while [konfigurera](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en) Om du vill ange destinationen måste du ange följande information:

* **[!UICONTROL Account Type]**: Välj **[!UICONTROL Existing Account]** alternativ.
* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Advertiser ID]**: din [!DNL Trade Desk Advertiser ID], som antingen kan delas av dina [!DNL Trade Desk] Kontohanteraren eller finns under [!DNL Advertiser Preferences] i [!DNL Trade Desk] Gränssnitt.

När du ansluter till målet är det helt valfritt att ange en datastyrningsprincip. Granska Experience Platform [datastyrningsöversikt](https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html?lang=en) för mer information.

## Aktivera segment till den här destinationen {#activate}

Se [aktivera målgruppsdata till exportmål för batchprofiler](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en) för instruktioner om hur du aktiverar målgruppssegment till ett mål.

I **[!UICONTROL Scheduling]** kan du konfigurera schemat och filnamnen för varje segment som du exporterar. Det är obligatoriskt att konfigurera schemat, men det är valfritt att konfigurera filnamnet.

>[!NOTE]
>
>Alla segment aktiverade för [!DNL The Trade Desk] CRM-målet ställs automatiskt in på en daglig frekvens och fullständig filexport.

I **[!UICONTROL Mapping]** måste du välja attribut eller identitetsnamnutrymmen i källkolumnen och mappa till målkolumnen.

Nedan visas ett exempel på korrekt identitetsmappning när segment aktiveras för [!DNL The Trade Desk] CRM-mål.

>[!IMPORTANT]
>
> [!DNL The Trade Desk] CRM-destinationen accepterar inte oformaterade och streckade e-postadresser som identiteter i samma aktiveringsflöde. Skapa separata aktiveringsflöden för oformaterade och streckade e-postadresser.

Välja källfält:

* Välj `Email` namnutrymmet eller attributet som källidentitet om du använder den oformaterade e-postadressen vid datahämtning.
* Välj `Email_LC_SHA256` namnutrymmet eller attributet som källidentitet om du hash-kodade kundens e-postadresser när data hämtas till Platform.

Markera målfält:

* Välj `Email` namnutrymme som målidentitet när källnamnutrymmet eller attributet är `Email`.
* Välj `Email_LC_SHA256` namnutrymme som målidentitet när källnamnutrymmet eller attributet är `Email_LC_SHA256`.

## Validera dataexport (#validate)

Validera att data exporteras korrekt från Experience Platform och till [!DNL The Trade Desk]hittar du segmenten under datapanelen Adobe 1PD i [!DNL The Trade Desk] Plattform för datahantering (DMP). Här följer stegen för att hitta motsvarande ID i [!DNL Trade Desk] Gränssnitt:

1. Klicka först på **[!UICONTROL Data]** Flikar och granska **[!UICONTROL First-Party]**.
2. Bläddra nedåt på sidan, under **[!UICONTROL Imported Data]** hittar du **[!UICONTROL Adobe 1PD Tile]**.
3. Klicka på**[!UICONTROL Adobe 1PD]** sida vid sida och visar alla segment som är aktiverade för [!DNL Trade Desk] mål för annonsören. Du kan också använda sökfunktionen.
4. Segment-ID # från Experience Platform visas som segmentnamn i [!DNL Trade Desk] Gränssnitt.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, se [Datastyrning - översikt](/help/data-governance/home.md).
