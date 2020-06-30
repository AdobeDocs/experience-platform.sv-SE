---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Google Cloud Storage Connector
topic: overview
translation-type: tm+mt
source-git-commit: 6ffdcc2143914e2ab41843a52dc92344ad51bcfb
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---


# Google Cloud Storage Connector

Adobe Experience Platform erbjuder inbyggd anslutningsbarhet för molnleverantörer som AWS [!DNL Google Cloud Platform]och [!DNL Azure]så att ni kan hämta data från dessa system.

Lagringskällor i molnet kan hämta dina egna data [!DNL Platform] utan att du behöver hämta, formatera eller överföra dem. Inkapslade data kan formateras som XDM JSON, XDM-parquet eller avgränsade. Varje steg i processen är integrerat i arbetsflödet för källor. [!DNL Platform] gör att du kan hämta in data från [!DNL Google Cloud Storage] grupper.

## Krav för att ansluta ditt [!DNL Google Cloud Storage] konto

För att kunna ansluta till [!DNL Platform]måste du först aktivera interoperabilitet för ditt [!DNL Google Cloud Storage] konto. Om du vill få åtkomst till inställningen för interoperabilitet öppnar du [!DNL Google Cloud Platform] och väljer **[!UICONTROL Settings]** ett av **[!UICONTROL Storage]** alternativen på navigeringspanelen.

![](../../images/tutorials/create/google-cloud-storage/nav.png)

Sidan visas **[!UICONTROL Settings]** . Härifrån kan du se information om ditt projekt- [!DNL Google] ID och information om ditt [!DNL Google Cloud Storage] konto. Om du vill komma åt inställningarna för interoperabilitet väljer du **[!UICONTROL Interoperability]** i det övre huvudet.

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

Sidan innehåller **[!UICONTROL Interoperability]** information om autentisering, åtkomstnycklar och standardprojektet som är kopplat till ditt användarkonto. Om du inte redan har etablerat ett standardprojekt för interoperabel åtkomst kan du konfigurera ett i *[!UICONTROL Default project for interoperable access]* -avsnittet. Om ett standardprojekt redan har etablerats visas en bekräftelse på att ett projekt har angetts som standard i avsnittet.

Om du vill generera ett nytt ID för åtkomstnyckel och en hemlig åtkomstnyckel för ditt användarkonto väljer du **[!UICONTROL Create a Key]**.

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

Du kan använda ditt nyligen genererade åtkomstnyckel-ID och den hemliga åtkomstnyckeln för att ansluta ditt [!DNL Google Cloud Storage] konto till [!DNL Platform].

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Google Cloud Storage] till [!DNL Platform] med API:er eller användargränssnittet:

## Anslut [!DNL Google Cloud Storage] till [!DNL Platform]

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Google Cloud Storage] till [!DNL Platform] med API:er eller användargränssnittet:

### Använda API:er

- [Skapa en Google Cloud-lagringskontakt med API:t för flödestjänsten](../../tutorials/api/create/cloud-storage/google.md)
- [Utforska ett molnlagringssystem med API:t för Flow Service](../../tutorials/api/explore/cloud-storage.md)
- [Samla in molnlagringsdata med API:t för Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Använda gränssnittet

- [Skapa en Google Cloud-källanslutning för lagring i användargränssnittet](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Konfigurera ett dataflöde för en molnlagringskontakt i användargränssnittet](../../tutorials/ui/dataflow/batch/cloud-storage.md)