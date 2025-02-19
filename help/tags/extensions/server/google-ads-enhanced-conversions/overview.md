---
title: Google Ads Enhanced Conversions Extension
description: Läs mer om tillägget Google Ads Enhanced Conversions för vidarebefordran av händelser i Adobe Experience Platform.
exl-id: 65cdff40-276f-4481-9621-6c6861dbd412
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 0d98183838125fac66768b94bc1993bde9a374b5
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 0%

---

# [!DNL Google Ads] Utökat konverteringstillägg

Med API:t [!DNL Google Ads] kan du utnyttja [förbättrade konverteringar](https://support.google.com/google-ads/answer/9888656) genom att skicka kunddata från första part i form av konverteringsjusteringar. Google använder dessa ytterligare data för att förbättra rapporteringen av dina onlinekonverteringar som styrs av annonsinteraktioner.

Tillägget [[!DNL Google Ads] Förbättrad konvertering av händelsevidarebefordran](https://exchange.adobe.com/apps/ec/108630/google-ads-enhanced-conversions) (kallas därför [!DNL Enhanced Conversions]-tillägget) innehåller en användarvänlig mall som gör det enkelt att implementera förbättrade konverteringar för [!DNL Google Ads] API.

>[!IMPORTANT]
>
>Förbättrade konverteringar fungerar bara för konverteringstyper där det finns kunddata, som prenumerationer, registreringar och inköp. En eller flera av följande kunddata måste vara tillgängliga eftersom de krävs när [en konverteringsåtgärd](#conversion-action-event-forwarding) konfigureras för en regel för vidarebefordran av händelser:
>
>* E-postadress (standard)
>* Namn och hemadress (gatuadress, ort, delstat/region och postnummer)
>* Telefonnummer (måste anges tillsammans med någon av de andra två uppgifterna ovan)

## Implementeringsöversikt

Förbättrade konverteringar använder API:t [!DNL Google Ads] för att lägga till egna data till en konvertering som sker på en klientenhet, vanligtvis en webbplats. Det innebär att det finns två steg för att implementera förbättrade konverteringar:

1. Skicka en konvertering från klienten.
1. Använd händelsevidarebefordran för att skicka ytterligare data från första part som förbättrar konverteringsdata som skickas från klienten.

>[!TIP]
>
>Om du vill associera konverteringshändelsen på klientsidan med förstahandsdata som skickas från händelsevidarebefordran måste `transaction_ID` vara samma i båda anropen. Mer information om var det här värdet måste anges för varje tjänst finns i avsnitten om konfigurering av konverteringsåtgärder för [tags](#conversion-action-tags) respektive [händelsevidarebefordran](#conversion-action-event-forwarding).

Eftersom sändning av konverteringshändelser innefattar både en implementering på klientsidan och på serversidan, innehåller det här dokumentet de nödvändiga stegen för konfiguration av [[!DNL Google Global Site Tag] (gtag)-tillägget ](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag) på klientsidan förutom [!DNL Enhanced Conversions]-tillägget för händelsevidarebefordran.

I följande video visas en introduktion till tillägget [!DNL Enhanced Conversions] som går igenom implementeringsstegen på en hög nivå:

>[!VIDEO](https://video.tv.adobe.com/v/3411365?quality=12&learn=on)

## Skicka en konvertering med hjälp av taggar

Om du vill skicka en konverteringshändelse från på en webbplats måste [!DNL Google Global Site Tag] (gtag) distribueras. Du kan uppnå detta med hjälp av taggar genom att konfigurera och installera tillägget [!DNL Google Global Site Tag] (gtag).

### Konfigurera och installera tillägget [!DNL Google Global Site Tag]

Navigera till användargränssnittet för [!UICONTROL Data Collection] eller Experience Platform och välj **[!UICONTROL Tags]** i den vänstra navigeringen. Välj den taggegenskap som du vill installera tillägget på och välj sedan **[!UICONTROL Extensions]** i den vänstra navigeringen. Gå till fliken **[!UICONTROL Catalog]**, leta upp tillägget [!UICONTROL Google Global Site Tag (gtag)] och välj **[!UICONTROL Install]**.

![Det [!UICONTROL Google Global Site Tag (gtag)]-tillägg som markeras under vyn [!UICONTROL Extensions] i gränssnittet [!UICONTROL Data Collection].](../../../images/extensions/server/google-ads-enhanced-conversions/install-gtag-extension.png)

Installationsdialogrutan visas. Här väljer du **[!UICONTROL Add Account]** och anger följande värden när du uppmanas till det:

| Kontoegenskap | Beskrivning |
| --- | --- |
| Kontonamn | Ett unikt namn för kontot. Det här namnet används bara i tagggränssnittet. |
| Konto-ID | Ditt konto-ID för [!DNL Google Ads]. Logga in på [!DNL Google Ads] och navigera till: **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Install the Tag yourself]** för att hitta det här värdet. Konto-ID-strängen finns i kodfragmentfönstret som börjar med `AW-` eller `d`. |
| Produkt | Välj **[!UICONTROL Google Ads (AdWords)]**. |

{style="table-layout:auto"}

När du är klar väljer du **[!UICONTROL Add Account]** och sedan **[!UICONTROL Save]**.

### Lägg till en sändningskonverteringsåtgärd {#conversion-action-tags}

När du har installerat tillägget kan du börja inkludera konverteringsåtgärder i taggreglerna. När du skapar eller redigerar en regel som avlyssnar den konvertering som du vill förbättra, väljer du **[!UICONTROL Add]** under [!UICONTROL Actions]. I nästa dialogruta väljer du **[!UICONTROL Google Global Site Tag (gtag)]** i listrutan [!UICONTROL Extension] och sedan **[!UICONTROL Send an event]** under [!UICONTROL Action Type].

![Åtgärdstypen [!UICONTROL Send an event] som väljs i åtgärdskonfigurationsvyn i regelredigeringsarbetsflödet.](../../../images/extensions/server/google-ads-enhanced-conversions/select-client-action.png)

Ytterligare kontroller visas som gör att du kan konfigurera [!DNL gtag]-händelsen. Minst följande fält måste fyllas i:

1. **[!UICONTROL Event Name (Action)]**: Ange `conversion` som värde.
1. Lägg till ett nytt fält där nyckeln är `transaction_id` och värdet är ett [dataelement](../../../ui/managing-resources/data-elements.md) som innehåller [transaktions-ID](https://support.google.com/google-ads/answer/6386790)-värdet.
1. **[!UICONTROL Conversion Label]**: Ange lämplig konverteringsetikett från ditt [!DNL Google Ads]-konto. Om du vill hitta det här värdet loggar du in på Google Ads och går till **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Use Google Tag Manager]**. Konverteringsetiketten finns under [!DNL Instructions].

   >[!IMPORTANT]
   >
   >Kontrollera att Förbättrade konverteringar är aktiverade när du är i tagginställningsområdet för ditt [!DNL Google Ads]-konto. Om du vill göra det granskar och godkänner du användarvillkoren och väljer sedan **[!DNL Turn on enhanced conversions]** och **[!DNL API]** som implementeringsmetod.

När du har konfigurerat åtgärden väljer du **[!UICONTROL Keep Changes]** för att lägga till åtgärden i regelkonfigurationen. När du är nöjd med regeln väljer du **[!UICONTROL Save to Library]**.

Publicera slutligen en ny [build](../../../ui/publishing/builds.md) för att aktivera ändringarna i biblioteket.

## Skicka data från första part med hjälp av händelsevidarebefordran

När du kan skicka konverteringshändelser från klientsidan kan du förbättra konverteringarna med tillägget [!DNL Enhanced Conversions] för händelsevidarebefordran.

### Skapa en Google OAuth 2-hemlighet och ett dataelement {#create-secret-data-element}

Innan du konfigurerar tillägget måste du skapa en åtkomsttoken i händelsevidarebefordran för att autentisera till [!DNL Google Ads] API.

Mer information finns i guiden [Skapa hemligheter för vidarebefordran av händelser](../../../ui/event-forwarding/secrets.md). Se till att du väljer **[!UICONTROL Google OAuth 2]** som hemlig typ. Fortsätt att följa anvisningarna, och när du ombeds att välja en Google-kontoprofil väljer du det konto som har tillgång till den konverteringsåtgärd du konfigurerar.

När hemligheten har skapats [skapar du ett nytt dataelement](../../../ui/managing-resources/data-elements.md#create-a-data-element) och väljer **[!UICONTROL Secret]** som dataelementtyp. Välj lämplig Google OAuth 2-hemlighet för varje miljö och välj **[!UICONTROL Save to Library]**.

### Konfigurera och installera tillägget [!DNL Enhanced Conversions] {#install-enhanced-conversions}

Leta reda på tillägget [!UICONTROL Google Ads Enhanced Conversions] i katalogen för händelsevidarebefordran och välj **[!UICONTROL Install]**.

![Det [!UICONTROL Google Ads Enhanced Conversions]-tillägg som markeras under vyn [!UICONTROL Extensions] i gränssnittet [!UICONTROL Data Collection].](../../../images/extensions/server/google-ads-enhanced-conversions/install-enhanced-conversions.png)

Om du vill konfigurera tillägget måste du fylla i de två obligatoriska fälten:

1. **[!UICONTROL Customer ID]**: Det ID som unikt identifierar ditt [!DNL Google Ads]-konto. Logga in på [!DNL Google Ads] och navigera till **[!DNL Help]** > **[!DNL Customer ID]** om du vill hitta det här värdet.
2. **[!UICONTROL Access Token Data Element]**: Välj dataelementikonen (![Dataelementsikon](/help/images/icons/database.png)) och välj det hemliga dataelement för Google OAuth 2 som du [konfigurerade i föregående steg](#create-secret-data-element) på menyn.

När du är klar väljer du **[!UICONTROL Save]** för att installera tillägget.

### Lägg till en [!UICONTROL Send Conversion]-åtgärd i en regel {#conversion-action-event-forwarding}

När tillägget har installerats kan du börja inkludera [!UICONTROL Send Conversion] åtgärder i reglerna för vidarebefordran av händelser. När du skapar eller redigerar en regel som avlyssnar den konvertering du vill förbättra, väljer du **[!UICONTROL Add]** under [!UICONTROL Actions]. I nästa dialogruta väljer du **[!UICONTROL Google Ads Enhanced Conversions]** i listrutan [!UICONTROL Extension] och sedan **[!UICONTROL Send Conversion]** under [!UICONTROL Action Type].

![Åtgärdstypen [!UICONTROL Send Conversion] som väljs i åtgärdskonfigurationsvyn i regelredigeringsarbetsflödet.](../../../images/extensions/server/google-ads-enhanced-conversions/select-server-action.png)

Nya kontroller visas på den högra panelen där du kan konfigurera konverteringen. Minst följande fält måste fyllas i:

**Konverteringsinformation**

| Indata | Beskrivning |
| --- | --- |
| Kund-ID | Ditt [!DNL Google Ads]-kund-ID. Standardvärdet är det kund-ID som du angav när [tillägget](#install-enhanced-conversions) installerades. |
| Konverterings-ID eller konverteringsetikett | Spårningsvärden som hämtats från [!DNL Google Ads] när konverteringsspårning konfigureras. Värdena börjar med `AW-`.<br><br>Mer information om hur du hittar dessa värden finns i [[!DNL Google Ads] dokumentationen](https://support.google.com/tagmanager/answer/6105160?hl=en). |
| Transaktions-ID | Välj ett dataelement som har samma transaktions-ID-värde som [skickas från klientsidan](#conversion-action-tags) med tillägget [!DNL Google Global Site Tag]. |

**Användar-ID**

* Minst en av de tre användaridentifierarna måste ingå:
   * E-post
   * Telefonnummer
   * Fullständig adress

>[!TIP]
>
>Användaridentifieringsdata måste hashas innan de skickas till Google. Om data inte hashas när händelsevidarebefordring tar emot dem väljer du **[!UICONTROL Normalize & Hash]**-växeln i ett givet fält för att instruera tillägget att hash-koda värdet.
>
>![Växeln [!UICONTROL Normalize & Hash] aktiverad för indata från [!UICONTROL Email] i [!UICONTROL Send Conversion] åtgärdskonfigurationsformuläret.](../../../images/extensions/server/google-ads-enhanced-conversions/hash-user-id-values.png)

När du är klar väljer du **[!UICONTROL Keep Changes]** för att lägga till åtgärden i regelkonfigurationen. När du är nöjd med regeln väljer du **[!UICONTROL Save to Library]**.

Publicera slutligen en ny händelse som vidarebefordrar [build](../../../ui/publishing/builds.md) för att aktivera ändringarna i biblioteket.

## Nästa steg

I den här guiden beskrivs hur du skickar konverteringshändelser till [!DNL Google Ads] med hjälp av tillägget [!DNL Enhanced Conversions] för vidarebefordran av händelser. Mer information om funktioner för vidarebefordran av händelser i Experience Platform finns i [översikten över vidarebefordran av händelser](../../../ui/event-forwarding/overview.md).
