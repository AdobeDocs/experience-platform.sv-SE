---
title: Arbetsflöde för molnlagringsmål
seo-title: Arbetsflöde för molnlagringsmål
description: Instruktioner för att ansluta till lagringsplatser i molnet
seo-description: Instruktioner för att ansluta till lagringsplatser i molnet
translation-type: tm+mt
source-git-commit: 3c598454a868139b7604c5c7ca2b98fa0f1bb961
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---


# Arbetsflöde för att skapa molnlagringsmål

## Översikt

På den här sidan beskrivs hur du kan ansluta till molnlagringsplatser i Adobe Real-time Customer Data Platform.

1. I **[!UICONTROL Connections > Destinations]** väljer du önskat molnlagringsmål och sedan **[!UICONTROL Connect destination]**.

   ![Anslut till molnlagringsmålet](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

2. Om du tidigare har konfigurerat en anslutning till molnlagringsmålet markerar du den befintliga anslutningen i **[!UICONTROL Authentication]** steget **[!UICONTROL Existing Account]** . Du kan också välja **[!UICONTROL New Account]** att konfigurera en ny anslutning till molnlagringsmålet. Fyll i autentiseringsuppgifter för ditt konto och välj **[!UICONTROL Connect to destination]**. <br> Se [Amazon S3](/help/rtcdp/destinations/amazon-s3-destination.md) -mål, [Amazon Kinesis](/help/rtcdp/destinations/amazon-kinesis-destination.md) -mål, [Azure Event Hubs](/help/rtcdp/destinations/azure-event-hubs-destination.md) -mål och [SFTP](/help/rtcdp/destinations/sftp-destination.md) -mål för mer information om inloggningsuppgifter i **autentiseringssteget** .

   >[!NOTE]
   >
   >Adobe CDP i realtid stöder validering av autentiseringsuppgifter i autentiseringsprocessen och visar ett felmeddelande om du anger felaktiga autentiseringsuppgifter för din molnlagringsplats. Detta säkerställer att du inte slutför arbetsflödet med felaktiga inloggningsuppgifter.

   ![Anslut till molnlagringsmålet - autentiseringssteg](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

3. I **[!UICONTROL Setup]** steget anger du ett **[!UICONTROL Name]** och ett **[!UICONTROL Description]** för aktiveringsflödet. <br>
I det här steget kan du även välja vilket som helst **[!UICONTROL Marketing use case]** som ska gälla för det här målet. Fall av marknadsanvändning anger avsikten för vilken data ska exporteras till destinationen. Du kan välja bland Adobes definierade användningsexempel för marknadsföring eller skapa ett eget exempel för marknadsföring. Mer information om användningsfall för marknadsföring finns på sidan [Datastyrning i CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) i realtid. Information om de enskilda användningsfallen för marknadsföring som definierats av Adobe finns i [översikten över](/help/data-governance/policies/overview.md#core-actions)dataanvändningspolicyn. <br>
För Amazon S3-destinationer anger du **[!UICONTROL Bucket name]** och **[!UICONTROL Folder path]** i molnlagringsdestinationen dit filerna ska levereras. Välj **[!UICONTROL Create Destination]** när du har fyllt i fälten ovan.

   ![Anslut till molnlagringsmålet för Amazon S3 - autentiseringssteg](/help/rtcdp/destinations/assets/amazon-s3-setup-step.png)

   För SFTP-mål anger du **[!UICONTROL Folder path]** var filerna ska levereras. Välj **[!UICONTROL Create Destination]** när du har fyllt i fälten ovan.

   ![Anslut till molnlagringsmålet för SFTP - autentiseringssteg](/help/rtcdp/destinations/assets/sftp-destinations-setup-step.png)

   Ange namnet på din befintliga dataström i ditt [!DNL Amazon Kinesis] konto för Amazon Kinesis-mål. Adobe CDP i realtid exporterar data till den här strömmen. Välj **[!UICONTROL Create Destination]** när du har fyllt i fälten ovan.

   ![Anslut till Kinesis molnlagringsmål - autentiseringssteg](/help/rtcdp/destinations/assets/kinesis-destinations-setup-step.png)

   Ange namnet på din befintliga dataström i ditt [!DNL Amazon Kinesis] konto för Azure Event Hubs-mål. Adobe CDP i realtid exporterar data till den här strömmen. Välj **[!UICONTROL Create Destination]** när du har fyllt i fälten ovan.

   ![Anslut till Kinesis molnlagringsmål - autentiseringssteg](/help/rtcdp/destinations/assets/eventhubs-destinations-setup-step.png)

4. Målet har skapats. Du kan välja **[!UICONTROL Save & Exit]** om du vill aktivera segment senare eller om du vill fortsätta med arbetsflödet och välja vilka segment **[!UICONTROL Next]** som ska aktiveras. I båda fallen finns mer information i nästa avsnitt, [Aktivera segment](#activate-segments), för resten av arbetsflödet för att exportera data.

## Aktivera segment {#activate-segments}

Mer information om arbetsflödet för [aktivering finns i Aktivera profiler och segment till ett mål](/help/rtcdp/destinations/activate-destinations.md) .