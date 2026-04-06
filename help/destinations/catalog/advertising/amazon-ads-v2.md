---
title: Amazon Ads v2
description: Amazon Ads v2 erbjuder en rad alternativ som hjälper er att nå era annonsmål för registrerade säljare, leverantörer, bokleverantörer, Kindle Direct Publishing-författare (KDP), apputvecklare och byråer. Integreringen av Amazon Ads v2 med Adobe Experience Platform ger körklar integrering med Amazon Ads-produkterna.
last-substantial-update: 2026-03-31T00:00:00Z
source-git-commit: 1e93c78b13159a2aed24d283e3768c670ad14097
workflow-type: tm+mt
source-wordcount: '1667'
ht-degree: 0%

---

# Amazon Ads v2-anslutning {#amazon-ads-v2}

## Översikt {#overview}

Med [!DNL Amazon Ads v2] kan annonsörer effektivt importera, hantera, aktivera och återanvända målgruppsdata i alla [!DNL Amazon Ads] -produkter.

>[!IMPORTANT]
>
>[!DNL Amazon Ads v2] är det aktuella målet för alla nya [!DNL Amazon Ads]-anslutningar. Om du har en befintlig [(äldre) [!DNL Amazon Ads]](./amazon-ads.md)-anslutning fortsätter den att fungera utan nödvändiga ändringar. [!DNL Amazon Ads v2] ansluter till [!DNL Ads Data Manager], som har stöd för utökade identitetstyper, adressrelaterade fält och datadelning mellan [!DNL Amazon Ads]-produkter, vilket förbättrar målgruppsanpassningen och målgruppsmatchningen jämfört med [(äldre) [!DNL Amazon Ads]](./amazon-ads.md).
>
>Efter slutet av april 2026 kommer namnet på [!DNL Amazon Ads v2] att ändras till [!DNL Amazon Ads] och det gamla kortet kommer att döljas, så att ett enda målkort finns kvar i katalogen. Befintliga gamla dataflöden fortsätter att fungera och du kan hantera dem på fliken **[!UICONTROL Browse]** efter det datumet.

Integrationen [!DNL Amazon Ads v2] med [!DNL Adobe Experience Platform] ger en direkt anslutning för att importera målgruppsmedlemmar till [!DNL Amazon Ads]. De överförda målgrupperna är tillgängliga i [!DNL Ads Data Manager (ADM)]-konsolen i [!DNL Amazon Ads]. Du kan använda konsolen [!DNL Ads Data Manager] för att dela data mellan olika [!DNL Amazon Ads]-produkter.

Mer information om [!DNL Ads Data Manager] finns i:

