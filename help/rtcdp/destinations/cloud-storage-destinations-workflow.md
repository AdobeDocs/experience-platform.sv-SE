---
title: Arbetsflöde för molnlagringsmål
seo-title: Arbetsflöde för molnlagringsmål
description: Instruktioner för att ansluta till lagringsplatser i molnet
seo-description: Instruktioner för att ansluta till lagringsplatser i molnet
translation-type: tm+mt
source-git-commit: 9221c11a30bda3a155d73afec16be55ef8f5d133

---


# Arbetsflöde för att skapa molnlagringsmål

## Översikt

På den här sidan beskrivs hur du kan ansluta till molnlagringsplatser i Adobe Customer Data Platform i realtid.

1. Välj önskat molnlagringsmål i **[!UICONTROL Anslutningar > Destinationer]** och välj sedan **[!UICONTROL Anslut som mål]**.

   ![Anslut till molnlagringsmålet](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

2. Om du tidigare har konfigurerat en anslutning till molnlagringsmålet i **autentiseringssteget** väljer du **[!UICONTROL Befintligt konto]** och väljer din befintliga anslutning. Du kan också välja **[!UICONTROL Nytt konto]** för att konfigurera en ny anslutning till molnlagringsmålet. Fyll i autentiseringsuppgifterna för ditt konto och välj **[!UICONTROL Anslut till mål]**.

   >[!NOTE]
   >
   >Adobe CDP i realtid stöder validering av autentiseringsuppgifter i autentiseringsprocessen och visar ett felmeddelande om du anger felaktiga autentiseringsuppgifter för din molnlagringsplats. Detta säkerställer att du inte slutför arbetsflödet med felaktiga inloggningsuppgifter.

   ![Anslut till molnlagringsmålet - autentiseringssteg](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

3. Under **[!UICONTROL Konfigurera]** anger du ett **[!UICONTROL namn]** och en **[!UICONTROL beskrivning]** för aktiveringsflödet.
   1. För Amazon S3-mål anger du **[!UICONTROL Bucket-namnet]** och **[!UICONTROL Mappsökvägen]** i molnlagringsmålet där filerna ska levereras. Välj **[!UICONTROL Skapa mål]** när du har fyllt i fälten ovan.
   2. För SFTP-mål infogar du **[!UICONTROL mappsökvägen]**
   ![Anslut till molnlagringsmålet - autentiseringssteg](/help/rtcdp/destinations/assets/cloud-destinations-setup-step.png)

4. Målet har skapats. Du kan välja **[!UICONTROL Spara och avsluta]** om du vill aktivera segment senare eller om du vill fortsätta med arbetsflödet genom att välja **[!UICONTROL Nästa]** och välja segment som ska aktiveras. I båda fallen finns mer information i nästa avsnitt, [Aktivera segment](#activate-segments), för resten av arbetsflödet för att exportera data.

## Aktivera segment {#activate-segments}

Mer information om arbetsflödet för [aktivering finns i Aktivera profiler och segment till ett mål](/help/rtcdp/destinations/activate-destinations.md) .