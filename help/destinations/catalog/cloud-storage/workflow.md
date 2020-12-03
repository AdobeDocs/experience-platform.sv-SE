---
keywords: cloud storage destination;cloud storage
title: Arbetsflöde för molnlagringsmål
seo-title: Arbetsflöde för molnlagringsmål
type: Tutorial
description: Instruktioner för att ansluta till lagringsplatser i molnet
seo-description: Instruktioner för att ansluta till lagringsplatser i molnet
translation-type: tm+mt
source-git-commit: 24c8dd0f01d7ea14b2fa5827722e797bd209f50c
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 0%

---


# Arbetsflöde för att skapa molnlagringsmål

## Översikt

På den här sidan beskrivs hur du kan ansluta till molnlagringsplatser i kunddataplattformen i realtid.

I **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** väljer du önskat molnlagringsmål och väljer sedan **[!UICONTROL Configure]**.

![Anslut till molnlagringsmålet](../../assets/catalog/cloud-storage/workflow/connect.png)

>[!NOTE]
>
>Om det redan finns en anslutning till det här målet kan du se en **[!UICONTROL Activate]** knapp på målkortet. Mer information om skillnaden mellan **[!UICONTROL Activate]** och **[!UICONTROL Configure]** finns i avsnittet [Katalog](../../ui/destinations-workspace.md#catalog) i dokumentationen för målarbetsytan.

Om du tidigare har konfigurerat en anslutning till molnlagringsmålet markerar du den befintliga anslutningen i **[!UICONTROL Authentication]** steget **[!UICONTROL Existing Account]** . Du kan också välja **[!UICONTROL New Account]** att konfigurera en ny anslutning till molnlagringsmålet. Fyll i autentiseringsuppgifter för ditt konto och välj **[!UICONTROL Connect to destination]**. Du kan också bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering till de exporterade filerna. Observera att den här offentliga nyckeln **måste** skrivas som en Base64-kodad sträng.

Mer information om inloggningsuppgifter finns i [Amazon S3](./amazon-s3.md) -målet, [[!DNL Amazon Kinesis]](./amazon-kinesis.md) -målet, - [[!DNL Azure Event Hubs]](./azure-event-hubs.md) målet och [SFTP](./sftp.md) -målet i **autentiseringssteget** .

>[!NOTE]
>
>CDP stöder validering av autentiseringsuppgifter i realtid i autentiseringsprocessen och visar ett felmeddelande om du anger felaktiga autentiseringsuppgifter för din molnlagringsplats. Detta säkerställer att du inte slutför arbetsflödet med felaktiga inloggningsuppgifter.

![Anslut till molnlagringsmålet - autentiseringssteg](../../assets/catalog/cloud-storage/workflow/destination-account.png)

I **[!UICONTROL Setup]** steget anger du ett **[!UICONTROL Name]** och ett **[!UICONTROL Description]** för aktiveringsflödet.

I det här steget kan du även välja vilket som helst **[!UICONTROL Marketing use case]** som ska gälla för det här målet. Fall av marknadsanvändning anger avsikten för vilken data ska exporteras till destinationen. Du kan välja bland Adobe-definierade användningsfall för marknadsföring eller skapa ett eget marknadsföringsexempel. Mer information om användningsfall för marknadsföring finns på sidan [Datastyrning i CDP](../../../rtcdp/privacy/data-governance-overview.md#destinations) i realtid. Mer information om de enskilda Adobe-definierade användningsfallen för marknadsföring finns i översikten över [dataanvändningspolicyn](../../../data-governance/policies/overview.md#core-actions).

För Amazon S3-destinationer anger du **[!UICONTROL Bucket name]** och **[!UICONTROL Folder path]** i molnlagringsdestinationen dit filerna ska levereras. Välj **[!UICONTROL Create Destination]** när du har fyllt i fälten ovan.

![Anslut till molnlagringsmålet för Amazon S3 - autentiseringssteg](../../assets/catalog/cloud-storage/workflow/amazon-s3-setup.png)

För SFTP-mål anger du **[!UICONTROL Folder path]** var filerna ska levereras. Välj **[!UICONTROL Create Destination]** när du har fyllt i fälten ovan.

![Anslut till molnlagringsmålet för SFTP - autentiseringssteg](../../assets/catalog/cloud-storage/workflow/sftp-setup.png)

Ange namnet på din befintliga dataström i ditt [!DNL Amazon Kinesis] konto för [!DNL Amazon Kinesis] destinationer. CDP-data exporteras i realtid till den här strömmen. Välj **[!UICONTROL Create Destination]** när du har fyllt i fälten ovan.

![Ansluta till Kinesis molnlagringsmål - autentiseringssteg](../../assets/catalog/cloud-storage/workflow/kinesis-setup.png)

Ange namnet på din befintliga dataström i ditt [!DNL Azure Event Hubs] konto för [!DNL Amazon Event Hubs] destinationer. CDP-data exporteras i realtid till den här strömmen. Välj **[!UICONTROL Create Destination]** när du har fyllt i fälten ovan.

![Anslut till molnlagringsmålet för Event Hubs - autentiseringssteg](../../assets/catalog/cloud-storage/workflow/event-hubs-setup.png)

Målet har skapats. Du kan välja **[!UICONTROL Save & Exit]** om du vill aktivera segment senare eller om du vill fortsätta med arbetsflödet och välja vilka segment **[!UICONTROL Next]** som ska aktiveras. I båda fallen finns mer information i nästa avsnitt, [Aktivera segment](#activate-segments), för resten av arbetsflödet för att exportera data.

## Aktivera segment {#activate-segments}

Mer information om arbetsflödet för [aktivering finns i Aktivera profiler och segment till ett mål](../../ui/activate-destinations.md) .