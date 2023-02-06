---
title: Identitetshantering i arbetsflödet för målaktivering
description: Läs om hur identitetsexport hanteras i aktiveringsarbetsflödet, beroende på måltyp
source-git-commit: 6ccf26cbdbbe675d0d731f59cee589d63ca6f8ad
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 0%

---

# Identitetshantering i arbetsflödet för målaktivering

Den här sidan beskriver hur identiteter exporteras till olika måltyper och lär dig hur du hittar vilka identiteter som är tillgängliga för export beroende på mål.

>[!TIP]
>
> Mer information om identiteter, namnutrymmen och definitioner av identitetsrelaterade termer finns i [Översikt över identitetstjänsten](/help/identity-service/home.md).

Varje mål i [katalog](/help/destinations/catalog/overview.md) är något annorlunda, så det finns ingen inställning för en storlek som passar alla för alla mål. Det finns dock några mönster som vägleder konfigurationen av destinationer och deras identitetskrav, vilket beskrivs i avsnitten nedan.

## Filbaserade mål {#file-based}

För [filbaserade mål](/help/destinations/destination-types.md#file-based) (till exempel [!DNL Amazon S3], SFTP, de flesta e-postmarknadsföringsmål som [!DNL Adobe Campaign], [!DNL Oracle Eloqua], [!DNL Salesforce Marketing Cloud]) är identitetsinställningarna i de flesta av dessa mål öppna, vilket innebär att du inte behöver välja någon identitet i [Välj attribut](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes) steg i gruppaktiveringsarbetsflödet.

Om du väljer att lägga till identiteter i din filexport bör du tänka på att det bara är en enda identitet från [identity namespace](/help/identity-service/ui/identity-graph-viewer.md#access-identity-graph-viewer) kan markeras i en export. När du väljer en identitet för export väljs den automatiskt som [obligatoriskt attribut](/help/destinations/ui/activate-batch-profile-destinations.md#mandatory-attributes) och [dedupliceringsnyckel](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-keys).

![En identitet har valts som obligatoriskt attribut och dedupliceringsnyckel.](/help/destinations/assets/how-destinations-work/selected-identity.png)

Som en tillfällig lösning kan du lägga till fler identiteter i exporten om de har importerats till Experience Platform som attribut. Nedan visas ett exempel där e-postadressen för XDM-attributet har valts för export, förutom identitetsnamnutrymmet `Phone_E.164`.

![Exempel på e-postadressattribut som har valts för export.](/help/destinations/assets/how-destinations-work/email-selected.png)

## Exportera en identitet från en identitetskarta jämfört med att exportera en identitet som ett XDM-attribut - skillnaderna {#identity-map-or-attribute}

Antalet exporterade poster kan skilja sig åt beroende på om du väljer att exportera identiteter från identitetskartan eller identiteter som har importerats som attribut till Experience Platform. [Sammanfoga profiler](/help/profile/merge-policies/overview.md) spelar också en viktig roll när det gäller antalet poster som exporteras när du väljer identiteter från identitetskartan.

Tänk dig till exempel att från två olika datauppsättningar har du följande profilfragment som kommer att sammanfogas i en enda kundprofil:

**Profilfragment ett**

| Identitetskarta | Förnamn | Efternamn | E-postattribut |
|---------|----------|---------|--------|
| email1, Loyalty ID1 | John | Doe | e-post 1 |


**Profilfragment två**

| Identitetskarta | Förnamn | Efternamn | E-postattribut |
|---------|----------|---------|--------|
| email2, Loyalty ID1 | John | Doe | e-post 2 |

Den sammanfogade profilen ser ut så här:

| Identitetskarta | Förnamn | Efternamn | E-postattribut |
|---------|----------|---------|--------|
| e-post 1, e-post2, Förmåns-ID1 | John | Doe | e-post 2 |

Exportbeteendet varierar beroende på om du väljer `IdentityMap: Email` eller `xdm: personalEmail.address` för export.

Om en kund aktiverar `IdentityMap: Email`, kommer det att finnas två poster i den exporterade filen, en för e-post1 och en annan för e-post2.

Men om en kund aktiverar `xdm: personalEmail.address`, finns endast e-post2 i posten eftersom e-postattributfältet endast innehåller e-post2. Dessa situationer kan användas vid olika tillfällen då du kanske vill aktivera för alla e-postadresser som du inte har registrerat för en kund, eller bara för den senaste e-postadressen som du inte har registrerat för kunden.

Detta innebär att antalet poster som du exporterar beror på vilka sammanfogningsprinciper du väljer och om du väljer identiteter eller attribut i exporten.

## API-baserade mål för direktuppspelning {#streaming-destinations}

[API-baserade mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destination) inbyggd med [Destination SDK](/help/destinations/destination-sdk/overview.md) (till exempel [!DNL Facebook], [!DNL Google Customer Match], [!DNL Pinterest], [!DNL Braze]och andra) stöder endast specifika ID:n för export. Mer information om vilka identiteter som kan exporteras till respektive mål finns i *identiteter som stöds* i varje måldokumentationssida (se t.ex. [identitetsavsnittet som stöds](/help/destinations/catalog/advertising/pinterest.md) i [!DNL Pinterest] målsida).

Observera dock att du kan använda data från antingen [privata diagram](/help/profile/merge-policies/overview.md#id-stitching) eller från attribut som identiteter. Det innebär att du kan mappa XDM-attribut till det identitetsfält som krävs för målet. Nedan finns ett exempel på [!DNL Pinterest] mål, där XDM-attributet `personalEmail.address` är mappad till den obligatoriska [!DNL Pinterest] identity `pinterest_audience`.

>[!TIP]
>
>När källfältet innehåller ohash-kodade attribut markerar du **[!UICONTROL Apply transformation]** att Experience Platform automatiskt ska hash-koda data vid aktiveringen. Läs mer om **[!UICONTROL Apply transformation]** i [direktuppspelningsmål - självstudiekurs](/help/destinations/ui/activate-segment-streaming-destinations.md#apply-transformation).

![Exempel på e-postadressattribut som har mappats till identitetsfält för Pinterest-mål.](/help/destinations/assets/how-destinations-work/email-mapped-to-identity.png)

### Annonsmål som förlitar sig på cookie-integreringar från tredje part {#third-party-cookie-destinations}

Annonseringsmål som förlitar sig på cookies från tredje part (till exempel: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google DV360], [!DNL Bing], [!DNL The Trade Desk]) kräver inte att kunderna väljer ID i aktiveringsarbetsflödet. För dessa mål, när Experience Platform ställer in ett aktiveringsarbetsflöde, söker automatiskt upp identitetsmatchningstabellen som skapats av [[!UICONTROL Experience Cloud ID service]](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=en) och exporterar alla identiteter som är tillgängliga för en profil och stöds av målet.

Dessa mål kräver att en ID-synkronisering utförs via antingen [!UICONTROL Experience Cloud ID service] eller via [!UICONTROL Experience Platform Web SDK].

Om du använder [!UICONTROL Experience Platform Web SDK] och äldre [!UICONTROL Experience Cloud ID service] är inte implementerat på sidan, måste du se till att dataströmmen för den aktuella webbplatsen är aktiverad för att tillåta synkronisering av tredjeparts-ID, enligt beskrivningen i [konfigurera datastream-dokumentation](/help/edge/datastreams/configure.md#create).

När du konfigurerar ett datastream enligt beskrivningen i den länkade dokumentationen ovan måste du se till att **[!UICONTROL Third Party ID Sync]** reglage är aktiverat. De flesta kunder lämnar `container_id` fältet är tomt (standardvärdet är 0). Du behöver bara ändra det här värdet om din tidigare Audience Manager-implementering använde ett visst behållar-ID (observera dock att detta skulle vara den stora mängden kunder).

>[!NOTE]
>
>De flesta av dessa reklamdestinationer stöds i Audience Manager (dessa destinationstyper kallas i Audience Manager som enhetsbaserade destinationer). Se en [lista över alla enhetsbaserade destinationer i Audience Manager som stöds](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/device-based/device-based-destinations-list.html?lang=en)). Endast ett fåtal är listade i Experience Platform. Mer information om datadelning mellan Experience Platform och Audience Manager finns i avsnittet om [möjliggöra datadelning från Experience Platform till Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#enable-aep-to-aam-data). För närvarande finns det ingen plan för att stödja fler cookie-destinationer från tredje part.

## Företagsmål {#enterprise-destinations}

[Företagsmål](/help/destinations/destination-types.md#streaming-profile-export) ([!DNL Amazon Kinesis], [!DNL Azure Event Hubs], HTTP API) kräver inga specifika ID:n i dataexporten eftersom dessa är utformade för företagsintegrering. Du kan dock exportera identiteter som XDM-attribut eller från identitetskartan om du vill. Visa en [exempel på exporterade data till HTTP-målet](/help/destinations/catalog/streaming/http-destination.md#exported-data), som innehåller både `personalEmail.address` XDM-attribut och identiteter `ECID` och `email_lc_sha256` (hashade e-postadress) från identitetskartan.

## Destinationer för personalisering {#personalization-destinations}

[Destinationer för personalisering (eller kant)](/help/destinations/destination-types.md#edge-personalization-destinations) (till exempel: Adobe Target, [!DNL Custom Personalization]) kräver inget identitetsval i aktiveringsarbetsflödet eftersom integreringen är en profilsökning. Klienten ([!DNL Target], [!DNL Web SDK], eller andra) frågar [[!UICONTROL Edge]](/help/collection/home.md#edge) och hämtar profilinformation som behövs för anpassning på plats.

<!--
![Table with all supported identities](/help/destinations/assets/how-destinations-work/identities-table.png)

-->

## Nästa steg {#next-steps}

När du har läst det här dokumentet vet du nu hur du tar reda på vilka identiteter som stöds eller krävs för enskilda mål. Nu vet du också hur identitetsmarkering fungerar för varje måltyp.

Sedan kan du läsa om [exportinställningar](/help/destinations/how-destinations-work/destinations-configurations.md) för destinationer är vanliga mellan olika måltyper, som kan konfigureras på en enskild målnivå av utvecklare, och vilka inställningar som kan redigeras av användare i aktiveringsarbetsflödet.