* [Ads Data Manager - Konsolöversikt](https://advertising.amazon.com/API/docs/en-us/adm/1_ads-data-manager-console-overview)
* [Använda Adds Data Manager-konsolen](https://advertising.amazon.com/API/docs/en-us/adm/2_ads-data-manager-console)
* [Kontoinställning i Ads Data Manager](https://advertising.amazon.com/API/docs/en-us/adm/2a_ads-data-manager_account_setup)

>[!IMPORTANT]
>
>Målanslutningen och dokumentationssidan skapas och underhålls av *[!DNL Amazon Ads]*-teamet. Om du har frågor eller uppdateringsförfrågningar kontaktar du dem direkt på *`amc-support@amazon.com`.*

## Användningsfall {#use-cases}

För att du bättre ska kunna förstå hur och när du ska använda målet [!DNL Amazon Ads v2] finns det exempel på användningsområden som [!DNL Adobe Experience Platform]-kunder kan lösa genom att använda det här målet.

### Målgruppsintag och -aktivering {#activation-and-targeting}

Ett sportklädmärke vill nå sina befintliga kunder med relevanta annonser över [!DNL Amazon Ads]. Varumärket kan importera e-postadresser från sina CRM till [!DNL Adobe Experience Platform], bygga målgrupper med hjälp av egna offlinedata och aktivera dessa målgrupper till [!DNL Amazon Ads] via målet [!DNL Amazon Ads v2]. Efter aktiveringen kan ni använda dessa målgrupper för att rikta annonser till dessa kunder i hela [!DNL Amazon Ads]-lagret, vilket hjälper varumärket att återengagera kända kunder och driva upprepade inköp. Mer information finns i [Hantera data](https://advertising.amazon.com/API/docs/en-us/adm/6_adm-manage-data).

## Förutsättningar {#prerequisites}

Om du vill använda anslutningen [!DNL Amazon Ads v2] med [!DNL Adobe Experience Platform] måste du ha åtkomst till **[!DNL Amazon Ads Data Manager]** med ett [hanterarkonto](https://advertising.amazon.com/help/G69CDSR9MNSWJH95). Mer information finns i [Kom igång med Amazon Ads Data Manager](https://advertising.amazon.com/API/docs/en-us/adm/1_ads-data-manager-console-overview).

### Acceptera Amazon Ads Data Manager-villkor {#accept-terms}

Logga in på ditt [!DNL Amazon Ads v2]-konto och godkänn villkoren för [!DNL Amazon Ads] innan du konfigurerar [!DNL Ads Data Manager]-målet. Navigera till [!DNL Ads Data Manager]-konsolen i [!DNL Amazon Ads] och acceptera villkoren när du uppmanas till det. Om du inte godkänner villkoren skapas inte målgrupper i [!DNL Amazon Ads].

## Identiteter som stöds {#supported-identities}

Målet [!DNL Amazon Ads v2] stöder aktivering av följande identiteter. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| `phone` | Telefonnummer hashas med SHA256-algoritmen | Både oformaterad text och SHA256-hashade telefonnummer stöds av [!DNL Adobe Experience Platform]. När källfältet innehåller ohashade attribut bör du kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Experience Platform] automatiskt hash-kodar data vid aktiveringen. |
| `email` | E-postadresser (nedsänkta) hashas med algoritmen SHA256 | Både oformaterad text och SHA256-hash-adresser stöds av [!DNL Adobe Experience Platform]. När källfältet innehåller ohashade attribut bör du kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Experience Platform] automatiskt hash-kodar data vid aktiveringen. |
| `firstname` | Användarens förnamn | Både oformaterad text och SHA256-hashade förnamn stöds av [!DNL Adobe Experience Platform]. När källfältet innehåller ohashade attribut bör du kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Experience Platform] automatiskt hash-kodar data vid aktiveringen. |
| `lastname` | Användarens efternamn | Både oformaterad text och SHA256-hashade efternamn stöds av [!DNL Adobe Experience Platform]. När källfältet innehåller ohashade attribut bör du kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Experience Platform] automatiskt hash-kodar data vid aktiveringen. |
| `address` | Användarens gatuadress | Både oformaterad text och SHA256-hashgator stöds av [!DNL Adobe Experience Platform]. När källfältet innehåller ohashade attribut bör du kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Experience Platform] automatiskt hash-kodar data vid aktiveringen. |
| `city` | Användarens ort | Både oformaterad text och SHA256-hashstreck stöds av [!DNL Adobe Experience Platform]. När källfältet innehåller ohashade attribut bör du kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Experience Platform] automatiskt hash-kodar data vid aktiveringen. |
| `state` | Användarens land | Både oformaterad text och SHA256-hash-lägen stöds av [!DNL Adobe Experience Platform]. När källfältet innehåller ohashade attribut bör du kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Experience Platform] automatiskt hash-kodar data vid aktiveringen. |
| `zip` | Användarens postnummer | Både oformaterad text och SHA256-hash-komprimerade zips stöds av [!DNL Adobe Experience Platform]. När källfältet innehåller ohashade attribut bör du kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Experience Platform] automatiskt hash-kodar data vid aktiveringen. |
| `countryCode` | Användarens land (ISO-kod med två tecken) | Stöder normal textinmatning. |
| `experianId` | Identifierare tilldelad av [!DNL Experian] | Stöder normal textinmatning. |
| `kantarId` | Identifierare tilldelad av [!DNL Kantar] | Stöder normal textinmatning. |
| `liveRampId` | Identifierare tilldelad av [!DNL LiveRamp] | Stöder normal textinmatning. |
| `maId` | Identifierare tilldelad av ett mobilprogram | Stöder normal textinmatning. |
| `merkleId` | Identifierare tilldelad av [!DNL Merkle] | Stöder normal textinmatning. |
| `neustarId` | Identifierare tilldelad av [!DNL Neustar] | Stöder normal textinmatning. |
| `realId` | Identifierare tilldelad av identitetsdiagrammet för Real ID | Stöder normal textinmatning. |
| `sambaTvId` | Identifierare tilldelad av [!DNL Samba TV] | Stöder normal textinmatning. |

