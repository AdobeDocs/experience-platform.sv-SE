---
keywords: Experience Platform;hem;populära ämnen;dataåtkomst;python sdk;spark sdk;data access api
solution: Experience Platform
title: Översikt över dataåtkomst
topic: overview
description: Data Access stöder Adobe Experience Platform genom att tillhandahålla användarverktyg som fokuserar på att upptäcka och tillgängliggöra inkapslade plattformsdatauppsättningar.
translation-type: tm+mt
source-git-commit: 37c1c98ccba50fa917acc5e93763294f4dde5c36
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 1%

---


# [!DNL Data Access] översikt

[!DNL Data Access] stöder Adobe Experience Platform genom att tillhandahålla användarverktyg som fokuserar på att upptäcka och tillgängliggöra inkapslade datauppsättningar i  [!DNL Experience Platform].

![Dataåtkomst i Experience Platform](images/Data_Access_Experience_Platform.png)

## [!DNL Data Access] API

Detaljerad information om hur du använder API:t [!DNL Data Access] för att ansluta till [!DNL Platform] finns i [Utvecklarhandboken för dataåtkomst](api.md).

## Åtkomst till data i arbetsytan Datavetenskap

Du kan läsa och skriva till datauppsättningar med [!DNL Python] och [!DNL Spark] för recept- och modellutveckling i Data Science Workspace. Mer information om hur du får åtkomst till dina data finns i [dokumentationen för Python-dataåtkomst](../data-science-workspace/authoring/python.md) eller [Spark-dataåtkomst](../data-science-workspace/authoring/spark.md).

Mer information om [!DNL Data Science Workspace] får du genom att läsa översikten [Data Science Workspace](../data-science-workspace/home.md).

## Prenumerera på dataöverföringshändelser

[!DNL Platform] gör specifika värdefulla händelser tillgängliga för prenumeration via  [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui). Du kan t.ex. prenumerera på dataöverföringshändelser för att få meddelanden om eventuella förseningar och fel. Mer information finns i självstudiekursen om [att prenumerera på meddelanden om dataöverföring](../ingestion/quality/subscribe-events.md).