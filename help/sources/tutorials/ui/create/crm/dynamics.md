---
keywords: Experience Platform;hem;populära ämnen;Microsoft Dynamics;microsoft dynamics;Dynamics;dynamics
solution: Experience Platform
title: Skapa en Microsoft Dynamics-källanslutning i användargränssnittet
type: Tutorial
description: Lär dig hur du skapar en Microsoft Dynamics-källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 1%

---

# Skapa en [!DNL Microsoft Dynamics] källanslutning i användargränssnittet

Den här självstudiekursen innehåller steg för att skapa en [!DNL Microsoft Dynamics] (nedan kallad[!DNL Dynamics]&quot;) källanslutning med Adobe Experience Platform UI.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet i Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Dynamics] kan du hoppa över resten av dokumentet och gå vidare till självstudiekursen om [konfigurera ett dataflöde för en CRM-källa](../../dataflow/crm.md).

### Samla in nödvändiga inloggningsuppgifter

För att autentisera [!DNL Dynamics] source, du måste ange värden för följande anslutningsegenskaper:

>[!BEGINTABS]

>[!TAB Grundläggande autentisering]

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `serviceUri` | Tjänst-URL:en för [!DNL Dynamics] -instans. |
| `username` | Ditt användarnamn [!DNL Dynamics] användarkonto. |
| `password` | Lösenordet för [!DNL Dynamics] konto. |

>[!TAB Tjänstens huvudnamn och nyckelautentisering]

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `servicePrincipalId` | Klient-ID för din [!DNL Dynamics] konto. Detta ID krävs när tjänstens huvudnamn och nyckelbaserad autentisering används. |
| `servicePrincipalKey` | Tjänstens hemliga huvudnyckel. Denna autentiseringsuppgift krävs när tjänstens huvudnamn och nyckelbaserad autentisering används. |

>[!ENDTABS]

Mer information om hur du kommer igång finns i [this [!DNL Dynamics] dokument](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Koppla samman [!DNL Dynamics] konto

Välj **[!UICONTROL Sources]** från vänster navigering för att komma åt [!UICONTROL Sources] arbetsyta. The [!UICONTROL Catalog] visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under [!UICONTROL CRM] kategori, välj **[!UICONTROL Microsoft Dynamics]** och sedan markera **[!UICONTROL Add data]**.

![Källkatalogen med Microsoft Dynamics vald.](../../../../images/tutorials/create/ms-dynamics/catalog.png)

The **[!UICONTROL Connect Microsoft Dynamics account]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Välj [!DNL Dynamics] det konto du vill använda och sedan välja **[!UICONTROL Next]** i det övre högra hörnet för att fortsätta.

![Det befintliga kontogränssnittet.](../../../../images/tutorials/create/ms-dynamics/existing.png)

### Nytt konto

>[!TIP]
>
>När du har skapat en fil kan du inte ändra autentiseringstypen för en [!DNL Dynamics] basanslutning. Om du vill ändra autentiseringstypen måste du skapa en ny basanslutning.

Om du vill skapa ett nytt konto väljer du **[!UICONTROL New account]** och ange sedan ett namn och en valfri beskrivning av ditt nya [!DNL Dynamics] konto.

![Det nya gränssnittet för kontoskapande.](../../../../images/tutorials/create/ms-dynamics/new.png)

Du kan antingen använda grundläggande autentisering eller tjänstens huvudnamn och nyckelautentisering när du skapar en [!DNL Dynamics] konto.

>[!BEGINTABS]

>[!TAB Grundläggande autentisering]

Skapa en [!DNL Dynamics] konto med grundläggande autentisering, välj [!UICONTROL Basic authentication] och sedan ange värden för [!UICONTROL Service URI], [!UICONTROL Username]och [!UICONTROL Password]. **Anteckning**: Grundläggande autentisering i [!DNL Dynamics] kan blockeras av tvåfaktorsautentisering, som för närvarande inte stöds av plattformen. I det här fallet rekommenderas du att använda nyckelbaserad autentisering för att skapa en källkoppling med [!DNL Dynamics].

När du är klar väljer du **[!UICONTROL Connect to source]** och sedan ge det nya kontot lite tid att etablera.

![Det grundläggande autentiseringsgränssnittet.](../../../../images/tutorials/create/ms-dynamics/basic-authentication.png)

>[!TAB Tjänstens huvudnamn och nyckelautentisering]

Skapa en [!DNL Dynamics] konto med tjänstens huvudnamn och nyckelautentisering, välj **[!UICONTROL Service-principal and key authentication]** och sedan ange värden för [!UICONTROL Service principal ID] och [!UICONTROL Service principal key].

När du är klar väljer du **[!UICONTROL Connect to source]** och sedan ge det nya kontot lite tid att etablera.

![Autentiseringsgränssnittet för tjänstens huvudnyckel.](../../../../images/tutorials/create/ms-dynamics/service-principal.png)

>[!ENDTABS]

## Nästa steg

Genom att följa den här självstudien har du upprättat en anslutning till [!DNL Dynamics] konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till plattformen](../../dataflow/crm.md).
