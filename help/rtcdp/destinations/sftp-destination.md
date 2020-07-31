---
title: SFTP-mål
seo-title: SFTP-mål
description: Skapa en utgående liveanslutning till SFTP-servern för att regelbundet exportera avgränsade datafiler från Experience Platform.
seo-description: Skapa en utgående liveanslutning till SFTP-servern för att regelbundet exportera avgränsade datafiler från Experience Platform.
translation-type: tm+mt
source-git-commit: 098dd31be4d6ee6971cd87bcbfe0f686e34918e1
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 0%

---


# SFTP-mål

## Översikt

Skapa en utgående liveanslutning till SFTP-servern för att regelbundet exportera avgränsade datafiler från Experience Platform.

Så här exporterar du data:

## Koppla mål {#connect-destination}

Mer information om hur du ansluter till molnlagringsmål, inklusive SFTP, finns [i arbetsflödet för ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)molnlagringsmål.

För SFTP-mål anger du följande information i arbetsflödet för att skapa mål i **autentiseringssteget** :

* **Värd**: adressen till SFTP-lagringsplatsen
* **Användarnamn**: användarnamnet för att logga in på din SFTP-lagringsplats
* **Lösenord**: lösenordet för att logga in på din SFTP-lagringsplats

## Exporterade data {#exported-data}

För [!SFTP] mål skapar Adobe Real-time CDP en tabbavgränsad fil `.txt` eller `.csv` fil på den lagringsplats som du angav. Mer information om filerna finns i [E-postmarknadsföringsmål och molnlagringsmål](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) i självstudiekursen om segmentaktivering.