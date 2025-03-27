---
title: Google Ads Source - översikt
description: Lär dig hur du ansluter Google Ads till Adobe Experience Platform med hjälp av API:er eller användargränssnittet.
exl-id: 1f6257e0-213c-4723-a240-511c11c5833c
source-git-commit: ac90eea69f493bf944a8f9920426a48d62faaa6c
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 0%

---

# [!DNL Google Ads]-källa

>[!NOTE]
>
>Källan [!DNL Google Ads] är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källöversikt](../../home.md#terms-and-conditions).

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform stöder inmatning av data från ett annonssystem från tredje part. Stöd för annonsleverantörer inkluderar [!DNL Google Ads].

## Förhandskrav {#prerequisites}

### IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress tillåtelselista](../../ip-address-allow-list.md).

### Konfigurera behörigheter i Experience Platform

Du måste ha både behörighet **[!UICONTROL View Sources]** och behörighet **[!UICONTROL Manage Sources]** aktiverat för ditt konto för att kunna ansluta ditt [!DNL Google Ads]-konto till Experience Platform. Kontakta produktadministratören för att få den behörighet som krävs. Mer information finns i [användargränssnittsguiden för åtkomstkontroll](../../../access-control/ui/overview.md).

### Samla in nödvändiga inloggningsuppgifter

Du måste ange lämpliga värden för följande autentiseringsuppgifter för att kunna ansluta ditt [!DNL Google Ads]-konto till Experience Platform.

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `clientCustomerId` | Klientens kund-ID är det kontonummer som motsvarar det [!DNL Google Ads]-klientkonto som du vill hantera med [!DNL Google Ads] API. Detta ID följer mallen för `123-456-7890`. |
| `loginCustomerId` | Inloggningskund-ID är det kontonummer som motsvarar ditt [!DNL Google Ads]-hanterarkonto och används för att hämta rapportdata från en viss operativkund. Mer information om användar-ID för inloggning finns i [[!DNL Google Ads] API-dokumentationen](https://developers.google.com/search-ads/reporting/concepts/login-customer-id). |
| `developerToken` | Utvecklartoken ger dig åtkomst till API:t [!DNL Google Ads]. Du kan använda samma utvecklartoken för att göra förfrågningar mot alla dina [!DNL Google Ads]-konton. Hämta din utvecklartoken genom att [logga in på ditt chefskonto](https://ads.google.com/home/tools/manager-accounts/) och sedan navigera till sidan [!DNL API Center]. |
| `refreshToken` | Uppdateringstoken är en del av [!DNL OAuth2]-autentiseringen. Med denna token kan du återskapa dina åtkomsttoken när de har upphört att gälla. |
| `clientId` | Klient-ID används tillsammans med klienthemligheten som en del av [!DNL OAuth2]-autentiseringen. Tillsammans gör klient-ID och klienthemlighet det möjligt för programmet att agera för ditt kontos räkning genom att identifiera ditt program för [!DNL Google]. |
| `clientSecret` | Klienthemligheten används tillsammans med klient-ID som en del av [!DNL OAuth2]-autentiseringen. Tillsammans gör klient-ID och klienthemlighet det möjligt för programmet att agera för ditt kontos räkning genom att identifiera ditt program för [!DNL Google]. |
| `googleAdsApiVersion` | Den aktuella API-versionen som stöds av [!DNL Google Ads]. Den senaste versionen är `v18`, men den senaste versionen som stöds på Experience Platform är `v17`. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Google Ads] är: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. Det här värdet krävs om du ansluter ditt [!DNL Google Ads]-konto med API:t [!DNL Flow Service]. |

## Anslut [!DNL Google Ads] till Experience Platform

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Google Ads] till Experience Platform med API:er eller användargränssnittet:

### Använda API:er

* [Skapa en Google Ads-basanslutning med API:t för Flow Service](../../tutorials/api/create/advertising/ads.md)
* [Utforska datatabeller med API:t för Flow Service](../../tutorials/api/explore/tabular.md)
* [Skapa ett dataflöde för en annonskälla med API:t för Flow Service](../../tutorials/api/collect/advertising.md)

### Använda gränssnittet

* [Skapa en Google Ads-källanslutning i användargränssnittet](../../tutorials/ui/create/advertising/ads.md)
* [Skapa ett dataflöde för en anslutning till en annonskälla i användargränssnittet](../../tutorials/ui/dataflow/advertising.md)
