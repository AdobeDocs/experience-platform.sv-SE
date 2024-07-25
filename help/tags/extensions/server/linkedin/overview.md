---
title: API-händelsevidarebefordringstillägg för LinkedIn Conversions
description: Med det här tillägget för vidarebefordran av Adobe Experience Platform-händelser kan du mäta resultatet av din LinkedIn-marknadsföringskampanj.
last-substantial-update: 2023-10-25T00:00:00Z
exl-id: 411e7b77-081e-4139-ba34-04468e519ea5
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 0%

---

# API-tillägg för [!DNL LinkedIn]-konverteringar

[[!DNL LinkedIn Conversions API]](https://learn.microsoft.com/en-us/linkedin/marketing/integrations/ads-reporting/conversions-api) är ett verktyg för konverteringsspårning som skapar en direkt anslutning mellan marknadsföringsdata från en annonsörs server och [!DNL LinkedIn]. På så sätt kan annonsörer utvärdera effektiviteten hos sina [!DNL LinkedIn]-marknadsföringskampanjer oavsett var konverteringen sker och använda den här informationen för att optimera kampanjer. Tillägget [!DNL LinkedIn Conversions API] kan hjälpa till att förbättra prestanda och minska kostnaden per åtgärd med mer fullständig attribuering, förbättrad datatillförlitlighet och bättre optimerad leverans.

## Förhandskrav {#prerequisites}

Du måste [skapa en konverteringsregel](https://www.linkedin.com/help/lms/answer/a1657171) i ditt [!DNL LinkedIn Campaign Manager]-konto. [!DNL Adobe] rekommenderar att du tar med&quot;CAPI&quot; i början av konversationsregelns namn så att det skiljer sig från andra typer av konverteringsregler som du har konfigurerat.

### Skapa en hemlighet och ett dataelement

Skapa en ny [!DNL LinkedIn] [händelsevidarebefordringshemlighet](../../../ui/event-forwarding/secrets.md) och ge den ett unikt namn som anger den autentiserande medlemmen. Detta används för att autentisera anslutningen till ditt konto samtidigt som värdet är säkert.

Sedan [skapar du ett dataelement](../../../ui/managing-resources/data-elements.md#create-a-data-element) med tillägget [!UICONTROL Core] och dataelementtypen [!UICONTROL Secret] som refererar till den `LinkedIn`-hemlighet som du nyss skapade.

## Installera och konfigurera tillägget [!DNL LinkedIn] {#install}

Om du vill installera tillägget [skapar du en egenskap för vidarebefordring av händelser](../../../ui/event-forwarding/overview.md#properties) eller väljer en befintlig egenskap som du vill redigera.

Välj **[!UICONTROL Extensions]** i den vänstra navigeringen. Välj tillägget **[!UICONTROL LinkedIn]** på fliken **[!UICONTROL Catalog]** och välj sedan **[!UICONTROL Install]**.

![Tilläggskatalogen som visar installationen av [!DNL LinkedIn] tilläggskort.](../../../images/extensions/server/linkedin/install-extension.png)

På nästa skärm anger du dataelementets hemlighet som du skapade tidigare i fältet `Access Token`. Dataelementets hemlighet innehåller din [!DNL LinkedIn] OAuth 2-token. Välj **[!UICONTROL Save]** när du är klar.

![Konfigurationssidan för [!DNL LinkedIn]-tillägget med fältet [!UICONTROL Access Token] och [!UICONTROL Save] markerad.](../../../images/extensions/server/linkedin/configure-extension.png)

## Skapa en [!DNL Send Conversion]-regel {#tracking-rule}

När alla dataelement har konfigurerats kan du börja skapa regler för vidarebefordran av händelser som avgör när och hur händelser skickas till [!DNL LinkedIn].

Skapa en ny händelsevidarebefordring av [regel](../../../ui/managing-resources/rules.md) i din händelsevidarebefordringsegenskap. Under **[!UICONTROL Actions]** lägger du till en ny åtgärd och anger tillägget till **[!UICONTROL LinkedIn]**. Välj sedan **[!UICONTROL Send Conversion]** för **[!UICONTROL Action Type]**.

![Vyn för egenskapsregler för vidarebefordran av händelser, med de fält som krävs för att lägga till en åtgärdskonfiguration för vidarebefordring av händelser, markerad.](../../../images/extensions/server/linkedin/linkedin-event-action.png)

Efter markeringen visas ytterligare kontroller för att ytterligare konfigurera händelsen. Välj **[!UICONTROL Keep Changes]** om du vill spara regeln.

**[!UICONTROL User Data]**

| Indata | Beskrivning |
| --- | --- |
| [!UICONTROL Email] | E-postadress till den kontakt som är associerad med konverteringshändelsen. E-postvärdet kodas av tilläggskoden i SHA256 om inte det angivna värdet redan är en SHA256-sträng. |
| [!UICONTROL LinkedIn First Party Ads Tracking UUID] | Detta är ett cookie-ID från första part. Annonsörer måste aktivera förbättrad konverteringsspårning från [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/help/lms/answer/a423304/enable-first-party-cookies-on-a-linkedin-insight-tag) för att aktivera cookies från första part som lägger till en click ID-parameter `li_fat_id` till klicknings-URL:erna. |
| [!UICONTROL Customer Information Data] | Det här fältet innehåller ett JSON-objekt med extra attribut som skickas tillsammans med meddelandet.<br><br>Under alternativet **[!UICONTROL Raw]** kan du klistra in JSON-objektet direkt i det angivna textfältet. Du kan också markera dataelementsikonen (![Datauppsättningsikonen](/help/images/icons/database.png)) och välja från en lista över befintliga dataelement som ska representera data.<br><br>Du kan också använda alternativet **[!UICONTROL JSON Key-Value Pairs Editor]** för att manuellt lägga till nyckelvärdepar via en gränssnittsredigerare. Varje värde kan representeras av en rådatainmatning, eller ett dataelement kan markeras i stället. Godkända nyckelvärden är: `firstName`, `lastName`, `companyName`, `title` och `country`. |

{style="table-layout:auto"}

![Avsnittet [!DNL User Data] som visar exempeldata i fälten.](../../../images/extensions/server/linkedin/configure-extension-user-data.png)

**[!UICONTROL Conversion Data]**

| Indata | Beskrivning |
| --- | --- |
| [!UICONTROL Conversion] | ID:t för konverteringsregeln som skapades i [LinkedIn Campaign Manager](https://www.linkedin.com/help/lms/answer/a1657171). Välj konverteringsregeln för att hämta ID:t och kopiera sedan ID:t från webbläsarens URL (till exempel `/campaignmanager/accounts/508111232/conversions/15588877`) som `/conversions/<id>`. |
| [!UICONTROL Conversion Time] | Varje tidsstämpel i millisekunder som konverteringshändelsen inträffade vid. <br><br> Obs! Om din källa registrerar konverteringstidsstämpeln i sekunder infogar du 000 i slutet för att omvandla den till millisekunder. |
| [!UICONTROL Currency] | Valutakod i ISO-format. |
| [!UICONTROL Amount] | Värdet för konverteringen i decimalsträng (till exempel &quot;100.05&quot;). |
| [!UICONTROL Event ID] | Det unika ID som annonsörer genererar för att ange varje händelse. Det här är ett valfritt fält och används för [deduplicering](https://learn.microsoft.com/en-us/linkedin/marketing/conversions/deduplication?view=li-lms-2024-02). |

{style="table-layout:auto"}

![Avsnittet [!DNL Conversion Data] som visar exempeldata i fälten.](../../../images/extensions/server/linkedin/configure-extension-conversions-data.png)

**[!UICONTROL Configuration Overrides]**

>ANMÄRKNING
>
>I fältet [!UICONTROL Configuration Overrides] kan en användare ange olika [!DNL LinkedIn]-åtkomsttoken för varje regel, så att varje regel kan använda en åtkomsttoken som kan ha åtkomst till olika [!DNL LinkedIn]-annonskonton.

| Indata | Beskrivning |
| --- | --- |
| [!UICONTROL Access Token] | Åtkomsttoken [!DNL LinkedIn]. |

![Avsnittet [!DNL Configuration Overrides] som visar exempeldata i fältet.](../../../images/extensions/server/linkedin/configure-extension-configuration-override.png)

## Nästa steg

I den här guiden beskrivs hur du skickar data till [!DNL LinkedIn] med hjälp av tillägget [!DNL LinkedIn Conversions API] för vidarebefordran av händelser. Mer information om funktioner för vidarebefordran av händelser i [!DNL Adobe Experience Platform] finns i [översikten över vidarebefordran av händelser](../../../ui/event-forwarding/overview.md).

Mer information om hur du felsöker implementeringen med verktyget för felsökning och övervakning av händelsevidarebefordran i Experience Platform finns i [Adobe Experience Platform Debugger-översikten](../../../../debugger/home.md) och [Övervaka aktiviteter i händelsevidarebefordran](../../../ui/event-forwarding/monitoring.md).
