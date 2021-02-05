---
keywords: Experience Platform;hem;populära ämnen;Microsoft Dynamics;microsoft dynamics;Dynamics;dynamics
solution: Experience Platform
title: Skapa en Microsoft Dynamics-källanslutning i användargränssnittet
topic: overview
type: Tutorial
description: Lär dig hur du skapar en Microsoft Dynamics-källanslutning med Adobe Experience Platform-gränssnittet.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 1%

---


# Skapa en [!DNL Microsoft Dynamics]-källanslutning i användargränssnittet

I den här självstudiekursen beskrivs hur du skapar en [!DNL Microsoft Dynamics]-källanslutning (kallas nedan &quot;[!DNL Dynamics]&quot;) med Adobe Experience Platform-gränssnittet.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har ett giltigt [!DNL Dynamics]-konto kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [konfigurera ett dataflöde för en CRM-källa](../../dataflow/crm.md).

### Samla in nödvändiga inloggningsuppgifter

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `serviceUri` | Tjänst-URL:en för din [!DNL Dynamics]-instans. |
| `username` | Användarnamnet för ditt [!DNL Dynamics]-användarkonto. |
| `password` | Lösenordet för ditt [!DNL Dynamics]-konto. |
| `servicePrincipalId` | Klient-ID för ditt [!DNL Dynamics]-konto. Detta ID krävs när tjänstens huvudnamn och nyckelbaserad autentisering används. |
| `servicePrincipalKey` | Tjänstens hemliga huvudnyckel. Denna autentiseringsuppgift krävs när tjänstens huvudnamn och nyckelbaserad autentisering används. |

Mer information om hur du kommer igång finns i [det här [!DNL Dynamics] dokumentet](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Anslut ditt [!DNL Dynamics]-konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka ditt [!DNL Dynamics]-konto till Platform.

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan [!UICONTROL Sources]. Skärmen **[!UICONTROL Catalog]** visar en mängd olika källor som du kan skapa ett konto för.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj **[!UICONTROL Microsoft Dynamics]** under kategorin **[!UICONTROL CRM]**. Om det här är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny [!DNL Dynamics]-koppling.

![katalog](../../../../images/tutorials/create/ms-dynamics/catalog.png)

Sidan **[!UICONTROL Connect to Dynamics]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn och en valfri beskrivning för ditt nya [!DNL Dynamics]-konto på det indataformulär som visas.

Anslutningen [!DNL Dynamics] ger dig olika autentiseringstyper för åtkomst. Under [!UICONTROL Account authentication] väljer du **[!UICONTROL Basic authentication]** om du vill använda lösenordsbaserade autentiseringsuppgifter.

När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan en tid för det nya kontot att upprätta.

![grundläggande autentisering](../../../../images/tutorials/create/ms-dynamics/basic-auth.png)

Du kan också välja **[!UICONTROL Service-principal and key authentication]** och ansluta ditt [!DNL Dynamics]-konto med en kombination av [!UICONTROL Service principal ID] och [!UICONTROL Service principal key].

>[!IMPORTANT]
>
> Grundläggande autentisering i [!DNL Dynamics] kan blockeras med tvåfaktorautentisering, vilket för närvarande inte stöds av plattformen. I det här fallet rekommenderas du att använda nyckelbaserad autentisering för att skapa en källkoppling med [!DNL Dynamics].

![nyckelbaserad autentisering](../../../../images/tutorials/create/ms-dynamics/key-based-auth.png)

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| [!UICONTROL Service principal ID] | Klient-ID för ditt [!DNL Dynamics]-konto. Detta ID krävs när tjänstens huvudnamn och nyckelbaserad autentisering används. |
| [!UICONTROL Service principal key] | Tjänstens hemliga huvudnyckel. Denna autentiseringsuppgift krävs när tjänstens huvudnamn och nyckelbaserad autentisering används. |

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det [!DNL Dynamics]-konto du vill ansluta till och sedan väljer du **[!UICONTROL Next]** i det övre högra hörnet för att fortsätta.

![befintlig](../../../../images/tutorials/create/ms-dynamics/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL Dynamics]-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till plattformen](../../dataflow/crm.md).