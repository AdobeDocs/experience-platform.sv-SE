---
title: Azure Synapse Analytics Source Connector - översikt
description: Lär dig hur du ansluter Azure Synapse Analytics till Adobe Experience Platform med API:er eller användargränssnittet.
badgeUltimate: label="Ultimate" type="Positive"
last-substantial-update: 2025-06-17T00:00:00Z
exl-id: 5b94ae74-e5a7-40e9-a952-41eddf06dcde
source-git-commit: f8eb8640360205e8ae9579d4b664d4880bf8a368
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---

# [!DNL Azure Synapse Analytics]

>[!IMPORTANT]
>
>Källan [!DNL Azure Synapse Analytics] är tillgänglig i källkatalogen för användare som har köpt Real-Time Customer Data Platform Ultimate.

[!DNL Azure Synapse Analytics] är en molnbaserad analystjänst som förenar lagring av big data och data. Du kan importera, utforska, förbereda och analysera data med hjälp av SQL-, [!DNL Spark]- eller realtidsverktyg - allt utan att behöva flytta dina data.

Du kan använda källan [!DNL Azure Synapse Analytics] för att ansluta ditt konto och överföra dina data till Adobe Experience Platform.

## Förhandskrav {#prerequisites}

Läs följande avsnitt för att slutföra kravkonfigurationen innan du ansluter ditt [!DNL Azure Synapse Analytics]-konto till Experience Platform.

### IP-adress tillåtelselista

Du måste lägga till regionspecifika IP-adresser i tillåtelselista innan du kan ansluta dina källor till Experience Platform. Mer information finns i guiden om att [tillåtslista IP-adresser för att ansluta till Experience Platform](../../ip-address-allow-list.md).

### Konfigurera behörigheter

Om du vill ansluta ditt källkonto till Experience Platform måste båda följande behörigheter vara aktiverade för ditt konto:

* **Visa källor**
* **Hantera källor**

Om du inte har de här behörigheterna kontaktar du produktadministratören och begär åtkomst. Mer information finns i [användargränssnittsguiden för åtkomstkontroll](../../../access-control/ui/overview.md).

### Autentisera till Experience Platform

Du kan använda autentisering av kontonyckel eller autentisering av tjänstens huvudnyckel för att ansluta [!DNL Azure Synapse Analytics] till Experience Platform.

>[!BEGINTABS]

>[!TAB Autentisering av kontonyckel]

Ange värden för följande autentiseringsuppgifter för att ansluta din [!DNL Azure Synapse Analytics]-databas till Experience Platform med autentisering av kontonycklar.

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Anslutningssträng | Det här är **anslutningssträngen** som används för autentisering med [!DNL Azure Synapse Analytics]. Standardformatet är: `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`. Du måste ersätta platshållarna med den faktiska anslutningsinformationen. |
| Anslutningsspecifikation-ID | Anslutningsspecifikationen **för** innehåller anslutningsegenskaperna för en datakälla. Detta innehåller information som autentiseringsspecifikationer och krav för att skapa både **base** - och **source** -anslutningar. För [!DNL Azure Synapse Analytics] är anslutningsspec-ID: `a49bcc7d-8038-43af-b1e4-5a7a089a7d79`. **Obs!** Den här autentiseringsuppgiften behövs bara när du ansluter via API:er. |

>[!TAB Autentisering av tjänstens huvudnyckel]

Om du vill hämta dina autentiseringsuppgifter för autentisering av tjänstens huvudnyckel går du till [[!DNL Microsfot Entra admin center]](https://entra.microsoft.com/#home) och hämtar värden för följande:

* Program-ID
* Visningsnamn
* Hemlighet
* Klient-ID

Navigera sedan till din [[!DNL Azure Synapse Analytics] instans](https://azure.microsoft.com/en-ca/products/synapse-analytics) och välj alternativet att skapa en användare från en extern leverantör. Här anger du lämplig behörighet för tjänstens huvudnamn i schemat. **OBS!**: Du måste inkludera SELECT eftersom det krävs för schemaförhandsgranskning, ungefär som COPY. Exempelkommandot kan till exempel vara:

```SQL
GRANT SELECT ON SCHEMA::dbo TO {APP_ID};
```

Ange värden för följande autentiseringsuppgifter för att ansluta din [!DNL Azure Synapse Analytics]-databas till Experience Platform med autentisering av tjänstens huvudnyckel.

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Server | Det fullständiga kvalificerade domännamnet för SQL-slutpunkten [!DNL Azure Synapse Analytics]. |
| Databas | Namnet på den specifika databasen på arbetsytan för [!DNL Azure Synapse Analytics]. |
| Klientorganisation | Det [!DNL Azure Active Directory]-klientorganisations-ID som är kopplat till din [!DNL Azure]-prenumeration. |
| Tjänsthuvudnamn-ID | Klient-ID för ett [!DNL Azure Active Directory]-program. |
| Huvudnyckel för tjänst | Klienthemligheten eller lösenordet som är kopplat till tjänstens huvudnamn. |
| Anslutningsspecifikation-ID | Anslutningsspecifikationen **för** innehåller anslutningsegenskaperna för en datakälla. Detta innehåller information som autentiseringsspecifikationer och krav för att skapa både **base** - och **source** -anslutningar. För [!DNL Azure Synapse Analytics] är anslutningsspec-ID: `a49bcc7d-8038-43af-b1e4-5a7a089a7d79`. **Obs!** Den här autentiseringsuppgiften behövs bara när du ansluter via API:er. |

Mer information finns i [[!DNL Azure] dokumentationen om att hantera identiteter för  [!DNL Azure Synapse Analytics]](https://learn.microsoft.com/en-us/azure/synapse-analytics/synapse-service-identity).

>[!ENDTABS]

## Anslut [!DNL Azure Synapse Analytics] till Experience Platform med API:er

* [Anslut [!DNL Azure Synapse Analytics] till Experience Platform med API:t för Flow Service](../../tutorials/api/create/databases/synapse-analytics.md)
* [Utforska datatabeller med API:t för Flow Service](../../tutorials/api/explore/tabular.md)
* [Skapa ett dataflöde för en datakälla med API:t för Flow Service](../../tutorials/api/collect/database-nosql.md)

## Anslut [!DNL Azure Synapse Analytics] till Experience Platform med användargränssnittet

* [Anslut [!DNL Azure Synapse Analytics] till Experience Platform i användargränssnittet](../../tutorials/ui/create/databases/synapse-analytics.md)
* [Skapa ett dataflöde för en datakällanslutning i användargränssnittet](../../tutorials/ui/dataflow/databases.md)

