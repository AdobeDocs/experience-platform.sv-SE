---
title: Översikt över Snowflake
description: Läs mer om hur du vidarebefordrar händelser i Snowflake i Adobe Experience Platform.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: abddf0c4-3d4c-4f66-a6e0-c10b54ea3430
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 0%

---

# [!DNL Snowflake] översikt

[[!DNL Snowflake]](https://www.snowflake.com/en/) är ett molndatalager som kan lagra och analysera alla dina dataposter på ett och samma ställe. Den kan användas för datalagerhantering, datalager, datateknik, datavetenskap, dataapplikationsutveckling samt säker delning och användning av realtidsdata eller delade data.

[!DNL Snowflake] är byggd ovanpå Amazon Web Services (AWS), Microsoft Azure (Azure) och Google Cloud Platform (GCP).

![Ett diagram som visar [!DNL Snowflake] dataarkitektur.](../../../images/extensions/server/snowflake/snowflake.png)

## Integrering med Snowflake

Ett Snowflake-konto kan finnas på någon av följande molnplattformar:

- [AMAZON WEB SERVICES ([!DNL AWS])](https://aws.amazon.com/) - [!DNL AWS] är en plattform för cloud computing som erbjuder ett brett utbud av tjänster som distribuerad datorhantering, databaslagring, innehållsleverans och SaaS-integrationstjänster (Software-as-a-service) för kundrelationshantering (CRM) och resursplanering (ERP) för företag.

Se [[!DNL AWS] översikt](../aws/overview.md) om du vill ha mer information om hur du installerar tillägget och konfigurerar regler för vidarebefordran av händelser.

- [Microsoft Azure ([!DNL Azure])](https://azure.microsoft.com/en-us/products/event-hubs/#overview) - [!DNL Azure] är en plattform för cloud computing och en onlineportal som gör att du kan komma åt och hantera molntjänster och molnresurser från Microsoft.

Se [[!DNL Azure] översikt](../azure/overview.md) om du vill ha mer information om hur du installerar tillägget och konfigurerar regler för vidarebefordran av händelser.

- [[!DNL Google Cloud Platform]](https://cloud.google.com/) - [!DNL Google Cloud Platform] är en plattform för cloud computing som erbjuder ett brett utbud av tjänster som distribuerad datorhantering, databaslagring, innehållsleverans och SaaS-integrationstjänster (Software-as-a-service) för kundrelationshantering (CRM) och resursplanering (ERP) för företag.

Se [[!DNL Google Cloud Platform] översikt](../google-cloud-platform/overview.md) om du vill ha mer information om hur du installerar tillägget och konfigurerar regler för vidarebefordran av händelser.

Vårt inbyggda [[!DNL AWS]](../aws/overview.md), [[!DNL Azure]](../azure/overview.md)och [[!DNL Google Cloud Platform]](../google-cloud-platform/overview.md) tillägg för vidarebefordran av händelser gör det möjligt för kunder att samla in, berika och vidarebefordra sina data på händelseservern i realtid till sina molntjänster för att kunna utnyttjas av [!DNL Snowflake]. Se nedan:

![The [!DNL Snowflake] rapportdiagram som visar länken mellan [!DNL AWS] och [!DNL Azure].](../../../images/extensions/server/snowflake/snowflake-workflow.png)

## Nästa steg

Den här guiden innehåller en översikt över [!DNL Snowflake] och användningen av [!DNL AWS] och [!DNL Azure] tillägg för händelsevidarebefordran.

Mer information om [!DNL AWS] och [!DNL Azure] funktioner för att vidarebefordra händelser i Experience Platform, se [[!DNL AWS] tilläggsöversikt](../aws/overview.md) och [[!DNL Azure] tilläggsöversikt](../azure/overview.md).
