---
title: Skapa en måldokumentationssida med en textredigerare i den lokala miljön
description: Instruktionerna på den här sidan visar hur du använder en textredigerare för att arbeta i din lokala miljö för att skapa en dokumentationssida för ditt Experience Platform-mål och skicka den för granskning.
exl-id: 125f2d10-0190-4255-909c-5bd5bb59fcba
source-git-commit: 0d98183838125fac66768b94bc1993bde9a374b5
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 0%

---

# Skapa en måldokumentationssida med en textredigerare i den lokala miljön {#local-authoring}

Instruktionerna på den här sidan visar hur du använder en textredigerare för att arbeta i din lokala miljö för att skapa dokumentation och skicka en pull-begäran (PR). Innan du går igenom de steg som anges här bör du läsa [Dokumentera ditt mål i Adobe Experience Platform Destinations](./documentation-instructions.md).

>[!TIP]
>
>Se även supportdokumentationen i Adobe Contributor Guide:
>* [Installera Git- och Markdown-redigeringsverktygen](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=sv-SE)
>* [Konfigurera Git-databasen lokalt för dokumentation](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=sv-SE)
>* [Arbetsflöde för GitHub-bidrag för större ändringar](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=sv-SE).

## Anslut till GitHub och konfigurera din lokala redigeringsmiljö {#set-up-environment}

1. Navigera till `https://github.com/AdobeDocs/experience-platform.en` i webbläsaren
2. Om du vill [förgrena](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=sv-SE#fork-the-repository) databasen klickar du på **Förgrening** enligt nedan. Detta skapar en kopia av Experience Platform-databasen i ditt eget GitHub-konto.

   ![Bläddra i Adobe dokumentationsarkiv](../assets/docs-framework/ssd-fork-repository.gif)

3. Klona databasen till din lokala dator. Välj **Kod > HTTPS > Öppna med GitHub Desktop**, så som visas nedan. Kontrollera att [GitHub Desktop](https://desktop.github.com/) är installerat. Mer information finns i [Skapa en lokal klon av databasen](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=sv-SE#create-a-local-clone-of-the-repository) i handboken för Adobe Contributor.

   ![Klona Adobe-dokumentationsarkivet till den lokala miljön](../assets/docs-framework/clone-local.png)

4. Navigera till `experience-platform.en/help/destinations/catalog/[...]` i den lokala filstrukturen, där `[...]` är den önskade kategorin för ditt mål. Om du till exempel lägger till ett anpassningsmål till Experience Platform väljer du mappen `personalization`.

## Skriv dokumentationssidan för ditt mål {#author-documentation}

1. Dokumentationssidan är baserad på [målmallen för självbetjäning](../docs-framework/self-service-template.md). Hämta [målmallen](../assets/docs-framework/yourdestination-template.zip). Zippa upp den och extrahera filen `yourdestination-template.md` till katalogen som nämns i steg 4 ovan.  Byt namn på filen `YOURDESTINATION.md`, där YOURDESTINATION är namnet på ditt mål i Adobe Experience Platform. Om ditt företag till exempel heter Moviestar skulle du kalla din fil `moviestar.md`.
2. Öppna den nya filen i den [textredigerare du vill använda](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=sv-SE#understand-markdown-editors). Adobe rekommenderar att du använder [Visual Studio Code](https://code.visualstudio.com/) och installerar tillägget Adobe Markdown Authoring. Om du vill installera tillägget öppnar du Visual Studio-kod, väljer fliken **[!DNL Extensions]** till vänster på skärmen och söker efter `adobe markdown authoring`. Markera tillägget och klicka på **[!DNL Install]**.
   ![Installera tillägget Adobe Markdown Authoring](../assets/docs-framework/install-adobe-markdown-extension.gif)
3. Redigera mallen med relevant information om destinationen. Följ instruktionerna i mallen.
4. För skärmbilder eller bilder som du planerar att lägga till i dokumentationen går du till `GitHub/experience-platform.en/help/destinations/assets/catalog/[...]`, där `[...]` är den önskade kategorin för ditt mål. Om du till exempel lägger till ett anpassningsmål till Experience Platform väljer du mappen `personalization`. Skapa en ny mapp för destinationen och spara bilderna här. Du måste länka till dem från sidan som du redigerar. Se [instruktioner om hur du länkar till bilder](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=sv-SE#link-to-images).
5. När du är klar sparar du filen som du arbetar med.

## Skicka in din dokumentation för granskning {#submit-review}

>[!TIP]
>
>Observera att det inte finns något du kan bryta här. Genom att följa instruktionerna i det här avsnittet föreslår du bara en uppdatering av dokumentationen. Den föreslagna uppdateringen kommer att godkännas eller redigeras av Adobe Experience Platform dokumentationsteam.

1. I GitHub Desktop skapar du en arbetsgren för dina uppdateringar och väljer **Publicera gren** för att publicera grenen på GitHub.

![Ny lokal gren](../assets/docs-framework/new-branch-local.gif)

1. I GitHub Desktop [utför](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#commit) ditt arbete, vilket visas nedan.

   ![Verkställ lokal](../assets/docs-framework/commit-local.png)

1. I GitHub Desktop [push](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#push) ditt arbete till grenen [remote](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#remote), vilket visas nedan.

   ![Skjut in din implementering](../assets/docs-framework/push-local-to-remote.png)

1. Öppna en pull-begäran (PR) i GitHub-webbgränssnittet för att sammanfoga din arbetsgren med huvudgrenen i Adobe dokumentationsdatabas. Kontrollera att grenen du arbetade med är markerad och välj **Contribute > Öppna pull-begäran**.

   ![Skapa pull-begäran](../assets/docs-framework/ssd-create-pull-request-1.gif)

1. Kontrollera att bas- och jämförelsegrenarna är korrekta. Lägg till en anteckning i PR, som beskriver uppdateringen och välj **Skapa pull-begäran**. Då öppnas en PR som sammanfogar arbetsgrenen i din gaffel med huvudgrenen i Adobe-databasen.

   >[!TIP]
   >
   >Låt kryssrutan **Tillåt redigeringar av underhållare** vara markerad så att Adobe dokumentationsteam kan göra ändringar i PR:en.

   ![Skapa pull-begäran till Adobe-dokumentationsarkivet](../assets/docs-framework/ssd-create-pull-request-2.png)

1. Nu visas ett meddelande som uppmanar dig att signera Adobe Contributor License Agreement (CLA). Detta är ett obligatoriskt steg. När du har signerat CLA-avtalet uppdaterar du PR-sidan och skickar pull-begäran.

1. Du kan bekräfta att pull-begäran har skickats genom att granska fliken **Pull-begäranden** i `https://github.com/AdobeDocs/experience-platform.en`.

![PR lyckades](../assets/docs-framework/ssd-pr-successful.png)

1. Tack! Adobe dokumentationsteam kommer att nå ut i PR om det skulle behövas ändringar och meddela när dokumentationen kommer att publiceras.

>[!TIP]
>
>Om du vill lägga till bilder och länkar i din dokumentation och om du vill ha andra frågor om Markdown kan du läsa [Använda Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=sv-SE) i Adobe guide för samarbete om skriftspråk.
