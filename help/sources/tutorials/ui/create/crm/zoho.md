---
keywords: Experience Platform;hem;populära ämnen;Zoho CRM;zoho crm;Zoho;zoho
solution: Experience Platform
title: Skapa en Zoho CRM Source-anslutning i användargränssnittet
type: Tutorial
description: Lär dig hur du skapar en Zoho CRM-källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: c648fc3e-beea-4030-8d36-dd8a7e2c281e
source-git-commit: 0e3fee4d78646b1d1d6730495358b3ced4127f4e
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# Skapa en [!DNL Zoho CRM]-källanslutning i användargränssnittet

>[!IMPORTANT]
>
>[!DNL Zoho CRM]-källan kommer att bli inaktuell i slutet av maj 2025. Du kan också använda källan [[!DNL Data Landing Zone]](../cloud-storage/data-landing-zone.md).

Source-anslutningar i Adobe Experience Platform ger möjlighet att importera externt källkodsdata i CRM på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en [!DNL Zoho CRM]-källkoppling med användargränssnittet i [!DNL Platform].

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata med.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har ett giltigt [!DNL Zoho CRM]-konto kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [Konfigurera ett dataflöde](../../dataflow/crm.md).

### Samla in nödvändiga inloggningsuppgifter

För att kunna ansluta [!DNL Zoho CRM] till plattformen måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Slutpunkt | Slutpunkten för den [!DNL Zoho CRM]-server som du gör din begäran på. |
| Konto-URL | Konton-URL:en används för att generera din åtkomst och uppdatera tokens. URL:en måste vara domänspecifik. |
| Klient-ID | Klient-ID som motsvarar ditt [!DNL Zoho CRM]-användarkonto. |
| Klienthemlighet | Klienthemligheten som motsvarar ditt [!DNL Zoho CRM]-användarkonto. |
| Åtkomsttoken | Åtkomsttoken ger dig säker och tillfällig åtkomst till ditt [!DNL Zoho CRM]-konto. |
| Uppdatera token | En uppdateringstoken är en token som används för att generera en ny åtkomsttoken när din åtkomsttoken har upphört att gälla. |

Mer information om dessa autentiseringsuppgifter finns i dokumentationen om [[!DNL Zoho CRM] autentisering](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## Anslut ditt [!DNL Zoho CRM]-konto

När du har samlat in dina nödvändiga inloggningsuppgifter kan du följa stegen nedan för att länka ditt [!DNL Zoho CRM]-konto till [!DNL Platform].

I plattformsgränssnittet väljer du **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan i [!UICONTROL Sources]. På skärmen [!UICONTROL Catalog] visas en mängd olika källor som du kan använda för att skapa ett konto.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under kategorin [!UICONTROL CRM] väljer du **[!UICONTROL Zoho CRM]** och sedan **[!UICONTROL Add data]**.

![katalog](../../../../images/tutorials/create/zoho/catalog.png)

Sidan **[!UICONTROL Connect Zoho CRM account]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill använda ett befintligt konto väljer du det [!DNL Zoho CRM]-konto som du vill skapa ett nytt dataflöde med och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/zoho/existing.png)

### Nytt konto

Om du skapar ett nytt konto väljer du **[!UICONTROL New account]** och anger sedan ett namn, en valfri beskrivning och dina [!DNL Zoho CRM]-inloggningsuppgifter. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

>[!TIP]
>
>Din konto-URL-domän måste motsvara rätt domänplats. Följande domäner och deras motsvarande konto-URL:er:<ul><li>USA: https://accounts.zoho.com</li><li>Australien: https://accounts.zoho.com.au</li><li>Europa: https://accounts.zoho.eu</li><li>Indien: https://accounts.zoho.in</li><li>Kina: https://accounts.zoho.com.cn</li></ul>

![ny](../../../../images/tutorials/create/zoho/new.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL Zoho CRM]-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till plattformen](../../dataflow/crm.md).
