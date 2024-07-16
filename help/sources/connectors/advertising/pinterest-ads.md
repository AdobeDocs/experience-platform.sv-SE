---
keywords: Experience Platform;hemmabruk;populära ämnen;Pinterest Ads;
title: Pinterest Ads Source - översikt
description: Lär dig hur du ansluter Pinterest Ads till Adobe Experience Platform med hjälp av API:er eller användargränssnittet.
badge: Beta
hide: true
hidefromtoc: true
exl-id: 8edbcb26-0a18-47f1-8012-ca209d99d7a6
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 0%

---

# [!DNL Pinterest Ads]

>[!NOTE]
>
>Källan [!DNL Pinterest Ads] är i betaversion. Läs [Källöversikt](../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade anslutningar.

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform stöder inmatning av data från ett annonssystem från tredje part. Stöd för annonsleverantörer inkluderar [!DNL Pinterest Ads].

[[!DNL Pinterest]](https://www.pinterest.com) är en motor för visuell identifiering som används för att hitta recept, heminredning, stilinspiration och andra idéer på webben. Dessa visas i liten skala med bilder, animerad GIF och videor i pinboard-format. Med [[!DNL Pinterest Ads]](https://ads.pinterest.com/) kan du utöka din verksamhet och nå 400 miljoner personer med [!DNL Pinterest].

Med [!DNL Pinterest Ads] kan du nå användare via riktade annonser för att identifiera och köpa dina produkter. Pins från [!DNL Pinterest Ads] sponsras för att få extra exponering i relevanta sökresultat. Användare som prenumererar på [!DNL Pinterest Business] kan välja att befordra befintliga nålar med bästa prestanda, skapa en ny bild eller video eller till och med befordra en bild som har fästs från en webbplats. [!DNL Pinterest Ads] erbjuder flera annonsformat som hjälper dig att uppnå dina specifika kampanjmål.

## [!DNL Pinterest] API:er {#pinterest-apis}

[!DNL Pinterest Ads]-källan utnyttjar [!DNL Pinterest]-API:erna för att hämta dina [!DNL Pinterest Ads]-data, tillsammans med alla prestanda och mått. Följande API-slutpunkter stöds:

* [Kampanjanalys](https://developers.pinterest.com/docs/api/v5/#operation/campaigns/analytics)
* [Lägg till gruppanalys](https://developers.pinterest.com/docs/api/v5/#operation/ad_groups/analytics)
* [Annonsanalys](https://developers.pinterest.com/docs/api/v5/#operation/ads/analytics)

Använd [!DNL Pinterest Ads]-källan för att hämta data från [!DNL Pinterest] till Experience Platform, där du sedan kan köra dataanalyser. Data returneras från och med datumet för intag i ett föråldrat intervall på 90 dagar. [!DNL Pinterest Ads] använder innehavartoken som autentiseringsmekanism för att kommunicera med [!DNL Pinterest] API:er.

## Förhandskrav {#prerequisites}

Det första steget för att skapa en [!DNL Pinterest Ads]-källanslutning är att se till att du har ett Pinterest-utvecklarkonto. Om du inte redan har en, gå till [registreringssidan](https://www.pinterest.com/business/create/?next=https://developers.pinterest.com/account-setup/) och registrera dig och skapa ditt konto.

### Konfigurera appen [!DNL Pinterest] och generera åtkomsttoken {#create-app-and-generate-token}

>[!IMPORTANT]
>
>Vi rekommenderar att du använder API:erna för [!DNL Pinterest] för att generera din åtkomsttoken, eftersom genereringen av din åtkomsttoken i gränssnittet ger begränsad åtkomst. Genom användargränssnittet kan du bara komma åt följande scope: `pins:read`, `boards:read` och `user_accounts:read`. Den här begränsningen är inte tillräcklig för användning med analysslutpunkterna i API:t [!DNL Pinterest].

Läs [!DNL Pinterest]-handböckerna om hur du konfigurerar din app](https://developers.pinterest.com/docs/getting-started/set-up-app/) och [autentiserar med OAuth 2.0](https://developers.pinterest.com/docs/getting-started/authentication/) om du vill generera din åtkomsttoken.[

### Samla in nödvändiga inloggningsuppgifter {#gather-required-credentials}

För att kunna ansluta [!DNL Pinterest Ads] till plattformen måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Åtkomsttoken | Åtkomsttoken [!DNL Pinterest Ads] för ditt användarkonto. Användarkontot för token måste antingen vara ägare till det angivna [!DNL Pinterest Ad]-kontot eller ha en av de nödvändiga rollerna som tilldelats dem via Business Access: Admin, Analyst eller Campaign Manager. Mer information om åtkomsttoken finns i [[!DNL Pinterest] guiden om hur du genererar åtkomsttoken](https://developers.pinterest.com/docs/getting-started/set-up-app/). |
| ID för annonskonto | Det relaterade [!DNL Pinterest Ads]-annonskontots ID för din affärsenhet. Mer information om hur du hämtar ditt ID för annonskonto. Besök [[!DNL Pinterest] guiden om hur du söker efter ID:n i annonshanteraren](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager). |
| Kampanj-, annonsgrupp- eller annons-ID | ID:n för `campaign`, `ad group` eller `ad` som motsvarar ditt annonskonto-ID. Om du vill få de ID:n som krävs går du till sidan [!DNL Pinterest] för **Pinterest Business Hub** > **Ad Account Summary** > **Campaigns** / **Ad Groups** / **Ads** och kopierar ID:n som krävs precis under namnen på dem. |

>[!NOTE]
>
>API:t [!DNL Pinterest] innehåller enskilda API:er för att hämta data som är associerade med varje ID. Därför behöver du bara skicka motsvarande ID:n för den ID-typ som du är intresserad av.

## Guardrails {#guardrails}

I följande avsnitt finns information om datavärdesutkast för [!DNL Pinterest].

### [!DNL Pinterest] datumintervall {#pinterest-date-range}

API:t [!DNL Pinterest] har stöd för både en `start_date`- och en `end_date`-parameter för att hämta analysdata mellan ett visst datumintervall.

* `start_date` får inte vara mer än 90 dagar före dagens datum.
* `end_date` får inte vara längre än 90 dagar efter `start_date`.

När du schemalägger dataflödet måste du konfigurera någon av följande inställningar för frekvens och intervall:

| Frekvens | Intervall |
| --- | --- |
| `Day` | 1 |
| `Hour` | 24 |

Om till exempel intag är inställt den 15 mars 2023 med en frekvens- och intervallinställning som är konfigurerad till `Day=1` eller `Hour=24` hämtar [!DNL Pinterest]-API:t bara data från den 15 december 2022 eftersom beräkningen är inaktuell i 90 dagar.

### [!DNL Pinterest] tidsintervall {#pinterest-time-range}

API:t [!DNL Pinterest] stöder olika typer av tidsgranularitet för hur data kan hämtas:

| Tidsgranularitet | Beskrivning |
| --- | --- |
| **TOTALT** | Datamätningarna aggregeras över ett angivet datumintervall. |
| **DAG** | Datamätningarna delas upp dagligen. |
| **TIMME** | Datamätningarna delas upp per timme. |
| **VECKA** | Uppgifterna delas upp på veckobasis. |
| **MÅNADSVIS** | Uppgifterna delas upp på månadsbasis. |

För Platform är källan [!DNL Pinterest Ads] internt konfigurerad till `Day`, vilket innebär att data samlas in dagligen. Om du t.ex. använder `impressions recorded` som mätvärde, eftersom granulariteten är konfigurerad som `DAY`, får du `xx` avtryck på `day 1`, `yy` avtryck på `day 2` och så vidare.

>[!IMPORTANT]
>
>Pinterest sätter en hastighetsgräns på 1 000 API-anrop dagligen till sitt API för att läsa information från annonser, annonsgrupper eller annonskampanjer. Mer information om vilka tariffgränser som gäller för underliggande API-anrop finns i [[!DNL Pinterest] dokumentationen om tariffgränser](https://developers.pinterest.com/docs/reference/ratelimits/).

## Anslut [!DNL Pinterest Ads] till plattformen {#connect-to-platform}

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Pinterest Ads] till plattformen med API:er eller användargränssnittet:

### Anslut [!DNL Pinterest Ads] till plattformen med API:er {#connect-to-platform-using-api}

* [Skapa en Pinterest-basanslutning med API:t för Flow Service](../../tutorials/api/create/advertising/pinterest-ads.md)
* [Utforska datatabeller med API:t för Flow Service](../../tutorials/api/explore/tabular.md)
* [Skapa ett dataflöde för en annonskälla med API:t för Flow Service](../../tutorials/api/collect/advertising.md)

### Anslut [!DNL Pinterest Ads] till plattformen med användargränssnittet {#connect-to-platform-using-ui}

* [Skapa en Pinterest-källanslutning i användargränssnittet](../../tutorials/ui/create/advertising/pinterest-ads.md)
* [Skapa ett dataflöde för en anslutning till en annonskälla i användargränssnittet](../../tutorials/ui/dataflow/advertising.md)
