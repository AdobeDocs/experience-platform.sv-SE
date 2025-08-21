---
title: Azure Blob Source Connector - översikt
description: Lär dig hur du ansluter ditt Azure Blob-konto till Experience Platform
exl-id: 62adc74f-3570-42c7-9ae6-3ddbc09eccc7
source-git-commit: 8e932a25026bef2b785cfddfb8b668b1dd47eb0d
workflow-type: tm+mt
source-wordcount: '1021'
ht-degree: 0%

---

# [!DNL Azure Blob Storage]-källa

[!DNL Azure Blob Storage] är en molnbaserad objektlagringstjänst som tillhandahålls av [!DNL Microsoft Azure]. Den är utformad för att lagra stora mängder ostrukturerade data, till exempel text, bilder, videor, säkerhetskopior och loggar. Du kan använda [!DNL Azure Blob Storage] för att lagra och hantera stora mängder ostrukturerade data, till exempel dokument, bilder, videor och ljudfiler. Det är idealiskt för säkerhetskopiering och arkivering av data, stöd för katastrofåterställning och hantering av stora datamängder för analys.

Använd källan [!DNL Azure Blob Storage] för att ansluta ditt konto och importera data från [!DNL Azure Blob Storage] till Adobe Experience Platform.

## Förhandskrav {#prerequisites}

Läs följande avsnitt för att slutföra kravkonfigurationen innan du ansluter ditt [!DNL Azure Blob Storage]-konto till Experience Platform.

### IP-adress tillåtelselista

Du måste lägga till regionspecifika IP-adresser i tillåtelselista innan du kan ansluta dina källor till Experience Platform. Mer information finns i guiden [tillåtslista IP-adresser för att ansluta till Experience Platform](../../ip-address-allow-list.md).

>[!IMPORTANT]
>
>Källan [!DNL Azure Blob] stöder inte anslutning mellan flera regioner och Experience Platform. Om din [!DNL Azure]-instans använder samma nätverksregion som Experience Platform går det inte att upprätta någon anslutning till Experience Platform-källor. För närvarande stöds bara anslutning mellan regioner.

### Namnbegränsningar för filer och kataloger

Nedan följer en lista över begränsningar som du måste ta hänsyn till när du namnger molnlagringsfilen eller -katalogen.

