---
title: Snowflake Source Connector - översikt
description: Lär dig hur du ansluter Snowflake till Adobe Experience Platform med API:er eller användargränssnittet.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 0%

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
* Navigera till [!DNL Default Role] i fönstret [!DNL Edit user] som visas för att visa rollen som är associerad med den angivna användaren.
* I samma fönster går du till [!DNL Default Warehouse] för att visa det lagerställe som är associerat med den angivna användaren.

![Användargränssnittet i Snowflake där du kan verifiera din roll och ditt lager.](../../images/tutorials/create/snowflake/snowflake-configs.png)

När kodningen är klar kan du sedan använda den [!DNL Base64]-kodade privata nyckeln på Experience Platform för att autentisera ditt [!DNL Snowflake]-konto.

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress tillåtelselista](../../ip-address-allow-list.md).

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Snowflake] till Experience Platform med API:er eller användargränssnittet:

## Anslut [!DNL Snowflake] till Experience Platform med API:er

* [Skapa en Snowflake-basanslutning med API:t för Flow Service](../../tutorials/api/create/databases/snowflake.md)
* [Utforska datatabeller med API:t för Flow Service](../../tutorials/api/explore/tabular.md)
* [Skapa ett dataflöde för en datakälla med API:t för Flow Service](../../tutorials/api/collect/database-nosql.md)

## Anslut [!DNL Snowflake] till Experience Platform med användargränssnittet

* [Skapa en Snowflake-källanslutning i användargränssnittet](../../tutorials/ui/create/databases/snowflake.md)
* [Skapa ett dataflöde för en datakällanslutning i användargränssnittet](../../tutorials/ui/dataflow/databases.md)
