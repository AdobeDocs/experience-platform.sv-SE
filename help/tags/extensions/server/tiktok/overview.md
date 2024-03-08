---
title: API-tillägg för webbhändelser i Adobe TikTok
description: Med Adobe Experience Platform webbevent-API kan du dela webbinteraktioner direkt med TikTok.
last-substantial-update: 2023-09-26T00:00:00Z
exl-id: 14b8e498-8ed5-4330-b1fa-43fd1687c201
source-git-commit: 4ee895cb8371646fd2013e2a8f65c2ffdae95850
workflow-type: tm+mt
source-wordcount: '1048'
ht-degree: 1%

---

# [!DNL TikTok] API-tillägg för webbhändelser - översikt

The [!DNL TikTok] events API är en säker [API för Edge Network Server](/help/server-api/overview.md) gränssnitt som gör att du kan dela information med [!DNL TikTok] direkt om användaråtgärder på dina webbplatser. Du kan använda reglerna för vidarebefordran av händelser för att skicka data från [!DNL Adobe Experience Platform Edge Network] till [!DNL TikTok] genom att använda [!DNL TikTok] API-tillägg för webbhändelser.

## [!DNL TikTok] krav {#prerequisites}

Konfigurera [!DNL TikTok] webbhändelsens API för att använda [!DNL TikTok] händelse-API, du måste generera en [!DNL TikTok] pixelkod och åtkomsttoken.

