---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en Microsoft Dynamics-källkoppling i användargränssnittet
topic: overview
translation-type: tm+mt
source-git-commit: 44c43afc653c147fa12e3e962904bfc79ee0fc64
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---


# Skapa en Microsoft Dynamics-källkoppling i användargränssnittet

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata i CRM på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en Microsoft Dynamics-källkoppling (nedan kallad Dynamics) med hjälp av användargränssnittet för plattformen.

## Komma igång

Den här självstudien kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Experience Data Model (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att organisera kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [Kundprofil](../../../../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har ett giltigt Dynamics-konto kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om [konfigurering av ett dataflöde](../../dataflow/crm.md).

### Samla in nödvändiga inloggningsuppgifter

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `serviceUri` | Tjänst-URL:en för Dynamics-instansen. |
| `username` | Användarnamnet för ditt Dynamics-användarkonto. |
| `password` | Lösenordet för ditt Dynamics-konto. |

Mer information om hur du kommer igång finns i [det här Dynamics-dokumentet](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Anslut ditt Dynamics-konto

När du har samlat in de nödvändiga inloggningsuppgifterna kan du följa stegen nedan för att skapa ett nytt Dynamics-konto för att ansluta till plattformen.

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt *[!UICONTROL Sources]* arbetsytan. På *[!UICONTROL Catalog]* skärmen visas en mängd olika källor som du kan skapa ett inkommande konto för, och varje källa visar antalet befintliga konton och datauppsättningsflöden som är kopplade till dem.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under *[!UICONTROL Databases]* kategorin väljer du **[!UICONTROL Dynamics]** klicka **på +-ikonen (+)** för att skapa en ny Dynamics-koppling.

![katalog](../../../../images/tutorials/create/ms-dynamics/catalog.png)

Sidan visas *[!UICONTROL Connect to Dynamics]* . På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. På indataformuläret som visas anger du anslutningen med ett namn, en valfri beskrivning och dina Dynamics-autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan en tid för det nya kontot att upprätta.

![koppla](../../../../images/tutorials/create/ms-dynamics/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det Dynamics-konto som du vill ansluta till och fortsätter sedan **[!UICONTROL Next]** i det övre högra hörnet.

![befintlig](../../../../images/tutorials/create/ms-dynamics/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt Dynamics-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till plattformen](../../dataflow/crm.md).