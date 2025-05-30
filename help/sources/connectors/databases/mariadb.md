---
title: MariaDB Source Connector - översikt
description: Lär dig hur du ansluter MariaDB till Adobe Experience Platform med API:er eller användargränssnittet.
last-substantial-update: 2025-04-29T00:00:00Z
exl-id: 37b8f991-dca9-4f85-9bdd-4927a015e4c0
source-git-commit: bca4f40d452f0a5e70a388872a65640d1fd58533
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# [!DNL MariaDB]

Adobe Experience Platform tillåter att data hämtas från externa källor samtidigt som du får möjlighet att strukturera, etikettera och förbättra inkommande data med [!DNL Experience Platform]-tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform har stöd för inmatning av data från en tredjepartsdatabas. [!DNL Experience Platform] kan ansluta till olika typer av databaser, till exempel relationsdatabaser, NoSQL eller datalager. Stöd för databasproviders är [!DNL MariaDB].

## Förhandskrav {#prerequisites}

Läs följande avsnitt för att slutföra kravkonfigurationen innan du ansluter ditt [!DNL MariaDB]-konto till Experience Platform.

### IP-adress tillåtelselista

Du måste lägga till regionspecifika IP-adresser i tillåtelselista innan du kan ansluta dina källor till Experience Platform. Mer information finns i guiden om att [tillåtslista IP-adresser för att ansluta till Experience Platform](../../ip-address-allow-list.md).

### Autentisera till Experience Platform

Du måste ange värden för följande autentiseringsuppgifter för att kunna ansluta [!DNL MariaDB] till Experience Platform.

>[!BEGINTABS]

>[!TAB Autentisering av kontonyckel]

Ange lämpliga värden för följande autentiseringsuppgifter om du vill använda autentisering av kontonycklar.

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `connectionString` | Anslutningssträngen som är associerad med din [!DNL MariaDB]-autentisering. Anslutningssträngsmönstret [!DNL MariaDB] är: `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL MariaDB] är `3000eb99-cd47-43f3-827c-43caf170f015`. **Obs!**: Den här autentiseringsuppgiften krävs bara vid anslutning via [!DNL Flow Service] API. |

Mer information om hur du hämtar en anslutningssträng finns i det här [[!DNL MariaDB] dokumentet](https://mariadb.com/kb/en/about-mariadb-connector-odbc/).

>[!TAB Grundläggande autentisering]

Ange lämpliga värden för följande autentiseringsuppgifter om du vill använda grundläggande autentisering.

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `server` | Namnet eller IP-adressen för din [!DNL MariaDB]-databas. |
| `username` | Namnet på databasen. |
| `port` | Portnumret för den kommunikationsslutpunkt du ansluter till. |
| `password` | Användarnamnet som motsvarar databasen. |
| `database` | Lösenordet som motsvarar databasen. |
| `sslMode` | Den metod som används för att kryptera data under dataöverföring. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL MariaDB] är `3000eb99-cd47-43f3-827c-43caf170f015`. **Obs!**: Den här autentiseringsuppgiften krävs bara vid anslutning via [!DNL Flow Service] API. |

Mer information om hur du hämtar en anslutningssträng finns i det här [[!DNL MariaDB] dokumentet](https://mariadb.com/kb/en/about-mariadb-connector-odbc/).

>[!ENDTABS]

## Anslut [!DNL MariaDB] till Experience Platform med API:er

- [Skapa en MariaDB-basanslutning med API:t för Flow Service](../../tutorials/api/create/databases/mariadb.md)
- [Utforska datatabeller med API:t för Flow Service](../../tutorials/api/explore/tabular.md)
- [Skapa ett dataflöde för en datakälla med API:t för Flow Service](../../tutorials/api/collect/database-nosql.md)

## Anslut [!DNL MariaDB] till Experience Platform med användargränssnittet

- [Skapa en MariaDB-källanslutning i användargränssnittet](../../tutorials/ui/create/databases/mariadb.md)
- [Skapa ett dataflöde för en datakällanslutning i användargränssnittet](../../tutorials/ui/dataflow/databases.md)
