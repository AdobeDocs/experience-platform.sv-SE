---
keywords: Experience Platform;hem;populära ämnen;Veeva CRM;veeva
solution: Experience Platform
title: Skapa en Veeva CRM-källanslutning i användargränssnittet
topic-legacy: overview
type: Tutorial
description: Lär dig hur du skapar en Vector CRM-källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: b67fa4c4-d8ff-4d2d-aa76-5d9d32aa22d6
source-git-commit: 076e0880c9efd1fe1cbfb4c610c5e15093adf460
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 1%

---

# Skapa en [!DNL Veeva CRM]-källanslutning i användargränssnittet

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata i CRM på schemalagd basis. I den här självstudien beskrivs stegen för hur du skapar en [!DNL Veeva CRM]-källkoppling med användargränssnittet i [!DNL Platform].

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverket som  [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har ett giltigt [!DNL Veeva CRM]-konto kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [konfigurera ett dataflöde](../../dataflow/crm.md).

### Samla in nödvändiga inloggningsuppgifter

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `environmentUrl` | URL:en för [!DNL Veeva CRM]-källinstansen. |
| `username` | Användarnamnet för användarkontot [!DNL Veeva CRM]. |
| `password` | Lösenordet för användarkontot [!DNL Veeva CRM]. |
| `securityToken` | Säkerhetstoken för användarkontot [!DNL Veeva CRM]. |

Mer information om hur du kommer igång finns i [det här veva CRM-dokumentet]

## Anslut ditt [!DNL Veeva CRM]-konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka ditt [!DNL Veeva CRM]-konto till [!DNL Platform].

Välj **[!UICONTROL Sources]** i det vänstra navigeringsfältet i plattformsgränssnittet för att komma åt arbetsytan [!UICONTROL Sources]. Skärmen [!UICONTROL Catalog] visar en mängd olika källor som du kan skapa ett konto för.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under kategorin [!UICONTROL CRM] väljer du **[!UICONTROL Veeva CRM]** och sedan **[!UICONTROL Add data]**.

![katalog](../../../../images/tutorials/create/veeva/catalog.png)

Sidan **[!UICONTROL Connect Veeva CRM account]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill använda ett befintligt konto väljer du det [!DNL Veeva CRM]-konto som du vill skapa ett nytt dataflöde med och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/veeva/existing.png)

### Nytt konto

Om du skapar ett nytt konto väljer du **[!UICONTROL New account]** och anger sedan ett namn, en valfri beskrivning och dina [!DNL Veeva CRM]-autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![new](../../../../images/tutorials/create/veeva/new.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL Veeva CRM]-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till plattformen](../../dataflow/crm.md).
