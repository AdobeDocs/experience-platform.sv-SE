---
keywords: Experience Platform;hem;populära ämnen;Oraclena objektlagring;oraclena objektlagring
solution: Experience Platform
title: Skapa en källanslutning för Oraclena objektlagring i användargränssnittet
type: Tutorial
description: Lär dig hur du skapar en källanslutning till Oraclet Object Storage med Adobe Experience Platform-gränssnittet.
exl-id: 32284163-5dde-4171-8977-f76ceeebcef2
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 1%

---

# Skapa en [!DNL Oracle Object Storage] Källanslutning i användargränssnittet

Den här självstudiekursen innehåller steg för att skapa en [!DNL Oracle Object Storage] källanslutning med Adobe Experience Platform UI.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

### Samla in nödvändiga inloggningsuppgifter

Ansluta till [!DNL Oracle Object Storage]måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `serviceUrl` | The [!DNL Oracle Object Storage] slutpunkt krävs för autentisering. Slutpunktsformatet är: `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | The [!DNL Oracle Object Storage] ID för åtkomstnyckel krävs för autentisering. |
| `secretKey` | The [!DNL Oracle Object Storage] lösenord krävs för autentisering. |
| `bucketName` | Det tillåtna bucket-namn som krävs om användaren har begränsad åtkomst. Bucket-namnet måste innehålla mellan 3 och 63 tecken, det måste börja och sluta med en bokstav eller en siffra och får bara innehålla gemena bokstäver, siffror eller bindestreck (`-`). Det går inte att formatera bucket-namnet som en IP-adress. |
| `folderPath` | Den tillåtna mappsökväg som krävs om användaren har begränsad åtkomst. |

Mer information om hur du hämtar dessa värden finns i [Autentiseringsguide för Oracle Object Storage](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

När du har samlat in de nödvändiga inloggningsuppgifterna kan du följa stegen nedan för att skapa ett nytt Oracle Object Storage-konto för att ansluta till plattformen.

## Anslut till Oracle Object Storage

Välj **[!UICONTROL Sources]** från vänster navigering för att komma åt [!UICONTROL Sources] arbetsyta. The [!UICONTROL Catalog] I visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också använda sökfältet till att hitta den källa du vill arbeta med.

Under [!UICONTROL Cloud storage] kategori, välj **[!UICONTROL Oracle Object Storage]** och sedan markera **[!UICONTROL Add data]**.

![katalog](../../../../images/tutorials/create/oracle-object-storage/catalog.png)

### Befintligt konto

Om du vill använda ett befintligt konto väljer du [!DNL Oracle Object Storage] konto som du vill skapa ett nytt dataflöde med och sedan välja **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/oracle-object-storage/existing.png)

### Nytt konto

Om du skapar ett nytt konto väljer du **[!UICONTROL New account]** och ange sedan ett namn, en valfri beskrivning och [!DNL Oracle Object Storage] autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![new](../../../../images/tutorials/create/oracle-object-storage/new.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till [!DNL Oracle Object Storage] konto. Du kan nu gå vidare till nästa självstudiekurs på [konfigurera ett dataflöde för att hämta data från ditt molnlagringsutrymme till plattformen](../../dataflow/batch/cloud-storage.md).
