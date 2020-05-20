---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Google Cloud Storage Connector
topic: overview
translation-type: tm+mt
source-git-commit: 256a193e56e69078d1c01c622656f0b1a18e73ff
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# Google Cloud Storage Connector

Adobe Experience Platform ger inbyggda anslutningsmöjligheter för molnleverantörer som AWS, Google Cloud Platform och Azure. Ni kan överföra data från dessa system till plattformen.

Lagringskällor i molnet kan hämta dina egna data till plattformen utan att du behöver hämta, formatera eller överföra dem. Inkapslade data kan formateras som XDM JSON, XDM-parquet eller avgränsade. Varje steg i processen är integrerat i arbetsflödet för källor. Med Platform kan ni hämta data från Google Cloud-lagring via batchar.

## Nödvändig konfiguration för att ansluta ditt Google Cloud-lagringskonto

För att kunna ansluta till plattformen måste du först aktivera interoperabilitet för ditt Google Cloud-lagringskonto. Öppna Google Cloud Platform och välj **[!UICONTROL Settings]** ett av **[!UICONTROL Storage]** alternativen i navigeringspanelen för att få åtkomst till interoperabilitetsinställningarna.

![](../../images/tutorials/create/google-cloud-storage/nav.png)

Sidan visas **[!UICONTROL Settings]** . Här kan du se information om ditt Google-projekt-ID och information om ditt Google Cloud-lagringskonto. Om du vill komma åt inställningarna för interoperabilitet väljer du **[!UICONTROL Interoperability]** i det övre huvudet.

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

Sidan innehåller **[!UICONTROL Interoperability]** information om autentisering, åtkomstnycklar och standardprojektet som är kopplat till ditt användarkonto. Om du inte redan har etablerat ett standardprojekt för interoperabel åtkomst kan du konfigurera ett i *[!UICONTROL Default project for interoperable access]* -avsnittet. Om ett standardprojekt redan har etablerats visas en bekräftelse på att ett projekt har angetts som standard i avsnittet.

Om du vill generera ett nytt ID för åtkomstnyckel och en hemlig åtkomstnyckel för ditt användarkonto väljer du **[!UICONTROL Create a Key]**.

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

Du kan använda ditt nyligen genererade åtkomstnyckel-ID och din hemliga åtkomstnyckel för att ansluta ditt Google Cloud-lagringskonto till plattformen.

Dokumentationen nedan innehåller information om hur du ansluter Google Cloud-lagring till plattformen med hjälp av API:er eller användargränssnittet:

## Anslut Google Cloud-lagring till plattform

Dokumentationen nedan innehåller information om hur du ansluter Google Cloud-lagring till plattformen med hjälp av API:er eller användargränssnittet:

### Använda API:er

- [Skapa en Google Cloud-lagringskontakt med API:t för flödestjänsten](../../tutorials/api/create/cloud-storage/google.md)
- [Utforska ett molnlagringssystem med API:t för Flow Service](../../tutorials/api/explore/cloud-storage.md)
- [Samla in molnlagringsdata med API:t för Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Använda gränssnittet

- [Skapa en Google Cloud-källanslutning för lagring i användargränssnittet](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Konfigurera ett dataflöde för en molnlagringskontakt i användargränssnittet](../../tutorials/ui/dataflow/batch/cloud-storage.md)