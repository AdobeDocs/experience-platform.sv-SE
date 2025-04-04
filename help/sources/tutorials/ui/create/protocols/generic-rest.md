---
keywords: Experience Platform;home;populära topics;Generic REST API
title: Skapa en allmän REST API Source Connection i användargränssnittet
type: Tutorial
description: Lär dig hur du skapar en allmän REST API-källanslutning med Adobe Experience Platform UI.
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 0%

---

# Skapa en [!DNL Generic REST API]-källanslutning i användargränssnittet

>[!NOTE]
>
> Källan [!DNL Generic REST API] är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källöversikt](../../../../home.md#terms-and-conditions).

I den här självstudiekursen beskrivs hur du skapar en [!DNL Generic REST API]-källanslutning med Adobe Experience Platform-användargränssnittet.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Experience Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

### Samla in nödvändiga inloggningsuppgifter

Om du vill få åtkomst till ditt [!DNL Generic REST API]-konto på Experience Platform måste du ange giltiga autentiseringsuppgifter för den autentiseringstyp som du väljer. Allmänt REST API har stöd för både OAuth 2-uppdateringskod och grundläggande autentisering. I följande tabeller finns information om autentiseringsuppgifter för de två autentiseringstyper som stöds.

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

I Experience Platform-gränssnittet väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i [!UICONTROL Sources]. På skärmen [!UICONTROL Catalog] visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också använda sökfältet till att hitta den källa du vill arbeta med.

Under kategorin [!UICONTROL Protocols] väljer du **[!UICONTROL Generic REST API]** och sedan **[!UICONTROL Add data]**.

![katalog](../../../../images/tutorials/create/generic-rest/catalog.png)

Sidan **[!UICONTROL Connect to Generic REST API]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det allmänna REST API-konto som du vill ansluta till och sedan **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/generic-rest/existing.png)

### Nytt konto

Om du skapar ett nytt konto väljer du **[!UICONTROL New account]** och anger sedan ett namn och en alternativbeskrivning för det nya [!DNL Generic REST API]-kontot.

![ny](../../../../images/tutorials/create/generic-rest/new.png)

#### Autentisera med OAuth 2-uppdateringskod

[!DNL Generic REST API] har stöd för både OAuth 2-uppdateringskod och grundläggande autentisering. Om du vill autentisera med en OAuth2-autentisering väljer du **[!UICONTROL OAuth2RefreshCode]**, anger dina OAuth 2-autentiseringsuppgifter och väljer sedan **[!UICONTROL Connect to source]**.

![](../../../../images/tutorials/create/generic-rest/oauth2.png)

#### Autentisera med grundläggande autentisering

Om du vill använda grundläggande autentisering väljer du **[!UICONTROL Basic authentication]**, anger värden, användarnamn och lösenord och väljer sedan **[!UICONTROL Connect to source]**.

![](../../../../images/tutorials/create/generic-rest/basic-authentication.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt allmänna REST API-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till Experience Platform](../../dataflow/protocols.md).
