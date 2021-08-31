---
keywords: Google ads;Google ads;Google Adwords;Google AdWords;Google Adwords
title: Google Ads-anslutning
description: Google Ads, tidigare Google AdWords, är en webbannonseringstjänst som gör att företag kan betala per klick för annonsering i textbaserade sökningar, bildskärmar, YouTube-videor och mobilskärmar i appar.
exl-id: 7143f476-49a8-42aa-bfb4-b11fc2b8f5c3
source-git-commit: f04ea9aed586c8582286de82bfeee3f6f04cc360
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 1%

---

# [!DNL Google Ads] anslutning

## Översikt {#overview}

[!DNL Google Ads], som tidigare kallades  [!DNL Google AdWords], är en onlinereklam som gör det möjligt för företag att betala per klick för annonsering över textbaserade sökningar, grafiska skärmar,  [!DNL YouTube] videor och mobilskärmar i appen.

## Destinationsspecifikationer {#specifics}

Observera följande information som är specifik för [!DNL Google Ads]-mål:

* Aktiverade målgrupper skapas programmatiskt i [!DNL Google]-plattformen.
* [!DNL Platform] innehåller för närvarande inga mätvärden som validerar den lyckade aktiveringen. Se antalet målgrupper i Google för att validera integrationen och förstå målgruppens målgruppsstorlek.

>[!IMPORTANT]
>
>Om du vill skapa ditt första mål med [!DNL Google Ads] och inte har aktiverat funktionen [ID-synkronisering](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) i Experience Cloud ID-tjänsten tidigare (med Audience Manager eller andra program) ber vi dig kontakta Adobe Consulting eller kundtjänst för att aktivera ID-synkronisering. Om du tidigare har konfigurerat Google-integreringar i Audience Manager överförs de ID-synkroniseringar du har konfigurerat till Platform.

## Identiteter som stöds {#supported-identities}

[!DNL Google Ad Manager] stöder aktivering av identiteter som beskrivs i tabellen nedan.

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Välj den här målidentiteten när din källidentitet är ett GAID-namnområde. |
| IDFA | [!DNL Apple ID for Advertisers] | Välj den här målidentiteten när din källidentitet är ett IDFA-namnutrymme. |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), även kallat  [!DNL Device ID]. Ett numeriskt 38-siffrigt enhets-ID som Audience Manager associerar med varje enhet som det interagerar med. | Google använder [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) för målanvändare i Kalifornien och Google Cookie ID för alla andra användare. |
| [!DNL Google] cookie-ID | [!DNL Google] cookie-ID | [!DNL Google] använder detta ID för att rikta sig till användare utanför Kalifornien. |
| RIDA | Roku-ID för annonsering. Detta ID identifierar Roku-enheter unikt. |  |
| MAID | Microsoft Advertising ID. Detta ID identifierar unikt enheter som kör Windows 10. |  |
| Amazon Fire TV-ID | Detta ID identifierar Amazon Fire TV-program unikt. |  |

## Exporttyp {#export-type}

**Segmentexport**  - du exporterar alla medlemmar i ett segment (publik) till Google-målet.

## Förutsättningar {#prerequisites}

### Befintligt [!DNL Google Ads]-konto

>[!IMPORTANT]
>
> [!DNL Google] har ersatt nya  [!DNL Google Ads] cookie-integreringar med tredjepartsleverantörer. För att kunna utföra tillåtelselista-stegen i nästa avsnitt måste du ha en befintlig integrering med [!DNL Google Ads]. Därför rekommenderar vi att du använder [!DNL Google Ads] för att konfigurera en [!DNL Google Customer Match]-integrering. Mer information om hur du skapar en [!DNL Google Customer Match]-integration finns i självstudiekursen om hur du skapar en [[!DNL Google Customer Match]](./google-customer-match.md)-anslutning.

### Tillåt listning {#allow-listing}

>[!NOTE]
>
>Tillåtelselista är obligatoriskt innan du konfigurerar ditt första [!DNL Google Ads]-mål i Platform. Kontrollera att tillåtelselista-processen som beskrivs nedan har slutförts av [!DNL Google] innan du skapar ett mål.

Innan du skapar [!DNL Google Ads]-målet i Platform måste du kontakta [!DNL Google] för att Adobe ska tas med i listan över tillåtna dataleverantörer och för att ditt konto ska läggas till i tillåtelselista. Kontakta [!DNL Google] och lämna följande information:

* **Konto-ID**: Adobe konto-ID med Google. Konto-ID: 87933855.
* **Kund-ID**: Adobe kundkonto-ID med Google. Kund-ID: 89690775.
* Kontotyp: **AdWords**
* **Google AdWords-ID**: Detta är ditt ID med  [!DNL Google]. ID-formatet är vanligtvis 123-456-7890.

## Anslut till målet {#connect}

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för målkonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

När du [konfigurerar](../../ui/connect-destination.md) det här målet måste du ange följande information:

* **[!UICONTROL Name]**: Fyll i det önskade namnet för det här målet.
* **[!UICONTROL Description]**: Valfritt. Du kan till exempel ange vilken kampanj du använder det här målet för.
* **[!UICONTROL Account Type]**: AdWords är det enda tillgängliga alternativet.
* **[!UICONTROL Account ID]**: Fyll i ditt konto-ID med  [!DNL Google Ads]. ID-formatet är vanligtvis 123-456-7890.

## Aktivera segment till den här destinationen {#activate}

Se [Aktivera målgruppsdata för att direktuppspela segmentets exportmål](../../ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgruppssegment till den här destinationen.

## Exporterade data

Kontrollera ditt [!DNL Google Ads]-konto för att kontrollera om data har exporterats till [!DNL Google Ads]-målet. Om aktiveringen lyckades fylls målgrupperna i ditt konto.

## Felsökning {#troubleshooting}

### 400 Felmeddelande för felaktig begäran {#bad-request}

När du konfigurerar det här målet kan du få följande fel:

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Det här felet inträffar antingen när kundkonton inte uppfyller [villkoren](#prerequisites) eller när kunder försöker konfigurera målet utan ett befintligt [!DNL Google Ads]-konto.

[!DNL Google] har ersatt nya  [!DNL Google Ads] cookie-integreringar med tredjepartsleverantörer. Om du vill utföra [allow-list](#allow-listing)-stegen måste du ha en befintlig integrering med [!DNL Google Ads].

Det rekommenderade sättet att använda [!DNL Google Ads] är att konfigurera en [[!DNL Google Customer Match]](google-customer-match.md)-integrering.
