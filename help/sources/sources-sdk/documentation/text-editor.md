---
keywords: Experience Platform;hem;populära ämnen;källor;kopplingar;källkopplingar;källor sdk;sdk;SDK
solution: Experience Platform
title: Skapa en källdokumentationssida med en textredigerare i din lokala miljö
description: Det här dokumentet innehåller anvisningar om hur du använder din lokala miljö för att skapa dokumentation för källan och skicka en pull-begäran (PR).
exl-id: 4cc89d1d-bc42-473d-ba54-ab3d1a2cd0d6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 0%

---

# Använda en textredigerare i den lokala miljön för att skapa en källdokumentationssida

Det här dokumentet innehåller anvisningar om hur du använder din lokala miljö för att skapa dokumentation för källan och skicka en pull-begäran (PR).

>[!TIP]
>
>Följande dokument från Adobe bidragsguide kan användas som ytterligare stöd för din dokumentationsprocess: <ul><li>[Installera Git- och Markdown-redigeringsverktygen](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=sv-SE)</li><li>[Konfigurera Git-databasen lokalt för dokumentation](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=sv-SE)</li><li>[Arbetsflöde för GitHub-bidrag för större ändringar](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=sv-SE)</li></ul>

## Förhandskrav

I följande självstudie måste du ha installerat GitHub Desktop på din lokala dator. Om du inte har GitHub Desktop kan du hämta programmet [här](https://desktop.github.com/).

## Anslut till GitHub och konfigurera din lokala redigeringsmiljö

Det första steget i att konfigurera din lokala redigeringsmiljö är att navigera till [Adobe Experience Platform GitHub-databasen](https://github.com/AdobeDocs/experience-platform.en).

![platform-repo](../assets/platform-repo.png)

På huvudsidan i Experience Platform GitHub-databasen väljer du **Förgrening**.

![förgrening](../assets/fork.png)

Välj **Kod** om du vill klona databasen till din lokala dator. I listrutan som visas väljer du **HTTPS** och sedan **Öppna med GitHub Desktop**.

>[!TIP]
>
>Mer information finns i självstudiekursen [Konfigurera Git-databasen lokalt för dokumentation](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=sv-SE#create-a-local-clone-of-the-repository).

![open-git-desktop](../assets/open-git-desktop.png)

Tillåt sedan några ögonblick för GitHub Desktop att klona databasen `experience-platform.en`.

![kloning](../assets/cloning.png)

När kloningsprocessen är klar går du till GitHub Desktop och skapar en ny gren. Välj **Huvudsida** i den övre navigeringen och välj sedan **Ny gren**

![ny gren](../assets/new-branch.png)

Ange ett beskrivande namn för din gren i pover-panelen som visas och välj sedan **Skapa gren**.

![create-branch-vs](../assets/create-branch-vs.png)

Välj sedan **Publicera gren**.

![publish-branch](../assets/publish-branch.png)

## Skriv dokumentationssidan för källan

När databasen är klonad till din lokala dator och en ny gren har skapats kan du nu börja skapa dokumentationssidan för den nya källan med den [textredigerare som du väljer](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=sv-SE#understand-markdown-editors).

Adobe rekommenderar att du använder [Visual Studio Code](https://code.visualstudio.com/) och att du installerar tillägget Adobe Markdown Authoring. Om du vill installera tillägget startar du Visual Studio-kod och väljer sedan fliken **Tillägg** i den vänstra navigeringen.

![tillägg](../assets/extension.png)

Ange sedan `Adobe Markdown Authoring` i sökfältet och välj **Installera** på sidan som visas.

![installera](../assets/install.png)

När den lokala datorn är klar hämtar du dokumentationsmallen för [källor](../assets/api-template.zip) och extraherar filen till `experience-platform.en/help/sources/tutorials/api/create/...` med [`...`] som representerar den kategori som du väljer. Om du t.ex. skapar en datakälla väljer du databasmappen.

Till sist följer du instruktionerna i mallen och redigerar mallen med relevant information om källan.

![edit-template](../assets/edit-template.png)

## Skicka in din dokumentation för granskning

Om du vill skapa en pull-begäran (PR) och skicka din dokumentation för granskning måste du först spara ditt arbete i [!DNL Visual Studio Code] (eller den textredigerare du valt). Sedan anger du ett implementeringsmeddelande med hjälp av GitHub Desktop och väljer **Verkställ för att skapa källdokumentation**.

![commit-vs](../assets/commit-vs.png)

Välj sedan **Push origin** för att överföra ditt arbete till fjärrgrenen.

![push-origin](../assets/push-origin.png)

Om du vill skapa en pull-begäran väljer du **Skapa pull-begäran**.

![create-pr-vs](../assets/create-pr-vs.png)

Kontrollera att bas- och jämförelsegrenarna är korrekta. Lägg till en anteckning i PR, som beskriver uppdateringen och välj sedan **Skapa pull-begäran**. Då öppnas en PR som sammanfogar arbetsgrenen i ditt arbete med huvudgrenen i Adobe-databasen.

>[!TIP]
>
>Låt kryssrutan **Tillåt redigeringar av underhållare** vara markerad för att se till att Adobe dokumentationsteam kan göra ändringar i PR-dokumentet.

![create-pr](../assets/create-pr.png)

Du kan bekräfta att pull-begäran har skickats genom att granska mottagarfliken i https://github.com/AdobeDocs/experience-platform.en.

![confirm-pr](../assets/confirm-pr.png)
