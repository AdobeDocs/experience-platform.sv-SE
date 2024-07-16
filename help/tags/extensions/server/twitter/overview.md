---
keywords: tillägg för händelsevidarebefordring;twitter;tillägg för vidarebefordran av twitter-händelse
title: Vidarekoppling av twitter-händelse
description: Med det här tillägget för vidarebefordran av Adobe Experience Platform-händelser kan du infoga händelser i Twitter efter dina affärsbehov.
last-substantial-update: 2023-05-24T00:00:00Z
exl-id: 54c240e5-6160-4654-ac5b-6afa8d99a765
source-git-commit: 4ee895cb8371646fd2013e2a8f65c2ffdae95850
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 0%

---

# [!DNL Twitter]-tillägg för händelsevidarebefordring

[[!DNL Twitter]](https://twitter.com/i/flow/login) är en onlinetjänst för sociala medier och sociala nätverk där användarna kan publicera och interagera med 280-teckenlånga meddelanden som kallas tweets. Användare kan interagera med Twitter via en webbläsare, mobil klientprogramvara eller programmatiskt via sina [API:er](https://developer.twitter.com/en/docs/twitter-api)

Med [!DNL Twitter] API:t [ för webbkonverteringar ](../../../ui/event-forwarding/overview.md) kan du utnyttja data som samlats in i Adobe Experience Platform Edge Network och skicka dem till [!DNL Twitter]. Det här dokumentet beskriver tilläggets användningsfall, hur det installeras och hur du integrerar dess funktioner i [regler](../../../ui/managing-resources/rules.md) för vidarebefordran av händelser.

[!DNL Twitter] kräver [OAuth 1.0](https://developer.twitter.com/en/docs/authentication/oauth-1-0a) för autentisering med API:t [!DNL Twitter] [!DNL Web Conversions].

## Användningsfall

Det här tillägget bör användas om du vill använda data från Edge Network i [!DNL Twitter] för att utnyttja dess funktioner för kundanalys och målinriktning.

Ta till exempel ett marknadsföringsteam i en organisation. Teamet samlar in händelsedata om användarinteraktion från sin webbplats som händelsedata från sin webbplats och läser in dem till [!DNL Twitter] med det här tillägget för händelsevidarebefordran.

Marknads- och analysteam kan sedan utnyttja [!DNL Twitter's]-funktioner för att utföra ytterligare analyser och inrikta sig på dessa användare för riktade annonskampanjer.

Mer information om användningsfall som är specifika för [!DNL Twitter] finns i dokumentationen för [[!DNL Twitter] användningsfall](https://developer.twitter.com/en/use-cases/build-for-businesses).

## [!DNL Twitter] krav och skyddsräcken {#prerequisites}

Du måste ha ett giltigt [!DNL Twitter]-konto för att kunna använda det här tillägget. Gå till registreringssidan [[!DNL Twitter] för att registrera dig och skapa ett konto om du inte redan har ett.](https://help.twitter.com/en/using-twitter/create-twitter-account)

Du måste konfigurera ditt konto som ett [!DNL Twitter]-utvecklarkonto. Information om hur du registrerar dig som utvecklare finns i [[!DNL Twitter] utvecklarkontot](https://developer.twitter.com/en/support/twitter-api/developer-account1).

### API-skyddsräcken {#guardrails}

Webbkonverterings-API:t [!DNL Twitter] har en hastighetsgräns på 60 000 begäranden per 15 minuters intervall, där varje begäran tillåter 500 händelser.

### Samla nödvändig konfigurationsinformation {#configuration-details}

Följande indata krävs för att ansluta Experience Platform till [!DNL Twitter]:

| Nyckeltyp | Beskrivning |
| --- | --- |
| Konsumentnyckel | &#x200B; Programmets API-nyckel för åtkomst till API:t [!DNL Twitter]. Mer information finns i [!DNL Twitter]-dokumentationen om [api-nycklar och hemligheter](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret). | |
| Konsumenthemlighet | API-hemligheten ger din app åtkomst till API:t [!DNL Twitter]. Mer information finns i [!DNL Twitter]-dokumentationen om [api-nycklar och hemligheter](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret). |
| Tokenhemlighet | Den token-hemlighet som inte förfaller för din app, som används för autentisering till [!DNL Twitter] API via OAuth. Mer information finns i [!DNL Twitter]-dokumentationen om att [hämta åtkomsttoken för användning](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens). |
| Åtkomsttoken | Åtkomsttoken som inte förfaller för din app, som används för autentisering till API:t [!DNL Twitter] via OAuth. Mer information finns i [!DNL Twitter]-dokumentationen om att [hämta åtkomsttoken för användning](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens). |
| Pixel-ID | Pixeln [!DNL Twitter] är en webbplatstagg som implementeras på din webbplats för att spåra webbplatsåtgärder eller konverteringar. Mer information finns i [!DNL Twitter]-dokumentationen om [konverteringsspårning för webbplatser](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html). |

## Installera och konfigurera tillägget [!DNL Twitter] {#install}

Om du vill installera tillägget [skapar du en egenskap för vidarebefordring av händelser](../../../ui/event-forwarding/overview.md#properties) eller väljer en befintlig egenskap att redigera i stället.

Välj **[!UICONTROL Extensions]** i den vänstra navigeringen. På fliken **[!UICONTROL Catalog]** väljer du **[!UICONTROL Install]** på kortet för tillägget [!DNL Twitter].

![Katalog som visar installationen av tillägget [!DNL Twitter].](../../../images/extensions/server/twitter/install.png)

>[!IMPORTANT]
>
>Beroende på implementeringsbehoven kan du behöva skapa ett schema, dataelement och en datauppsättning innan du konfigurerar tillägget. Granska alla konfigurationssteg innan du startar för att avgöra vilka enheter du måste konfigurera för ditt användningsfall.

På nästa skärm anger du följande [konfigurationsvärden](#configuration-details) som du tidigare har hämtat från [!DNL Twitter]:

* **[!UICONTROL Pixel Id]**
* **[!UICONTROL Consumer Key]**
* **[!UICONTROL Consumer Secret]**
* **[!UICONTROL Token]**
* **[!UICONTROL Token Secret]**

När du är klar väljer du **[!UICONTROL Save]**.

![[!DNL Twitter] konfigurationsskärm för tillägget [!DNL Twitter].](../../../images/extensions/server/twitter/configure.png)

## Konfigurera en regel för vidarebefordran av händelser {#config-rule}

När alla dataelement har konfigurerats kan du börja skapa regler för vidarebefordran av händelser som avgör när och hur händelser skickas till [!DNL Twitter].

Skapa en ny [regel](../../../ui/managing-resources/rules.md) i egenskapen för vidarebefordran av händelser. Under **[!UICONTROL Actions]** lägger du till en ny åtgärd och anger tillägget till **[!UICONTROL Twitter]**. Om du vill skicka Edge Network-händelser till [!DNL Twitter] anger du **[!UICONTROL Action Type]** till **[!UICONTROL Send Web Conversion].**

Efter markeringen visas ytterligare kontroller för att ytterligare konfigurera händelsen. Du måste mappa händelseegenskaperna [!DNL Twitter] till dataelementen som du tidigare har skapat. Mer information finns i [[!DNL Twitter] API:t för webbkonvertering](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions).

![[!DNL Twitter] skapar en konverteringshändelseregel.](../../../images/extensions/server/twitter/action-configuration.png)

**[!UICONTROL User Identification]**

| Fältnamn | Beskrivning | Exempel | Obligatoriskt |
| --- | --- | --- | --- |
| [!UICONTROL [!DNL Twitter] Click ID] | [!DNL Twitter] Klicka på ID som tolkat från klicknings-URL:en. | 26l6412g5p4iyj65a2oic2ayg2 | Krävs om ingen annan identifierare läggs till. |
| [!UICONTROL Email] | En e-postadress hashas med SHA256. Texten måste skrivas med gemener och alla efterföljande eller inledande blanksteg måste tas bort innan hash-kodning. | eventforwarding@example.com | Krävs om ingen annan identifierare läggs till. |
| [!UICONTROL Phone] | Telefonen fungerar som en identifierare som matchar konverteringshändelsen. Telefonnumret måste vara i E164-format [+][landskod][riktnummer][local phone number] innan hashning utförs. | +911234567875 | Krävs om ingen annan identifierare läggs till. |

**[!UICONTROL Conversion Data]**

| Fältnamn | Beskrivning | Exempel | Obligatoriskt |
| --- | --- | --- | --- |
| [!UICONTROL Conversion Time] | Datum-tid som sträng i ISO 8601 eller i formatet `yyyy-MM-dd'T'HH:mm:ss:SSSZ`. | 2022-02-18T01:14:00.603Z | Ja |
| [!UICONTROL Event Id] | ID:t för bas-36 för en specifik händelse. Detta ID ska matcha en förkonfigurerad händelse i ditt [!DNL Twitter]-annonskonto. Detta kallas ID för motsvarande händelse i Händelsehanteraren. | o87ne eller tw-o8z6j-o87ne (tw-pixel_id-event-id) | Ja |
| [!UICONTROL Number of Items] | Antalet artiklar som köpts i händelsen. Detta måste vara ett positivt tal större än 0. | 4 | Nej |
| [!UICONTROL Currency] | Valutan för de artiklar som köps in i händelsen. Detta uttrycks i ISO-4217 och om det inte anges kommer standardvärdet att vara USD. | USD | Nej |
| [!UICONTROL Value] | Prisvärdet för artiklar som köpts i händelsen. | 100,00 | Nej |
| [!UICONTROL Conversion ID] | En identifierare för en konverteringshändelse som kan användas för borttagning av dubbletter mellan API-konverteringar för webb-pixlar och konvertering i samma händelsetagg. | 23294827 | Nej |
| [!UICONTROL Description] | En beskrivning med eventuell ytterligare information om konverteringarna. | Testkonvertering | Nej |

## Validera data i [!DNL Twitter]

När regeln för vidarebefordran av händelser har skapats och körts kontrollerar du om händelsen som skickades till [!DNL Twitter]-API:t visas som förväntat i [!DNL Twitter]-gränssnittet.

Om händelsesamlingen och integreringen av [!DNL Experience Platform] lyckades, kommer du att se händelser i [!DNL Twitter] [!UICONTROL Events manager].

![Händelsehanteraren [!DNL Twitter]](../../../images/extensions/server/twitter/event-manager.png)

## Nästa steg

I den här guiden beskrivs hur du skickar konverteringshändelser till [!DNL Twitter] med hjälp av händelsevidarebefordran. Mer information om dessa underliggande tekniker finns i den officiella dokumentationen:

* [[!DNL Twitter] API:er](https://developer.twitter.com/en/docs/twitter-api)
* [[!DNL Twitter] Webbkonverterings-API](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions)
* [[!DNL Twitter] Användaråtkomsttoken](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens)
* [Pixel-ID och konverteringsspårning](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html)
