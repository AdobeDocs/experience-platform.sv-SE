---
keywords: SFTP;sftp
title: SFTP-mål
seo-title: SFTP-mål
description: Skapa en utgående liveanslutning till SFTP-servern för att regelbundet exportera avgränsade datafiler från Experience Platform.
seo-description: Skapa en utgående liveanslutning till SFTP-servern för att regelbundet exportera avgränsade datafiler från Experience Platform.
translation-type: tm+mt
source-git-commit: 67a353c950bef11ccbaa52c49d213f08449baa96
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---


# SFTP-mål

## Översikt

Skapa en utgående liveanslutning till SFTP-servern för att regelbundet exportera avgränsade datafiler från Experience Platform.

## Exporttyp {#export-type}

**Profilbaserad** - du exporterar alla medlemmar i ett segment tillsammans med önskade schemafält (till exempel: e-postadress, telefonnummer, efternamn), som du väljer på skärmen Välj attribut i arbetsflödet [för](/help/rtcdp/destinations/activate-destinations.md#select-attributes)målaktivering.

![Profilbaserad SFTP-exporttyp](/help/rtcdp/destinations/assets/sftp-export-type.png)

## Koppla mål {#connect-destination}

Mer information om hur du ansluter till molnlagringsmål, inklusive SFTP, finns [i arbetsflödet för ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)molnlagringsmål.

För SFTP-mål anger du följande information i arbetsflödet för att skapa mål i **autentiseringssteget** :

* **Värd**: adressen till SFTP-lagringsplatsen
* **Användarnamn**: användarnamnet för att logga in på din SFTP-lagringsplats
* **Lösenord**: lösenordet för att logga in på din SFTP-lagringsplats

## Exporterade data {#exported-data}

För SFTP-mål skapar Adobe Real-time CDP en tabbavgränsad `.txt` eller `.csv` fil på den lagringsplats som du angav. Mer information om filerna finns i [E-postmarknadsföringsmål och molnlagringsmål](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) i självstudiekursen om segmentaktivering.