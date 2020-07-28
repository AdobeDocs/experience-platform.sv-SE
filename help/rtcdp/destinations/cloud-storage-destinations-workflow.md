---
title: Arbetsflöde för molnlagringsmål
seo-title: Arbetsflöde för molnlagringsmål
description: Instruktioner för att ansluta till lagringsplatser i molnet
seo-description: Instruktioner för att ansluta till lagringsplatser i molnet
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---


# Arbetsflöde för att skapa molnlagringsmål

## Översikt

På den här sidan beskrivs hur du kan ansluta till molnlagringsplatser i Adobe Real-time Customer Data Platform.

1. I **[!UICONTROL Connections > Destinations]** väljer du önskat molnlagringsmål och sedan **[!UICONTROL Connect destination]**.

   ![Anslut till molnlagringsmålet](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

2. Om du tidigare har konfigurerat en anslutning till molnlagringsmålet markerar du den befintliga anslutningen i **[!UICONTROL Authentication]** steget **[!UICONTROL Existing Account]** . Du kan också välja **[!UICONTROL New Account]** att konfigurera en ny anslutning till molnlagringsmålet. Fyll i autentiseringsuppgifter för ditt konto och välj **[!UICONTROL Connect to destination]**. <br> Mer information om inloggningsuppgifter finns i [Amazon S3](/help/rtcdp/destinations/amazon-s3-destination.md) -målet, [!DNL Amazon Kinesis](/help/rtcdp/destinations/amazon-kinesis-destination.md) -målet, - [!DNL Azure Event Hubs](/help/rtcdp/destinations/azure-event-hubs-destination.md) målet och [SFTP](/help/rtcdp/destinations/sftp-destination.md) -målet i **autentiseringssteget** .

   >[!NOTE]
   >
   >CDP i realtid i Adobe stöder validering av autentiseringsuppgifter i autentiseringsprocessen och visar ett felmeddelande om du anger felaktiga autentiseringsuppgifter för din molnlagringsplats. Detta säkerställer att du inte slutför arbetsflödet med felaktiga inloggningsuppgifter.

   ![Anslut till molnlagringsmålet - autentiseringssteg](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

3. I **[!UICONTROL Setup]** steget anger du ett **[!UICONTROL Name]** och ett **[!UICONTROL Description]** för aktiveringsflödet. <br>
I det här steget kan du även välja vilket som helst **[!UICONTROL Marketing use case]** som ska gälla för det här målet. Fall av marknadsanvändning anger avsikten för vilken data ska exporteras till destinationen. Du kan välja bland Adobe-definierade användningsfall för marknadsföring eller skapa ett eget marknadsföringsexempel. Mer information om användningsfall för marknadsföring finns på sidan [Datastyrning i CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) i realtid. Mer information om de enskilda Adobe-definierade användningsfallen för marknadsföring finns i översikten över [dataanvändningspolicyn](/help/data-governance/policies/overview.md#core-actions). <br>
För Amazon S3-destinationer anger du **[!UICONTROL Bucket name]** och **[!UICONTROL Folder path]** i molnlagringsdestinationen dit filerna ska levereras. Välj **[!UICONTROL Create Destination]** när du har fyllt i fälten ovan.

   ![Anslut till molnlagringsmålet för Amazon S3 - autentiseringssteg](/help/rtcdp/destinations/assets/amazon-s3-setup-step.png)

   För SFTP-mål anger du **[!UICONTROL Folder path]** var filerna ska levereras. Välj **[!UICONTROL Create Destination]** när du har fyllt i fälten ovan.

   ![Anslut till molnlagringsmålet för SFTP - autentiseringssteg](/help/rtcdp/destinations/assets/sftp-destinations-setup-step.png)

   Ange namnet på din befintliga dataström i ditt [!DNL Amazon Kinesis] konto för [!DNL Amazon Kinesis] destinationer. Adobe CDP i realtid exporterar data till den här strömmen. Välj **[!UICONTROL Create Destination]** när du har fyllt i fälten ovan.

   ![Ansluta till Kinesis molnlagringsmål - autentiseringssteg](/help/rtcdp/destinations/assets/kinesis-destinations-setup-step.png)

   Ange namnet på din befintliga dataström i ditt [!DNL Azure Event Hubs] konto för [!DNL Amazon Kinesis] destinationer. Adobe CDP i realtid exporterar data till den här strömmen. Välj **[!UICONTROL Create Destination]** när du har fyllt i fälten ovan.

   ![Ansluta till Kinesis molnlagringsmål - autentiseringssteg](/help/rtcdp/destinations/assets/eventhubs-destinations-setup-step.png)

4. Målet har skapats. Du kan välja **[!UICONTROL Save & Exit]** om du vill aktivera segment senare eller om du vill fortsätta med arbetsflödet och välja vilka segment **[!UICONTROL Next]** som ska aktiveras. I båda fallen finns mer information i nästa avsnitt, [Aktivera segment](#activate-segments), för resten av arbetsflödet för att exportera data.

## Aktivera segment {#activate-segments}

Mer information om arbetsflödet för [aktivering finns i Aktivera profiler och segment till ett mål](/help/rtcdp/destinations/activate-destinations.md) .