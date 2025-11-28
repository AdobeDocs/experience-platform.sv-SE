---
title: Snowflake Source Connector - översikt
description: Lär dig hur du ansluter Snowflake till Adobe Experience Platform med API:er eller användargränssnittet.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: 687363ab664e43cc854b535760dfbfc55acefd2c
workflow-type: tm+mt
source-wordcount: '1570'
ht-degree: 2%

---

# [!DNL Snowflake]-källa

>[!IMPORTANT]
>
>* Källan [!DNL Snowflake] är tillgänglig i källkatalogen för användare som har köpt Real-Time Customer Data Platform Ultimate.
>* Som standard tolkar [!DNL Snowflake]-källan `null` som en tom sträng. Kontakta din Adobe-representant för att kontrollera att dina `null`-värden är korrekt skrivna som `null` i Adobe Experience Platform.
>* För att Experience Platform ska kunna importera data måste tidszoner för alla tabellbaserade batchkällor konfigureras till UTC. Den enda tidsstämpeln som stöds för källan [!DNL Snowflake] är TIMESTAMP_NTZ med UTC-tid.

[!DNL Snowflake] är en molnbaserad datalagerplattform som är utformad för att organisationer ska kunna lagra, bearbeta och analysera stora datavolymer effektivt. [!DNL Snowflake] har skapats för att utnyttja molnets skalbarhet och flexibilitet och stöder dataintegrering, avancerad analys och sömlös delning mellan team. Som en helt hanterad tjänst eliminerar [!DNL Snowflake] underhållsproblem som är gemensamma för traditionella databaser, vilket gör att du kan fokusera på att få insikter och värde från dina data.

