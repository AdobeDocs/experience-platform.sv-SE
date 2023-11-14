---
keywords: Experience Platform;hem;populära ämnen;Allmänt REST API
title: Skapa en allmän REST API-källanslutning i användargränssnittet
type: Tutorial
description: Lär dig hur du skapar en allmän REST API-källanslutning med Adobe Experience Platform UI.
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 1%

---

# Skapa en [!DNL Generic REST API] källanslutning i användargränssnittet

>[!NOTE]
>
> The [!DNL Generic REST API] källan är i betaversion. Se [Översikt över källor](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder beta-märkta anslutningar.

Den här självstudiekursen innehåller steg för att skapa en [!DNL Generic REST API] källanslutning med Adobe Experience Platform användargränssnitt.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande plattformskomponenter:

* [Källor](../../../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till [!DNL Generic REST API] på Platform måste du ange giltiga autentiseringsuppgifter för den autentiseringstyp som du väljer. Allmänt REST API har stöd för både OAuth 2-uppdateringskod och grundläggande autentisering. I följande tabeller finns information om autentiseringsuppgifter för de två autentiseringstyper som stöds.

#### OAuth 2-uppdateringskod

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Värd | Värd-URL:en för källan som du begär från. Det här värdet är obligatoriskt och kan inte åsidosättas med parameteråsidosättning för begäran. |
| Verifieringstestets URL | (Valfritt) URL:en för auktoriseringstestet används för att validera autentiseringsuppgifter när en basanslutning skapas. Om inget anges kontrolleras autentiseringsuppgifterna automatiskt när du skapar en källanslutning i stället. |
| Klient-ID | (Valfritt) Det klient-ID som är kopplat till ditt användarkonto. |
| Klienthemlighet | (Valfritt) Klienthemligheten som är kopplad till ditt användarkonto. |
| Åtkomsttoken | Den primära autentiseringsreferens som används för att komma åt programmet. Åtkomsttoken representerar behörigheten för ditt program, för åtkomst till vissa aspekter av en användares data. Det här värdet är obligatoriskt och kan inte åsidosättas med parameteråsidosättning för begäran. |
| Uppdatera token | (Valfritt) En token som används för att generera en ny åtkomsttoken när åtkomsttoken har upphört att gälla. |
| Åtkomsttoken-URL | (Valfritt) URL-slutpunkten som används för att hämta din åtkomsttoken. |
| Åsidosättning av begärandeparameter | (Valfritt) En egenskap som gör att du kan ange vilka autentiseringsparametrar som ska åsidosättas. |


#### Grundläggande autentisering

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Värd | Värd-URL:en för källan som du begär från. |
| Användarnamn | Användarnamnet som motsvarar ditt användarkonto. |
| Lösenord | Lösenordet som motsvarar ditt användarkonto. |

## Anslut ditt allmänna REST API-konto

Välj **[!UICONTROL Sources]** från vänster navigering för att komma åt [!UICONTROL Sources] arbetsyta. The [!UICONTROL Catalog] I visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också använda sökfältet till att hitta den källa du vill arbeta med.

Under [!UICONTROL Protocols] kategori, välj **[!UICONTROL Generic REST API]** och sedan **[!UICONTROL Add data]**.

![katalog](../../../../images/tutorials/create/generic-rest/catalog.png)

The **[!UICONTROL Connect to Generic REST API]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det allmänna REST API-konto som du vill ansluta till och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/generic-rest/existing.png)

### Nytt konto

Om du skapar ett nytt konto väljer du **[!UICONTROL New account]** och ange sedan ett namn och en alternativbeskrivning för ditt nya [!DNL Generic REST API] konto.

![new](../../../../images/tutorials/create/generic-rest/new.png)

#### Autentisera med OAuth 2-uppdateringskod

[!DNL Generic REST API] har stöd för både OAuth 2-uppdateringskod och grundläggande autentisering. Om du vill autentisera med en OAuth2-autentisering väljer du **[!UICONTROL OAuth2RefreshCode]**, ange dina OAuth 2-autentiseringsuppgifter och välj sedan **[!UICONTROL Connect to source]**.

![](../../../../images/tutorials/create/generic-rest/oauth2.png)

#### Autentisera med grundläggande autentisering

Om du vill använda grundläggande autentisering väljer du **[!UICONTROL Basic authentication]**, ange värden, användarnamn och lösenord och välj **[!UICONTROL Connect to source]**.

![](../../../../images/tutorials/create/generic-rest/basic-authentication.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt allmänna REST API-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till plattformen](../../dataflow/protocols.md).