{style="table-layout:auto"}

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilka typer av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
|---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Publiker som genererats via [!DNL Experience Platform] [segmenteringstjänsten](/help/segmentation/home.md). |
| Alla andra målgrupper kommer | Ja | Den här kategorin omfattar alla målgrupper som kommer utanför målgrupper som genereras via [!DNL Segmentation Service]. Läs om de [olika målgruppernas ursprung](/help/segmentation/ui/audience-portal.md#customize). Några exempel är: <ul><li> anpassade uppladdningsgrupper [importerade](/help/segmentation/ui/audience-portal.md#import-audience) till [!DNL Experience Platform] från CSV-filer,</li><li> lookalike-målgrupper, </li><li> federerade målgrupper, </li><li> målgrupper som har genererats i andra [!DNL Experience Platform]-appar som [!DNL Adobe Journey Optimizer], </li><li> med mera. </li></ul> |

{style="table-layout:auto"}

Målgrupper som stöds av olika typer av målgruppsdata:

| Typ av målgruppsdata | Stöds | Beskrivning | Användningsfall |
|--------------------|-----------|-------------|-----------|
| [Målgrupper](/help/segmentation/types/people-audiences.md) | Ja | Baserat på kundprofiler kan ni inrikta er på specifika grupper av människor för marknadsföringskampanjer. | Ofta köpare, övergivna varukorgar |
| [Kontomålgrupper](/help/segmentation/types/account-audiences.md) | Nej | Rikta er till individer inom specifika organisationer för kontobaserade marknadsföringsstrategier. | B2B-marknadsföring |
| [Prospektera målgrupper](/help/segmentation/types/prospect-audiences.md) | Nej | Rikta er till individer som ännu inte är kunder men som delar egenskaper med er målgrupp. | Prospektera med data från tredje part |
| [Datauppsättningsexport](/help/catalog/datasets/overview.md) | Nej | Samlingar med strukturerade data lagrade i datasjön [!DNL Adobe Experience Platform]. | Arbetsflöden för rapportering, datavetenskap |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Tabellen nedan beskriver typ och frekvens för målexport.

| Objekt | Typ | Anteckningar |
| ---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en målgrupp med identifierare som stöds av [!DNL Amazon Ads]. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Målgruppsuppdateringar i [!DNL Experience Platform] skickas omedelbart till [!DNL Ads Data Manager]. |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
>
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](/help/destinations/ui/connect-destination.md). I arbetsflödet för målkonfiguration fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Fyll i de obligatoriska fälten och välj **[!UICONTROL Connect to destination]** om du vill autentisera mot målet.

* **[!UICONTROL Account name]**: Ange ett namn som hjälper dig att identifiera det här målkontot. Detta är särskilt användbart om du har flera anslutningar till samma mål.
* **[!UICONTROL Description]** (valfritt): Lägg till information som hjälper dig eller ditt team att skilja mellan konton, t.ex. syftet med anslutningen eller relevant affärskontext.

![Anslut till måldialogrutan i Experience Platform för Amazon Ads](../../assets/catalog/advertising/amazon-ads/amazon-ads-v2-connect-to-destination.png)

Du omdirigeras till gränssnittet [!DNL Amazon Ads v2]. Välj **[!UICONTROL Allow]** om du vill logga in på ditt Amazon-konto.

![Amazon Ads OAuth-auktoriseringsfråga som uppmanar användaren att tillåta](../../assets/catalog/advertising/amazon-ads/amazon-ads-v2-allow.png)

Efter autentiseringen omdirigeras du tillbaka till [!DNL Adobe Experience Platform] med din nya anslutning.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

