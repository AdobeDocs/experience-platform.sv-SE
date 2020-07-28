---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en PayPal-källanslutning i användargränssnittet
topic: overview
translation-type: tm+mt
source-git-commit: 4f7d7e2bf255afe1588dbe7cfb2ec055f2dcbf75
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 0%

---


# Skapa en [!DNL PayPal] källanslutning i användargränssnittet

>[!NOTE]
> Kopplingen [!DNL PayPal] är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källor-översikten](../../../../home.md#terms-and-conditions) .

Källkopplingar i Adobe Experience Platform ger möjlighet att importera externt källdata på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en [!DNL PayPal] källkoppling med [!DNL Platform] användargränssnittet.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Experience Data Model (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [Kundprofil](../../../../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en [!DNL PayPal] basanslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om [att konfigurera ett dataflöde](../../dataflow/payments.md)

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till ditt [!DNL PayPal] konto [!DNL Platform]måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | URL:en för [!DNL PayPal] instansen. |
| `clientID` | Klient-ID som är kopplat till ditt [!DNL PayPal] program. |
| `clientSecret` | Klienthemligheten som är kopplad till ditt [!DNL PayPal] program. |

Mer information om hur du kommer igång finns i det här [PayPal-dokumentet](https://developer.paypal.com/docs/api/overview/#get-credentials)

## Anslut ditt [!DNL PayPal] konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att skapa en ny inkommande basanslutning som du kan länka ditt [!DNL PayPal] konto till [!DNL Platform].

Logga in på <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt *[!UICONTROL Sources]* arbetsytan. På *[!UICONTROL Catalog]* skärmen visas en mängd olika källor som du kan skapa inkommande basanslutningar med, och varje källa visar antalet befintliga basanslutningar som är kopplade till dem.

Under *[!UICONTROL CRM]* kategorin väljer du **[!UICONTROL PayPal]** att visa ett informationsfält till höger på skärmen. Informationsfältet innehåller en kort beskrivning av den valda källan samt alternativ för att ansluta till källan eller visa dess dokumentation. Om du vill skapa en ny inkommande basanslutning väljer du **[!UICONTROL Connect source]**.

![katalog](../../../../images/tutorials/create/paypal/catalog.png)

Sidan visas *[!UICONTROL Connect to PayPal]* . På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. På det indataformulär som visas anger du ett namn, en valfri beskrivning och dina [!DNL PayPal] inloggningsuppgifter för basanslutningen. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya basanslutningen.

![koppla](../../../../images/tutorials/create/paypal/connect.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto markerar du det [!DNL PayPal] konto du vill ansluta till och väljer sedan **[!UICONTROL Next]** att fortsätta.

![befintlig](../../../../images/tutorials/create/paypal/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en basanslutning till ditt [!DNL PayPal] konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta CRM-data till Platform](../../dataflow/payments.md).