---
keywords: personalisering, Mål. destination, personaliseringsplatser, konfigurera destinationer för personalisering, samma sida, nästa sida;
title: Konfigurera personaliseringsmål för personalisering på samma sida och nästa sida
type: Tutorial
seo-title: Configure personalization destinations for same-page and next-page personalization
description: Lär dig hur du konfigurerar personaliseringsmål för personalisering på samma sida och nästa sida
seo-description: Configure personalization destinations for same-page and next-page personalization
source-git-commit: 628e7a993a3566322e0249a5a9864cf6b3fe4493
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 1%

---


# Konfigurera personaliseringsmål för personalisering på samma sida och nästa sida

## Översikt {#overview}

Adobe Experience Platform använder [kantsegmentering](../../segmentation/ui/edge-segmentation.md) för att kunderna ska kunna skapa och inrikta sig på målgruppssegment i stor skala i realtid.

Den här funktionen hjälper er att konfigurera användningen av personalisering på samma sida och nästa sida.

I den här artikeln finns stegvisa instruktioner för hur du konfigurerar Experience Platform och dina anpassningsmål för dessa användningsfall.

## Steg 1: Konfigurera ett Experience Platform Web SDK-datastream {#configure-datastream}

Det första steget när du konfigurerar ditt användningsexempel för personalisering är att konfigurera en [!DNL Web SDK datastream].

Följ instruktionerna som beskrivs i [datastream-konfiguration](../../edge/fundamentals/datastreams.md) dokumentation.

## Steg 2: Konfigurera ditt personaliseringsmål {#configure-destination}

När du har konfigurerat dataströmmen kan du börja konfigurera ditt personaliseringsmål.

Följ [självstudiekurs om hur du skapar målanslutning](../ui/connect-destination.md) om du vill ha detaljerade anvisningar om hur du skapar en ny målanslutning.

Beroende på vilket mål du konfigurerar kan du läsa följande artiklar för att få information om målspecifika krav och relaterad information:

* [Adobe Target-anslutning](../catalog/personalization/adobe-target-connection.md)
* [Anpassad personaliseringsanslutning](../catalog/personalization/custom-personalization.md)

## Steg 3: Skapa en [!DNL Active-On-Edge] sammanfogningsprincip {#create-merge-policy}

När du har skapat målanslutningen måste du skapa en [!DNL Active-On-Edge] sammanfogningsprincip.

Följ instruktionerna på [skapa en sammanfogningsprincip](../../profile/merge-policies/ui-guide.md#create-a-merge-policy)och se till att aktivera **[!UICONTROL Active-On-Edge Merge Policy]** växla.

## Steg 4: Skapa ett nytt segment i plattformen {#create-segment}

När du har skapat [!DNL Active-On-Edge] måste du skapa ett nytt segment i Platform.

Följ [segmentbyggare](../../segmentation/ui/segment-builder.md) för att skapa ditt nya segment och se till att [tilldela den](../../segmentation/ui/segment-builder.md#merge-policies) den [!DNL Active-On-Edge] sammanfogningsprincip som du skapade i steg 3.

## Steg 5: Aktivera segmentet till målet

Det sista steget i konfigurationsprocessen är att aktivera segmentet som du skapade i steg 4 till målet som du skapade i steg 2.

Gör så här: [självstudiekurs om aktivering](../ui/activate-profile-request-destinations.md).

## Validera konfigurationen {#validate-configuration}

När du har följt stegen ovan bör du se de nya segmenten i ditt personaliseringsmål.