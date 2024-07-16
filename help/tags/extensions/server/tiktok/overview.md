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

# API-tilläggets [!DNL TikTok] för webbhändelser - översikt

Händelse-API:t [!DNL TikTok] är ett säkert [Edge Network Server-API](/help/server-api/overview.md) som gör att du kan dela information med [!DNL TikTok] direkt om användaråtgärder på dina webbplatser. Du kan utnyttja reglerna för vidarebefordran av händelser för att skicka data från [!DNL Adobe Experience Platform Edge Network] till [!DNL TikTok] med hjälp av API-tillägget [!DNL TikTok] för webbhändelser.

## Krav för [!DNL TikTok] {#prerequisites}

Om du vill konfigurera [!DNL TikTok]-webbhändelseAPI:t så att det använder [!DNL TikTok]-händelse-API:t måste du generera en [!DNL TikTok] pixelkod och komma åt token.

Du måste ha en giltig [!DNL TikTok] för företagskonto för att kunna skapa en [!DNL TikTok] pixel med partnerkonfigurationen. Gå till sidan [[!DNL TikTok] för företagsregistrering](https://www.tiktok.com/business/en-US/solutions/business-account) om du vill registrera dig och skapa ett konto om du inte redan har ett.

Du måste vara inloggad på ditt företagskonto för att kunna konfigurera [!DNL TikTok] pixlar med partnerkonfiguration. Gör så här:

1. Navigera till fliken **[!UICONTROL Assets]** och välj **[!UICONTROL Event]**.
2. Välj **[!UICONTROL Manage]** under Webbhändelser.
3. Välj **[!UICONTROL Set Up Web Events]**.
4. Välj **[!UICONTROL Partner Setup]** som anslutningsmetod.

Mer information om hur du ställer in pixeln [!DNL TikTok] finns i guiden [Kom igång med Pixel](https://ads.tiktok.com/help/article/get-started-pixel) .

Du kan generera en åtkomsttoken när pixeln har skapats. Om du vill göra det går du till pixeln och väljer fliken **[!UICONTROL Settings]**. Välj **[!UICONTROL Generate Access Token]** under Händelse-API.

Mer information om hur du konfigurerar pixelkoden och får åtkomst till token finns i [[!DNL TikTok] Komma igång-guiden](https://business-api.tiktok.com/portal/docs?id=1739584855420929).

## Installera och konfigurera API-tillägget för [!DNL TikTok]-webbhändelser {#install}

Om du vill installera tillägget väljer du **[!UICONTROL Extensions]** i den vänstra navigeringen. Markera **[!UICONTROL TikTok Web Events API Extension]** på fliken **[!UICONTROL Catalog]** och välj sedan **[!UICONTROL Install]**.

![Tilläggskatalogen som visar installationen av [!DNL TikTok] tilläggskort.](../../../images/extensions/server/tiktok/install-extension.png)

På nästa skärm anger du följande konfigurationsvärden som du tidigare har genererat från [!DNL TikTok] Ads Manager:

* **[!UICONTROL Pixel Code]**
* **[!UICONTROL Access Token]**

När du är klar väljer du **[!UICONTROL Save]**.

![[!DNL TikTok] konfigurationsskärm för API-tillägget [!DNL TikTok] för webbhändelser.](../../../images/extensions/server/tiktok/configure.png)

## Konfigurera en regel för vidarebefordran av händelser {#config-rule}

När alla dataelement har konfigurerats kan du börja skapa regler för vidarebefordran av händelser som avgör när och hur händelser skickas till [!DNL TikTok].

Skapa en ny [regel](../../../ui/managing-resources/rules.md) i egenskapen för vidarebefordran av händelser. Under **[!UICONTROL Actions]** lägger du till en ny åtgärd och anger tillägget till **[!UICONTROL TikTok Web Events API Extension]**. Om du vill skicka Edge Network-händelser till [!DNL TikTok] anger du **[!UICONTROL Action Type]** till **[!UICONTROL Send TikTok Web Events API Event].**

![Åtgärdstypen [!UICONTROL Send TikTok Web Events API Event] som väljs för en [!DNL TikTok]-regel i användargränssnittet för datainsamling.](../../../images/extensions/server/tiktok/select-action.png)

Efter markeringen visas ytterligare kontroller för att ytterligare konfigurera händelsen enligt instruktionerna nedan. När du är klar väljer du **[!UICONTROL Keep Changes]** för att spara regeln.

**[!UICONTROL Web Events and Parameters]**

Webbhändelser och parametrar innehåller allmän information om händelsen. Standardhändelser stöds i alla [!DNL TikTok]-integreringsverktyg och kan användas för att rapportera, optimera för konverteringar och skapa målgrupper.

| Indata | Beskrivning |
| --- | --- |
| Händelsenamn | Namnet på händelsen. Det här är åtgärder med fördefinierade namn skapade av [!DNL TikTok] och är ett obligatoriskt fält. Mer information om händelser som stöds finns i dokumentationen för [[!DNL TikTok] Marketing API](https://business-api.tiktok.com/portal/docs?id=1741601162187777). |
| Händelsetid | Datum-tid som sträng i ISO 8601 eller i formatet `yyyy-MM-dd'T'HH:mm:ss:SSSZ`. Detta är ett obligatoriskt fält. |
| Händelse-ID | Det unika ID som genereras av annonsörer för att ange varje händelse. Det här är ett valfritt fält och används för borttagning av dubbletter. |

{style="table-layout:auto"}

![Avsnittet [!DNL Web Events and Parameters] som visar exempeldata i fälten.](../../../images/extensions/server/tiktok/configure-web-events-parameters.png)

**[!UICONTROL User Context Parameters]**

Parametrar för användarkontext innehåller kundinformation som används för att matcha webbbesökshändelser med [!DNL TikTok] användare. Genom att ta med flera typer av matchande data kan ni öka noggrannheten i målinriktning och optimeringsmodeller.

| Indata | Beskrivning |
| --- | --- |
| IP-adress | Webbläsarens offentliga IP-adress som inte hashats. Stöd ges för IPv4- och IPv6-adresser. Både fullständiga och komprimerade former av IPv6-adresser känns igen. |
| Användaragent | Den icke-hash-kodade användaragenten från användarens enhet. |
| E-post | E-postadress till den kontakt som är associerad med konverteringshändelsen. |
| Telefon | Telefonnumret måste vara i E164-format [+][landskod][riktnummer][local phone number] innan hashning utförs. |
| Cookie-ID | Om du använder Pixel SDK sparas automatiskt en unik identifierare i `_ttp`-cookien, om cookies är aktiverade. Värdet `_ttp` kan extraheras och användas för det här fältet. |
| Externt ID | Alla unika identifierare, till exempel användar-ID:n, externa cookie-ID:n och så vidare, måste hash-kodas med SHA256. |
| TikTok Click ID | `ttclid` som läggs till i URL:en för landningssidan varje gång en annons väljs [!DNL TikTok]. |
| Sidans URL | Sidans URL vid tidpunkten för händelsen. |
| URL för sidreferens | URL för sidreferenten. |

{style="table-layout:auto"}

![Avsnittet [!DNL User Context Parameters] som visar exempeldata i fälten.](../../../images/extensions/server/tiktok/configure-user-context-parameters.png)

**[!UICONTROL Properties Parameters]**

Använd egenskapsparametrarna för att konfigurera ytterligare egenskaper som stöds.

| Indata | Beskrivning |
| --- | --- |
| Pris | Kostnaden för en enstaka artikel. |
| Kvantitet | Antalet artiklar som köpts i händelsen. Detta måste vara ett positivt tal större än 0. |
| Innehållstyp | Värdet `product` eller `product_group` måste tilldelas objektegenskapen content_type, beroende på hur du konfigurerar dataflödet när du konfigurerar produktkatalogen. |
| Innehålls-ID | En unik identifierare för produktartikeln. |
| Innehållskategori | Sidans/produktens kategori. |
| Innehållsnamn | Namn på sidan/produkten. |
| Valuta | Valutan för de artiklar som köps in i händelsen. Detta anges i ISO-4217. |
| Värde | Orderns totala pris. Det här värdet är lika med priset * kvantitet. |
| Beskrivning | En beskrivning av objektet eller sidan. |
| Fråga | Den textsträng som användes för att söka efter en produkt. |
| Status | Status för en order, artikel eller tjänst. Till exempel&quot;skickat&quot;. |

{style="table-layout:auto"}

![Avsnittet [!DNL Properties Parameters] som visar exempeldata i fälten.](../../../images/extensions/server/tiktok/configure-properties-parameters.png)

## Borttagning av händelser {#deduplication}

[!DNL TikTok] pixel måste vara konfigurerad för borttagning av dubbletter om du använder både [!DNL TikTok] pixel SDK och [!DNL TikTok] API-tillägget för webbhändelser för att skicka samma händelser till [!DNL TikTok].

Deduplicering krävs inte om distinkta händelsetyper skickas från klienten och servern utan någon överlappning. Om du vill vara säker på att din rapportering inte påverkas negativt måste du se till att alla enskilda händelser som delas av [!DNL TikTok] pixel-SDK och API-tillägget för [!DNL TikTok]-webbhändelser dedupliceras.

När du skickar delade händelser måste du se till att alla händelser innehåller ett pixel-ID, händelse-ID och namn. Duplicerade händelser som kommer inom fem minuter från varandra sammanfogas. Om datafältet inte fanns med i den första händelsen kombineras det med den efterföljande händelsen. Alla dubbletthändelser som tas emot inom 48 timmar tas bort.

Mer information om den här processen finns i [!DNL TikTok]-dokumentationen om [händelseborttagning](https://ads.tiktok.com/help/article/event-deduplication).

## Nästa steg

I den här guiden beskrivs hur du skickar händelsedata på serversidan till [!DNL TikTok] med API-tillägget för webbhändelser i [!DNL TikTok]. Mer information om funktioner för vidarebefordran av händelser i [!DNL Adobe Experience Platform] finns i [översikten över vidarebefordran av händelser](../../../ui/event-forwarding/overview.md).
