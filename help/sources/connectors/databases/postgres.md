---
title: PostgreSQL Source Connector - översikt
description: Läs mer om PostgreSQL-källan på Adobe Experience Platform.
last-substantial-update: 2025-04-29T00:00:00Z
exl-id: 27b891c5-5fc5-4539-8f98-e3a53e2eefe3
source-git-commit: 04634c6edc13d8b8da01a01077161866235c61b1
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 0%

---

# [!DNL PostgreSQL]

Läs det här dokumentet om du vill veta mer om nödvändiga steg som du måste slutföra innan du kan ansluta din [!DNL PostgreSQL]-databas till Adobe Experience Platform.

## Förhandskrav {#prerequisites}

Läs följande avsnitt för att slutföra kravkonfigurationen innan du ansluter din [!DNL PostgreSQL]-databas till Experience Platform.

### IP-adress tillåtelselista

Du måste lägga till regionspecifika IP-adresser i tillåtelselista innan du kan ansluta dina källor till Experience Platform på antingen Azure eller Amazon Web Services (AWS). Mer information finns i guiden [tillåtslista IP-adresser för att ansluta till Experience Platform på Azure och AWS](../../ip-address-allow-list.md).

### Autentisera till Experience Platform på Azure {#azure}

Du måste ange värden för följande autentiseringsuppgifter för att ansluta [!DNL PostgreSQL] till Experience Platform på Azure.

>[!BEGINTABS]

>[!TAB Autentisering av kontonyckel]

Ange värden för följande autentiseringsuppgifter för att ansluta din [!DNL PostgreSQL]-databas till Experience Platform på Azure med autentisering av kontonycklar.

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `connectionString` | Anslutningssträngen som är associerad med ditt [!DNL PostgreSQL]-konto. Anslutningssträngsmönstret [!DNL PostgreSQL] är: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL PostgreSQL] är `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

Mer information finns i [[!DNL PostgreSQL] dokumentationen](https://www.postgresql.org/docs/current/).

>[!TAB Grundläggande autentisering]

Ange värden för följande autentiseringsuppgifter för att ansluta din [!DNL PostgreSQL]-databas till Experience Platform på Azure med grundläggande autentisering.

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `server` | Namnet eller IP-adressen för din [!DNL PostgreSQL]-databas. |
| `port` | TCP-porten för din [!DNL PostgreSQL]-server. |
| `username` | Det användarnamn som är associerat med din [!DNL PostgreSQL]-databasautentisering. |
| `password` | Lösenordet som är kopplat till din [!DNL PostgreSQL]-databasautentisering. |
| `database` | Namnet på den [!DNL PostgreSQL]-databas som du vill ansluta till. |
| `sslMode` | Den [!DNL Secure Sockets Layer]-metod (SSL) som ska användas för anslutningen. De tillgängliga värdena är: <ul><li>`Disable`: Använd det här alternativet om du vill inaktivera SSL. Om servern kräver en SSL-konfiguration kommer anslutningen att misslyckas.</li><li>`Allow`: Använd det här alternativet om du vill tillåta SSL-anslutningar. Icke-SSL-anslutningar kan fortfarande användas om servern stöder dem.</li><li>`Prefer`: Använd det här alternativet om du vill använda SSL-anslutningar eftersom servern stöder dem. Det här alternativet tillåter även andra anslutningar än SSL.</li><li>`Require`: Använd det här alternativet om du vill göra SSL-anslutningar obligatoriska. Om servern inte stöder SSL kommer anslutningarna att misslyckas.</li><li>`Verify-Ca`: Använd det här alternativet om du vill verifiera servercertifikat medan anslutningar misslyckas om servern inte stöder SSL.</li><li>`Verify-Full`: Använd det här alternativet om du vill verifiera servercertifikat med värdnamnet när anslutningar misslyckas om servern inte stöder SSL.</li></ul> |

Mer information finns i [[!DNL PostgreSQL] dokumentationen](https://www.postgresql.org/docs/current/).

>[!ENDTABS]

### Autentisera till Experience Platform på Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Detta avsnitt gäller implementeringar av Experience Platform som körs på Amazon Web Services (AWS). Experience Platform som körs på AWS är för närvarande tillgängligt för ett begränsat antal kunder. Mer information om den Experience Platform-infrastruktur som stöds finns i [Experience Platform översikt över flera moln](../../../landing/multi-cloud.md).

Ange värden för följande autentiseringsuppgifter för att ansluta din [!DNL PostgreSQL]-databas till Experience Platform på AWS med grundläggande autentisering.

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `server` | Namnet eller IP-adressen för din [!DNL PostgreSQL]-databas. |
| `port` | TCP-porten för din [!DNL PostgreSQL]-server. |
| `username` | Det användarnamn som är associerat med din [!DNL PostgreSQL]-databasautentisering. |
| `password` | Lösenordet som är kopplat till din [!DNL PostgreSQL]-databasautentisering. |
| `database` | Namnet på den [!DNL PostgreSQL]-databas som du vill ansluta till. |
| `sslMode` | Den [!DNL Secure Sockets Layer]-metod (SSL) som ska användas för anslutningen. De tillgängliga värdena är: <ul><li>`Disable`: Använd det här alternativet om du vill inaktivera SSL. Om servern kräver en SSL-konfiguration kommer anslutningen att misslyckas.</li><li>`Allow`: Använd det här alternativet om du vill tillåta SSL-anslutningar. Icke-SSL-anslutningar kan fortfarande användas om servern stöder dem.</li><li>`Prefer`: Använd det här alternativet om du vill använda SSL-anslutningar eftersom servern stöder dem. Det här alternativet tillåter även andra anslutningar än SSL.</li><li>`Require`: Använd det här alternativet om du vill göra SSL-anslutningar obligatoriska. Om servern inte stöder SSL kommer anslutningarna att misslyckas.</li><li>`Verify-Ca`: Använd det här alternativet om du vill verifiera servercertifikat medan anslutningar misslyckas om servern inte stöder SSL.</li><li>`Verify-Full`: Använd det här alternativet om du vill verifiera servercertifikat med värdnamnet när anslutningar misslyckas om servern inte stöder SSL.</li></ul> |

Mer information finns i [[!DNL PostgreSQL] dokumentationen](https://www.postgresql.org/docs/current/).

## Anslut [!DNL PostgreSQL] till Experience Platform med API:er

* [Skapa en  [!DNL PostgreSQL] basanslutning med API:t för Flow Service](../../tutorials/api/create/databases/postgres.md)
* [Utforska datatabeller med API:t för Flow Service](../../tutorials/api/explore/tabular.md)
* [Skapa ett dataflöde för en datakälla med API:t för Flow Service](../../tutorials/api/collect/database-nosql.md)

## Anslut [!DNL PostgreSQL] till Experience Platform med användargränssnittet

* [Skapa en  [!DNL PostgreSQL] källanslutning i användargränssnittet](../../tutorials/ui/create/databases/postgres.md)
* [Skapa ett dataflöde för en datakällanslutning i användargränssnittet](../../tutorials/ui/dataflow/databases.md)
