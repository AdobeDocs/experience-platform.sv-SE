---
title: Arbetsflöde för molnlagringsmål
seo-title: Arbetsflöde för molnlagringsmål
description: Instruktioner för att ansluta till lagringsplatser i molnet
seo-description: Instruktioner för att ansluta till lagringsplatser i molnet
translation-type: tm+mt
source-git-commit: c4f1c0a6ef4d16e5fe763826016d56506fdca5dc

---


# Arbetsflöde för att skapa molnlagringsmål

## Översikt

På den här sidan beskrivs hur du kan ansluta till molnlagringsplatser i Adobe Customer Data Platform i realtid.

1. I **[!UICONTROL Connections > Destinations]** väljer du önskat molnlagringsmål och sedan **[!UICONTROL Connect destination]**.

   ![Anslut till molnlagringsmålet](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

1. Om du tidigare har konfigurerat en anslutning till molnlagringsmålet i **autentiseringssteget** markerar du **[!UICONTROL Existing Account]** och väljer den befintliga anslutningen. Du kan också välja **[!UICONTROL New Account]** att konfigurera en ny anslutning till molnlagringsmålet. Fyll i autentiseringsuppgifter för ditt konto och välj **[!UICONTROL Connect to destination]**. Se [Amazon S3-mål](/help/rtcdp/destinations/amazon-s3-destination.md) och [SFTP-mål](/help/rtcdp/destinations/sftp-destination.md) för mer information om inloggningsuppgifter i steget **Autentisering** .

   >[!NOTE]
   >
   >Adobe CDP i realtid stöder validering av autentiseringsuppgifter i autentiseringsprocessen och visar ett felmeddelande om du anger felaktiga autentiseringsuppgifter för din molnlagringsplats. Detta säkerställer att du inte slutför arbetsflödet med felaktiga inloggningsuppgifter.

   ![Anslut till molnlagringsmålet - autentiseringssteg](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

1. I **[!UICONTROL Setup]** steget anger du ett **[!UICONTROL Name]** och ett **[!UICONTROL Description]** för aktiveringsflödet. <br>
För Amazon S3-destinationer anger du **[!UICONTROL Bucket name]** och **[!UICONTROL Folder path]** i molnlagringsdestinationen dit filerna ska levereras. Välj **[!UICONTROL Create Destination]** när du har fyllt i fälten ovan.

   ![Anslut till molnlagringsmålet för Amazon S3 - autentiseringssteg](/help/rtcdp/destinations/assets/cloud-destinations-setup-step.png)



   <br>För SFTP-mål infogar du **[!UICONTROL Folder path]**

   ![Anslut till molnlagringsmålet för SFTP - autentiseringssteg](/help/rtcdp/destinations/assets/sftp-destinations-setup-step.png)

1. Målet har skapats. Du kan välja **[!UICONTROL Save & Exit]** om du vill aktivera segment senare eller om du vill fortsätta med arbetsflödet och välja vilka segment **[!UICONTROL Next]** som ska aktiveras. I båda fallen finns mer information i nästa avsnitt, [Aktivera segment](#activate-segments), för resten av arbetsflödet för att exportera data.

## Aktivera segment {#activate-segments}

Mer information om arbetsflödet för [aktivering finns i Aktivera profiler och segment till ett mål](/help/rtcdp/destinations/activate-destinations.md) .