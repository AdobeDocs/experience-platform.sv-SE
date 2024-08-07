---
solution: Experience Platform
title: API-migreringsguide för molnlagringsmål
description: Lär dig mer om förändringarna i arbetsflödet för att aktivera molnlagringsmål som en del av migreringen till de nya målkorten för molnlagring med ytterligare funktioner.
type: Tutorial
exl-id: 4acaf718-794e-43a3-b8f0-9b19177a2bc0
source-git-commit: 4b9e7c22282a5531f2f25f3d225249e4eb0e178e
workflow-type: tm+mt
source-wordcount: '1334'
ht-degree: 0%

---

# API-migreringsguide för molnlagringsmål

>[!IMPORTANT]
>
>* Funktionerna som beskrivs på den här sidan är tillgängliga för kunder som har köpt paketen Real-Time CDP Prime och Ultimate. Kontakta din Adobe-representant om du vill ha mer information.

## Migreringskontext {#migration-context}

Från och med [oktober 2022](/help/release-notes/2022/october-2022.md#new-or-updated-destinations) kan du använda de nya filexportfunktionerna för att få tillgång till förbättrade anpassningsfunktioner när du exporterar filer från Experience Platform:

* Ytterligare [namngivningsalternativ](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).
* Möjlighet att ange anpassade filhuvuden i de exporterade filerna via det [nya mappningssteget](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* Möjlighet att välja [filtypen](/help/destinations/ui/connect-destination.md#file-formatting-and-compression-options) för den exporterade filen.
* Möjlighet att [anpassa formateringen för exporterade CSV-datafiler](/help/destinations/ui/batch-destinations-file-formatting-options.md).

Den här funktionaliteten stöds av de betolmolnlagringskort som anges nedan:

* [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

<!--

Commenting out the three net new cloud storage destinations

* [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)

-->

Observera att du för närvarande kan se två målkort sida vid sida för de tre Experience Platform. Nedan visas de [!DNL Amazon S3] gamla och nya destinationerna. I samtliga fall är de kort som har markerats med **Beta** de nya målkorten.

![Bild av de två Amazon S3-målkorten i en sida vid sida-vy.](../assets/catalog/cloud-storage/amazon-s3/two-amazons3-destination-cards.png)

Dessa mål med utökad funktionalitet erbjöds ursprungligen som en betaversion, men *Adobe flyttar nu alla Real-Time CDP-kunder till de nya molnlagringsmålen*. För kunder som redan använder [!DNL Amazon S3], [!DNL Azure Blob] eller SFTP innebär detta att befintliga dataflöden migreras till de nya korten. Läs vidare om du vill ha mer information om de specifika ändringarna som ingår i migreringen.

## Vem den här sidan gäller för {#who-this-applies-to}

Om du redan använder [Flow Service API](https://developer.adobe.com/experience-platform-apis/references/destinations/) för att exportera profiler till molnlagringsmålen Amazon S3, Azure Blob eller SFTP gäller den här API-migreringsguiden dig.

Om du har skript som körs i molnlagringsplatserna [!DNL Amazon S3], [!DNL Azure Blob] eller SFTP ovanpå de exporterade filerna från Experience Platform, bör du tänka på att vissa parametrar ändras när det gäller anslutnings- och flödesspecifikationerna för de nya korten, samt mappningssteget.

Om du t.ex. använder ett skript för att filtrera måldata till målet [!DNL Amazon S3], baserat på anslutningsspecifikationen för målet [!DNL Amazon S3], måste du vara medveten om att anslutningsspecifikationen ändras så att du måste uppdatera filtren.

## Relevanta dokumentationslänkar {#relevant-documentation-links}

I det här avsnittet finns relevant API-självstudiekurs och referensdokumentation för den utökade funktionaliteten för att exportera data till molnlagringsmål.

<!--

TBD if we keep this link but will likely remove it

[Legacy API tutorial to export data to cloud storage destinations](/help/destinations/api/connect-activate-batch-destinations.md) (outdated, do not use anymore)

-->
* [API-självstudiekurs för att exportera målgrupper till molnlagringsmål](/help/destinations/api/activate-segments-file-based-destinations.md)
* [Referensdokumentation för API:t för destinationsflödestjänsten](https://developer.adobe.com/experience-platform-apis/references/destinations/)

## Sammanfattning av bakåtkompatibla ändringar {#summary-backwards-incompatible-changes}

Med migreringen till de nya målen tilldelas alla befintliga dataflöden till [!DNL Amazon S3], [!DNL Azure Blob] och SFTP-mål nu nya målanslutningar och basanslutningar. Steget för profilmappning ändras också. De bakåtkompatibla ändringarna sammanfattas i avsnitten nedan för varje mål. Visa även [målordlistan](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) om du vill ha mer information om villkoren i diagrammet nedan.

![Översikt över migreringsguiden](/help/destinations/assets/api/api-migration-guide/migration-guide-diagram.png)

### Bakåtkompatibla ändringar av målet [!DNL Amazon S3] {#changes-amazon-s3-destination}

De bakåtkompatibla ändringarna för API-användarna är uppdaterade `connection spec ID` och `flow spec ID` enligt tabellen nedan:

| [!DNL Amazon S3] | Äldre | Nytt |
|---------|----------|---------|
| Flödesspecifikation | 71471eba-b620-49e4-90fd-23f1fa0174d8 | 1a0514a6-33d4-4c7f-aff8-594799c47549 |
| Anslutningsspecifikation | 4890fc95-5a1f-4983-94bb-e060c08e3f81 | 4fce964d-3f37-408f-9778-e597338a21ee |

Visa de fullständiga, gamla och nya basanslutningsexemplen och målanslutningsexemplen för [!DNL Amazon S3] på flikarna nedan. Parametrarna som krävs för att skapa basanslutningar för [!DNL Amazon S3] mål ändras inte.

På samma sätt finns det inga bakåtkompatibla ändringar i parametrarna som krävs för att skapa målanslutningar.

>[!BEGINTABS]

>[!TAB Äldre basanslutning och målanslutning]

+++Visa äldre [!DNL base connection] för [!DNL Amazon S3]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "amazon-s3",
  "connectionSpec": {
    "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Access Key",
    "params": {
      "authorizedDate": "2022-10-26",
      "s3SecretKey": "<your-secret-key>",
      "s3AccessKey": "<your-access-key>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"640418e2-0000-0200-0000-6359b9ef0000\"",
  "etag": "\"640418e2-0000-0200-0000-6359b9ef0000\""
}
```

+++

+++Visa äldre [!DNL target connection] för [!DNL Amazon S3]

```json {line-numbers="true" start-line="1" highlight="12"}
{
  ...
  "name": "test 121",
  "baseConnectionId": "ee86d122-10d3-434b-81c7-7252e4d747a7",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
    "version": "1.0"
  },
  "params": {
    "mode": "S3",
    "path": "testpath",
    "bucketName": "test"
  },
  "version": "\"1609cd86-0000-0200-0000-63892cbb0000\"",
  "etag": "\"1609cd86-0000-0200-0000-63892cbb0000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "ee86d122-10d3-434b-81c7-7252e4d747a7",
      "connectionSpec": {
        "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!TAB Ny basanslutning och målanslutning]

+++Visa nya [!DNL base connection] för [!DNL Amazon S3]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "Amazon S3",
  "connectionSpec": {
    "id": "4fce964d-3f37-408f-9778-e597338a21ee",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Access Key",
    "params": {
      "authorizedDate": "2022-10-26",
      "s3SecretKey": "<your-secret-key>",
      "s3AccessKey": "<your-access-key>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"3708da21-0000-0200-0000-638940b10000\"",
  "etag": "\"3708da21-0000-0200-0000-638940b10000\""
}
```

+++

+++Visa nya [!DNL target connection] för [!DNL Amazon S3]

```json {line-numbers="true" start-line="1" highlight="12, 16-27"}
{
  ...
  "name": "test 121",
  "baseConnectionId": "d114c86f-fd47-4bb6-846c-cb1d15a00fe9",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "4fce964d-3f37-408f-9778-e597338a21ee",
    "version": "1.0"
  },
  "params": {
    "csvOptions": {
      "nullValue": "null",
      "emptyValue": "",
      "escape": "\\",
      "quote": "",
      "delimiter": ","
    },
    "compression": "NONE",
    "fileType": "CSV",
    "mode": "Server-to-server",
    "path": "testpath",
    "bucketName": "test"
  },
  "version": "\"1b0985c6-0000-0200-0000-638940b10000\"",
  "etag": "\"1b0985c6-0000-0200-0000-638940b10000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "d114c86f-fd47-4bb6-846c-cb1d15a00fe9",
      "connectionSpec": {
        "id": "4fce964d-3f37-408f-9778-e597338a21ee",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!ENDTABS]

### Bakåtkompatibla ändringar av [!DNL Azure Blob]-målet {#changes-azure-blob-destination}

De bakåtkompatibla ändringarna för API-användarna är uppdaterade `connection spec ID` och `flow spec ID` enligt tabellen nedan:

| [!DNL Azure Blob] | Äldre | Nytt |
|---------|----------|---------|
| Flödesspecifikation | 71471eba-b620-49e4-90fd-23f1fa0174d8 | 752d422f-b16f-4f0d-b1c6-26e44e3b388 |
| Anslutningsspecifikation | e258278b-a4cf-43ac-b158-4fa0ca0d948b | 6d6b59bf-fb58-4107-9064-4d246c0e5bb2 |

Visa de fullständiga, gamla och nya basanslutningsexemplen och målanslutningsexemplen för [!DNL Azure Blob] på flikarna nedan. Parametrarna som krävs för att skapa basanslutningar för Azure Blob-mål ändras inte.

På samma sätt finns det inga bakåtkompatibla ändringar i parametrarna som krävs för att skapa målanslutningar.

>[!BEGINTABS]

>[!TAB Äldre basanslutning och målanslutning]

+++Visa äldre [!DNL base connection] för [!DNL Azure Blob]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "azure-blob",
  "connectionSpec": {
    "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "ConnectionString",
    "params": {
      "authorizedDate": "2022-06-02",
      "connectionString": "<your-connection-string>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  }, 
  "version": "\"d000d23c-0000-0200-0000-6299051c0000\"",
  "etag": "\"d000d23c-0000-0200-0000-6299051c0000\""
}
```

+++

+++Visa äldre [!DNL target connection] för [!DNL Azure Blob]

```json {line-numbers="true" start-line="1" highlight="13"}
{
  ...
  "name": "v1",
  "description": "v2",
  "baseConnectionId": "d10fcecf-9963-4062-820c-0f878be98805",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
    "version": "1.0"
  },
  "params": {
    "mode": "AZURE_BLOB",
    "container": "usdasda",
    "path": "v3"
  },
  "version": "\"cb0468ba-0000-0200-0000-631ab0790000\"",
  "etag": "\"cb0468ba-0000-0200-0000-631ab0790000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "d10fcecf-9963-4062-820c-0f878be98805",
      "connectionSpec": {
        "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!TAB Ny basanslutning och målanslutning]

+++Visa nya [!DNL base connection] för [!DNL Azure Blob]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "Azure Blob Storage",
  "connectionSpec": {
    "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "ConnectionString",
    "params": {
      "authorizedDate": "2022-06-02",      
      "connectionString": "<your-connection-string>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"4008a892-0000-0200-0000-6389890d0000\"",
  "etag": "\"4008a892-0000-0200-0000-6389890d0000\""
}
```

+++

+++Visa nya [!DNL target connection] för [!DNL Azure Blob]

```json {line-numbers="true" start-line="1" highlight="13, 17-25"}
{
  ...
  "name": "v1",
  "description": "v2",
  "baseConnectionId": "1329d183-a3ee-4454-ab3f-e2388082bf29",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
    "version": "1.0"
  },
  "params": {
    "csvOptions": {
      "nullValue": "null",
      "emptyValue": "",
      "escape": "\\",
      "quote": "",
      "delimiter": ","
    },
    "compression": "NONE",
    "fileType": "CSV",
    "mode": "Server-to-server",
    "container": "usdasda",
    "path": "v3"
  },
  "version": "\"5509fe3f-0000-0200-0000-638a28880000\"",
  "etag": "\"5509fe3f-0000-0200-0000-638a28880000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "1329d183-a3ee-4454-ab3f-e2388082bf29",
      "connectionSpec": {
        "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!ENDTABS]

### Bakåtkompatibla ändringar av SFTP-målet {#changes-sftp-destination}

De bakåtkompatibla ändringarna för API-användarna är uppdaterade `connection spec ID` och `flow spec ID` enligt tabellen nedan:

| SFTP | Äldre | Nytt |
|---------|----------|---------|
| Flödesspecifikation | 71471eba-b620-49e4-90fd-23f1fa0174d8 | fd36aaa4-bf2b-43fb-9387-43785eeb799 |
| Anslutningsspecifikation | 64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0 | 36965a81-b1c6-401b-99f8-22508f1e6a26 |

Förutom den uppdaterade flödes- och anslutningsspecifikationen ovan, finns det ändringar i parametrarna som krävs när du skapar SFTP-basanslutningar.

* Tidigare krävdes en `host`-parameter för basanslutningen för SFTP-mål. Den här parametern har nu bytt namn till `domain`.

Se alla exempel på tidigare och nya basanslutningar och målanslutningar för SFTP på flikarna nedan, med de rader som ändras markerade. Parametrarna som krävs för att skapa målanslutningar för SFTP-mål ändras inte.

>[!BEGINTABS]

>[!TAB Äldre basanslutning och målanslutning]

+++Visa äldre [!DNL base connection] för SFTP - lösenordsautentisering

```json {line-numbers="true" start-line="1" highlight="5,15"}
{
  ...
  "name": "sftp",
  "connectionSpec": {
    "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Basic Authentication for sftp",
    "params": {
      "authorizedDate": "2022-06-02",
      "password": "<your-password>",
      "userName": "DPID12345",
      "host": "ftp-out.demdex.com"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"d000013c-0000-0200-0000-629903bd0000\"",
  "etag": "\"d000013c-0000-0200-0000-629903bd0000\""
}
```

+++

+++Visa äldre [!DNL base connection] för [!DNL SFTP - SSH key]-autentisering

```json {line-numbers="true" start-line="1" highlight="5,15"}
{
  ...
  "name": "sftp",
  "connectionSpec": {
    "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Basic Authentication for sftp",
    "params": {
      "authorizedDate": "2022-06-02",
      "sshKey": "<your-ssh-key>",
      "userName": "DPID12345",
      "port": 22
      "domain": "ftp-out.demdex.com"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"d000013c-0000-0200-0000-629903bd0000\"",
  "etag": "\"d000013c-0000-0200-0000-629903bd0000\""
}
```

+++

+++Visa äldre [!DNL target connection] för SFTP

```json {line-numbers="true" start-line="1" highlight="13"}
{
  ...
  "name": "test sftp 6/2",
  "description": "",
  "baseConnectionId": "e6f3a300-0bf7-4755-b7f8-308dc2a99133",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
    "version": "1.0"
  },
  "params": {
    "mode": "FTP",
    "remotePath": "test"
  },
  "version": "\"8503ab91-0000-0200-0000-629903ce0000\"",
  "etag": "\"8503ab91-0000-0200-0000-629903ce0000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "e6f3a300-0bf7-4755-b7f8-308dc2a99133",
      "connectionSpec": {
        "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!TAB Ny basanslutning och målanslutning]

+++Visa nya [!DNL base connection] för [!DNL SFTP - password authentication]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "SFTP",
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "SFTP with Password",
    "params": {
      "authorizedDate": "2022-06-02",
      "domain": "ftp-out.demdex.com",
      "username": "DPID12345",
      "password": "<your-password>",
      "port": 22      
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"420826cc-0000-0200-0000-638999a60000\"",
  "etag": "\"420826cc-0000-0200-0000-638999a60000\""
}
```

+++

+++Visa nya [!DNL base connection] för [!DNL SFTP - SSH key]-autentisering

```json {line-numbers="true" start-line="1" highlight="5,12"}
{
  ...
  "name": "SFTP",
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Basic Authentication for sftp",
    "params": {
      "authorizedDate": "2022-06-02",
      "domain": "ftp-out.demdex.com",
      "username": "DPID12345",
      "sshKey": "<your-ssh-key>",
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"420826cc-0000-0200-0000-638999a60000\"",
  "etag": "\"420826cc-0000-0200-0000-638999a60000\""
}
```

+++

+++Visa nya [!DNL target connection] för SFTP

```json {line-numbers="true" start-line="1" highlight="13, 17-25"}
{
  ...
  "name": "test sftp 6/2",
  "description": "",
  "baseConnectionId": "af63fbe1-45ff-4722-a9de-fbbe789dc7b0",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
    "version": "1.0"
  },
  "params": {
    "csvOptions": {
      "nullValue": "null",
      "emptyValue": "",
      "escape": "\\",
      "quote": "",
      "delimiter": ","
    },
    "compression": "NONE",
    "fileType": "CSV",
    "mode": "FTP",
    "remotePath": "test"
  },
  "version": "\"5509b5cf-0000-0200-0000-638a2ab60000\"",
  "etag": "\"5509b5cf-0000-0200-0000-638a2ab60000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "af63fbe1-45ff-4722-a9de-fbbe789dc7b0",
      "connectionSpec": {
        "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!ENDTABS]

### Bakåtkompatibla ändringar som är gemensamma för [!DNL Amazon S3]-, [!DNL Azure Blob]- och SFTP-mål {#changes-all-destinations}

Stegen för profilväljare på alla tre destinationerna ersätts av ett mappningssteg som gör att du kan byta namn på kolumnrubrikerna i de exporterade filerna om du vill. Se bilden sida vid sida nedan med det gamla attributväljarsteget till vänster och det nya mappningssteget till höger.

![Översikt över migreringsguiden](/help/destinations/assets/api/api-migration-guide/old-and-new-mapping-step.png)

Observera hur objektet `profileSelectors` i de äldre exemplen ersätts av det nya `profileMapping`-objektet.

Fullständig information om hur du konfigurerar objektet `profileMapping` i [API-självstudiekursen för att exportera data till molnlagringsmål](/help/destinations/api/activate-segments-file-based-destinations.md#attribute-and-identity-mapping) finns.

>[!BEGINTABS]

>[!TAB Gamla omformningsparametrar]

+++Visa ett exempel på gamla omformningsparametrar

```json{line-numbers="true" start-line="1" highlight="4-40, 45-53"}
{
  "segmentSelectors": { // shortened for brevity since nothing changes in the audience selectors
  },  
  "profileSelectors": {
    "selectors": [
      {
        "type": "JSON_PATH",
        "value": {
          "path": "CORE",
          "operator": "EXISTS",
          "mapping": {
            "sourceType": "text/x.schema-path",
            "source": "CORE",
            "destination": "CORE",
            "identity": false,
            "primaryIdentity": false,
            "functionVersion": 0,
            "sourceAttribute": "CORE",
            "destinationXdmPath": "CORE"
          },
          "identity": {
            "namespace": "CORE"
          }
        }
      },
      ...
      {
        "type": "JSON_PATH",
        "value": {
          "path": "segmentMembership.status",
          "operator": "EXISTS",
          "mapping": {
            "sourceType": "text/x.schema-path",
            "source": "segmentMembership.status",
            "destination": "segmentMembership.status",
            "identity": false,
            "primaryIdentity": false,
            "functionVersion": 0,
            "sourceAttribute": "segmentMembership.status",
            "destinationXdmPath": "segmentMembership.status"
          }
        }
      }
    ],
    "mandatoryFields": [
      "CORE",
      "person.name.lastName",
      "personalEmail.address"
    ],
    "primaryFields": [
      {
        "identityNamespace": "CORE",
        "fieldType": "IDENTITY"
      }
    ]
  }
}
```

+++

>[!TAB Nya omformningsparametrar]

+++Visa ett exempel på omformningsparametrar efter migreringen

Observera i konfigurationsexemplet nedan hur `profileSelectors` fält har ersatts av ett `profileMapping`-objekt.

```json {line-numbers="true" start-line="1" highlight="4-12, 18-20"}
{
  "segmentSelectors": { // shortened for brevity since nothing changes in the audience selectors
  },  
  "mandatoryFields": [
    "CORE",
    "person_name_lastName",
    "personalEmail_address"
  ],
  "primaryFields": [
    {
      "identityNamespace": "CORE",
      "fieldType": "IDENTITY"
    }
  ],
  "identityMapping": {
    "mappings": []
  },
  "profileMapping": {
    "mappingId": "40dfd952fe09498ba65145c7a5de3e07",
    "mappingVersion": 0
  },
  "attributeMapping": {}
}
```

+++

>[!ENDTABS]

## Tidslinje för migrering och åtgärdsobjekt {#timeline-and-action-items}

Migreringen av tidigare dataflöden till de nya målkorten för [!DNL Amazon S3], [!DNL Azure Blob] och SFTP-destinationer sker så snart din organisation är redo att migrera och inte senare än **26 juli 2023**.

Du får påminnelser från Adobe när migreringsdatumet närmar sig. Läs avsnittet Åtgärdsobjekt nedan som förberedelse för migreringen.

### Åtgärdsobjekt {#action-items}

Innan du migrerar molnlagringsdestinationerna [!DNL Amazon S3], [!DNL Azure Blob] och SFTP till de nya korten förbereder du dig för att uppdatera dina skript och automatiska API-anrop enligt nedan.

1. Uppdatera eventuella skript eller automatiska API-anrop för befintliga [!DNL Amazon S3]-, [!DNL Azure Blob]- eller SFTP-molnlagringsmål senast 26 juli 2023. Alla automatiserade API-anrop eller skript som utnyttjar de gamla anslutningsspecifikationerna eller flödesspecifikationerna måste uppdateras till de nya anslutningsspecifikationerna eller flödesspecifikationerna.
2. Kontakta din kontorepresentant på Adobe när dina skript har uppdaterats före den 26 juli.
3. `targetConnectionSpecId` kan till exempel användas som flagga för att avgöra om dataflödet har migrerats till det nya målkortet. Du kan uppdatera dina skript med ett `if`-villkor för att undersöka de gamla och uppdaterade målanslutningsspecifikationerna i `flow.inheritedAttributes.targetConnections[0].connectionSpec.id` och avgöra om dataflödet har migrerats. Du kan se de gamla och nya anslutningsspecifikations-ID:n i de specifika avsnitten på den här sidan för varje mål.
4. Ditt Adobe-kontoteam kommer att få mer information om när dataflödena kommer att migreras.
5. Efter den 26 juli migreras alla dataflöden. Alla dina befintliga dataflöden har nu nya flödesentiteter (anslutningsspecifikationer, flödesspecifikationer, basanslutningar och målanslutningar). Alla skript eller API-anrop på din sida som använder de äldre flödesentiteterna slutar att fungera.

## Andra migreringsfaktorer {#other-considerations}

Observera att det inte påverkar ditt befintliga schema för export under eller efter migreringen.

## Nästa steg {#next-steps}

Genom att läsa den här sidan vet du nu om du behöver göra något för att förbereda migreringen av molnlagringsdestinationerna. Du vet också vilka dokumentationssidor som ska användas som referens när du konfigurerar API-baserade arbetsflöden för att exportera filer från Experience Platform till de molnlagringsmål du föredrar. Sedan kan du visa API-självstudiekursen för att [exportera data till molnlagringsmål](/help/destinations/api/activate-segments-file-based-destinations.md).
