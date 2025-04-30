---
title: Skapa en Oracle Eloqua-källanslutning med Experience Platform UI
description: Lär dig hur du ansluter Adobe Experience Platform till Oracle Eloqua med hjälp av Experience Platform användargränssnitt.
exl-id: c4431d85-5948-4122-9a99-dbacdde5a09f
source-git-commit: 7ff0709b62590bb80c1ed664368f28cdc4a950ea
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---

# Skapa en [!DNL Oracle Eloqua]-källanslutning med Experience Platform UI

>[!WARNING]
>
>[!DNL Oracle Eloqua]-källan kommer att bli inaktuell i januari 2026. En ny källa kommer att släppas senare i år som ett alternativ. När den nya källan har släppts måste du planera migreringen till den nya källan genom att skapa nya kontoanslutningar och dataflöden före utgången av januari 2026.

I den här självstudien beskrivs hur du skapar en [!DNL Oracle Eloqua]-källanslutning med Adobe Experience Platform-användargränssnittet.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Experience Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

Om du redan har ett autentiserat [!DNL Oracle Eloqua]-konto på Experience Platform kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om att [skapa ett dataflöde för att skicka marknadsföringsdata till Experience Platform](../../dataflow/marketing-automation.md).

### Samla in nödvändiga inloggningsuppgifter

För att kunna ansluta [!DNL Oracle Eloqua] till Experience Platform måste du ange värden för följande autentiseringsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Slutpunkt | Slutpunkten för [!DNL Oracle Eloqua]-servern. [!DNL Oracle Eloqua] har stöd för flera datacenter. Logga in på [[!DNL Oracle Eloqua] gränssnittet](https://login.eloqua.com) med dina autentiseringsuppgifter och kopiera sedan bas-URL-delen från omdirigerings-URL:en för att hitta slutpunkten. Formatet för URL-mönstret är `xxx.xx.eloqua.com` och bör anges utan `http` eller `https`. |
| Användarnamn | Användarnamnet för [!DNL Oracle Eloqua]-servern. Användarnamnet måste vara formaterat som `siteName + \\ + username`, där `siteName` är det företagsnamn som du använde för att logga in på [!DNL Oracle Eloqua] och `username` är ditt användarnamn. Ditt inloggningsnamn kan till exempel vara: `Eloqua\Andy`. **Obs!**: Du måste använda ett enkelt omvänt snedstreck (`\`) när du använder användargränssnittet eftersom ett ytterligare omvänt snedstreck (`\`) automatiskt läggs till i Experience Platform-gränssnittet när du anger ett användarnamn. |
| Lösenord | Lösenordet som motsvarar ditt [!DNL Oracle Eloqua]-användarnamn. |

Mer information om autentiseringsuppgifter för [!DNL Oracle Eloqua] finns i [[!DNL Oracle Eloqua] handboken om autentisering](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

När du har samlat in de nödvändiga inloggningsuppgifterna kan du följa stegen nedan för att länka ditt [!DNL Oracle Eloqua]-konto till Experience Platform.

## Anslut ditt [!DNL Oracle Eloqua]-konto

I Experience Platform-gränssnittet väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i [!UICONTROL Sources]. På skärmen [!UICONTROL Catalog] visas en mängd olika källor som du kan använda för att skapa ett konto.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under kategorin [!UICONTROL Marketing automation] väljer du **[!UICONTROL Oracle Eloqua]** och sedan **[!UICONTROL Add data]**.

![katalog](../../../../images/tutorials/create/oracle-eloqua/catalog.png)

Sidan **[!UICONTROL Connect Oracle Eloqua account]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill använda ett befintligt konto väljer du det [!DNL Oracle Eloqua]-konto som du vill skapa ett nytt dataflöde med och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/oracle-eloqua/existing.png)

### Nytt konto

Om du skapar ett nytt konto väljer du **[!UICONTROL New account]** och anger sedan ett namn, en valfri beskrivning och lämpliga värden för dina [!DNL Oracle Eloqua]-inloggningsuppgifter. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![ny](../../../../images/tutorials/create/oracle-eloqua/new.png)

## Nästa steg

Genom att följa den här självstudiekursen har du autentiserat och skapat en källanslutning mellan ditt [!DNL Oracle Eloqua]-konto och Experience Platform. Du kan nu fortsätta med nästa självstudiekurs och [skapa ett dataflöde för att skicka automatiserade marknadsföringsdata till Experience Platform](../../dataflow/marketing-automation.md).
