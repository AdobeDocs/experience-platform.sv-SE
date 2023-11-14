---
keywords: Experience Platform;hem;populära ämnen;källor;kontakter;oracle;
title: (Beta) Skapa en Oraclena svarssystemkällanslutning med hjälp av plattformsgränssnittet
description: Lär dig hur du ansluter Adobe Experience Platform till Oracle Responssys med hjälp av plattformsgränssnittet.
hide: true
hidefromtoc: true
exl-id: 9ec5e1c2-3d9e-4729-be81-89a85d5ea782
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 1%

---

# (Beta) Skapa en [!DNL Oracle Responsys] källanslutning med plattformsgränssnitt

>[!NOTE]
>
>The [!DNL Oracle Responsys] källan är i betaversion. Se [Översikt över källor](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder beta-märkta anslutningar.

Den här självstudiekursen innehåller steg för att skapa en [[!DNL Oracle Responsys]](../../../../connectors/marketing-automation/oracle-responsys.md) källanslutning med Adobe Experience Platform användargränssnitt.

## Komma igång

Handboken kräver en fungerande förståelse av följande plattformskomponenter:

* [Källor](../../../../home.md): Plattformen tillåter att data hämtas från olika källor samtidigt som du får möjlighet att strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Plattformen innehåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

Om du redan har en autentiserad [!DNL Oracle Responsys] på Platform kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen på [skapa ett dataflöde för att ta fram automatiserade marknadsföringsdata för plattformen](../../dataflow/marketing-automation.md).

### Samla in nödvändiga inloggningsuppgifter

För att kunna ansluta [!DNL Oracle Responsys] På plattformen måste du ange värden för följande autentiseringsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Slutpunkt | Slutpunkts-URL för REST-autentisering för din [!DNL Oracle Responsys] -instans. |
| Klient-ID | Klient-ID för din [!DNL Oracle Responsys] -instans. |
| Klienthemlighet | Klienthemligheten för din [!DNL Oracle Responsys] -instans. |

Mer information om autentiseringsuppgifter för [!DNL Oracle Responsys], se [[!DNL Oracle Responsys] guide om autentisering](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm).

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka dina [!DNL Oracle Responsys] konto till plattform.

## Koppla samman [!DNL Oracle Responsys] konto

Välj **[!UICONTROL Sources]** från vänster navigering för att komma åt [!UICONTROL Sources] arbetsyta. The [!UICONTROL Catalog] visas en mängd olika källor som du kan använda för att skapa ett konto.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under [!UICONTROL Marketing automation] kategori, välj **[!UICONTROL Oracle Responsys]** och sedan markera **[!UICONTROL Add data]**.

![Adobe Experience Platform-källkatalogen med Oraclets svarskälla markerad.](../../../../images/tutorials/create/oracle-responsys/catalog.png)

The **[!UICONTROL Connect Oracle Responsys account]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Välj [!DNL Oracle Responsys] konto som du vill skapa ett nytt dataflöde med och sedan välja **[!UICONTROL Next]** för att fortsätta.

![Den befintliga kontoautentiseringsskärmen för Oraclena.](../../../../images/tutorials/create/oracle-responsys/existing.png)

### Nytt konto

Om du vill skapa ett nytt konto väljer du **[!UICONTROL New account]** och ange sedan ett namn, en valfri beskrivning och lämpliga värden för [!DNL Oracle Responsys] autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![Den nya kontoautentiseringsskärmen för Oraclena.](../../../../images/tutorials/create/oracle-eloqua/new.png)

## Nästa steg

I den här självstudiekursen har du autentiserat och skapat en källanslutning mellan [!DNL Oracle Responsys] konto och plattform. Du kan nu fortsätta med nästa självstudiekurs och [skapa ett dataflöde för att ta fram automatiserade marknadsföringsdata för plattformen](../../dataflow/marketing-automation.md).
