---
title: 'Använd GitHub-webbgränssnittet för att skapa en måldokumentationssida '
seo-title: Use the GitHub web interface to create a destination documentation page
description: Instruktionerna på den här sidan visar hur du använder GitHub-webbgränssnittet för att skapa dokumentation och skicka en pull-begäran.
seo-description: The instructions on this page show you how to use the GitHub web interface to author documentation and submit a pull request.
exl-id: 4780e05e-3d1d-4f1b-8441-df28d09c1a88
source-git-commit: d2452bf0e59866d3deca57090001c4c5a0935525
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 0%

---

# Använd GitHub-webbgränssnittet för att skapa en måldokumentationssida {#github-interface}

Instruktionerna nedan visar hur du använder GitHub-webbgränssnittet för att skapa dokumentation och skicka en pull-begäran (PR). Innan du går igenom de steg som anges här bör du läsa [Dokumentera ditt mål i Adobe Experience Platform Destinations](./documentation-instructions.md).

>[!TIP]
>
>Se även supportdokumentationen i Adobe Contributor Guide:
>* [Installera Git- och Markdown Authoring tools](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)
>* [Konfigurera Git-databasen lokalt för dokumentation](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)
>* [Arbetsflöde för GitHub-bidrag för större ändringar](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en).


## Konfigurera din GitHub-redigeringsmiljö {#set-up-environment}

1. Navigera till `https://github.com/AdobeDocs/experience-platform.en` i webbläsaren.
2. Om du vill [förgrening](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository) databasen klickar du på **Förgrening** enligt bilden nedan.

   ![Dokumentationsarkiv för Adobe](./assets/ssd-fork-repo.png)

3. Skapa en ny gren för ditt projekt i databasens gaffel, så som visas nedan. Använd den här nya grenen för ditt arbete.

   ![Skapa ny GitHub-gren](./assets/new-branch-github.gif)

4. Navigera till `experience-platform.en/help/destinations/catalog/[...]`, där `[...]` är den önskade kategorin för ditt mål, i mappstrukturen GitHub för den förankrade databasen. Om du till exempel lägger till ett anpassningsmål i Experience Platform väljer du kategorin `personalization`. Välj **Lägg till fil > Skapa ny fil**.

   ![Lägg till ny fil](./assets/github-navigate-and-create-file.gif)

5. Ange ett namn på målet `YOURDESTINATION.md`, där YOURDESTINATION är namnet på målet i Adobe Experience Platform. Om ditt företag till exempel heter Moviestar skulle du namnge filen `moviestar.md`.

## Skriv dokumentationssidan för ditt mål {#author-documentation}

1. Du skapar innehållet på målsidan baserat på självbetjäningsmallen [för dokumentationen](./self-service-template.md). **[Ladda](assets/yourdestination-template.zip)** ned mallen och zippa upp den för att extrahera  `.md` filmallen.
2. Klistra in och redigera innehållet i mallen med relevant information om målet i en markeringsredigerare online, till exempel [dillinger.io](https://dillinger.io/). Följ instruktionerna i mallen för mer information om vad du ska fylla i och vilka stycken som kan tas bort.
3. Kopiera innehållet från markeringsredigeraren till den nya filen i GitHub.
4. För skärmbilder eller bilder som du tänker använda använder du GitHub-gränssnittet för att överföra filerna till `experience-platform.en/help/destinations/assets/catalog/[...]`, där `[...]` är den önskade kategorin för målet. Om du till exempel lägger till ett anpassningsmål i Experience Platform väljer du kategorin `personalization`. Du måste länka till bilderna från sidan som du redigerar. Se [instruktioner om hur du länkar till bilder](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en#link-to-images).

   ![Överför bild till GitHub](./assets/upload-image.gif)

5. När du är klar sparar du filen i din gren.

![Bekräfta skapande av fil](./assets/ssd-confirm-file-creation.png)

## Skicka in din dokumentation för granskning {#submit-review}

1. När du har sparat filen och överfört de önskade bilderna kan du öppna en pull-begäran (PR) för att sammanfoga din arbetsgren med den överordnad grenen i dokumentationsdatabasen för Adobe. Kontrollera att grenen du arbetade med är markerad och välj **Pull request**.

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
