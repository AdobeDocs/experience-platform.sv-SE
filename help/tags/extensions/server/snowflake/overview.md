---
title: Översikt över Snowflake
description: Läs mer om hur du vidarebefordrar händelser i Snowflake i Adobe Experience Platform.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: abddf0c4-3d4c-4f66-a6e0-c10b54ea3430
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# [!DNL Snowflake] översikt

[[!DNL Snowflake]](https://www.snowflake.com/en/) är ett molndatalager som kan lagra och analysera alla dina dataposter på ett och samma ställe. Den kan användas för datalagerhantering, datalager, datateknik, datavetenskap, dataapplikationsutveckling samt säker delning och användning av realtidsdata eller delade data.

[!DNL Snowflake] byggs ovanpå Amazon Web Services (AWS), Microsoft Azure (Azure) och Google Cloud Platform (GCP).

![Ett diagram som visar [!DNL Snowflake]-dataarkitekturen.](../../../images/extensions/server/snowflake/snowflake.png)

## Integrering med Snowflake

Ett Snowflake-konto kan finnas på någon av följande molnplattformar:

- [Amazon Web Services ([!DNL AWS])](https://aws.amazon.com/) - [!DNL AWS] är en molnbaserad datorplattform som erbjuder en rad olika tjänster, till exempel distribuerad datorhantering, databaslagring, innehållsleverans och SaaS-integrationstjänster (Software-as-service) för kundrelationshantering (CRM) och resursplanering (ERP) för företag.

Mer information om hur du installerar tillägget och konfigurerar reglerna för händelsevidarebefordran finns i [[!DNL AWS] översikten](../aws/overview.md).

- [Microsoft Azure ([!DNL Azure])](https://azure.microsoft.com/en-us/products/event-hubs/#overview) - [!DNL Azure] är en molnbaserad datorplattform och en onlineportal där du kan komma åt och hantera molntjänster och molnresurser som tillhandahålls av Microsoft.

Mer information om hur du installerar tillägget och konfigurerar reglerna för händelsevidarebefordran finns i [[!DNL Azure] översikten](../azure/overview.md).

- [[!DNL Google Cloud Platform]](https://cloud.google.com/) - [!DNL Google Cloud Platform] är en molnbaserad datorplattform som erbjuder en mängd olika tjänster, till exempel distribuerad databehandling, databaslagring, innehållsleverans och SaaS-integrationstjänster (Software-as-a-service) för kundrelationshantering (CRM) och resursplanering (ERP).

Mer information om hur du installerar tillägget och konfigurerar reglerna för händelsevidarebefordran finns i [[!DNL Google Cloud Platform] översikten](../google-cloud-platform/overview.md).

Våra interna [[!DNL AWS]](../aws/overview.md)-, [[!DNL Azure]](../azure/overview.md)- och [[!DNL Google Cloud Platform]](../google-cloud-platform/overview.md)-tillägg för händelsevidarebefordran gör det möjligt för kunder att samla in, berika och vidarebefordra sin händelsedatadrift på serversidan i realtid till sina molntjänster som ska användas av [!DNL Snowflake]. Se nedan:

![Rapportdiagrammet [!DNL Snowflake] som visar länken mellan [!DNL AWS] och [!DNL Azure].](../../../images/extensions/server/snowflake/snowflake-workflow.png)

## Nästa steg

Den här guiden gav en översikt över [!DNL Snowflake] och användningen av tillägg för vidarebefordran av händelser för [!DNL AWS] och [!DNL Azure].

Mer information om funktionerna för att vidarebefordra [!DNL AWS] och [!DNL Azure] händelser i Experience Platform finns i [[!DNL AWS] tilläggsöversikten](../aws/overview.md) och [[!DNL Azure] tilläggsöversikten](../azure/overview.md).
