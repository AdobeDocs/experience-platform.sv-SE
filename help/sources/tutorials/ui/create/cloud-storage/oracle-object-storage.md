---
keywords: Experience Platform;hem;populära ämnen;Oraclena objektlagring;oraclena objektlagring
solution: Experience Platform
title: Skapa en källanslutning för Oraclena objektlagring i användargränssnittet
topic-legacy: overview
type: Tutorial
description: Lär dig hur du skapar en källanslutning till Oraclet Object Storage med Adobe Experience Platform-gränssnittet.
exl-id: 32284163-5dde-4171-8977-f76ceeebcef2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 1%

---

# Skapa en [!DNL Oracle Object Storage]-källanslutning i användargränssnittet

I den här självstudiekursen beskrivs hur du skapar en [!DNL Oracle Object Storage]-källanslutning med Adobe Experience Platform-gränssnittet.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

### Samla in nödvändiga inloggningsuppgifter

För att kunna ansluta till [!DNL Oracle Object Storage] måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `serviceUrl` | Slutpunkten [!DNL Oracle Object Storage] krävs för autentisering. Slutpunktsformatet är: `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | Åtkomstnyckel-ID för [!DNL Oracle Object Storage] krävs för autentisering. |
| `secretKey` | Lösenordet [!DNL Oracle Object Storage] krävs för autentisering. |
| `bucketName` | Det tillåtna bucket-namn som krävs om användaren har begränsad åtkomst. Bucketnamnet måste innehålla mellan tre och 63 tecken, det måste börja och sluta med en bokstav eller en siffra och får bara innehålla gemena bokstäver, siffror eller bindestreck (`-`). Det går inte att formatera bucket-namnet som en IP-adress. |
| `folderPath` | Den tillåtna mappsökväg som krävs om användaren har begränsad åtkomst. |

Mer information om hur du hämtar dessa värden finns i [autentiseringsguiden för Oraclena objektlagring](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

När du har samlat in de nödvändiga inloggningsuppgifterna kan du följa stegen nedan för att skapa ett nytt Oracle Object Storage-konto för att ansluta till plattformen.

## Anslut till Oracle Object Storage

Välj **[!UICONTROL Sources]** från vänster navigering i plattformsgränssnittet för att komma åt arbetsytan [!UICONTROL Sources]. Skärmen [!UICONTROL Catalog] innehåller en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också använda sökfältet till att hitta den källa du vill arbeta med.

Under kategorin [!UICONTROL Cloud storage] väljer du **[!UICONTROL Oracle Object Storage]** och sedan **[!UICONTROL Add data]**.

![katalog](../../../../images/tutorials/create/oracle-object-storage/catalog.png)

### Befintligt konto

Om du vill använda ett befintligt konto väljer du det [!DNL Oracle Object Storage]-konto som du vill skapa ett nytt dataflöde med och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/oracle-object-storage/existing.png)

### Nytt konto

Om du skapar ett nytt konto väljer du **[!UICONTROL New account]** och anger sedan ett namn, en valfri beskrivning och dina [!DNL Oracle Object Storage]-autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![new](../../../../images/tutorials/create/oracle-object-storage/new.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL Oracle Object Storage]-konto. Du kan nu gå vidare till nästa självstudiekurs om att [konfigurera ett dataflöde för att hämta data från ditt molnlagringsutrymme till plattformen](../../dataflow/batch/cloud-storage.md).
