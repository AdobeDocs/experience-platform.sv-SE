---
title: Snowflake Source Connector - översikt
description: Lär dig hur du ansluter Snowflake till Adobe Experience Platform med API:er eller användargränssnittet.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: 0476c42924bf0163380e650141fad8e50b98d4cf
workflow-type: tm+mt
source-wordcount: '1502'
ht-degree: 1%

---

# [!DNL Snowflake]-källa

>[!IMPORTANT]
>
>* Källan [!DNL Snowflake] är tillgänglig i källkatalogen för användare som har köpt Real-Time Customer Data Platform Ultimate.
>* Som standard tolkar [!DNL Snowflake]-källan `null` som en tom sträng. Kontakta din Adobe-representant för att kontrollera att dina `null`-värden är korrekt skrivna som `null` i Adobe Experience Platform.
>* För att Experience Platform ska kunna importera data måste tidszoner för alla tabellbaserade batchkällor konfigureras till UTC. Den enda tidsstämpeln som stöds för källan [!DNL Snowflake] är TIMESTAMP_NTZ med UTC-tid.

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform har stöd för inmatning av data från en tredjepartsdatabas. Experience Platform kan ansluta till olika typer av databaser, till exempel relationsdatabaser, NoSQL-databaser eller datalager. Stöd för databasproviders är [!DNL Snowflake].

## Förhandskrav {#prerequisites}

I det här avsnittet beskrivs de konfigurationsåtgärder som du måste slutföra innan du kan ansluta [!DNL Snowflake]-källan till Experience Platform.

### IP-adress tillåtelselista

Du måste lägga till regionspecifika IP-adresser i tillåtelselista innan du kan ansluta dina källor till Experience Platform. Mer information finns i guiden om att [tillåtslista IP-adresser för att ansluta till Experience Platform](../../ip-address-allow-list.md).

### Samla in nödvändiga inloggningsuppgifter

Du måste ange värden för följande autentiseringsegenskaper för att autentisera [!DNL Snowflake]-källan.

>[!BEGINTABS]

>[!TAB Autentisering av kontonyckel (Azure)]

