---
keywords: Google-annonser;Google-annonser;Google-adwords;Google AdWords;Google Adwords
title: Google Ads-anslutning
description: Google Ads, som tidigare kallades Google AdWords, är en onlinereklam som gör det möjligt för företag att betala per klick för annonsering i textbaserade sökningar, bildskärmar, YouTube-videor och mobilskärmar i appen.
exl-id: 7143f476-49a8-42aa-bfb4-b11fc2b8f5c3
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 1%

---

# [!DNL Google Ads] anslutning

## Översikt {#overview}

[!DNL Google Ads], tidigare känt som [!DNL Google AdWords], är en onlinereklam som gör att företag kan betala annonser per klick för textbaserade sökningar, grafiska displayer, [!DNL YouTube] videor och mobilskärmar i appen.

## Destinationsspecifikationer {#specifics}

Observera följande information som är specifik för [!DNL Google Ads] mål:

* Aktiverade målgrupper skapas programmatiskt i [!DNL Google] plattform.
* [!DNL Platform] innehåller för närvarande inga mätvärden som validerar den lyckade aktiveringen. Se antalet målgrupper i Google för att validera integrationen och förstå målgruppens målgruppsstorlek.

>[!IMPORTANT]
>
>Om du vill skapa ditt första mål med [!DNL Google Ads] och har inte aktiverat [Synkroniseringsfunktion för ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) tidigare i Experience Cloud ID-tjänsten (med Audience Manager eller andra program), kontakta Adobe Consulting eller kundtjänst för att aktivera ID-synkronisering. Om du tidigare har konfigurerat Google-integreringar i Audience Manager, överförs de ID-synkroniseringar du har konfigurerat till Platform.

## Identiteter som stöds {#supported-identities}

[!DNL Google Ad Manager] stöder aktivering av identiteter som beskrivs i tabellen nedan.

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Välj den här målidentiteten när din källidentitet är ett GAID-namnområde. |
| IDFA | [!DNL Apple ID for Advertisers] | Välj den här målidentiteten när din källidentitet är ett IDFA-namnutrymme. |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), även känt som [!DNL Device ID]. Ett numeriskt 38-siffrigt enhets-ID som Audience Manager associerar med varje enhet som det interagerar med. | Google använder [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) för användare i Kalifornien och Google Cookie ID för alla andra användare. |
| [!DNL Google] cookie-ID | [!DNL Google] cookie-ID | [!DNL Google] använder detta ID för att rikta sig till användare utanför Kalifornien. |
| RIDA | Roku-ID för annonsering. Detta ID identifierar Roku-enheter unikt. |  |
| MAID | Microsoft Advertising ID. Detta ID identifierar unikt enheter som kör Windows 10. |  |
| Amazon Fire TV-ID | Detta ID identifierar Amazon Fire TV-program unikt. |  |

{style=&quot;table-layout:auto&quot;}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Segment export]** | Du exporterar alla medlemmar i ett segment (publik) till Google-målet. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på segmentutvärdering skickar kopplingen uppdateringen nedåt till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Förutsättningar {#prerequisites}

### Befintlig [!DNL Google Ads] konto

>[!IMPORTANT]
>
> [!DNL Google] har ersatt nytt [!DNL Google Ads] cookie-integreringar med tredjepartsleverantörer. För att kunna utföra tillåtelselista-stegen i nästa avsnitt måste du ha en befintlig integrering med [!DNL Google Ads]. Detta resulterar i den rekommenderade metoden för att använda [!DNL Google Ads] konfigurerar en [!DNL Google Customer Match] integrering. Mer information om hur du skapar en [!DNL Google Customer Match] integrering, läs självstudiekursen om hur du skapar en [[!DNL Google Customer Match]](./google-customer-match.md) anslutning.

### Tillåt listning {#allow-listing}

>[!NOTE]
>
>Tillåtelselista är obligatoriskt innan du konfigurerar din första [!DNL Google Ads] mål i Platform. Se till att tillåtelselista-processen som beskrivs nedan har slutförts av [!DNL Google] innan du skapar ett mål.

Innan du skapar [!DNL Google Ads] mål i plattform måste du kontakta [!DNL Google] för att Adobe ska föras upp på listan över tillåtna dataleverantörer och för att ditt konto ska läggas till tillåtelselista. Kontakt [!DNL Google] och lämna följande information:

* **Konto-ID**: Adobe konto-ID hos Google. Konto-ID: 87933855.
* **Kund-ID**: Adobe kundkonto-ID hos Google. Kund-ID: 89690775.
* Kontotyp: **AdWords**
* **Google AdWords ID**: Detta är ditt ID med [!DNL Google]. ID-formatet är vanligtvis 123-456-7890.

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

while [konfigurera](../../ui/connect-destination.md) Om du vill ange destinationen måste du ange följande information:

* **[!UICONTROL Name]**: Fyll i det önskade namnet för det här målet.
* **[!UICONTROL Description]**: Valfritt. Du kan till exempel ange vilken kampanj du använder det här målet för.
* **[!UICONTROL Account Type]**: AdWords är det enda tillgängliga alternativet.
* **[!UICONTROL Account ID]**: Fyll i ditt konto-ID med [!DNL Google Ads]. ID-formatet är vanligtvis 123-456-7890.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om status för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med hjälp av användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
> 
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Se [Aktivera målgruppsdata för att direktuppspela segmentexportmål](../../ui/activate-segment-streaming-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

## Exporterade data

Verifiera om data har exporterats till [!DNL Google Ads] mål, kontrollera [!DNL Google Ads] konto. Om aktiveringen lyckades fylls målgrupperna i ditt konto.

## Felsökning {#troubleshooting}

### 400 Felmeddelande för felaktig begäran {#bad-request}

När du konfigurerar det här målet kan du få följande fel:

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Det här felet inträffar antingen när kundkonton inte uppfyller [krav](#prerequisites) eller när kunderna försöker konfigurera målet utan något befintligt [!DNL Google Ads] konto.

[!DNL Google] har ersatt nytt [!DNL Google Ads] cookie-integreringar med tredjepartsleverantörer. Utför [allow-list](#allow-listing) måste du ha en befintlig integrering med [!DNL Google Ads].

Rekommenderad metod för att använda [!DNL Google Ads] konfigurerar en [[!DNL Google Customer Match]](google-customer-match.md) integrering.
