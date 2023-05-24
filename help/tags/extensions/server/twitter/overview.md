---
keywords: tillägg för händelsevidarebefordran;twitter;twitter tillägg för händelsevidarebefordran
title: Twitter-tillägg för händelsevidarebefordran
description: Med det här tillägget för vidarebefordran av Adobe Experience Platform-händelser kan du importera händelser till Twitter för dina verksamhetsbehov.
last-substantial-update: 2023-05-24T00:00:00Z
source-git-commit: c5cc36d9530ff6fbb52a1995844f495b38e938b3
workflow-type: tm+mt
source-wordcount: '1098'
ht-degree: 2%

---

# [!DNL Twitter] tillägg för händelsevidarebefordran

[[!DNL Twitter]](https://www.twitter.com) är en onlinetjänst för sociala medier och sociala nätverk, där användarna publicerar och interagerar med 280-teckenlånga meddelanden som kallas tweets. Användare kan interagera med Twitter via en webbläsare, mobil klientprogramvara eller via programmering via [API:er](https://developer.twitter.com/en/docs/twitter-api)

The [!DNL Twitter] API för webbkonverteringar [händelsevidarebefordran](../../../ui/event-forwarding/overview.md) kan du utnyttja data som samlats in i Adobe Experience Platform Edge Network och skicka dem till [!DNL Twitter]. Det här dokumentet beskriver tilläggets användningsfall, hur det installeras och hur du integrerar dess funktioner i din händelsevidarebefordran [regler](../../../ui/managing-resources/rules.md).

[!DNL Twitter] kräver [OAuth 1.0](https://developer.twitter.com/en/docs/authentication/oauth-1-0a) för autentisering med [!DNL Twitter] [!DNL Web Conversions] API.

## Användningsfall

Det här tillägget bör användas om du vill använda data från Edge Network i [!DNL Twitter] för att utnyttja sina funktioner för kundanalys och målgruppsanpassning.

Ta till exempel ett marknadsföringsteam i en organisation. Teamet samlar in data om användarinteraktionshändelser från sin webbplats som händelsedata från sin webbplats och läser in dem i [!DNL Twitter] med det här tillägget för händelsevidarebefordran.

Marknadsförings- och analysteam kan sedan utnyttja [!DNL Twitter's] funktioner för att utföra ytterligare analyser och inrikta sig på dessa användare för riktade annonskampanjer.

Mer information om användningsfall för [!DNL Twitter], se [[!DNL Twitter] användningsfall](https://developer.twitter.com/en/use-cases/build-for-businesses) dokumentation.

## [!DNL Twitter] krav och skyddsräcken {#prerequisites}

Du måste ha en giltig [!DNL Twitter] för att kunna använda tillägget. Gå till [[!DNL Twitter] registreringssida](https://help.twitter.com/en/using-twitter/create-twitter-account) för att registrera och skapa ett konto om du inte redan har ett.

Du måste konfigurera ditt konto som [!DNL Twitter] utvecklarkonto. Information om hur du registrerar dig som utvecklare finns i [[!DNL Twitter] utvecklarkonto](https://developer.twitter.com/en/support/twitter-api/developer-account).

### API-skyddsutkast {#guardrails}

The [!DNL Twitter] Webbkonverterings-API:t har en hastighetsgräns på 60 000 begäranden per 15 minuters intervall, där varje begäran tillåter 500 händelser.

### Samla nödvändig konfigurationsinformation {#configuration-details}

För att ansluta Experience Platform till [!DNL Twitter]krävs följande indata:

| Nyckeltyp | Beskrivning |
| --- | --- |
| Konsumentnyckel | &#x200B; Programmets API-nyckel för åtkomst till [!DNL Twitter] API. Se [!DNL Twitter] dokumentation om [api-nycklar och hemligheter](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret) för vägledning. |  |
| Konsumenthemlighet | API-hemligheten ger din app åtkomst till [!DNL Twitter] API. Se [!DNL Twitter] dokumentation om [api-nycklar och hemligheter](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret) för vägledning. |
| Tokenhemlighet | Den tokenhemlighet som inte förfaller för din app, som används för autentisering till [!DNL Twitter] API via OAuth. Se [!DNL Twitter] dokumentation om [hämta åtkomsttoken](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens) för vägledning. |
| Åtkomsttoken | Åtkomsttoken för din app som inte förfaller, som används för autentisering till [!DNL Twitter] API via OAuth. Se [!DNL Twitter] dokumentation om [hämta åtkomsttoken](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens) för vägledning. |
| Pixel-ID | The [!DNL Twitter] Pixel är en webbplatstagg som implementeras på din webbplats för att spåra webbplatsåtgärder eller konverteringar. Se [!DNL Twitter] dokumentation om [konverteringsspårning för webbplatser](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html) för vägledning. |

## Installera och konfigurera [!DNL Twitter] extension {#install}

Installera tillägget genom att [skapa en egenskap för vidarebefordring av händelser](../../../ui/event-forwarding/overview.md#properties) eller välj en befintlig egenskap att redigera i stället.

Välj **[!UICONTROL Extensions]** i den vänstra navigeringen. I **[!UICONTROL Catalog]** flik, välja **[!UICONTROL Install]** på kortet för [!DNL Twitter] tillägg.

![Katalog med [!DNL Twitter] tillägg som markerar installationen.](../../../images/extensions/server/twitter/install.png)

>[!IMPORTANT]
>
>Beroende på implementeringsbehoven kan du behöva skapa ett schema, dataelement och en datauppsättning innan du konfigurerar tillägget. Granska alla konfigurationssteg innan du startar för att avgöra vilka enheter du måste konfigurera för ditt användningsfall.

På nästa skärm anger du följande [konfigurationsvärden](#configuration-details) som du tidigare har samlat in från [!DNL Twitter]:

* **[!UICONTROL Pixel Id]**
* **[!UICONTROL Consumer Key]**
* **[!UICONTROL Consumer Secret]**
* **[!UICONTROL Token]**
* **[!UICONTROL Token Secret]**

När du är klar väljer du **[!UICONTROL Save]**.

![[!DNL Twitter] konfigurationsskärmen för [!DNL Twitter] tillägg.](../../../images/extensions/server/twitter/configure.png)

## Konfigurera en regel för vidarebefordran av händelser {#config-rule}

När alla dataelement har konfigurerats kan du börja skapa regler för vidarebefordran av händelser som bestämmer när och hur händelserna ska skickas till [!DNL Twitter].

Skapa ett nytt [regel](../../../ui/managing-resources/rules.md) i egenskapen för vidarebefordran av händelser. Under **[!UICONTROL Actions]**, lägga till en ny åtgärd och ange tillägget till **[!UICONTROL Twitter]**. Skicka Adobe Experience Edge Network-händelser till [!DNL Twitter], ange **[!UICONTROL Action Type]** till **[!UICONTROL Send Web Conversion].**

Efter markeringen visas ytterligare kontroller för att ytterligare konfigurera händelsen. Du måste mappa [!DNL Twitter] händelseegenskaper för de dataelement som du skapade tidigare. Mer information finns i [[!DNL Twitter] API för webbkonverteringar](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions).

![The [!DNL Twitter] skapa en konverteringshändelseregel.](../../../images/extensions/server/twitter/action-configuration.png)

**[!UICONTROL User Identification]**

| Fältnamn | Beskrivning | Exempel | Obligatoriskt |
| --- | --- | --- | --- |
| [!UICONTROL [!DNL Twitter] Click ID] | [!DNL Twitter] Klicka på ID så som det tolkas från klicknings-URL:en. | 26l6412g5p4iyj65a2oic2ayg2 | Krävs om ingen annan identifierare läggs till. |
| [!UICONTROL Email] | En e-postadress hashas med SHA256. Texten måste skrivas med gemener och alla efterföljande eller inledande blanksteg måste tas bort innan hash-kodning. | eventforwarding@example.com | Krävs om ingen annan identifierare läggs till. |
| [!UICONTROL Phone] | Telefonen fungerar som en identifierare som matchar konverteringshändelsen. Telefonnumret måste vara i E164-format [+][landskod][riktnummer][local phone number] före hashning. | +911234567875 | Krävs om ingen annan identifierare läggs till. |

**[!UICONTROL Conversion Data]**

| Fältnamn | Beskrivning | Exempel | Obligatoriskt |
| --- | --- | --- | --- |
| [!UICONTROL Conversion Time] | Datum-tid som sträng i ISO 8601 eller i åååå-MM-dd&#39;T&#39;HH:mm:ss:SSSZ-format. | 2022-02-18T01:14:00,603Z | Ja |
| [!UICONTROL Event Id] | ID:t för bas-36 för en specifik händelse. Detta ID bör matcha en förkonfigurerad händelse i din [!DNL Twitter] annonskonto. Detta kallas ID för motsvarande händelse i Händelsehanteraren. | o87ne eller tw-o8z6j-o87ne (tw-pixel_id-event-id) | Ja |
| [!UICONTROL Number of Items] | Antalet artiklar som köpts i händelsen. Detta måste vara ett positivt tal som är större än 0. | 4 | Nej |
| [!UICONTROL Currency] | Valutan för de artiklar som köps in i händelsen. Detta uttrycks i ISO-4217 och om det inte anges kommer standardvärdet att vara USD. | USD | Nej |
| [!UICONTROL Value] | Prisvärdet för artiklar som köpts i händelsen. | 100.00 | Nej |
| [!UICONTROL Conversion ID] | En identifierare för en konverteringshändelse som kan användas för borttagning av dubbletter mellan API-konverteringar för webb-pixlar och konvertering i samma händelsetagg. | 23294827 | Nej |
| [!UICONTROL Description] | En beskrivning med eventuell ytterligare information om konverteringarna. | Testkonvertering | Nej |

## Validera data i [!DNL Twitter]

När regeln för vidarebefordran av händelser har skapats och körts validerar du om händelsen som skickades till [!DNL Twitter] API visas som förväntat i [!DNL Twitter] Gränssnitt.

Om händelsesamlingen och [!DNL Experience Platform] integreringen lyckades, du kommer att se händelser i [!DNL Twitter] [!UICONTROL Events manager].

![The [!DNL Twitter] händelsehanterare](../../../images/extensions/server/twitter/event-manager.png)

## Nästa steg

I den här guiden beskrivs hur du skickar konverteringshändelser till [!DNL Twitter] med händelsevidarebefordran. Mer information om dessa underliggande tekniker finns i den officiella dokumentationen:

* [[!DNL Twitter] API:er](https://developer.twitter.com/en/docs/twitter-api)
* [[!DNL Twitter] Webbkonverterings-API](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions)
* [[!DNL Twitter] Åtkomsttoken för användare](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens)
* [Pixel-ID och konverteringsspårning](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html)
