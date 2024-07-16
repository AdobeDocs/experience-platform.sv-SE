---
keywords: Experience Platform;hem;populära ämnen;Microsoft Dynamics;microsoft dynamics;Dynamics;dynamics
solution: Experience Platform
title: Skapa en Microsoft Dynamics Source-anslutning i användargränssnittet
type: Tutorial
description: Lär dig hur du skapar en Microsoft Dynamics-källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# Skapa en [!DNL Microsoft Dynamics]-källanslutning i användargränssnittet

I den här självstudiekursen beskrivs hur du skapar en [!DNL Microsoft Dynamics]-källanslutning (kallas nedan [!DNL Dynamics]) med hjälp av Adobe Experience Platform-gränssnittet.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har ett giltigt [!DNL Dynamics]-konto kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [Konfigurera ett dataflöde för en CRM-källa](../../dataflow/crm.md).

### Samla in nödvändiga inloggningsuppgifter

Om du vill autentisera [!DNL Dynamics]-källan måste du ange värden för följande anslutningsegenskaper:

>[!BEGINTABS]

>[!TAB Grundläggande autentisering]

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `serviceUri` | Tjänst-URL:en för din [!DNL Dynamics]-instans. |
| `username` | Användarnamnet för ditt [!DNL Dynamics]-användarkonto. |
| `password` | Lösenordet för ditt [!DNL Dynamics]-konto. |

>[!TAB Tjänstens huvudnamn och nyckelautentisering]

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `servicePrincipalId` | Klient-ID för ditt [!DNL Dynamics]-konto. Detta ID krävs när tjänstens huvudnamn och nyckelbaserad autentisering används. |
| `servicePrincipalKey` | Tjänstens hemliga huvudnyckel. Denna autentiseringsuppgift krävs när tjänstens huvudnamn och nyckelbaserad autentisering används. |

>[!ENDTABS]

Mer information om hur du kommer igång finns i [det här [!DNL Dynamics] dokumentet](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Anslut ditt [!DNL Dynamics]-konto

I plattformsgränssnittet väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i [!UICONTROL Sources]. På skärmen [!UICONTROL Catalog] visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under kategorin [!UICONTROL CRM] väljer du **[!UICONTROL Microsoft Dynamics]** och sedan **[!UICONTROL Add data]**.

![Källkatalogen med Microsoft Dynamics har valts.](../../../../images/tutorials/create/ms-dynamics/catalog.png)

Sidan **[!UICONTROL Connect Microsoft Dynamics account]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill använda ett befintligt konto markerar du det [!DNL Dynamics]-konto du vill använda och väljer sedan **[!UICONTROL Next]** i det övre högra hörnet för att fortsätta.

![Det befintliga kontogränssnittet.](../../../../images/tutorials/create/ms-dynamics/existing.png)

### Nytt konto

>[!TIP]
>
>När du väl har skapat den kan du inte ändra autentiseringstypen för en [!DNL Dynamics]-basanslutning. Om du vill ändra autentiseringstypen måste du skapa en ny basanslutning.

Om du vill skapa ett nytt konto väljer du **[!UICONTROL New account]** och anger sedan ett namn och en valfri beskrivning för det nya [!DNL Dynamics]-kontot.

![Det nya gränssnittet för att skapa konton.](../../../../images/tutorials/create/ms-dynamics/new.png)

Du kan antingen använda grundläggande autentisering eller tjänstens huvudnamn och nyckelautentisering när du skapar ett [!DNL Dynamics]-konto.

>[!BEGINTABS]

>[!TAB Grundläggande autentisering]

Om du vill skapa ett [!DNL Dynamics]-konto med grundläggande autentisering väljer du [!UICONTROL Basic authentication] och anger sedan värden för [!UICONTROL Service URI], [!UICONTROL Username] och [!UICONTROL Password]. **Obs!**: Grundläggande autentisering i [!DNL Dynamics] kan blockeras av tvåfaktorautentisering, vilket för närvarande inte stöds av plattformen. I det här fallet rekommenderas du att använda nyckelbaserad autentisering för att skapa en källkoppling med [!DNL Dynamics].

När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta det nya kontot.

![Det grundläggande autentiseringsgränssnittet.](../../../../images/tutorials/create/ms-dynamics/basic-authentication.png)

>[!TAB Tjänstens huvudnamn och nyckelautentisering]

Om du vill skapa ett [!DNL Dynamics]-konto med tjänstens huvudnamn och nyckelautentisering väljer du **[!UICONTROL Service-principal and key authentication]** och anger sedan värden för [!UICONTROL Service principal ID] och [!UICONTROL Service principal key].

När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta det nya kontot.

![Autentiseringsgränssnittet för tjänstens huvudnyckel.](../../../../images/tutorials/create/ms-dynamics/service-principal.png)

>[!ENDTABS]

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL Dynamics]-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till plattformen](../../dataflow/crm.md).