Ange värden för följande autentiseringsuppgifter för att ansluta [!DNL Snowflake] till Experience Platform på Azure med kontonyckelautentisering.

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `account` | Ett kontonamn identifierar unikt ett konto inom organisationen. I det här fallet måste du unikt identifiera ett konto i olika [!DNL Snowflake]-organisationer. Om du vill göra det måste du lägga till ditt organisationsnamn i kontonamnet. Till exempel: `orgname-account_name`. Mer information finns i avsnittet [Hämta din [!DNL Snowflake] kontoidentifierare](#retrieve-your-account-identifier). Mer information finns i [[!DNL Snowflake] dokumentationen](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `warehouse` | Lagerstället [!DNL Snowflake] hanterar frågekörningsprocessen för programmet. Varje [!DNL Snowflake]-lagerställe är oberoende av varandra och måste nås individuellt när data överförs till Experience Platform. |
| `database` | Databasen [!DNL Snowflake] innehåller de data som du vill hämta Experience Platform. |
| `username` | Användarnamnet för kontot [!DNL Snowflake]. |
| `password` | Lösenordet för användarkontot [!DNL Snowflake]. |
| `role` | Standardrollen för åtkomstkontroll som ska användas i sessionen [!DNL Snowflake]. Rollen ska vara en befintlig roll som redan har tilldelats den angivna användaren. Standardrollen är `PUBLIC`. |
| `connectionString` | Anslutningssträngen som används för att ansluta till din [!DNL Snowflake]-instans. Anslutningssträngsmönstret för [!DNL Snowflake] är `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |

>[!TAB Autentisering med nyckelpar (Azure)]

Generera först ett 2 048-bitars RSA-nyckelpar om du vill använda nyckelpars-autentisering. Ange sedan värden för följande autentiseringsuppgifter för att ansluta till Experience Platform på Azure med nyckelparautentisering.

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `account` | Ett kontonamn identifierar unikt ett konto inom organisationen. I det här fallet måste du unikt identifiera ett konto i olika [!DNL Snowflake]-organisationer. Om du vill göra det måste du lägga till ditt organisationsnamn i kontonamnet. Till exempel: `orgname-account_name`. Mer information finns i avsnittet [Hämta din [!DNL Snowflake] kontoidentifierare](#retrieve-your-account-identifier). Mer information finns i [[!DNL Snowflake] dokumentationen](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | Användarnamnet för ditt [!DNL Snowflake]-konto. |
| `privateKey` | Den [!DNL Base64-]kodade privata nyckeln för ditt [!DNL Snowflake]-konto. Du kan generera antingen krypterade eller okrypterade privata nycklar. Om du använder en krypterad privat nyckel måste du även ange en lösenfras för den privata nyckeln vid autentisering mot Experience Platform. Mer information finns i avsnittet [Hämta din privata nyckel](#retrieve-your-private-key). |
| `privateKeyPassphrase` | Lösenfrasen för den privata nyckeln är ett extra säkerhetslager som du måste använda när du autentiserar med en krypterad privat nyckel. Du behöver inte ange lösenfrasen om du använder en okrypterad privat nyckel. |
| `port` | Portnumret som används av [!DNL Snowflake] vid anslutning till en server via Internet. |
| `database` | Databasen [!DNL Snowflake] som innehåller de data som du vill importera till Experience Platform. |
| `warehouse` | Lagerstället [!DNL Snowflake] hanterar frågekörningsprocessen för programmet. Varje [!DNL Snowflake]-lagerställe är oberoende av varandra och måste nås individuellt när data överförs till Experience Platform. |

Mer information om dessa värden finns i [[!DNL Snowflake] autentiseringsguiden för nyckelpar](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!TAB Grundläggande autentisering (AWS)]

Ange värden för följande autentiseringsuppgifter för att ansluta [!DNL Snowflake] till Experience Platform på AWS med grundläggande autentisering.

>[!WARNING]
>
>Grundläggande autentisering (eller kontonyckelautentisering) för källan [!DNL Snowflake] kommer att bli inaktuell i november 2025. Du måste gå över till nyckelparsbaserad autentisering för att kunna fortsätta använda källan och hämta data från din databas till Experience Platform. Mer information om borttagningen finns i [[!DNL Snowflake] metodguiden om bästa praxis för att minska riskerna för kreditvärdighetsförluster](https://www.snowflake.com/en/resources/white-paper/best-practices-to-mitigate-the-risk-of-credential-compromise/).

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `host` | Den värd-URL som ditt [!DNL Snowflake]-konto ansluter till. |
| `port` | Portnumret som används av [!DNL Snowflake] vid anslutning till en server via Internet. |
| `username` | Användarnamnet som är associerat med ditt [!DNL Snowflake]-konto. |
| `password` | Lösenordet som är kopplat till ditt [!DNL Snowflake]-konto. |
| `database` | Databasen [!DNL Snowflake] från vilken data hämtas. |
| `schema` | Namnet på schemat som är associerat med din [!DNL Snowflake]-databas. Du måste se till att användaren som du vill ge databasåtkomst till också har åtkomst till det här schemat. |
| `warehouse` | Det [!DNL Snowflake]-lagerställe som du använder. |

>[!TAB Autentisering med nyckelpar (AWS)]

Generera först ett 2 048-bitars RSA-nyckelpar om du vill använda nyckelpars-autentisering. Ange sedan värden för följande autentiseringsuppgifter för att ansluta till Experience Platform på AWS med nyckelpars-autentisering.

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `account` | Ett kontonamn identifierar unikt ett konto inom organisationen. I det här fallet måste du unikt identifiera ett konto i olika [!DNL Snowflake]-organisationer. Om du vill göra det måste du lägga till ditt organisationsnamn i kontonamnet. Till exempel: `orgname-account_name`. Läs guiden om att [hämta din [!DNL Snowflake] kontoidentifierare](#etrieve-your-account-identifier) om du vill ha mer information. Mer information finns i [[!DNL Snowflake] dokumentationen](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | Användarnamnet för ditt [!DNL Snowflake]-konto. |
| `privateKey` | Den privata nyckeln för användaren [!DNL Snowflake], base64-kodad som en enda rad utan rubriker eller radbrytningar. Om du vill förbereda den kopierar du innehållet i PEM-filen, tar bort `BEGIN`/`END`-raderna och alla radbrytningar och kodar sedan resultatet med base64. Mer information finns i avsnittet [Hämta din privata nyckel](#retrieve-your-private-key). **Obs!** Krypterade privata nycklar stöds för närvarande inte för en AWS-anslutning. |
| `port` | Portnumret som används av [!DNL Snowflake] vid anslutning till en server via Internet. |
| `database` | Databasen [!DNL Snowflake] som innehåller de data som du vill importera till Experience Platform. |
| `warehouse` | Lagerstället [!DNL Snowflake] hanterar frågekörningsprocessen för programmet. Varje [!DNL Snowflake]-lagerställe är oberoende av varandra och måste nås individuellt när data överförs till Experience Platform. |

Mer information om dessa värden finns i [[!DNL Snowflake] autentiseringsguiden för nyckelpar](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

### Hämta din kontoidentifierare {#retrieve-your-account-identifier}

Du måste hämta din kontoidentifierare från [!DNL Snowflake]-gränssnittspanelen eftersom du kommer att använda kontoidentifieraren för att autentisera din [!DNL Snowflake]-instans på Experience Platform.

Så här hämtar du din kontoidentifierare:

* Navigera till ditt konto på [[!DNL Snowflake] programmets gränssnittspanel](https://app.snowflake.com/).
* I den vänstra navigeringen väljer du **[!DNL Accounts]** följt av **[!DNL Active Accounts]** i sidhuvudet.
* Välj sedan informationsikonen och markera och kopiera domännamnet för den aktuella URL:en.

![Snowflake UI-instrumentpanel med domännamnet markerat.](../../images/tutorials/create/snowflake/snowflake-dashboard.png)

### Hämta din privata nyckel {#retrieve-your-private-key}

Om du använder nyckelparautentisering för din [!DNL Snowflake]-anslutning måste du också generera din privata nyckel innan du ansluter till Experience Platform.

>[!BEGINTABS]

>[!TAB Skapa en krypterad privat nyckel]

Kör följande kommando på terminalen för att generera din krypterade privata nyckel [!DNL Snowflake]:

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -v2 des3 -inform PEM -out rsa_key.p8
```

Om det lyckas bör du få din privata nyckel i PEM-format.

```shell
-----BEGIN ENCRYPTED PRIVATE KEY-----
MIIE6T...
-----END ENCRYPTED PRIVATE KEY-----
```

>[!TAB Skapa en okrypterad privat nyckel]

Om du vill generera din okrypterade privata [!DNL Snowflake]-nyckel kör du följande kommando på terminalen:

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -inform PEM -out rsa_key.p8 -nocrypt
```

Om det lyckas bör du få din privata nyckel i PEM-format.

```shell
-----BEGIN PRIVATE KEY-----
MIIE6T...
-----END PRIVATE KEY-----
```

>[!ENDTABS]

Ta sedan din privata nyckel och koda den i [!DNL Base64]. Se till att du inte gör några omformningar eller formatkonverteringar på din privata nyckel för [!DNL Snowflake]. Dessutom måste du se till att det inte finns några efterföljande radmatningstecken i slutet av den privata nyckeln innan du kodar den i [!DNL Base64].

### Verifiera konfigurationer

Innan du kan skapa en källanslutning för dina [!DNL Snowflake]-data måste du också se till att följande konfigurationer uppfylls:

* Det standardlagerställe som tilldelats en viss användare måste vara samma som det lagerställe som du angav vid autentisering till Experience Platform.
* Den standardroll som tilldelats en viss användare måste ha tillgång till samma databas som du anger när du autentiserar dig för Experience Platform.

Så här verifierar du din roll och ditt lager:

* Välj **[!DNL Admin]** till vänster och välj sedan **[!DNL Users & Roles]**.
* Välj lämplig användare och markera sedan ellipserna (`...`) i det övre högra hörnet.
* Navigera till [!DNL Edit user] i fönstret [!DNL Default Role] som visas för att visa rollen som är associerad med den angivna användaren.
* I samma fönster går du till [!DNL Default Warehouse] för att visa det lagerställe som är associerat med den angivna användaren.

![Användargränssnittet i Snowflake där du kan verifiera din roll och ditt lager.](../../images/tutorials/create/snowflake/snowflake-configs.png)

När kodningen är klar kan du sedan använda den [!DNL Base64]-kodade privata nyckeln på Experience Platform för att autentisera ditt [!DNL Snowflake]-konto.

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Snowflake] till Experience Platform med API:er eller användargränssnittet:

## Anslut [!DNL Snowflake] till Experience Platform med API:er

* [Skapa en Snowflake-basanslutning med API:t för Flow Service](../../tutorials/api/create/databases/snowflake.md)
* [Utforska datatabeller med API:t för Flow Service](../../tutorials/api/explore/tabular.md)
* [Skapa ett dataflöde för en datakälla med API:t för Flow Service](../../tutorials/api/collect/database-nosql.md)

## Anslut [!DNL Snowflake] till Experience Platform med användargränssnittet

* [Skapa en Snowflake-källanslutning i användargränssnittet](../../tutorials/ui/create/databases/snowflake.md)
* [Skapa ett dataflöde för en datakällanslutning i användargränssnittet](../../tutorials/ui/dataflow/databases.md)
