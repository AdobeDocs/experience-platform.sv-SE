---
title: Använda Adobe Experience Platform Assurance
description: I den här guiden beskrivs hur du använder Adobe Experience Platform Assurance när det har installerats och implementerats.
source-git-commit: 24f452bdb923179eefe53fdb28d3a92d43e533cd
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---


# Använda Adobe Experience Platform Assurance

I den här självstudiekursen beskrivs hur du använder Adobe Experience Platform Assurance. Instruktioner om hur du installerar och implementerar Adobe Experience Platform Assurance-tillägget finns i självstudiekursen om [implementera tillägget Assurance](./implement-assurance.md).

## Skapa sessioner

När du loggat in på [Försäkringsgränssnitt](https://experience.adobe.com/assurance)kan du välja **[!UICONTROL Create Session]** för att börja skapa en session.

![Knappen Skapa session markeras och visar var du kan skapa en session.](./images/using-assurance/create-session.png)

The **[!UICONTROL Create New Session]** visas. Läs instruktionerna och fortsätt genom att välja **[!UICONTROL Start]**.

![Dialogrutan Skapa ny session visas med instruktioner om hur du använder Assurance.](./images/using-assurance/create-new-session.png)

Nu kan du ange ett namn som identifierar sessionen och sedan ange en **[!UICONTROL Base URL]** (djuplänknings-URL för din app). När du har angett dessa uppgifter väljer du **[!UICONTROL Next]**.

>[!INFO]
>
>Bas-URL är rotdefinitionen som används för att starta programmet från en URL. En sessions-URL skapas som du kan använda för att initiera Assurance-sessionen. Ett exempelvärde kan se ut så här: `myapp://default` I **[!UICONTROL Base URL]** anger du programmets grundläggande definition av djuplänken.

![Det fullständiga arbetsflödet för att skapa en ny session visas.](./images/using-assurance/create-session.gif)

## Anslut till en session

När du har skapat en session ser du till att du ser **[!UICONTROL Create New Session]** visas nu en länk, en QR-kod och en PIN-kod.

![En dialogruta med alternativ för att ansluta till din Assurance-session visas.](./images/using-assurance/create-new-session-pin.png)

Om den här dialogrutan visas kan du antingen använda enhetens kameraapp för att skanna QR-koden och öppna din app eller kopiera länken och öppna den i din app. När appen startas bör du se hur skärmen för PIN-koden visas. Skriv PIN-koden från föregående steg och tryck på **[!UICONTROL Connect]**.

Du kan verifiera att din app är ansluten till Assurance när Adobe Experience Platform-ikonen (röd Adobe &quot;A&quot;) visas i din app.

![Det fullständiga arbetsflödet för att ansluta programmet till en Assurance-session visas.](./images/using-assurance/connect-session.gif)

## Exportera en session

Om du vill exportera en Assurance-session väljer du **[!UICONTROL Export to JSON]** i en session:

![Exportera en session](./images/using-assurance/export-session.png)

Exportalternativet respekterar sökfilterresultat och exporterar endast händelser som visas i händelseläget. Om du t.ex. sökte efter &quot;spåra&quot;-händelser och sedan väljer **[!UICONTROL Export to JSON]**, exporteras bara&quot;track&quot;-händelseresultatet&quot;.
