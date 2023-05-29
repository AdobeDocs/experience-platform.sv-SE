---
keywords: Experience Platform;hemmabruk;populära ämnen;Pinterest Ads;
title: Pinterest Ads Source Overview
description: Lär dig hur du ansluter Pinterest Ads till Adobe Experience Platform med hjälp av API:er eller användargränssnittet.
badge: Beta
hide: true
hidefromtoc: true
exl-id: 8edbcb26-0a18-47f1-8012-ca209d99d7a6
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 0%

---

# [!DNL Pinterest Ads]

>[!NOTE]
>
>The [!DNL Pinterest Ads] källan är i betaversion. Läs [Översikt över källor](../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder beta-märkta anslutningar.

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform stöder inmatning av data från ett annonssystem från tredje part. Stöd för annonsleverantörer innefattar [!DNL Pinterest Ads].

[[!DNL Pinterest]](https://www.pinterest.com) är en motor för visuell identifiering som används för att hitta recept, heminredning, stilinspiration och andra idéer på webben. Dessa visas i liten skala med bilder, animerad GIF och videor i pinboard-format. [[!DNL Pinterest Ads]](https://ads.pinterest.com/) kan ni utöka verksamheten och nå 400 miljoner människor med [!DNL Pinterest].

Med [!DNL Pinterest Ads]kan ni nå ut till användarna via riktade annonser för att identifiera och köpa era produkter. Fäst från [!DNL Pinterest Ads] sponsras för att få extra exponering i relevanta sökresultat. Användare prenumererar på [!DNL Pinterest Business] kan välja att befordra befintliga nålar med bästa prestanda, skapa en ny bild eller video eller till och med befordra en bild som har fästs från en webbplats. [!DNL Pinterest Ads] erbjuder flera annonsformat som hjälper er att uppnå era specifika kampanjmål.

## [!DNL Pinterest] API:er {#pinterest-apis}

The [!DNL Pinterest Ads] källa utnyttjar [!DNL Pinterest] API:er för att hämta [!DNL Pinterest Ads] data, tillsammans med alla prestanda och mätvärden. Följande API-slutpunkter stöds:

* [Kampanjanalys](https://developers.pinterest.com/docs/api/v5/#operation/campaigns/analytics)
* [Annonsgruppsanalys](https://developers.pinterest.com/docs/api/v5/#operation/ad_groups/analytics)
* [Annonsanalys](https://developers.pinterest.com/docs/api/v5/#operation/ads/analytics)

Använd [!DNL Pinterest Ads] källa att hämta data från [!DNL Pinterest] till Experience Platform, där ni sedan kan utföra dataanalys. Data returneras från och med datumet för intag i ett föråldrat intervall på 90 dagar. [!DNL Pinterest Ads] använder lagervariabler som en autentiseringsmekanism för att kommunicera med [!DNL Pinterest] API:er.

## Förutsättningar {#prerequisites}

Det första steget i att skapa en [!DNL Pinterest Ads] måste du vara säker på att du har ett Pinterest-utvecklarkonto. Om du inte redan har en går du till [registrera dig](https://www.pinterest.com/business/create/?next=https://developers.pinterest.com/account-setup/) för att registrera och skapa ditt konto.

### Inställningar [!DNL Pinterest] app och generera åtkomsttoken {#create-app-and-generate-token}

>[!IMPORTANT]
>
>Det rekommenderas att du använder [!DNL Pinterest] API:er som genererar din åtkomsttoken eftersom genereringen av din åtkomsttoken i gränssnittet ger begränsad åtkomst. Genom användargränssnittet kan du bara komma åt följande scope: `pins:read`, `boards:read` och `user_accounts:read`. Den här begränsningen är inte lämplig för användning med analysens slutpunkter i [!DNL Pinterest] API.

Om du vill generera en åtkomsttoken läser du [!DNL Pinterest] stödlinjer på [konfigurera din app](https://developers.pinterest.com/docs/getting-started/set-up-app/) och [autentisera med OAuth 2.0](https://developers.pinterest.com/docs/getting-started/authentication/).

### Samla in nödvändiga inloggningsuppgifter {#gather-required-credentials}

För att kunna ansluta [!DNL Pinterest Ads] till Platform måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Åtkomsttoken | The [!DNL Pinterest Ads] åtkomsttoken för ditt användarkonto. Token-användarkontot måste antingen vara ägare av det angivna [!DNL Pinterest Ad] kontot eller har en av de nödvändiga roller som de tilldelats via Business Access: Administratör, analytiker eller kampanjchef. Mer information om åtkomsttoken finns i [[!DNL Pinterest] guide om hur du genererar din åtkomsttoken](https://developers.pinterest.com/docs/getting-started/set-up-app/). |
| ID för annonskonto | Den relaterade [!DNL Pinterest Ads] annonskonto-ID för din affärsenhet. Mer information om hur du hämtar ditt ID för annonskonto. Besök [[!DNL Pinterest] guide för att hitta ID:n i Ads Manager](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager). |
| Kampanj-, annonsgrupp- eller annons-ID | The `campaign`, `ad group`, eller `ad` ID:n som motsvarar ditt annonskonto-ID. Navigera till [!DNL Pinterest] sida för **Pinterest Business Hub** > **Översikt över annonskonto** > **Kampanjer** / **Annonsgrupper** / **Annonser** och kopiera de ID:n som krävs precis under namnen. |

>[!NOTE]
>
>The [!DNL Pinterest] API innehåller enskilda API:er för att hämta data som är kopplade till varje ID. Därför behöver du bara skicka motsvarande ID:n för den ID-typ som du är intresserad av.

## Guardrails {#guardrails}

I följande avsnitt finns information om säkerhetsutkast för data för [!DNL Pinterest].

### [!DNL Pinterest] datumintervall {#pinterest-date-range}

The [!DNL Pinterest] API har stöd för båda `start_date` och `end_date` parameter för att hämta analysdata mellan ett visst datumintervall.

* The `start_date` kan inte vara mer än 90 dagar före aktuellt datum.
* The `end_date` får inte vara mer än 90 dagar efter `start_date`.

När du schemalägger dataflödet måste du konfigurera någon av följande inställningar för frekvens och intervall:

| Frekvens | Intervall |
| --- | --- |
| `Day` | 1 |
| `Hour` | 24 |

Om t.ex. intag är inställt den 15 mars 2023 med en frekvens- och intervallinställning konfigurerad till `Day=1` eller `Hour=24`och sedan [!DNL Pinterest] API hämtar bara data från den 15 december 2022 eftersom beräkningen är inaktuell i 90 dagar.

### [!DNL Pinterest] tidsintervall {#pinterest-time-range}

The [!DNL Pinterest] API har stöd för olika typer av tidsgranularitet för hur data kan hämtas:

| Tidsgranularitet | Beskrivning |
| --- | --- |
| **TOTALT** | Datamätningarna aggregeras över ett angivet datumintervall. |
| **DAG** | Datamätningarna delas upp dagligen. |
| **TIMME** | Datamätningarna delas upp per timme. |
| **VECKA** | Uppgifterna delas upp varje vecka. |
| **MÅNADSVIS** | Uppgifterna delas upp på månadsbasis. |

För Platform [!DNL Pinterest Ads] källan är internt konfigurerad till `Day`, vilket innebär att data samlas in dagligen. Använd till exempel `impressions recorded` som ett mått eftersom granulariteten är konfigurerad som en `DAY`får du `xx` intryck på `day 1`, `yy` intryck på `day 2` och så vidare.

>[!IMPORTANT]
>
>Pinterest sätter en hastighetsgräns på 1 000 API-anrop dagligen till sitt API för att läsa information från annonser, annonsgrupper eller annonskampanjer. Information om vilka tariffgränser som gäller för underliggande API-anrop finns i [[!DNL Pinterest] dokumentation om avgiftsgränser](https://developers.pinterest.com/docs/reference/ratelimits/).

## Anslut [!DNL Pinterest Ads] till plattform {#connect-to-platform}

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Pinterest Ads] till Plattform med API:er eller användargränssnittet:

### Anslut [!DNL Pinterest Ads] till plattform med API:er {#connect-to-platform-using-api}

* [Skapa en Pinterest-basanslutning med API:t för Flow Service](../../tutorials/api/create/advertising/pinterest-ads.md)
* [Utforska datatabeller med API:t för Flow Service](../../tutorials/api/explore/tabular.md)
* [Skapa ett dataflöde för en annonskälla med API:t för Flow Service](../../tutorials/api/collect/advertising.md)

### Anslut [!DNL Pinterest Ads] till plattform med användargränssnittet {#connect-to-platform-using-ui}

* [Skapa en Pinterest-källanslutning i användargränssnittet](../../tutorials/ui/create/advertising/pinterest-ads.md)
* [Skapa ett dataflöde för en anslutning till en annonskälla i användargränssnittet](../../tutorials/ui/dataflow/advertising.md)