![Amazon Ads v2-målkonfigurationsfält i Experience Platform](../../assets/catalog/advertising/amazon-ads/amazon-ads-v2-configure-destination.png)

* **[!UICONTROL Name]**: Ett namn som identifierar det här målet.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet.
* **[!UICONTROL Manager Account]**: Målhanterarens konto-ID från listrutan.
* **[!UICONTROL All audience members sent to Amazon are consented for use for Advertising]**: Ange samtycke för dataanvändning (`GRANTED` eller `DENIED`).
* **[!UICONTROL Ads data manager Terms & Conditions]**: Acceptera villkoren för [!DNL Amazon Ads] Data Manager. Läs avsnittet [Acceptera villkor](#accept-terms) för mer information.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](/help/destinations/ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
>
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera identiteter måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera profiler och målgrupper för att direktuppspela målgruppsexportdestinationer](/help/destinations/ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

### Obligatoriska mappningar {#map}

Målet [!DNL Amazon Ads v2] kräver att du konfigurerar följande mappningar för att dataaktiveringen ska lyckas.

| Source | Målfält | Beskrivning |
|---------|----------|---------|
| `IdentityMap: Email_LC_SHA256` eller `IdentityMap: Email` | `Identity: email` | När källfältet innehåller ohashade attribut bör du kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Experience Platform] automatiskt hash-kodar data vid aktiveringen. |
| `xdm: homeAddress.countryCode` | `Identity: countryCode` | Användarens land (ISO-kod med två tecken) |

![Konfiguration för mappning av identitetsfält för Amazon Ads v2-målet](../../assets/catalog/advertising/amazon-ads/amazon-ads-v2-mapping.png)

### Bästa praxis för mappning {#mapping-best-practices}

Kombinera identifierare från första part (till exempel telefonnummer och adress) med identifierare som tillhandahålls av partner. Detta gör att [!DNL Amazon Ads] kan använda flera identitetssignaler under målgruppsmatchning, vilket leder till bättre matchningsfrekvenser.

Använd identifierare som tillhandahålls av partner endast när de är ifyllda i dina källdata. Om ett mappat partner-ID-fält är tomt eller inte finns för en viss profil ignoreras det under målgruppsmatchning och bidrar inte till matchningsfrekvenser.

### Exempel {#examples}

* Använd `kantarId` när du aktiverar målgrupper som har byggts eller ökats med [!DNL Kantar] identitetsdata.
* Använd `merkleId` när målgruppsdata kommer från [!DNL Merkle]-hanterade identitetslösningar.
* Använd `neustarId` när dina data är länkade via identitetsupplösning för [!DNL Neustar].
* Använd `experianId` för målgrupper som har ökats med [!DNL Experian] identitetsdata.
* Använd `liveRampId` när du aktiverar målgrupper som är beroende av [!DNL LiveRamp]-identitetsupplösning.
* Använd `sambaTvId` när du arbetar med målgruppsdata som tillhandahålls av [!DNL Samba TV].

Dessa identifierare tillhandahålls vanligtvis av respektive partner som vanliga textidentifierare och kräver ingen hash.

## Validera dataexport {#exported-data}

Verifiera målgruppsintaget i **[!DNL Ads Data Manager]-konsolen** efter aktiveringen.

Navigera till **[!UICONTROL Audiences]** → **[!UICONTROL Uploaded Sources]**. Kontrollera målgruppens användningsstatus, storlek och eventuella felloggar. Sidorna [Hantera data](https://advertising.amazon.com/API/docs/en-us/adm/6_adm-manage-data) och [Destinationer](https://advertising.amazon.com/API/docs/en-us/adm/7_adm-destinations) i [!DNL Amazon Ads]-dokumentationen innehåller ytterligare riktlinjer för validering.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Översikt över datastyrning](/help/data-governance/home.md).

## Ytterligare resurser {#additional-resources}

Mer information om [!DNL Amazon Ads Data Manager] finns i följande resurs:

* [Amazon Ads Data Manager - översikt](https://advertising.amazon.com/API/docs/en-us/adm/1_ads-data-manager-console-overview)
