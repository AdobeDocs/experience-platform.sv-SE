---
title: Översikt över fästpunktstillägg
description: Lär dig hur du kan använda taggtillägget Fäst pixel för att fånga upp värdefulla användarinteraktioner i Adobe Experience Platform.
last-substantial-update: 2025-09-17T00:00:00Z
source-git-commit: d846bd5dee5ce0ee8836dc25e20d9fd070714114
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 0%

---

# Översikt över tillägget [!DNL Snap Pixel]

[[!DNL Snap Pixel]](https://businesshelp.snapchat.com/s/article/snap-pixel-about) är ett JavaScript-baserat analysverktyg som gör att du kan samla in värdefulla användarinteraktioner på din webbplats. Viktiga besöksåtgärder, som köp, registreringar eller andra konverteringar, skickas automatiskt till din [Ads Manager](http://ads.snapchat.com/) så att du kan mäta och optimera annonsernas prestanda, kampanjer, konverteringsvägar och mycket annat.

Med taggtillägget [!DNL Snap Pixel] kan du integrera [!DNL Snap Pixel]-funktioner direkt i dina klientkodsbibliotek. I den här dokumentationen beskrivs hur du installerar tillägget och implementerar dess funktioner i tagghanteringsreglerna.

Taggtillägget [!DNL Snap Pixel] effektiviserar integreringen av funktionen [!DNL Snap Pixel] i dina befintliga kodbibliotek på klientsidan. I den här dokumentationen beskrivs hur du installerar tillägget och konfigurerar dess funktioner i [reglerna](../../../ui/managing-resources/rules.md) för tagghanteringen.

## Förhandskrav {#prerequisites}

Om du vill använda tillägget måste du ha ett giltigt [!DNL Snap]-konto med åtkomst till [!DNL Ads Manager]. Du måste [skapa en ny [!DNL Snap Pixel]](https://forbusiness.snapchat.com/advertising/snap-pixel#about) och kopiera dess Pixel-ID för att konfigurera tillägget för ditt konto. Om du har en befintlig [!DNL Snap Pixel] kan du helt enkelt använda dess ID.

Vi rekommenderar att du använder [!DNL Snap Pixel] tillsammans med [!DNL Snap Conversions API] för att skicka samma händelser både från klientsidan och från serversidan. Den här metoden kan hjälpa till att återställa händelser som kanske inte fångas av enbart [!DNL Snap Pixel]. Gå till [[!DNL Snap] API-tillägget för konvertering för vidarebefordran av händelser](../../server/snap/overview.md) för steg om hur du integrerar det i implementeringarna på serversidan. Observera att din organisation måste ha åtkomst till [vidarebefordran av händelser](../../../ui/event-forwarding/overview.md) för att kunna använda tillägget på serversidan.

## Installera tillägget {#install}

Om du vill installera tillägget [!DNL Snap Pixel] går du till användargränssnittet för datainsamlingen eller användargränssnittet för Experience Platform och väljer **[!UICONTROL Tags]** i den vänstra navigeringen. Här väljer du en egenskap som tillägget ska läggas till i eller skapar en ny egenskap i stället.

När du har markerat eller skapat den önskade egenskapen väljer du **[!UICONTROL Extensions]** i den vänstra navigeringen och väljer sedan fliken **[!UICONTROL Catalog]**. Sök efter kortet [!UICONTROL Snap Pixel] och välj sedan **[!UICONTROL Install]**.

![Knappen [!UICONTROL Install] som väljs för tillägget [!UICONTROL Snap Pixel] i användargränssnittet för datainsamling.](./images/install.png)

I konfigurationsvyn som visas måste du ange det Pixel-ID som du kopierade tidigare för att kunna länka tillägget till ditt konto. Du kan klistra in ID:t direkt i indata eller markera ett befintligt dataelement i stället.

När du är klar väljer du **[!UICONTROL Save]**.

![Det [!DNL Pixel]-ID som anges som ett dataelement i tilläggskonfigurationsvyn.](./images/configure.png)

Tillägget är installerat och du kan nu använda dess olika åtgärder i taggreglerna.

## Konfigurera en taggregel {#rule}

[!DNL Snap Pixel] stöder en uppsättning fördefinierade standardhändelser, var och en med specifika kontexter och godkända parametrar. Regelåtgärderna som är tillgängliga i tillägget [!DNL Snap Pixel] justeras mot de här händelsetyperna, vilket gör det enkelt att kategorisera och konfigurera händelser som skickas till [!DNL Snap] utifrån deras typ.

I det här avsnittet visas hur du skapar en regel som skickar en inköpshändelse till [!DNL Snap].

Börja med att skapa en ny taggregel och definiera villkoren efter behov. När du ställer in regelns åtgärder väljer du [!DNL Snap Pixel] som tillägg och sedan **[!UICONTROL Send Purchase Event]** som åtgärdstyp.

När du är klar med konfigurationen av åtgärden [!UICONTROL Send Purchase Event] väljer du **[!UICONTROL Keep Changes]** för att lägga till den i regelkonfigurationen.

![Åtgärdstypen [!UICONTROL Send Purchase Event] som har valts för en regel i användargränssnittet för datainsamling.](./images/action-type.png)

Välj **[!UICONTROL Save to Library]** när du är nöjd med den övergripande regelkonfigurationen.

Om du vill använda dina uppdateringar publicerar du en ny tagg, [build](../../../ui/publishing/builds.md), som aktiverar ändringarna i biblioteket.

## Bekräfta att [!DNL Snap] tar emot data {#confirm}

När den uppdaterade versionen har distribuerats till webbplatsen kan du verifiera att data skickas som förväntat genom att utlösa konverteringshändelser i webbläsaren och kontrollera att de visas i [[!DNL Snap Events Manager]](https://businesshelp.snapchat.com/s/article/events-manager).

## Nästa steg {#next-steps}

Den här guiden beskriver hur du skickar data till [!DNL Snap] med taggtillägget [!DNL Snap Pixel]. Om du även planerar att skicka händelser på serversidan till [!DNL Snap] kan du fortsätta med att installera och konfigurera [[!DNL Snap Conversions API event forwarding extension]](../../server/snap/overview.md).