- Katalog- och filkomponentnamn får inte innehålla fler än 255 tecken.
- Katalog- och filnamn får inte sluta med ett snedstreck (`/`). Den tas bort automatiskt om den anges.
- Följande reserverade URL-tecken måste ha escape-konverterats: `! ' ( ) ; @ & = + $ , % # [ ]`
- Följande tecken tillåts inte: `" \ / : | < > * ?`.
- Ogiltiga URL-sökvägstecken tillåts inte. Kodpunkter som `\uE000` är inte giltiga Unicode-tecken, men de är giltiga i NTFS-filnamn. Dessutom tillåts inte vissa ASCII- eller Unicode-tecken, som kontrolltecken (0x00 till 0x1F, \u0081 osv.). Information om regler som styr Unicode-strängar i HTTP/1.1 finns i [RFC 2616, Section 2.2: Basic Rules](https://www.ietf.org/rfc/rfc2616.txt) och [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Följande filnamn tillåts inte: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, punkttecken (.) och två punkttecken (. .).

### Autentisera [!DNL Azure Blob Storage] till Experience Platform {#authentication}

Du kan ansluta ditt [!DNL Azure Blob Storage]-konto till Experience Platform med följande autentiseringstyper:

- **Verifiering av kontonyckel**: Lagringskontots åtkomstnyckel används för att autentisera och ansluta till ditt [!DNL Azure Blob Storage]-konto.
- **Delad åtkomstsignatur (SAS)**: Använder en SAS-URI för att ge delegerad, tidsbegränsad åtkomst till resurser i ditt [!DNL Azure Blob Storage]-konto.
- **Tjänsthuvudbaserad autentisering**: Använder ett Azure Active Directory-tjänstens huvudnamn (AAD) (klient-ID och hemlighet) för att autentisera på ditt Azure Blob Storage-konto på ett säkert sätt.

>[!BEGINTABS]

>[!TAB Autentisering av kontonyckel]

Ange värden för följande autentiseringsuppgifter för att ansluta ditt [!DNL Azure Blob Storage]-konto till Experience Platform med autentisering av kontonycklar.

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `connectionString` | Anslutningssträngen [!DNL Azure Blob Storage] för ditt lagringskonto. Strängen innehåller den information som krävs för att autentisera och ansluta till din [!DNL Azure Blob Storage]-instans. Exempelformat: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY};EndpointSuffix=core.windows.net` |
| `container` | Namnet på behållaren [!DNL Azure Blob Storage] där dina datafiler lagras. En behållare organiserar en uppsättning bloggar som liknar en katalog i ett filsystem. |
| `folderPath` | Sökvägen inom den angivna behållaren där filerna finns. Detta är en valfri underkatalogsökväg (virtuell mapp) inuti behållaren. Om inget anges används behållarens rot. |
| `connectionSpec.id` | Anslutningens spec-ID returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningens spec-ID för [!DNL Azure Blob Storage] är `4c10e202-c428-4796-9208-5f1f5732b1cf`. **Obs!**: Den här autentiseringsuppgiften krävs bara vid anslutning via [!DNL Flow Service] API. |

Läs den officiella [!DNL Azure Blob Storage]autentiseringsguiden för Microsoft Azure[ om du vill veta mer om hur du använder kontonyckelautentisering med ](https://learn.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage?tabs=data-factory#account-key-authentication).

>[!TAB Delad åtkomstsignatur]

Ange värden för följande autentiseringsuppgifter för att ansluta ditt [!DNL Azure Blob Storage]-konto till Experience Platform med signatur för delad åtkomst.

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `SasURI` | Den URI för signatur för delad åtkomst som du kan använda som en alternativ autentiseringstyp för att ansluta ditt konto. SAS URI-mönstret är: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}`. Mer information finns i det här [!DNL Azure]-dokumentet om [URI:er för delad åtkomst](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| `container` | Namnet på behållaren [!DNL Azure Blob Storage] där dina datafiler lagras. En behållare organiserar en uppsättning bloggar som liknar en katalog i ett filsystem. |
| `folderPath` | Sökvägen inom den angivna behållaren där filerna finns. Detta är en valfri underkatalogsökväg (virtuell mapp) inuti behållaren. Om inget anges används behållarens rot. |
| `connectionSpec.id` | Anslutningens spec-ID returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningens spec-ID för [!DNL Azure Blob Storage] är `4c10e202-c428-4796-9208-5f1f5732b1cf`. **Obs!**: Den här autentiseringsuppgiften krävs bara vid anslutning via [!DNL Flow Service] API. |

Läs den officiella [!DNL Azure Blob Storage]autentiseringsguiden för Microsoft Azure[ om du vill veta mer om hur du använder signaturen för delad åtkomst med ](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication).

>[!TAB Tjänstens huvudbaserade autentisering]

Ange värden för följande autentiseringsuppgifter för att ansluta ditt [!DNL Azure Blob Storage]-konto till Experience Platform med huvudbaserad autentisering.

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `serviceEndpoint` | Slutpunkts-URL för ditt [!DNL Azure Blob Storage]-konto. Vanligtvis i formatet: `https://{ACCOUNT_NAME}.blob.core.windows.net`. |
| `accountKind` | Typen för ditt [!DNL Azure Blob Storage]-konto. Vanliga värden är `Storage` (allmänt syfte V1), `StorageV2` (allmänt syfte V2), `BlobStorage` och `BlockBlobStorage`. |
| `servicePrincipalId` | Klient-/program-ID för Azure Active Directory-tjänstens huvudnamn (AAD) som används för autentisering. |
| `servicePrincipalKey` | Klienthemligheten eller lösenordet som är associerat med Azure-tjänstens huvudnamn. |
| `tenant` | Klient-ID för Azure Active Directory (AAD) där tjänstens huvudnamn är registrerat. |
| `container` | Namnet på Azure Blob Storage-behållaren där dina datafiler lagras. |
| `folderPath` | Sökvägen inom den angivna behållaren där filerna finns. Detta är en valfri underkatalogsökväg (virtuell mapp) inuti behållaren. Om inget anges används behållarens rot. |
| `connectionSpec.id` | Anslutningens spec-ID returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningens spec-ID för Azure Blob Storage är `4c10e202-c428-4796-9208-5f1f5732b1cf`. **Obs!**: Den här autentiseringsuppgiften krävs bara vid anslutning via [!DNL Flow Service] API. |

Läs den officiella [!DNL Azure Blob Storage]autentiseringsguiden för Microsoft Azure[ om du vill veta mer om hur du använder tjänstens huvudbaserade autentisering med ](https://learn.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage?tabs=data-factory#service-principal-authentication).

>[!ENDTABS]

## Anslut [!DNL Azure Blob Storage] till [!DNL Experience Platform]

Dokumentationen nedan innehåller information om hur du ansluter Azure Blob till Adobe Experience Platform med API:er eller användargränssnittet:

### Använda API:er

- [Anslut [!DNL Azure Blob Storage] till Experience Platform](../../tutorials/api/create/cloud-storage/blob.md)
- [Utforska datastrukturen och innehållet i en molnlagringskälla med API:t för Flow Service](../../tutorials/api/explore/cloud-storage.md)
- [Skapa ett dataflöde för en molnlagringskälla med API:t för Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Använda gränssnittet

- [Anslut [!DNL Azure Blob Storage] till Experience Platform](../../tutorials/ui/create/cloud-storage/blob.md)
- [Skapa ett dataflöde för en molnlagringsanslutning i användargränssnittet](../../tutorials/ui/dataflow/batch/cloud-storage.md)
