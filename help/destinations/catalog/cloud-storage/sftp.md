---
keywords: SFTP;sftp
title: SFTP-anslutning
description: Skapa en utgående liveanslutning till SFTP-servern för att regelbundet exportera avgränsade datafiler från Experience Platform.
translation-type: tm+mt
source-git-commit: e13a19640208697665b0a7e0106def33fd1e456d
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# SFTP-anslutning

Skapa en utgående liveanslutning till SFTP-servern för att regelbundet exportera avgränsade datafiler från Experience Platform.

## Exporttyp {#export-type}

**Profilbaserat**  - du exporterar alla medlemmar i ett segment tillsammans med önskade schemafält (till exempel: e-postadress, telefonnummer, efternamn), som du väljer på skärmen Välj attribut i arbetsflödet [ för ](../../ui/activate-destinations.md#select-attributes)målaktivering.

![Profilbaserad SFTP-exporttyp](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Anslutningsmål {#connect-destination}

Mer information om hur du ansluter till molnlagringsmål, inklusive SFTP, finns i [Arbetsflöde för molnlagringsmål ](./workflow.md).

För SFTP-mål anger du följande information i arbetsflödet för att skapa mål i steget **Autentisering**:

* **Värd**: Adress till din SFTP-lagringsplats
* **Användarnamn**: Användarnamnet som loggas in på din SFTP-lagringsplats
* **Lösenord**: Lösenordet för att logga in på din SFTP-lagringsplats

## Exporterade data {#exported-data}

För SFTP-mål skapar Platform en tabbavgränsad `.txt`- eller `.csv`-fil på den angivna lagringsplatsen. Mer information om filerna finns i [E-postmarknadsföringsmål och molnlagringsmål](../../ui/activate-destinations.md#esp-and-cloud-storage) i självstudiekursen om segmentaktivering.