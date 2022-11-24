---
title: Google Ads Enhanced Conversions Extension
description: Läs mer om tillägget Google Ads Enhanced Conversions för vidarebefordran av händelser i Adobe Experience Platform.
exl-id: 65cdff40-276f-4481-9621-6c6861dbd412
source-git-commit: bfbad3c11df64526627e4ce2d766b527df678bca
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 0%

---

# [!DNL Google Ads] Utökat tillägg för konvertering

Använda [!DNL Google Ads] API, du kan använda [förbättrad konvertering](https://support.google.com/google-ads/answer/9888656) genom att skicka kunddata från första part i form av konverteringsjusteringar. Google använder dessa ytterligare data för att förbättra rapporteringen av dina onlinekonverteringar som styrs av annonsinteraktioner.

The [[!DNL Google Ads] Förbättrat tillägg för händelsevidarebefordran av konverteringar](https://exchange.adobe.com/apps/ec/108630/google-ads-enhanced-conversions) (kallas därför [!DNL Enhanced Conversions] tillägg) innehåller en användarvänlig mall för att enkelt implementera förbättrade konverteringar för [!DNL Google Ads] API.

>[!IMPORTANT]
>
>Förbättrade konverteringar fungerar bara för konverteringstyper där det finns kunddata, som prenumerationer, registreringar och inköp. En eller flera av följande kunddata måste vara tillgängliga, eftersom de krävs när [konfigurera en konverteringsåtgärd](#conversion-action-event-forwarding) för en regel för vidarebefordran av händelser:
>
>* E-postadress (standard)
>* Namn och hemadress (gatuadress, ort, delstat/region och postnummer)
>* Telefonnummer (måste anges tillsammans med någon av de andra två uppgifterna ovan)


## Implementeringsöversikt

Förbättrade konverteringar utnyttjar [!DNL Google Ads] API för att lägga till egna data i en konvertering som sker på en klientenhet, vanligtvis en webbplats. Det innebär att det finns två steg för att implementera förbättrade konverteringar:

1. Skicka en konvertering från klienten.
1. Använd händelsevidarebefordran för att skicka ytterligare data från första part som förbättrar konverteringsdata som skickas från klienten.

>[!TIP]
>
>Om du vill associera konverteringshändelsen på klientsidan med förstahandsdata som skickas från händelsevidarebefordring kan du `transaction_ID` måste vara detsamma i båda samtalen. Mer information om var det här värdet måste anges för varje tjänst finns i avsnitten om konfigurering av konverteringsåtgärder för [taggar](#conversion-action-tags) och [händelsevidarebefordran](#conversion-action-event-forwarding), respektive.

Eftersom sändning av konverteringshändelser innefattar både en implementering på klientsidan och på serversidan, innehåller det här dokumentet de nödvändiga stegen för att konfigurera klientsidan [[!DNL Google Global Site Tag] (gtag)-tillägg](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag) utöver [!DNL Enhanced Conversions] tillägg för händelsevidarebefordran.

I följande video ges en introduktion till [!DNL Enhanced Conversions] och går igenom implementeringsstegen på hög nivå:

>[!VIDEO](https://video.tv.adobe.com/v/3411365?quality=12&learn=on)

## Skicka en konvertering med hjälp av taggar

Om du vill skicka en konverteringshändelse från på en webbplats [!DNL Google Global Site Tag] (gtag) måste distribueras. Du kan göra detta med hjälp av taggar genom att konfigurera och installera [!DNL Google Global Site Tag] (gtag).

### Konfigurera och installera [!DNL Google Global Site Tag] extension

Navigera till [!UICONTROL Data Collection] Användargränssnittet eller användargränssnittet för Experience Platform och markera **[!UICONTROL Tags]** i den vänstra navigeringen. Välj den taggegenskap som du vill installera tillägget på och välj sedan **[!UICONTROL Extensions]** i den vänstra navigeringen. Under **[!UICONTROL Catalog]** -fliken, leta upp [!UICONTROL Google Global Site Tag (gtag)] tillägg och markera **[!UICONTROL Install]**.

![The [!UICONTROL Google Global Site Tag (gtag)] som väljs under [!UICONTROL Extensions] visa i [!UICONTROL Data Collection] Gränssnitt.](../../../images/extensions/server/google-ads-enhanced-conversions/install-gtag-extension.png)

Installationsdialogrutan visas. Här väljer du **[!UICONTROL Add Account]** och ange följande värden när du uppmanas till det:

| Kontoegenskap | Beskrivning |
| --- | --- |
| Kontonamn | Ett unikt namn för kontot. Det här namnet används bara i tagggränssnittet. |
| Konto-ID | Dina [!DNL Google Ads] konto-ID. Logga in på [!DNL Google Ads] och navigera till: **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Install the Tag yourself]**. Konto-ID-strängen finns i kodfragmentfönstret som börjar med `AW-` eller `d`. |
| Produkt | Välj **[!UICONTROL Google Ads (AdWords)]**. |

{style=&quot;table-layout:auto&quot;}

När du är klar väljer du **[!UICONTROL Add Account]** väljer **[!UICONTROL Save]**.

### Lägg till en sändningskonverteringsåtgärd {#conversion-action-tags}

När du har installerat tillägget kan du börja inkludera konverteringsåtgärder i taggreglerna. När du skapar eller redigerar en regel som avlyssnar den konvertering du vill förbättra, markerar du **[!UICONTROL Add]** under [!UICONTROL Actions]. I nästa dialogruta väljer du **[!UICONTROL Google Global Site Tag (gtag)]** från [!UICONTROL Extension] listruta och välj **[!UICONTROL Send an event]** under [!UICONTROL Action Type].

![The [!UICONTROL Send an event] åtgärdstypen som väljs i åtgärdskonfigurationsvyn i regelredigeringsarbetsflödet.](../../../images/extensions/server/google-ads-enhanced-conversions/select-client-action.png)

Ytterligare kontroller som gör att du kan konfigurera [!DNL gtag] -händelse. Minst följande fält måste fyllas i:

1. **[!UICONTROL Event Name (Action)]**: Retur `conversion` som värdet.
1. Lägg till ett nytt fält där nyckeln finns `transaction_id` och värdet är [dataelement](../../../ui/managing-resources/data-elements.md) som innehåller [transaktions-ID](https://support.google.com/google-ads/answer/6386790) värde.
1. **[!UICONTROL Conversion Label]**: Ange rätt konverteringsetikett från [!DNL Google Ads] konto. Logga in på Google Ads och navigera till **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Use Google Tag Manager]**. Konverteringsetiketten finns under [!DNL Instructions].
   >[!IMPORTANT]
   >
   >När du befinner dig i tagginställningsområdet för [!DNL Google Ads] ska du kontrollera att de förbättrade konverteringarna är aktiverade. Om du vill göra det granskar och godkänner du användarvillkoren och väljer **[!DNL Turn on enhanced conversions]** och **[!DNL API]** som implementeringsmetod.

När du har konfigurerat åtgärden väljer du **[!UICONTROL Keep Changes]** för att lägga till åtgärden i regelkonfigurationen. När du är nöjd med regeln väljer du **[!UICONTROL Save to Library]**.

Publicera slutligen en ny [bygga](../../../ui/publishing/builds.md) för att aktivera ändringar i biblioteket.

## Skicka data från första part med hjälp av händelsevidarebefordran

När du kan skicka konverteringshändelser från klienten kan du förbättra konverteringarna med [!DNL Enhanced Conversions] tillägg för händelsevidarebefordran.

### Skapa en Google OAuth 2-hemlighet och ett dataelement {#create-secret-data-element}

Innan du konfigurerar tillägget måste du skapa en åtkomsttoken i händelsevidarebefordran för att autentisera till [!DNL Google Ads] API.

Se guiden [skapa hemligheter för vidarebefordran av händelser](../../../ui/event-forwarding/secrets.md) för detaljerade steg. Se till att du väljer **[!UICONTROL Google OAuth 2]** som hemlig typ. Fortsätt att följa anvisningarna, och när du ombeds att välja en Google-kontoprofil väljer du det konto som har tillgång till den konverteringsåtgärd du konfigurerar.

När hemligheten har skapats [skapa ett nytt dataelement](../../../ui/managing-resources/data-elements.md#create-a-data-element) och markera **[!UICONTROL Secret]** för elementtypen data. Välj lämplig Google OAuth 2-hemlighet för varje miljö och välj **[!UICONTROL Save to Library]**.

### Konfigurera och installera [!DNL Enhanced Conversions] extension {#install-enhanced-conversions}

Hitta [!UICONTROL Google Ads Enhanced Conversions] i katalogen för vidarebefordran av händelser och välj **[!UICONTROL Install]**.

![The [!UICONTROL Google Ads Enhanced Conversions] som väljs under [!UICONTROL Extensions] visa i [!UICONTROL Data Collection] Gränssnitt.](../../../images/extensions/server/google-ads-enhanced-conversions/install-enhanced-conversions.png)

Om du vill konfigurera tillägget måste du fylla i de två obligatoriska fälten:

1. **[!UICONTROL Customer ID]**: Det ID som unikt identifierar [!DNL Google Ads] konto. Logga in på [!DNL Google Ads] och navigera till **[!DNL Help]** > **[!DNL Customer ID]**.
1. **[!UICONTROL Access Token Data Element]**: Markera dataelementsikonen (![Dataelementikon](../../../images/extensions/server/google-ads-enhanced-conversions/data-element-icon.png)) och välj det hemliga Google OAuth 2-dataelement som du [som konfigurerats i föregående steg](#create-secret-data-element) på menyn.

När du är klar väljer du **[!UICONTROL Save]** för att installera tillägget.

### Lägg till en [!UICONTROL Send Conversion] åtgärd för en regel {#conversion-action-event-forwarding}

När tillägget har installerats kan du börja ta med [!UICONTROL Send Conversion] åtgärder i reglerna för vidarebefordran av händelser. När du skapar eller redigerar en regel som avlyssnar den konvertering du vill förbättra, markerar du **[!UICONTROL Add]** under [!UICONTROL Actions]. I nästa dialogruta väljer du **[!UICONTROL Google Ads Enhanced Conversions]** från [!UICONTROL Extension] listruta och välj **[!UICONTROL Send Conversion]** under [!UICONTROL Action Type].

![The [!UICONTROL Send Conversion] åtgärdstypen som väljs i åtgärdskonfigurationsvyn i regelredigeringsarbetsflödet.](../../../images/extensions/server/google-ads-enhanced-conversions/select-server-action.png)

Nya kontroller visas på den högra panelen där du kan konfigurera konverteringen. Minst följande fält måste fyllas i:

**Konverteringsinformation**

| Indata | Beskrivning |
| --- | --- |
| Kund-ID | Dina [!DNL Google Ads] kund-ID. Standardvärdet är det kund-ID du angav när [installera tillägget](#install-enhanced-conversions). |
| Konverterings-ID eller konverteringsetikett | Spårningsvärden som erhållits från [!DNL Google Ads] när du ställer in konverteringsspårning. Värden börjar med `AW-`.<br><br>Mer information om hur du hittar dessa värden finns i [[!DNL Google Ads] dokumentation](https://support.google.com/tagmanager/answer/6105160?hl=en). |
| Transaktions-ID | Välj ett dataelement som har samma transaktions-ID-värde som [skickas från klientsidan](#conversion-action-tags) med [!DNL Google Global Site Tag] tillägg. |

**Användaridentifiering**

* Minst en av de tre användaridentifierarna måste ingå:
   * E-post
   * Telefonnummer
   * Fullständig adress

>[!TIP]
>
>Användaridentifieringsdata måste hashas innan de skickas till Google. Om data inte hashas när händelsevidarebefordran tar emot dem väljer du **[!UICONTROL Normalize & Hash]** om du vill att tillägget ska hash-koda värdet trycker du på ett visst fält.
>
>![The [!UICONTROL Normalize & Hash] växla aktiverat för [!UICONTROL Email] indata i [!UICONTROL Send Conversion] åtgärdskonfigurationsformulär.](../../../images/extensions/server/google-ads-enhanced-conversions/hash-user-id-values.png)

När du är klar väljer du **[!UICONTROL Keep Changes]** för att lägga till åtgärden i regelkonfigurationen. När du är nöjd med regeln väljer du **[!UICONTROL Save to Library]**.

Publicera slutligen en ny händelsevidarebefordring [bygga](../../../ui/publishing/builds.md) för att aktivera ändringar i biblioteket.

## Nästa steg

Den här guiden beskriver hur du skickar konverteringshändelser till [!DNL Google Ads] med [!DNL Enhanced Conversions] tillägg för händelsevidarebefordran. Mer information om funktioner för att vidarebefordra händelser i Experience Platform finns i [händelsevidarebefordring - översikt](../../../ui/event-forwarding/overview.md).
