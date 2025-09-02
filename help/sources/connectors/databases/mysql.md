---
title: MySQL Source Connector - översikt
description: Lär dig hur du ansluter MySQL till Adobe Experience Platform med API:er eller användargränssnittet.
last-substantial-update: 2025-05-20T00:00:00Z
exl-id: a18e8e69-880f-4bee-b339-726091d6f858
source-git-commit: 16fe5340582dcea0ff40000fb516c1b72d5f150e
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 0%

---

# [!DNL MySQL]

[!DNL MySQL] är ett relationsdatabashanteringssystem med öppen källkod som används för att lagra och hantera strukturerade data. Data ordnas i tabeller och SQL (Structured Query Language) används för att hämta och uppdatera information. [!DNL MySQL] används ofta i webbprogram, har stöd för flera plattformar och är känt för hastighet, tillförlitlighet och användarvänlighet.

Du kan använda källan [!DNL MySQL] för att ansluta ditt konto och importera data från din [!DNL MySQL]-databas till Adobe Experience Platform.

## Förhandskrav {#prerequisites}

Läs följande avsnitt för att slutföra kravkonfigurationen innan du ansluter ditt [!DNL MySQl]-konto till Experience Platform.

### IP-adress tillåtelselista

Du måste lägga till regionspecifika IP-adresser i tillåtelselista innan du kan ansluta dina källor till Experience Platform på antingen Azure eller Amazon Web Services (AWS). Mer information finns i guiden [tillåtslista IP-adresser för att ansluta till Experience Platform på Azure och AWS](../../ip-address-allow-list.md).

### Autentisera till Experience Platform på Azure {#azure}

Du kan antingen använda kontonyckelautentisering eller grundläggande autentisering för att ansluta din [!DNL MySQL]-databas till Experience Platform på Azure.

>[!BEGINTABS]

>[!TAB Autentisering av kontonyckel]

Ange värden för följande autentiseringsuppgifter för att ansluta din [!DNL MySQL]-databas till Experience Platform med autentisering av kontonycklar.

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `connectionString` | Anslutningssträngen [!DNL MySQL] som är associerad med ditt konto. Anslutningssträngsmönstret [!DNL MySQL] är: `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningens spec-ID för [!DNL MySQL] är `26d738e0-8963-47ea-aadf-c60de735468a`. |

Mer information finns i [[!DNL MySQL] dokumentationen om anslutningssträngar](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html).

>[!TAB Grundläggande autentisering]

Ange värden för följande autentiseringsuppgifter för att ansluta din [!DNL MySQL]-databas till Experience Platform med grundläggande autentisering.

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `server` | Namnet eller IP-adressen för din [!DNL MySQL]-databas. |
| `username` | Det användarnamn som är associerat med din [!DNL MySQL]-databasautentisering. |
| `password` | Lösenordet som är kopplat till din [!DNL MySQL]-databasautentisering. |
| `database` | Namnet på den [!DNL MySQL]-databas som du vill ansluta till. |
| `sslMode` | Den [!DNL Secure Sockets Layer]-metod (SSL) som ska användas för anslutningen. De tillgängliga värdena är: <ul><li>`DISABLED`: Använd det här alternativet om du vill inaktivera SSL. Om servern kräver en SSL-konfiguration kommer anslutningen att misslyckas</li><li>`PREFERRED`: Använd det här alternativet om du vill använda SSL-anslutningar eftersom servern stöder dem. Det här alternativet tillåter även andra anslutningar än SSL.</li><li>`REQUIRED`: Använd det här alternativet om du vill göra SSL-anslutningar obligatoriska. Om servern inte stöder SSL kommer anslutningarna att misslyckas.</li><li>`Verify-Ca`: Använd det här alternativet om du vill verifiera servercertifikat medan anslutningar misslyckas om servern inte stöder SSL.</li><li>`Verify Identity`: Använd det här alternativet om du vill verifiera servercertifikat med värdnamnet när anslutningar misslyckas om servern inte stöder SSL.</li></ul> |

>[!ENDTABS]

### Autentisera till Experience Platform på Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Detta avsnitt gäller implementeringar av Experience Platform som körs på Amazon Web Services (AWS). Experience Platform som körs på AWS är för närvarande tillgängligt för ett begränsat antal kunder. Mer information om den Experience Platform-infrastruktur som stöds finns i [Experience Platform översikt över flera moln](../../../landing/multi-cloud.md).

Du måste ange värden för följande autentiseringsuppgifter för att kunna ansluta [!DNL MySQL] till Experience Platform på AWS.

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `server` | Namnet eller IP-adressen för din [!DNL MySQL]-databas. |
| `username` | Namnet på databasen. |
| `password` | Användarnamnet som motsvarar databasen. |
| `database` | Lösenordet som motsvarar databasen. |
| `sslMode` | Ett booleskt värde som styr om SSL används eller inte, beroende på serverstödet. Den här konfigurationen är som standard `false`. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL MySQL] är `26d738e0-8963-47ea-aadf-c60de735468a`. **Obs!**: Den här autentiseringsuppgiften krävs bara vid anslutning via [!DNL Flow Service] API. |

## Anslut [!DNL MySQL] till Experience Platform med API:er

- [Anslut  [!DNL MySQL] databasen med API:t för Flow Service](../../tutorials/api/create/databases/mysql.md)
- [Utforska datatabeller med API:t för Flow Service](../../tutorials/api/explore/tabular.md)
- [Skapa ett dataflöde för en datakälla med API:t för Flow Service](../../tutorials/api/collect/database-nosql.md)

## Anslut MySQL till Experience Platform med användargränssnittet

- [Anslut din [!DNL MySQL] databas till Experience Platform med användargränssnittet](../../tutorials/ui/create/databases/mysql.md)
- [Skapa ett dataflöde för en datakällanslutning i användargränssnittet](../../tutorials/ui/dataflow/databases.md)
