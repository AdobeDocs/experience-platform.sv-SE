---
title: Skapa en måldokumentationssida med en textredigerare i den lokala miljön
seo-title: Use a text editor in your local environment to create a destination documentation page
description: Instruktionerna på den här sidan visar hur du använder en textredigerare för att arbeta i din lokala miljö med att skapa dokumentation och skicka in en pull-begäran.
seo-description: The instructions on this page show you how to use a text editor to work in your local environment to author documentation and submit a pull request.
exl-id: 125f2d10-0190-4255-909c-5bd5bb59fcba
source-git-commit: e1e7d2f70c032d02f96b3999e4fca736070c6ca9
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 0%

---

# Skapa en måldokumentationssida med en textredigerare i den lokala miljön {#local-authoring}

Instruktionerna på den här sidan visar hur du använder en textredigerare för att arbeta i din lokala miljö för att skapa dokumentation och skicka en pull-begäran (PR). Innan du går igenom de steg som anges här bör du läsa [Dokumentera ditt mål i Adobe Experience Platform Destinations](./documentation-instructions.md).

>[!TIP]
>
>Se även supportdokumentationen i Adobe Contributor Guide:
>* [Installera Git- och Markdown Authoring tools](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)
>* [Konfigurera Git-databasen lokalt för dokumentation](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)
>* [Arbetsflöde för GitHub-bidrag för större ändringar](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en).


## Anslut till GitHub och konfigurera din lokala redigeringsmiljö {#set-up-environment}

1. Navigera till `https://github.com/AdobeDocs/experience-platform.en` i webbläsaren
2. Om du vill [förgrening](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository) databasen klickar du på **Förgrening** så som visas på skärmbilden.

   ![Dokumentationsarkiv för Adobe](./assets/ssd-fork-repo.png)

3. Klona databasen till din lokala dator. Välj **Kod > HTTPS > Öppna med GitHub Desktop**, så som visas nedan. Kontrollera att du har [GitHub Desktop](https://desktop.github.com/) installerat. Mer information finns i [Skapa en lokal klon av databasen](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#create-a-local-clone-of-the-repository) i handboken för medverkande på Adobe.

   ![Klona dokumentationsarkivet för Adobe till lokal miljö](./assets/clone-local.png)

4. Navigera till `experience-platform.en/help/destinations/catalog/[...]`, där `[...]` är den önskade kategorin för målet i den lokala filstrukturen. Om du till exempel lägger till ett anpassningsmål i Experience Platform väljer du mappen `personalization`.

## Skriv dokumentationssidan för ditt mål {#author-documentation}

1. Dokumentationssidan är baserad på [självbetjäningsmålmallen](./self-service-template.md). Hämta [målmallen](assets/yourdestination-template.zip). Zippa upp den och extrahera filen `yourdestination-template.md` till den katalog som nämns i steg 4 ovan.  Byt namn på filen `YOURDESTINATION.md` där YOURDESTINATION är namnet på målet i Adobe Experience Platform. Om ditt företag till exempel heter Moviestar skulle du namnge filen `moviestar.md`.
2. Öppna den nya filen i [valfri textredigerare](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en#understand-markdown-editors). Adobe rekommenderar att du använder [Visual Studio-kod](https://code.visualstudio.com/) och installerar redigeringstillägget Adobe Markdown. Om du vill installera tillägget öppnar du Visual Studio Code, väljer fliken **[!DNL Extensions]** till vänster på skärmen och söker efter `adobe markdown authoring`. Markera tillägget och klicka på **[!DNL Install]**.
   ![Installera tillägget Adobe Markdown Authoring](./assets/install-adobe-markdown-extension.gif)
3. Redigera mallen med relevant information om destinationen. Följ instruktionerna i mallen.
4. För skärmbilder eller bilder som du planerar att lägga till i dokumentationen går du till `GitHub/experience-platform.en/help/destinations/assets/catalog/[...]`, där `[...]` är den önskade kategorin för ditt mål. Om du till exempel lägger till ett anpassningsmål i Experience Platform väljer du mappen `personalization`. Skapa en ny mapp för destinationen och spara bilderna här. Du måste länka till dem från sidan som du redigerar. Se [instruktioner om hur du länkar till bilder](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en#link-to-images).
5. När du är klar sparar du filen som du arbetar med.

## Skicka in din dokumentation för granskning {#submit-review}

1. I GitHub Desktop skapar du en arbetsgren för dina uppdateringar och väljer **Publiceringsgren** för att publicera grenen på GitHub.

![Ny lokal gren](./assets/new-branch-local.gif)

1. I GitHub Desktop [utför](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#commit) ditt arbete, vilket visas nedan.

   ![Genomför lokal](./assets/commit-local.png)

1. I GitHub Desktop [push](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#push) ditt arbete till grenen [remote](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#remote) enligt nedan.

   ![Gör din implementering](./assets/push-local-to-remote.png)

1. Öppna en pull-begäran (PR) i GitHub-webbgränssnittet för att sammanfoga din arbetsgren med den överordnad grenen i dokumentationsdatabasen för Adobe. Kontrollera att grenen du arbetade med är markerad och välj **Pull request**.

   ![Skapa pull-begäran](./assets/ssd-create-pull-request-1.png)

1. Kontrollera att bas- och jämförelsegrenarna är korrekta. Lägg till en anteckning i PR:en som beskriver uppdateringen och välj **Skapa pull-begäran**. Då öppnas en PR som sammanfogar arbetsgrenen i din gaffel till den överordnad grenen i Adobe-databasen.
   >[!TIP]
   >
   >Låt kryssrutan **Tillåt redigeringar av underhållare** vara markerad så att dokumentationsteamet på Adobe kan göra ändringar i PR-dokumentet.

   ![Skapa pull-begäran till Adobe-dokumentationsarkivet](./assets/ssd-create-pull-request-2.png)

1. Nu visas ett meddelande som uppmanar dig att signera Adobe Contributor License Agreement (CLA). Detta är ett obligatoriskt steg. När du har signerat CLA-avtalet uppdaterar du PR-sidan och skickar pull-begäran.

1. Du kan bekräfta att pull-begäran har skickats genom att granska fliken **Pull-begäranden** i `https://github.com/AdobeDocs/experience-platform.en`.

![PR lyckades](./assets/ssd-pr-successful.png)

1. Tack! Dokumentationsteamet på Adobe kommer att nå ut i PR om det skulle behövas ändringar och informera dig om när dokumentationen kommer att publiceras.

>[!TIP]
>
>Om du vill lägga till bilder och länkar i din dokumentation och om du vill ha andra frågor om Markdown, ska du läsa [Använda Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en) i Adobe samarbetshandbok.
