---
title: Använd den senaste kvalificeringstiden för XDM-attributet i det nya betmolnlagringsmålet
description: Lär dig hur du använder XDM-attributet för senaste kvalificeringstid i de nya lagringsplatserna för betmolnet
badgeBeta: label="Beta" type="Informative"
exl-id: d077ea10-5ff2-4acc-8ee6-78ea6cd752d1
source-git-commit: 7130ac46a7768ea6e71bf73eb970bf2890323d0f
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---

# Använd den senaste kvalificeringstiden för XDM-attributet i det nya betmolnlagringsmålet {#last-qualification-time}

>[!IMPORTANT]
> 
>Den här sidan beskriver funktioner som finns i betaversionen. Funktionen och dokumentationen kan komma att ändras. Kontakta din Adobe-representant eller kundtjänst om du vill ha tillgång till betaprogrammet.

## Förutsättningar {#prerequisites}

Använda den senaste kvalificeringstiden (`lastQualificationTime`) XDM-attribut, du måste exportera data till ett av de sex molnlagringsmålen som anges nedan:

* [[!DNL ADLS Gen 2]](/help/destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md)
* [[!DNL Azure Blob]](/help/destinations/catalog/cloud-storage/azure-blob.md)
* [[!DNL Data Landing Zon]e](/help/destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](/help/destinations/catalog/cloud-storage/google-cloud-storage.md)
* [SFTP](/help/destinations/catalog/cloud-storage/sftp.md)

## Så här använder du XDM-attributet för senaste kvalificeringstid {#how-to-use}

Om du använder någon av de sex molnlagringsanslutningarna som anges ovan kan du använda det senaste kvalificeringstidsattributet för XDM i [mappningssteg](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) av aktiveringsarbetsflödet för att skapa en kolumn i den exporterade filen med den senaste tidsstämpeln när en profil kvalificerar sig för ett segment. Detta kan hjälpa er med vissa mätnings- eller analysexempel och ge er en bättre uppfattning om när ni ska aktivera vissa målgrupper.

Lägg till `lastQualificationTime` vid export av filer måste du infoga värdet manuellt `xdm: segmentMembership.ups.seg_id.lastQualificationTime` till källfältet, som visas nedan. Du kan även redigera målfältet till `lastQualificationTime` eller något annat värde som du vill namnge den här kolumnen. Observera att eftersom det här är en betafunktion är syntaxen för `xdm: segmentMembership.ups.seg_id.lastQualificationTime` värdet kan komma att ändras i framtiden.

![Skärminspelning som visar den senaste kvalificeringstiden för XDM-attribut klistras in i mappningssteget](/help/destinations/ui/last-qualification-time.gif)

## Mer information {#more-information}

Mer information om hur du aktiverar data till filbaserade mål, inklusive alla steg i arbetsflödet och nödvändiga behörigheter, finns i [aktivera filbaserade mål, genomgång](/help/destinations/ui/activate-batch-profile-destinations.md).
