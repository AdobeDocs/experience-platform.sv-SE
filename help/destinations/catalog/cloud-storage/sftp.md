---
keywords: SFTP;sftp
title: SFTP-anslutning
description: Skapa en utgående liveanslutning till SFTP-servern för att regelbundet exportera avgränsade datafiler från Adobe Experience Platform.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: a21abb44bb9cbe6fefa0ff70a1ff19e31cc0c7de
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---

# SFTP-anslutning

## Översikt {#overview}

Skapa en utgående liveanslutning till SFTP-servern för att regelbundet exportera avgränsade datafiler från Adobe Experience Platform.

>[!IMPORTANT]
>
> Adobe stöder dataexport till SFTP-servrar, men de rekommenderade molnlagringsplatserna för dataexport är [!DNL Amazon S3] och [!DNL Azure Blob].

## Exporttyp {#export-type}

**Profilbaserat**  - du exporterar alla medlemmar i ett segment tillsammans med önskade schemafält (till exempel: e-postadress, telefonnummer, efternamn), som du väljer på skärmen Välj attribut i arbetsflödet [ för ](../../ui/activate-destinations.md#select-attributes)målaktivering.

![Profilbaserad SFTP-exporttyp](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Anslutningsmål {#connect-destination}

Mer information om hur du ansluter till molnlagringsmål, inklusive SFTP, finns i arbetsflödet [för molnlagringsmål ](./workflow.md).

För SFTP-mål anger du följande information i arbetsflödet för att skapa mål i steget **Autentisering**:

* **Värd**: Adress till din SFTP-lagringsplats
* **Användarnamn**: Användarnamnet som loggas in på din SFTP-lagringsplats
* **Lösenord**: Lösenordet för att logga in på din SFTP-lagringsplats

## Exporterade data {#exported-data}

För [!DNL SFTP]-mål skapar Plattform en tabbavgränsad `.csv`-fil på den angivna lagringsplatsen. Mer information om filerna finns i [E-postmarknadsföringsmål och molnlagringsmål](../../ui/activate-destinations.md#esp-and-cloud-storage) i självstudiekursen om segmentaktivering.

## IP-adress tillåtelselista

Se [IP-adressen tillåtelselista för molnlagringsdestinationer](./ip-address-allow-list.md) om du behöver lägga till IP-adresser för Adobe i ett tillåtelselista.
