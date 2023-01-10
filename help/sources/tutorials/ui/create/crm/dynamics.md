---
keywords: Experience Platform;hem;populära ämnen;Microsoft Dynamics;microsoft dynamics;Dynamics;dynamics
solution: Experience Platform
title: Skapa en Microsoft Dynamics-källanslutning i användargränssnittet
type: Tutorial
description: Lär dig hur du skapar en Microsoft Dynamics-källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 1%

---

# Skapa en [!DNL Microsoft Dynamics] källanslutning i användargränssnittet

Den här självstudiekursen innehåller steg för att skapa en [!DNL Microsoft Dynamics] (nedan kallad[!DNL Dynamics]&quot;) källanslutning med Adobe Experience Platform UI.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Dynamics] kan du hoppa över resten av dokumentet och gå vidare till självstudiekursen om [konfigurera ett dataflöde för en CRM-källa](../../dataflow/crm.md).

### Samla in nödvändiga inloggningsuppgifter

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `serviceUri` | Tjänstens URL [!DNL Dynamics] -instans. |
| `username` | Ditt användarnamn [!DNL Dynamics] användarkonto. |
| `password` | Lösenordet för [!DNL Dynamics] konto. |
| `servicePrincipalId` | Klient-ID för din [!DNL Dynamics] konto. Detta ID krävs när tjänstens huvudnamn och nyckelbaserad autentisering används. |
| `servicePrincipalKey` | Tjänstens hemliga huvudnyckel. Denna autentiseringsuppgift krävs när tjänstens huvudnamn och nyckelbaserad autentisering används. |

Mer information om hur du kommer igång finns i [this [!DNL Dynamics] dokument](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Koppla samman [!DNL Dynamics] konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka dina [!DNL Dynamics] konto till plattform.

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och sedan markera **[!UICONTROL Sources]** från det vänstra navigeringsfältet för att komma åt [!UICONTROL Sources] arbetsyta. The **[!UICONTROL Catalog]** I visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under **[!UICONTROL CRM]** kategori, välj **[!UICONTROL Microsoft Dynamics]**. Om det är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny [!DNL Dynamics] koppling.

![katalog](../../../../images/tutorials/create/ms-dynamics/catalog.png)

The **[!UICONTROL Connect to Dynamics]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn och en valfri beskrivning för det nya indataformuläret som visas [!DNL Dynamics] konto.

The [!DNL Dynamics] anslutningsprogrammet ger dig olika typer av autentisering för åtkomst. Under [!UICONTROL Account authentication] välj **[!UICONTROL Basic authentication]** för att använda lösenordsbaserade autentiseringsuppgifter.

När du är klar väljer du **[!UICONTROL Connect to source]** och sedan ge det nya kontot lite tid att etablera.

![grundläggande autentisering](../../../../images/tutorials/create/ms-dynamics/basic-auth.png)

Du kan också välja **[!UICONTROL Service-principal and key authentication]** och koppla samman [!DNL Dynamics] konto med en kombination av [!UICONTROL Service principal ID] och [!UICONTROL Service principal key].

>[!IMPORTANT]
>
> Grundläggande autentisering i [!DNL Dynamics] kan blockeras av tvåfaktorsautentisering, som för närvarande inte stöds av plattformen. I det här fallet rekommenderas du att använda nyckelbaserad autentisering för att skapa en källkoppling med [!DNL Dynamics].

![nyckelbaserad autentisering](../../../../images/tutorials/create/ms-dynamics/key-based-auth.png)

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| [!UICONTROL Service principal ID] | Klient-ID för din [!DNL Dynamics] konto. Detta ID krävs när tjänstens huvudnamn och nyckelbaserad autentisering används. |
| [!UICONTROL Service principal key] | Tjänstens hemliga huvudnyckel. Denna autentiseringsuppgift krävs när tjänstens huvudnamn och nyckelbaserad autentisering används. |

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du [!DNL Dynamics] konto som du vill ansluta till och välj **[!UICONTROL Next]** i det övre högra hörnet för att fortsätta.

![befintlig](../../../../images/tutorials/create/ms-dynamics/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till [!DNL Dynamics] konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till plattformen](../../dataflow/crm.md).
