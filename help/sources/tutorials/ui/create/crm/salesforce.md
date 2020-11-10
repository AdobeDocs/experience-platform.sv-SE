---
keywords: Experience Platform;home;popular topics;Salesforce;salesforce
solution: Experience Platform
title: Skapa en Salesforce-källanslutning i användargränssnittet
topic: overview
type: Tutorial
description: I den här självstudiekursen beskrivs hur du skapar en Salesforce-källanslutning med hjälp av användargränssnittet för plattformen.
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 1%

---


# Skapa en [!DNL Salesforce] källanslutning i användargränssnittet

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata i CRM på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en [!DNL Salesforce] källkoppling med [!DNL Platform] användargränssnittet.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har ett giltigt [!DNL Salesforce] konto kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om hur du [konfigurerar ett dataflöde](../../dataflow/crm.md).

### Samla in nödvändiga inloggningsuppgifter

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `environmentUrl` | URL:en för [!DNL Salesforce] källinstansen. |
| `username` | Användarnamnet för [!DNL Salesforce] användarkontot. |
| `password` | Lösenordet för [!DNL Salesforce] användarkontot. |
| `securityToken` | Säkerhetstoken för [!DNL Salesforce] användarkontot. |

Mer information om hur du kommer igång finns i [det här Salesforce-dokumentet](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

## Anslut ditt [!DNL Salesforce] konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka ditt [!DNL Salesforce] konto till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt **[!UICONTROL Sources]** arbetsytan. På **[!UICONTROL Catalog]** skärmen visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj under **[!UICONTROL Databases]** kategorin **[!UICONTROL Salesforce]**. Om det är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** att skapa en ny Salesforce-anslutning.

![katalog](../../../../images/tutorials/create/salesforce/catalog.png)

Sidan visas **[!UICONTROL Connect to Salesforce]** . På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och dina [!DNL Salesforce] inloggningsuppgifter i det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan en tid för att upprätta den nya anslutningen.

![koppla](../../../../images/tutorials/create/salesforce/new.png)

### Befintligt konto

Om du vill ansluta till ett befintligt konto markerar du det [!DNL Salesforce] konto du vill ansluta till och fortsätter sedan **[!UICONTROL Next]** i det övre högra hörnet.

![befintlig](../../../../images/tutorials/create/salesforce/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL Salesforce] konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till [!DNL Platform]](../../dataflow/crm.md).