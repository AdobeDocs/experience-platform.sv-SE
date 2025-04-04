---
keywords: Experience Platform;hem;populära ämnen;källor;kontakter;oracle;
title: (Beta) Skapa en Oracle Responsys-källanslutning med Experience Platform UI
description: Lär dig hur du ansluter Adobe Experience Platform till Oracle Responsys med hjälp av Experience Platform användargränssnitt.
hide: true
hidefromtoc: true
exl-id: 9ec5e1c2-3d9e-4729-be81-89a85d5ea782
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# (Beta) Skapa en [!DNL Oracle Responsys]-källanslutning med Experience Platform UI

>[!NOTE]
>
>Källan [!DNL Oracle Responsys] är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källöversikt](../../../../home.md#terms-and-conditions).

I den här självstudiekursen får du anvisningar om hur du skapar en [[!DNL Oracle Responsys]](../../../../connectors/marketing-automation/oracle-responsys.md)-källanslutning med Adobe Experience Platform användargränssnitt.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Experience Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

Om du redan har ett autentiserat [!DNL Oracle Responsys]-konto på Experience Platform kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om att [skapa ett dataflöde för att skicka marknadsföringsdata till Experience Platform](../../dataflow/marketing-automation.md).

### Samla in nödvändiga inloggningsuppgifter

För att kunna ansluta [!DNL Oracle Responsys] till Experience Platform måste du ange värden för följande autentiseringsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Slutpunkt | URL:en för REST-autentiseringsslutpunkten för din [!DNL Oracle Responsys]-instans. |
| Klient-ID | Klient-ID för din [!DNL Oracle Responsys]-instans. |
| Klienthemlighet | Klienthemligheten för din [!DNL Oracle Responsys]-instans. |

Mer information om autentiseringsuppgifter för [!DNL Oracle Responsys] finns i [[!DNL Oracle Responsys] handboken om autentisering](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm).

När du har samlat in de nödvändiga inloggningsuppgifterna kan du följa stegen nedan för att länka ditt [!DNL Oracle Responsys]-konto till Experience Platform.

## Anslut ditt [!DNL Oracle Responsys]-konto

I Experience Platform-gränssnittet väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i [!UICONTROL Sources]. På skärmen [!UICONTROL Catalog] visas en mängd olika källor som du kan använda för att skapa ett konto.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under kategorin [!UICONTROL Marketing automation] väljer du **[!UICONTROL Oracle Responsys]** och sedan **[!UICONTROL Add data]**.

![Adobe Experience Platform-källkatalogen med Oracle Responsys-källan markerad.](../../../../images/tutorials/create/oracle-responsys/catalog.png)

Sidan **[!UICONTROL Connect Oracle Responsys account]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill använda ett befintligt konto väljer du det [!DNL Oracle Responsys]-konto som du vill skapa ett nytt dataflöde med och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![Den befintliga kontoautentiseringsskärmen för Oracle-svar.](../../../../images/tutorials/create/oracle-responsys/existing.png)

### Nytt konto

Om du vill skapa ett nytt konto väljer du **[!UICONTROL New account]** och anger sedan ett namn, en valfri beskrivning och lämpliga värden för dina [!DNL Oracle Responsys]-autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![Den nya kontoautentiseringsskärmen för Oracle-svar.](../../../../images/tutorials/create/oracle-eloqua/new.png)

## Nästa steg

Genom att följa den här självstudiekursen har du autentiserat och skapat en källanslutning mellan ditt [!DNL Oracle Responsys]-konto och Experience Platform. Du kan nu fortsätta med nästa självstudiekurs och [skapa ett dataflöde för att skicka automatiserade marknadsföringsdata till Experience Platform](../../dataflow/marketing-automation.md).