Du måste ha en giltig [!DNL TikTok] för företagskonto för att skapa en [!DNL TikTok] pixel med partnerinställningen. Gå till [[!DNL TikTok] för företagsregistrering](https://www.tiktok.com/business/en-US/solutions/business-account) för att registrera och skapa ett konto om du inte redan har ett.

Du måste vara inloggad på ditt företagskonto för att kunna konfigurera [!DNL TikTok] Pixel med partnerkonfiguration. Gör så här:

1. Navigera till **[!UICONTROL Assets]** och markera **[!UICONTROL Event]**.
2. Under Webbhändelser väljer du **[!UICONTROL Manage]**.
3. Välj **[!UICONTROL Set Up Web Events]**.
4. Välj **[!UICONTROL Partner Setup]** som anslutningsmetod.

Se [Kom igång med Pixel](https://ads.tiktok.com/help/article/get-started-pixel) för mer information om hur du ställer in [!DNL TikTok] pixel.

Du kan generera en åtkomsttoken när pixeln har skapats. Navigera till pixeln och välj **[!UICONTROL Settings]** -fliken. Välj under Händelse-API **[!UICONTROL Generate Access Token]**.

Se [[!DNL TikTok] komma igång-guide](https://business-api.tiktok.com/portal/docs?id=1739584855420929) om du vill ha mer information om hur du ställer in pixelkoden och får åtkomst till token.

## Installera och konfigurera [!DNL TikTok] API-tillägg för webbhändelser {#install}

Om du vill installera tillägget väljer du **[!UICONTROL Extensions]** i den vänstra navigeringen. I **[!UICONTROL Catalog]** väljer du **[!UICONTROL TikTok Web Events API Extension]** och sedan **[!UICONTROL Install]**.

![Tilläggskatalogen med [!DNL TikTok] installation av tilläggskort.](../../../images/extensions/server/tiktok/install-extension.png)

På nästa skärm anger du följande konfigurationsvärden som du tidigare har genererat från [!DNL TikTok] Ads Manager:

* **[!UICONTROL Pixel Code]**
* **[!UICONTROL Access Token]**

När du är klar väljer du **[!UICONTROL Save]**.

![[!DNL TikTok] konfigurationsskärmen för [!DNL TikTok] API-tillägg för webbhändelser.](../../../images/extensions/server/tiktok/configure.png)

## Konfigurera en regel för vidarebefordran av händelser {#config-rule}

När alla dataelement har konfigurerats kan du börja skapa regler för vidarebefordran av händelser som bestämmer när och hur händelserna ska skickas till [!DNL TikTok].

Skapa ett nytt [regel](../../../ui/managing-resources/rules.md) i egenskapen för vidarebefordran av händelser. Under **[!UICONTROL Actions]**, lägga till en ny åtgärd och ange tillägget till **[!UICONTROL TikTok Web Events API Extension]**. Skicka Edge Network-händelser till [!DNL TikTok], ange **[!UICONTROL Action Type]** till **[!UICONTROL Send TikTok Web Events API Event].**

![The [!UICONTROL Send TikTok Web Events API Event] åtgärdstyp som väljs för en [!DNL TikTok] i användargränssnittet för datainsamling.](../../../images/extensions/server/tiktok/select-action.png)

Efter markeringen visas ytterligare kontroller för att ytterligare konfigurera händelsen enligt instruktionerna nedan. När du är klar väljer du **[!UICONTROL Keep Changes]** för att spara regeln.

**[!UICONTROL Web Events and Parameters]**

Webbhändelser och parametrar innehåller allmän information om händelsen. Standardhändelser stöds i alla [!DNL TikTok] integreringsverktyg och kan användas för att rapportera, optimera för konverteringar och skapa målgrupper.

| Indata | Beskrivning |
| --- | --- |
| Händelsenamn | Namnet på händelsen. Detta är åtgärder med fördefinierade namn som skapas av [!DNL TikTok] och är ett obligatoriskt fält. Se [[!DNL TikTok] Marknadsförings-API](https://business-api.tiktok.com/portal/docs?id=1741601162187777) dokumentation för mer information om händelser som stöds. |
| Händelsetid | Datum-tid som sträng i ISO 8601 eller i `yyyy-MM-dd'T'HH:mm:ss:SSSZ` format. Detta är ett obligatoriskt fält. |
| Händelse-ID | Det unika ID som genereras av annonsörer för att ange varje händelse. Det här är ett valfritt fält och används för borttagning av dubbletter. |

{style="table-layout:auto"}

![The [!DNL Web Events and Parameters] som visar exempeldata i fälten.](../../../images/extensions/server/tiktok/configure-web-events-parameters.png)

**[!UICONTROL User Context Parameters]**

Parametrar för användarkontext innehåller kundinformation som används för att matcha webbbesökshändelser med [!DNL TikTok] -användare. Genom att ta med flera typer av matchande data kan ni öka noggrannheten i målinriktning och optimeringsmodeller.

| Indata | Beskrivning |
| --- | --- |
| IP-adress | Webbläsarens offentliga IP-adress som inte hashats. Stöd ges för IPv4- och IPv6-adresser. Både fullständiga och komprimerade former av IPv6-adresser känns igen. |
| Användaragent | Den icke-hash-kodade användaragenten från användarens enhet. |
| E-post | E-postadress till den kontakt som är associerad med konverteringshändelsen. |
| Telefon | Telefonnumret måste vara i E164-format [+][landskod][riktnummer][local phone number] före hashning. |
| Cookie-ID | Om du använder Pixel SDK sparas en unik identifierare automatiskt i `_ttp` cookie, om cookies är aktiverade. The `_ttp` kan extraheras och användas för det här fältet. |
| Externt ID | Alla unika identifierare, till exempel användar-ID:n, externa cookie-ID:n och så vidare, måste hash-kodas med SHA256. |
| TikTok Click ID | The `ttclid` som läggs till på landningssidans URL varje gång en annons väljs [!DNL TikTok]. |
| Sidans URL | Sidans URL vid tidpunkten för händelsen. |
| URL för sidreferens | URL för sidreferenten. |

{style="table-layout:auto"}

![The [!DNL User Context Parameters] som visar exempeldata i fälten.](../../../images/extensions/server/tiktok/configure-user-context-parameters.png)

**[!UICONTROL Properties Parameters]**

Använd egenskapsparametrarna för att konfigurera ytterligare egenskaper som stöds.

| Indata | Beskrivning |
| --- | --- |
| Pris | Kostnaden för en enstaka artikel. |
| Kvantitet | Antalet artiklar som köpts i händelsen. Detta måste vara ett positivt tal större än 0. |
| Innehållstyp | Ett värde för antingen `product` eller `product_group` måste tilldelas till egenskapen content_type-objekt, beroende på hur du konfigurerar dataflödet när du konfigurerar produktkatalogen. |
| Innehålls-ID | En unik identifierare för produktartikeln. |
| Innehållskategori | Sidans/produktens kategori. |
| Innehållsnamn | Namn på sidan/produkten. |
| Valuta | Valutan för de artiklar som köps in i händelsen. Detta anges i ISO-4217. |
| Värde | Orderns totala pris. Det här värdet är lika med priset * kvantitet. |
| Beskrivning | En beskrivning av objektet eller sidan. |
| Fråga | Den textsträng som användes för att söka efter en produkt. |
| Status | Status för en order, artikel eller tjänst. Till exempel&quot;skickat&quot;. |

{style="table-layout:auto"}

![The [!DNL Properties Parameters] som visar exempeldata i fälten.](../../../images/extensions/server/tiktok/configure-properties-parameters.png)

## Borttagning av händelser {#deduplication}

[!DNL TikTok] pixeln måste vara inställd för borttagning av dubbletter om du använder båda [!DNL TikTok] pixel SDK och [!DNL TikTok] API-tillägg för webbhändelser för att skicka samma händelser till [!DNL TikTok].

Deduplicering krävs inte om distinkta händelsetyper skickas från klienten och servern utan någon överlappning. För att din rapportering inte ska påverkas negativt måste du se till att alla händelser som delas av [!DNL TikTok] pixel SDK och [!DNL TikTok] API-tillägget för webbhändelser har deduplicerats.

När du skickar delade händelser måste du se till att alla händelser innehåller ett pixel-ID, händelse-ID och namn. Duplicerade händelser som kommer inom fem minuter från varandra sammanfogas. Om datafältet inte fanns med i den första händelsen kombineras det med den efterföljande händelsen. Alla dubbletthändelser som tas emot inom 48 timmar tas bort.

Se [!DNL TikTok] dokumentation om [Händelseborttagning](https://ads.tiktok.com/help/article/event-deduplication) om du vill ha mer information om processen.

## Nästa steg

I den här guiden beskrivs hur du skickar händelsedata på serversidan till [!DNL TikTok] med [!DNL TikTok] API-tillägg för webbhändelser. Mer information om funktioner för vidarebefordran av händelser finns i [!DNL Adobe Experience Platform], se [händelsevidarebefordring - översikt](../../../ui/event-forwarding/overview.md).
