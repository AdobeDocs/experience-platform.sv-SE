---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Google Cloud Storage Connector
topic: overview
translation-type: tm+mt
source-git-commit: 1bb896f7629d7b71b94dd107eeda87701df99208
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---


# Google Cloud Storage Connector

Adobe Experience Platform erbjuder inbyggd anslutningsbarhet för molnleverantörer som AWS [!DNL Google Cloud Platform]och [!DNL Azure]så att ni kan hämta data från dessa system.

Lagringskällor i molnet kan hämta dina egna data [!DNL Platform] utan att du behöver hämta, formatera eller överföra dem. Inkapslade data kan formateras som XDM JSON, XDM-parquet eller avgränsade. Varje steg i processen är integrerat i arbetsflödet för källor. [!DNL Platform] gör att du kan hämta in data från [!DNL Google Cloud Storage] grupper.

## IP-adress tillåtelselista

Följande IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor.

### USA, östra

- `20.41.2.0/23`
- `20.41.4.0/26`
- `20.44.17.80/28`
- `20.49.102.16/29`
- `40.70.148.160/28`
- `52.167.107.224/28`

### Västeuropa

- `13.69.67.192/28`
- `13.69.107.112/28`
- `13.69.112.128/28`
- `40.74.24.192/26`
- `40.74.26.0/23`
- `40.113.176.232/29`
- `52.236.187.112/28`

### Australien, östra

- `13.70.74.144/28`
- `20.37.193.0/25`
- `20.37.193.128/26`
- `20.37.198.224/29`
- `40.79.163.80/28`
- `40.79.171.160/28`

## Krav för att ansluta ditt [!DNL Google Cloud Storage] konto

För att kunna ansluta till [!DNL Platform]måste du först aktivera interoperabilitet för ditt [!DNL Google Cloud Storage] konto. Om du vill få åtkomst till inställningen för interoperabilitet öppnar du [!DNL Google Cloud Platform] och väljer **[!UICONTROL Settings]** ett av **[!UICONTROL Storage]** alternativen på navigeringspanelen.

![](../../images/tutorials/create/google-cloud-storage/nav.png)

Sidan visas **[!UICONTROL Settings]** . Härifrån kan du se information om ditt projekt- [!DNL Google] ID och information om ditt [!DNL Google Cloud Storage] konto. Om du vill komma åt inställningarna för interoperabilitet väljer du **[!UICONTROL Interoperability]** i det övre huvudet.

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

Sidan innehåller **[!UICONTROL Interoperability]** information om autentisering, åtkomstnycklar och standardprojektet som är kopplat till ditt användarkonto. Om du inte redan har etablerat ett standardprojekt för interoperabel åtkomst kan du konfigurera ett i **[!UICONTROL Default project for interoperable access]** -avsnittet. Om ett standardprojekt redan har etablerats visas en bekräftelse på att ett projekt har angetts som standard i avsnittet.

Om du vill generera ett nytt ID för åtkomstnyckel och en hemlig åtkomstnyckel för ditt användarkonto väljer du **[!UICONTROL Create a Key]**.

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

Du kan använda ditt nyligen genererade ID för åtkomstnyckel och hemlig åtkomstnyckel för att ansluta ditt [!DNL Google Cloud Storage] konto till [!DNL Platform].

## Anslut [!DNL Google Cloud Storage] till [!DNL Platform]

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Google Cloud Storage] till [!DNL Platform] med API:er eller användargränssnittet:

### Använda API:er

- [Skapa en Google Cloud-lagringskontakt med API:t för flödestjänsten](../../tutorials/api/create/cloud-storage/google.md)
- [Utforska ett molnlagringssystem med API:t för Flow Service](../../tutorials/api/explore/cloud-storage.md)
- [Samla in molnlagringsdata med API:t för Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Använda gränssnittet

- [Skapa en Google Cloud-källanslutning för lagring i användargränssnittet](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Konfigurera ett dataflöde för en molnlagringskontakt i användargränssnittet](../../tutorials/ui/dataflow/batch/cloud-storage.md)