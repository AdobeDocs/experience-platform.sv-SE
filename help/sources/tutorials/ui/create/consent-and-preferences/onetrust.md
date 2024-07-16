---
keywords: Experience Platform;hem;populära ämnen;ontrust;OneTrust
solution: Experience Platform
title: Skapa en OneTrust Source-anslutning i användargränssnittet
type: Tutorial
description: Lär dig hur du skapar en OneTrust-källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: 6af0604d-cbb6-4c8e-b017-3eb82ec6ee1c
source-git-commit: 35095ec8c22106ba0a8f11e0a970ed7989a7f06c
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# Skapa en [!DNL OneTrust Integration]-källanslutning i användargränssnittet

>[!NOTE]
>
>Källan [!DNL OneTrust Integration] stöder endast inmatning av medgivanden och inställningsdata, inte cookies.

I den här självstudiekursen beskrivs hur du skapar en [[!DNL OneTrust Integration]](https://my.onetrust.com/s/contactsupport?language=en_US)-källanslutning för att kunna importera både historiska och schemalagda medgivandedata till Adobe Experience Platform med hjälp av användargränssnittet för plattformen.

## Förhandskrav

>[!IMPORTANT]
>
>[!DNL OneTrust Integration]-källkopplingen och dokumentationen skapades av [!DNL OneTrust Integration]-teamet. Kontakta [[!DNL OneTrust] teamet](https://my.onetrust.com/s/contactsupport?language=en_US) direkt om du har frågor eller uppdateringsförfrågningar.

Innan du kan ansluta [!DNL OneTrust Integration] till plattformen måste du hämta din åtkomsttoken. Detaljerade instruktioner om hur du hittar din åtkomsttoken finns i [[!DNL OneTrust Integration] OAuth 2-guiden](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

Åtkomsttoken uppdateras inte automatiskt när den har upphört att gälla eftersom uppdateringstoken för system-till-system inte stöds av [!DNL OneTrust]. Det är därför nödvändigt att se till att din åtkomsttoken uppdateras i anslutningen innan den upphör att gälla. Den maximala konfigurerbara livslängden för en åtkomsttoken är ett år. Mer information om hur du uppdaterar din åtkomsttoken finns i [[!DNL OneTrust] dokumentet om att hantera dina OAuth 2.0-klientautentiseringsuppgifter](https://developer.onetrust.com/docs/documentation/ZG9jOjIyODk1MTUw-managing-o-auth-2-0-client-credentials).

### Samla in nödvändiga inloggningsuppgifter

För att kunna ansluta [!DNL OneTrust Integration] till plattformen måste du ange värden för följande autentiseringsuppgifter:

| Autentiseringsuppgifter | Beskrivning | Exempel |
| --- | --- | --- |
| Värdnamn | Miljön som [!DNL OneTrust Integration]-data måste hämtas från. | `app.onetrust.com` |
| Test-URL för auktorisering | (Valfritt) URL:en för auktoriseringstestet används för att validera autentiseringsuppgifter när en basanslutning skapas. Om inget anges kontrolleras autentiseringsuppgifterna automatiskt när du skapar en källanslutning i stället. | |
| Åtkomsttoken | Åtkomsttoken som motsvarar ditt [!DNL OneTrust Integration]-konto. | `ZGFkZDMyMjFhMmEyNDQ2ZGFhNTdkZjNkZjFmM2IyOWE6QjlUSERVUTNjOFVsRmpEZTJ6Vk9oRnF3Sk8xNlNtcm4=` |

Mer information om dessa autentiseringsuppgifter finns i [[!DNL OneTrust Integration] autentiseringsdokumentationen](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

## Anslut ditt [!DNL OneTrust Integration]-konto

>[!NOTE]
>
>API-specifikationerna för [!DNL OneTrust Integration] delas med Adobe för datainhämtning.

I plattformsgränssnittet väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i [!UICONTROL Sources] för en katalog med källor som är tillgängliga i Experience Platform.

Använd menyn *[!UICONTROL Categories]* för att filtrera källor efter kategori. Du kan också ange ett källnamn i sökfältet för att hitta en viss källa från katalogen.

Gå till kategorin [!UICONTROL Consent & Preferences] för källkortet [!DNL OneTrust Integration]. Börja genom att välja **[!UICONTROL Add data]**.

![Källkatalogen för användargränssnittet i Experience Platform.](../../../../images/tutorials/create/onetrust/catalog.png)

Sidan **[!UICONTROL Connect OneTrust Integration account]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill använda ett befintligt konto väljer du det [!DNL OneTrust Integration]-konto som du vill skapa ett nytt dataflöde med och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![Det befintliga kontoautentiseringssteget i källarbetsflödet.](../../../../images/tutorials/create/onetrust/existing.png)

### Nytt konto

Om du skapar ett nytt konto väljer du **[!UICONTROL New account]** och anger sedan ett namn, en valfri beskrivning och dina autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![Det nya kontoautentiseringssteget i källarbetsflödet.](../../../../images/tutorials/create/onetrust/new.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL OneTrust Integration]-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data om samtycke till plattformen](../../dataflow/consent-and-preferences.md).
