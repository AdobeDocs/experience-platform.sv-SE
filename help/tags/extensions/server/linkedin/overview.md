---
title: API-händelsevidarebefordringstillägg för LinkedIn Conversions
description: Med det här tillägget för vidarebefordran av Adobe Experience Platform-händelser kan du mäta resultatet av din LinkedIn-marknadsföringskampanj.
last-substantial-update: 2023-10-25T00:00:00Z
exl-id: 411e7b77-081e-4139-ba34-04468e519ea5
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 0%

---

# [!DNL LinkedIn] API-tillägg för konverteringar

[[!DNL LinkedIn Conversions API]](https://learn.microsoft.com/en-us/linkedin/marketing/integrations/ads-reporting/conversions-api) är ett verktyg för konverteringsspårning som skapar en direkt koppling mellan marknadsföringsdata från en annonsörs server och [!DNL LinkedIn]. På så sätt kan annonsörer utvärdera hur effektiva deras [!DNL LinkedIn] marknadsföringskampanjer oavsett var konverteringen sker och använder informationen för att optimera kampanjer. The [!DNL LinkedIn Conversions API] tillägg kan hjälpa till att förbättra prestanda och minska kostnaden per åtgärd med mer fullständig attribuering, förbättrad datatillförlitlighet och bättre optimerad leverans.

## Förutsättningar {#prerequisites}

Du måste skapa en konverteringsregel i [!DNL LinkedIn] kampanjannonskonto. [!DNL Adobe] rekommenderar att du tar med&quot;CAPI&quot; i början av konversationsregelns namn så att det skiljer sig från andra typer av konverteringsregler som du har konfigurerat.

### Skapa en hemlighet och ett dataelement

Skapa ett nytt [!DNL LinkedIn] [hemlighet för vidarebefordran av händelser](../../../ui/event-forwarding/secrets.md) och ge den ett unikt namn som betecknar den verifierande medlemmen. Detta används för att autentisera anslutningen till ditt konto samtidigt som värdet är säkert.

Nästa, [skapa ett dataelement](../../../ui/managing-resources/data-elements.md#create-a-data-element) med [!UICONTROL Core] tillägg och [!UICONTROL Secret] dataelementtyp som refererar till `LinkedIn` hemlighet du nyss skapade.

## Installera och konfigurera [!DNL LinkedIn] extension {#install}

Installera tillägget genom att [skapa en egenskap för vidarebefordring av händelser](../../../ui/event-forwarding/overview.md#properties) eller markera en befintlig egenskap som du vill redigera.

Välj **[!UICONTROL Extensions]** i den vänstra navigeringen. I **[!UICONTROL Catalog]** väljer du **[!UICONTROL LinkedIn]** och välj sedan **[!UICONTROL Install]**.

![Tilläggskatalogen med [!DNL LinkedIn] installation av tilläggskort.](../../../images/extensions/server/linkedin/install-extension.png)

På nästa skärm anger du dataelementets hemlighet som du skapade tidigare i `Access Token` fält. Dataelementets hemlighet innehåller din [!DNL LinkedIn] OAuth 2-token. Välj **[!UICONTROL Save]** när du är klar.

![The [!DNL LinkedIn] konfigurationssida för tillägg med [!UICONTROL Access Token] fält och [!UICONTROL Save] markerad.](../../../images/extensions/server/linkedin/configure-extension.png)

## Skapa en [!DNL Send Conversion] regel {#tracking-rule}

När alla dataelement har konfigurerats kan du börja skapa regler för vidarebefordran av händelser som bestämmer när och hur händelserna ska skickas till [!DNL LinkedIn].

Skapa en ny händelsevidarebefordring [regel](../../../ui/managing-resources/rules.md) i egenskapen för vidarebefordran av händelser. Under **[!UICONTROL Actions]**, lägga till en ny åtgärd och ange tillägget till **[!UICONTROL LinkedIn]**. Nästa, välj **[!UICONTROL Send Web Conversion]** för **[!UICONTROL Action Type]**.

![Vyn Egenskapsregler för händelsevidarebefordring, med fälten som krävs för att lägga till en händelsevidarebefordringsregel, markerad.](../../../images/extensions/server/linkedin/linkedin-event-action.png)

Efter markeringen visas ytterligare kontroller för att ytterligare konfigurera händelsen. Välj **[!UICONTROL Keep Changes]** för att spara regeln.

**[!UICONTROL User Data]**

| Indata | Beskrivning |
| --- | --- |
| [!UICONTROL Email] | E-postadress till den kontakt som är associerad med konverteringshändelsen. E-postvärdet kodas av tilläggskoden i SHA256 om inte det angivna värdet redan är en SHA256-sträng. |
| [!UICONTROL LinkedIn First Party Ads Tracking UUID] | Detta är ett cookie-ID från första part. Annonsörer måste aktivera förbättrad konverteringsspårning från [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/help/lms/answer/a423304/enable-first-party-cookies-on-a-linkedin-insight-tag) för att aktivera cookies från första part som bifogar en click ID-parameter `li_fat_id` till klicka på URL:er. |
| [!UICONTROL Customer Information Data] | Det här fältet innehåller ett JSON-objekt med extra attribut som skickas tillsammans med meddelandet.<br><br>Under **[!UICONTROL Raw]** kan du klistra in JSON-objektet direkt i det angivna textfältet, eller så kan du välja dataelementsikonen (![Ikon för datauppsättning](../../../images/extensions/server/aws/data-element-icon.png)) för att välja från en lista med befintliga dataelement som ska representera data.<br><br>Du kan också använda **[!UICONTROL JSON Key-Value Pairs Editor]** om du vill lägga till nyckelvärdepar manuellt via en UI-redigerare. Varje värde kan representeras av en rådatainmatning, eller ett dataelement kan markeras i stället. Godkända nyckelvärden är: `firstName`, `lastName`, `companyName`, `title` och `country`. |

{style="table-layout:auto"}

![The [!DNL User Data] som visar exempeldata i fälten.](../../../images/extensions/server/linkedin/configure-extension-user-data.png)

**[!UICONTROL Conversion Data]**

| Indata | Beskrivning |
| --- | --- |
| [!UICONTROL Conversion] | ID:t för konverteringsregeln som skapades i [LinkedIn Campaign Manager](https://www.linkedin.com/help/lms/answer/a1657171) eller via [!DNL LinkedIn Campaign Manager]. |
| [!UICONTROL Conversion Time] | Varje tidsstämpel i millisekunder som konverteringshändelsen inträffade vid. <br><br> Obs! Om din källa sparar konverteringstidstämpeln i sekunder infogar du 000 i slutet för att omvandla den till millisekunder. |
| [!UICONTROL Currency] | Valutakod i ISO-format. |
| [!UICONTROL Amount] | Värdet för konverteringen i decimalsträng (till exempel &quot;100.05&quot;). |
| [!UICONTROL Event ID] | Det unika ID som annonsörer genererar för att ange varje händelse. Det här är ett valfritt fält och används för borttagning av dubbletter. |

{style="table-layout:auto"}

![The [!DNL Conversion Data] -avsnittet som visar exempeldata i fälten.](../../../images/extensions/server/linkedin/configure-extension-conversions-data.png)

**[!UICONTROL Configuration Overrides]**

>OBS!
>
>The [!UICONTROL Configuration Overrides] kan användaren ange ett annat fält [!DNL LinkedIn] åtkomsttoken för alla regler, vilket gör att varje regel kan använda en åtkomsttoken som kan ha åtkomst till olika [!DNL LinkedIn] annonskonton.

| Indata | Beskrivning |
| --- | --- |
| [!UICONTROL Access Token] | The [!DNL LinkedIn] åtkomsttoken. |

![The [!DNL Configuration Overrides] -avsnitt som visar exempeldata i fältet.](../../../images/extensions/server/linkedin/configure-extension-configuration-override.png)

## Nästa steg

Den här guiden beskriver hur du skickar data till [!DNL LinkedIn] med [!DNL LinkedIn Conversions API] tillägg för händelsevidarebefordran. Mer information om funktioner för vidarebefordran av händelser finns i [!DNL Adobe Experience Platform], se [händelsevidarebefordring - översikt](../../../ui/event-forwarding/overview.md).