Du kan använda källan [!DNL Snowflake] för att ansluta och hämta data från [!DNL Snowflake] till Adobe Experience Platform. Läs dokumentationen nedan för att lära dig hur du konfigurerar din [!DNL Snowflake]-källa och ansluter till Experience Platform.

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
| `account` | Ett kontonamn identifierar unikt ett konto inom organisationen. I det här fallet måste du unikt identifiera ett konto i olika [!DNL Snowflake]-organisationer. Om du vill göra det måste du lägga till ditt organisationsnamn i kontonamnet. Till exempel: `myorg-myaccount.snowflakecomputing.com`. Mer information finns i avsnittet [Hämta din [!DNL Snowflake] kontoidentifierare](#retrieve-your-account-identifier). Mer information finns i [[!DNL Snowflake] dokumentationen](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
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
| `account` | Ett kontonamn identifierar unikt ett konto inom organisationen. I det här fallet måste du unikt identifiera ett konto i olika [!DNL Snowflake]-organisationer. Om du vill göra det måste du lägga till ditt organisationsnamn i kontonamnet. Till exempel: `myorg-myaccount.snowflakecomputing.com`. Mer information finns i avsnittet [Hämta din [!DNL Snowflake] kontoidentifierare](#retrieve-your-account-identifier). Mer information finns i [[!DNL Snowflake] dokumentationen](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
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
| `account` | Ett kontonamn identifierar unikt ett konto inom organisationen. I det här fallet måste du unikt identifiera ett konto i olika [!DNL Snowflake]-organisationer. Om du vill göra det måste du lägga till ditt organisationsnamn i kontonamnet. Till exempel: `http://myorg-myaccount.snowflakecomputing.com/`. Läs guiden om att [hämta din [!DNL Snowflake] kontoidentifierare](#etrieve-your-account-identifier) om du vill ha mer information. Mer information finns i [[!DNL Snowflake] dokumentationen](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | Användarnamnet för ditt [!DNL Snowflake]-konto. |
| `privateKey` | Den privata nyckeln för användaren [!DNL Snowflake], base64-kodad som en enda rad utan rubriker eller radbrytningar. Om du vill förbereda den kopierar du innehållet i PEM-filen, tar bort `BEGIN`/`END`-raderna och alla radbrytningar och kodar sedan resultatet med base64. Mer information finns i avsnittet [Hämta din privata nyckel](#retrieve-your-private-key). **Obs!** Krypterade privata nycklar stöds för närvarande inte för en AWS-anslutning. |
| `port` | Portnumret som används av [!DNL Snowflake] vid anslutning till en server via Internet. |
| `database` | Databasen [!DNL Snowflake] som innehåller de data som du vill importera till Experience Platform. |
| `warehouse` | Lagerstället [!DNL Snowflake] hanterar frågekörningsprocessen för programmet. Varje [!DNL Snowflake]-lagerställe är oberoende av varandra och måste nås individuellt när data överförs till Experience Platform. |

Mer information om dessa värden finns i [[!DNL Snowflake] autentiseringsguiden för nyckelpar](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

### Hämta din kontoidentifierare {#retrieve-your-account-identifier}

Du måste hämta din kontoidentifierare från [!DNL Snowflake]-gränssnittspanelen eftersom du använder den för att autentisera din [!DNL Snowflake]-instans på Experience Platform.

Så här hämtar du din kontoidentifierare:

* Använd [[!DNL Snowflake] programmets gränssnitt](https://app.snowflake.com/) för att komma åt ditt konto.
* I den vänstra navigeringen väljer du **[!DNL Accounts]** och sedan **[!DNL Active Accounts]** i sidhuvudet.
* Välj sedan informationsikonen och markera och kopiera domännamnet för den aktuella URL:en.

![Snowflake UI-instrumentpanel med domännamnet markerat.](../../images/tutorials/create/snowflake/snowflake-dashboard.png)

### Generera RSA-nyckelpar

Använd OpenSSL i kommandoradsgränssnittet för att generera ett 2 048-bitars RSA-nyckelpar i PKCS#8-format. Det är bäst att skapa en krypterad privat nyckel för säkerhet, som kräver en lösenfras.

>[!BEGINTABS]

>[!TAB Generera en krypterad privat nyckel]

Kör följande kommando på terminalen för att generera din krypterade privata nyckel [!DNL Snowflake]:

```bash
openssl genrsa 2048 | openssl pkcs8 -topk8 -v2 des3 -inform PEM -out rsa_key.p8# You will be prompted to enter a passphrase. Store this securely!
```

>[!TAB Generera en okrypterad privat nyckel]

Om du vill generera din okrypterade privata [!DNL Snowflake]-nyckel kör du följande kommando på terminalen:

```bash
openssl genrsa 2048 | openssl pkcs8 -topk8 -inform PEM -out rsa_key.p8 -nocrypt
```

>[!ENDTABS]

### Generera en offentlig nyckel från din privata nyckel

Kör sedan följande kommando i kommandoradsgränssnittet för att skapa en offentlig nyckel baserad på din privata nyckel.

```bash
openssl rsa -in rsa_key.p8 -pubout -out rsa_key.pub# You will be prompted to enter the passphrase if the private key is encrypted.
```

### Tilldela den offentliga nyckeln till användaren [!DNL Snowflake]

Du måste använda en [!DNL Snowflake]-administratörsroll (till exempel **SECURITYADMIN**) för att associera den genererade offentliga nyckeln med den [!DNL Snowflake]-tjänstanvändare som Experience Platform ska använda. Om du vill hämta innehållet i den offentliga nyckeln öppnar du filen `rsa_key.pub` och kopierar hela innehållet, exklusive `-----BEGIN PUBLIC KEY----- and -----END PUBLIC KEY-----` rader. Kör sedan följande SQL i [!DNL Snowflake]:

```sql
ALTER USER {YOUR_SNOWFLAKE_USERNAME}>SET RSA_PUBLIC_KEY='{PUBLIC_KEY_CONTENT}';
```

### Koda den privata nyckeln i [!DNL Base64]

Experience Platform kräver att den privata nyckeln är [!DNL Base64]-kodad och tillhandahålls som en sträng under anslutningskonfigurationen. Använd ett lämpligt verktyg eller skript för att koda innehållet i filen `rsa_key.p8` till en enda [!DNL Base64]-sträng.

>[!TIP]
>
>Kontrollera att det inte finns några extra mellanslag eller radbrytningar, inklusive huvud-/fotrader `(-----BEGIN ENCRYPTED PRIVATE KEY----- and -----END ENCRYPTED PRIVATE KEY-----)`, före eller efter kodningsprocessen, eftersom detta kan orsaka autentiseringsfel.

### Verifiera konfigurationer

Innan du skapar [!DNL Snowflake]-källanslutningen i Experience Platform måste du se till att användarens **[!DNL Default Role]** och **[!DNL Default Warehouse]** matchar de värden som du anger i Experience Platform. Du kan verifiera de här inställningarna i användargränssnittet för [!DNL Snowflake] med hjälp av SQL-kommandot `DESCRIBE USER {USERNAME}`.

Du kan även följa stegen nedan för att verifiera dina inställningar:

* Välj **[!DNL Admin]** till vänster och välj sedan **[!DNL Users & Roles]**.
* Välj lämplig användare och markera sedan ellipserna (`...`) i det övre högra hörnet.
* Navigera till [!DNL Edit user] i fönstret [!DNL Default Role] som visas för att visa rollen som är associerad med den angivna användaren.
* I samma fönster går du till [!DNL Default Warehouse] för att visa det lagerställe som är associerat med den angivna användaren.

![Användargränssnittet i Snowflake där du kan verifiera din roll och ditt lager.](../../images/tutorials/create/snowflake/snowflake-configs.png)

## Nästa steg

När konfigurationen är klar kan du nu ansluta ditt [!DNL Snowflake]-konto till Experience Platform. Mer information finns i följande dokumentation:

### Anslut [!DNL Snowflake] till Experience Platform med API:er

* [Anslut [!DNL Snowflake] till Experience Platform med API:t](../../tutorials/api/create/databases/snowflake.md)
* [Utforska datatabeller med API:t för Flow Service](../../tutorials/api/explore/tabular.md)
* [Skapa ett dataflöde för en datakälla med API:t för Flow Service](../../tutorials/api/collect/database-nosql.md)

### Anslut [!DNL Snowflake] till Experience Platform med användargränssnittet

* [Anslut [!DNL Snowflake] till Experience Platform med användargränssnittet](../../tutorials/ui/create/databases/snowflake.md)
* [Skapa ett dataflöde för en datakällanslutning i användargränssnittet](../../tutorials/ui/dataflow/databases.md)
