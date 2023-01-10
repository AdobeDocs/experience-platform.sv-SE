---
keywords: Experience Platform;hem;populära ämnen;källor;kopplingar;oracle;oracle eloqua;eloqua
solution: Experience Platform
title: Skapa en Oraclena Eloqua-källanslutning med hjälp av plattformsgränssnittet
description: Lär dig hur du ansluter Adobe Experience Platform till Oracle Eloqua med hjälp av plattformsgränssnittet.
exl-id: c4431d85-5948-4122-9a99-dbacdde5a09f
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---

# Skapa en [!DNL Oracle Eloqua] källanslutning med plattformsgränssnitt

Den här självstudiekursen innehåller steg för att skapa en [!DNL Oracle Eloqua] källanslutning med Adobe Experience Platform användargränssnitt.

## Komma igång

Handboken kräver en fungerande förståelse av följande plattformskomponenter:

* [Källor](../../../../home.md): Plattformen gör att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Plattformen innehåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

Om du redan har en autentiserad [!DNL Oracle Eloqua] på Platform kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen på [skapa ett dataflöde för att ta fram automatiserade marknadsföringsdata för plattformen](../../dataflow/marketing-automation.md).

### Samla in nödvändiga inloggningsuppgifter

För att kunna ansluta [!DNL Oracle Eloqua] På plattformen måste du ange värden för följande autentiseringsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Slutpunkt | Slutpunkten för [!DNL Oracle Eloqua]. |
| Användarnamn | Användarnamnet för [!DNL Oracle Eloqua] konto. Användarnamnet måste vara formaterat som `siteName + \\ + username`, där `siteName` är företagsnamnet som du använde för att logga in på [!DNL Oracle Eloqua] och `username` är ditt användarnamn. Användarnamnet för inloggning kan till exempel vara: `adobe\\emily`. |
| Lösenord | Lösenordet som motsvarar [!DNL Oracle Eloqua] användarnamn. |

Mer information om autentiseringsuppgifter för [!DNL Oracle Eloqua], se [[!DNL Oracle Eloqua] guide om autentisering](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka dina [!DNL Oracle Eloqua] konto till plattform.

## Koppla samman [!DNL Oracle Eloqua] konto

Välj **[!UICONTROL Sources]** från vänster navigering för att komma åt [!UICONTROL Sources] arbetsyta. The [!UICONTROL Catalog] visas en mängd olika källor som du kan använda för att skapa ett konto.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under [!UICONTROL Marketing automation] kategori, välj **[!UICONTROL Oracle Eloqua]** och sedan markera **[!UICONTROL Add data]**.

![katalog](../../../../images/tutorials/create/oracle-eloqua/catalog.png)

The **[!UICONTROL Connect Oracle Eloqua account]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill använda ett befintligt konto väljer du [!DNL Oracle Eloqua] konto som du vill skapa ett nytt dataflöde med och sedan välja **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/oracle-eloqua/existing.png)

### Nytt konto

Om du skapar ett nytt konto väljer du **[!UICONTROL New account]** och ange sedan ett namn, en valfri beskrivning och lämpliga värden för [!DNL Oracle Eloqua] autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![new](../../../../images/tutorials/create/oracle-eloqua/new.png)

## Nästa steg

I den här självstudiekursen har du autentiserat och skapat en källanslutning mellan [!DNL Oracle Eloqua] konto och plattform. Du kan nu fortsätta med nästa självstudiekurs och [skapa ett dataflöde för att ta fram automatiserade marknadsföringsdata för plattformen](../../dataflow/marketing-automation.md).
