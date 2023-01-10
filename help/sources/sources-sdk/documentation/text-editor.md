---
keywords: Experience Platform;hem;populära ämnen;källor;kopplingar;källkopplingar;källor sdk;sdk;SDK
solution: Experience Platform
title: Använd en textredigerare i din lokala miljö för att skapa en källdokumentationssida
description: Det här dokumentet innehåller anvisningar om hur du använder din lokala miljö för att skapa dokumentation för källan och skicka en pull-begäran (PR).
exl-id: 4cc89d1d-bc42-473d-ba54-ab3d1a2cd0d6
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 0%

---

# Använda en textredigerare i den lokala miljön för att skapa en källdokumentationssida

Det här dokumentet innehåller anvisningar om hur du använder din lokala miljö för att skapa dokumentation för källan och skicka en pull-begäran (PR).

>[!TIP]
>
>Följande dokument från Adobe medverkande kan användas som ytterligare stöd för din dokumentationsprocess: <ul><li>[Installera Git- och Markdown Authoring tools](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)</li><li>[Konfigurera Git-databasen lokalt för dokumentation](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)</li><li>[Arbetsflöde för GitHub-bidrag för större ändringar](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en)</li></ul>

## Förutsättningar

I följande självstudie måste du ha installerat GitHub Desktop på din lokala dator. Om du inte har GitHub Desktop kan du hämta programmet [här](https://desktop.github.com/).

## Anslut till GitHub och konfigurera din lokala redigeringsmiljö

Det första steget i att konfigurera din lokala redigeringsmiljö är att navigera till [Adobe Experience Platform GitHub-databas](https://github.com/AdobeDocs/experience-platform.en).

![platform-repo](../assets/platform-repo.png)

På huvudsidan i GitHub-databasen väljer du **Gaffel**.

![gaffel](../assets/fork.png)

Om du vill klona databasen till din lokala dator väljer du **Code**. I listrutan som visas väljer du **HTTPS** och sedan väljer **Öppna med GitHub Desktop**.

>[!TIP]
>
>Mer information finns i självstudiekursen om [konfigurera Git-databasen lokalt för dokumentation](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#create-a-local-clone-of-the-repository).

![open-git-desktop](../assets/open-git-desktop.png)

Låt sedan GitHub Desktop klona `experience-platform.en` databas.

![kloning](../assets/cloning.png)

När kloningsprocessen är klar går du till GitHub Desktop och skapar en ny gren. Välj **Överordnad** i den övre navigeringen och välj **Ny gren**

![ny gren](../assets/new-branch.png)

Ange ett beskrivande namn för din gren på pover-panelen som visas och välj sedan **Skapa gren**.

![create-branch-vs](../assets/create-branch-vs.png)

Nästa, välj **Publicera gren**.

![publish-branch](../assets/publish-branch.png)

## Skriv dokumentationssidan för källan

När databasen är klonad till din lokala dator och en ny gren skapas kan du nu börja skapa dokumentationssidan för den nya källan via [valfri textredigerare](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en#understand-markdown-editors).

Adobe rekommenderar att du använder [Visual Studio Code](https://code.visualstudio.com/) och att du installerar tillägget för redigering av Adobe Markdown. Om du vill installera tillägget startar du Visual Studio Code och väljer **Tillägg** från vänster navigering.

![extension](../assets/extension.png)

Nästa, ange `Adobe Markdown Authoring` i sökfältet och välj **Installera** från sidan som visas.

![installera](../assets/install.png)

Ladda ned [dokumentationsmall för källor](../assets/api-template.zip) och extrahera filen till `experience-platform.en/help/sources/tutorials/api/create/...` med [`...`] som representerar den kategori som du väljer. Om du t.ex. skapar en datakälla väljer du databasmappen.

Till sist följer du instruktionerna i mallen och redigerar mallen med relevant information om källan.

![edit-template](../assets/edit-template.png)

## Skicka in din dokumentation för granskning

Om du vill skapa en pull-begäran (PR) och skicka in din dokumentation för granskning sparar du först ditt arbete i [!DNL Visual Studio Code] (eller den textredigerare du valt). Sedan anger du ett implementeringsmeddelande med hjälp av GitHub Desktop och väljer **Verkställ för att skapa källdokumentation**.

![commit-vs](../assets/commit-vs.png)

Nästa, välj **Penselursprung** för att överföra ditt arbete till fjärrgrenen.

![push-origin](../assets/push-origin.png)

Om du vill skapa en pull-begäran väljer du **Skapa pull-begäran**.

![create-pr-vs](../assets/create-pr-vs.png)

Kontrollera att bas- och jämförelsegrenarna är korrekta. Lägg till en anteckning i PR-rapporten som beskriver uppdateringen och välj sedan **Skapa pull-begäran**. Då öppnas en PR för att sammanfoga arbetsgrenen i ditt arbete med den överordnad grenen i Adobe-databasen.

>[!TIP]
>
>Lämna **Tillåt redigeringar av underhållare** kryssrutan markerad för att säkerställa att dokumentationsteamet på Adobe kan göra ändringar i PR.

![create-pr](../assets/create-pr.png)

Du kan bekräfta att pull-begäran har skickats genom att granska mottagarfliken i https://github.com/AdobeDocs/experience-platform.en.

![confirm-pr](../assets/confirm-pr.png)
