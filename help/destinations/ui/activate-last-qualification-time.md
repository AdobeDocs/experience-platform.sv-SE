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

## Förhandskrav {#prerequisites}

Om du vill använda den senaste kvalificeringstiden (`lastQualificationTime`) för XDM-attribut måste du exportera data till ett av de sex molnlagringsmålen som listas nedan:

* [[!DNL ADLS Gen 2]](/help/destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md)
* [[!DNL Azure Blob]](/help/destinations/catalog/cloud-storage/azure-blob.md)
* [[!DNL Data Landing Zon]e](/help/destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](/help/destinations/catalog/cloud-storage/google-cloud-storage.md)
* [SFTP](/help/destinations/catalog/cloud-storage/sftp.md)

## Så här använder du XDM-attributet för senaste kvalificeringstid {#how-to-use}

Om du använder någon av de sex molnlagringsanslutningarna som anges ovan kan du använda det senaste XDM-attributet för kvalificeringstid i [mappningssteget](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) i aktiveringsarbetsflödet för att skapa en kolumn i den exporterade filen med den senaste tidsstämpeln för när en profil är kvalificerad för ett segment. Detta kan hjälpa er med vissa mätnings- eller analysexempel och ge er en bättre uppfattning om när ni ska aktivera vissa målgrupper.

Observera att om du vill lägga till `lastQualificationTime` i din filexport måste du för närvarande infoga värdet `xdm: segmentMembership.ups.seg_id.lastQualificationTime` manuellt i källfältet, vilket visas nedan. Du kan också redigera målfältet till `lastQualificationTime` eller något annat värde som du vill namnge den här kolumnen. Observera att eftersom det här är en betafunktion kan syntaxen för värdet `xdm: segmentMembership.ups.seg_id.lastQualificationTime` ändras i framtiden.

![Skärminspelning som visar den senaste kvalificeringstiden för XDM-attribut klistra in i mappningssteget](/help/destinations/ui/last-qualification-time.gif)

## Mer information {#more-information}

Mer information om hur du aktiverar data till filbaserade mål, inklusive alla steg i arbetsflödet och nödvändiga behörigheter, finns i självstudiekursen [Aktivera filbaserade mål](/help/destinations/ui/activate-batch-profile-destinations.md).
