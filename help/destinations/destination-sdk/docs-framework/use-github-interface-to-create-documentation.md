---
title: Använd GitHub-webbgränssnittet för att skapa en måldokumentationssida
description: Instruktionerna på den här sidan visar hur du använder GitHub-webbgränssnittet för att skapa en dokumentationssida för ditt Experience Platform-mål och skicka den för granskning.
exl-id: 4780e05e-3d1d-4f1b-8441-df28d09c1a88
source-git-commit: e239de97a26ea2ff36bb74390e249851a13d2e13
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 0%

---

# Använd GitHub-webbgränssnittet för att skapa en måldokumentationssida {#github-interface}

Instruktionerna nedan visar hur du använder GitHub-webbgränssnittet för att skapa dokumentation och skicka en pull-begäran (PR). Innan du går igenom de steg som anges här bör du kontrollera att du läser [Dokumentera destinationen i Adobe Experience Platform Destinations](./documentation-instructions.md).

>[!TIP]
>
>Se även supportdokumentationen i Adobe Contributor Guide:
>* [Installera Git- och Markdown Authoring tools](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)
>* [Konfigurera Git-databasen lokalt för dokumentation](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)
>* [Arbetsflöde för GitHub-bidrag för större ändringar](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en).


## Konfigurera din GitHub-redigeringsmiljö {#set-up-environment}

1. I webbläsaren går du till `https://github.com/AdobeDocs/experience-platform.en`.
2. Till [gaffel](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository) databasen klickar du på **Gaffel** enligt nedan. Detta skapar en kopia av databasen Experience Platform i ditt eget GitHub-konto.

   ![Dokumentationsarkiv för Adobe](../assets/docs-framework/ssd-fork-repository.gif)

3. Skapa en ny gren för ditt projekt i databasens gaffel, så som visas nedan. Använd den här nya grenen för ditt arbete.

   ![Skapa ny GitHub-gren](../assets/docs-framework/new-branch-github.gif)

4. I mappstrukturen GitHub för den förankrade databasen navigerar du till `experience-platform.en/help/destinations/catalog/[...]`, där `[...]` är den önskade kategorin för destinationen. Om du till exempel lägger till ett anpassningsmål till Experience Platform väljer du `personalization` kategori. Välj **Lägg till fil > Skapa ny fil**.

   ![Lägg till ny fil](../assets/docs-framework/github-navigate-and-create-file.gif)

5. Namnge målet `YOURDESTINATION.md`, där YOURDESTINATION är namnet på destinationen i Adobe Experience Platform. Om ditt företag till exempel heter Moviestar skulle du namnge filen `moviestar.md`.

## Skriv dokumentationssidan för ditt mål {#author-documentation}

1. Du skapar innehållet på målsidan baserat på [självbetjäningsmall för dokumentation](./self-service-template.md). **[Hämta](../assets/docs-framework/yourdestination-template.zip)** mallen och zippa upp den för att extrahera `.md` filmall.
2. Klistra in och redigera innehållet i mallen med relevant information om destinationen i en markeringsredigerare online, som [dillinger.io](https://dillinger.io/). Följ instruktionerna i mallen för mer information om vad du ska fylla i och vilka stycken som kan tas bort.

   >[!TIP]
   >
   >Du kan när som helst stänga webbläsarfönstret och öppna det igen senare. Ditt arbete sparas automatiskt och väntar på dig när du öppnar webbläsaren igen.
3. Kopiera innehållet från markeringsredigeraren till den nya filen i GitHub.
4. Använd GitHub-gränssnittet för att överföra filerna till `experience-platform.en/help/destinations/assets/catalog/[...]`, där `[...]` är den önskade kategorin för destinationen. Om du till exempel lägger till ett anpassningsmål till Experience Platform väljer du `personalization` kategori. Du måste länka till bilderna från sidan som du redigerar. Se [anvisningar om hur du länkar till bilder](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en#link-to-images).

   ![Överför bild till GitHub](../assets/docs-framework/upload-image.gif)

5. När du är klar sparar du filen i din gren.

![Bekräfta skapande av fil](../assets/docs-framework/ssd-confirm-file-creation.png)

## Skicka in din dokumentation för granskning {#submit-review}

>[!TIP]
>
>Observera att det inte finns något du kan bryta här. Genom att följa instruktionerna i det här avsnittet föreslår du bara en uppdatering av dokumentationen. Den föreslagna uppdateringen kommer att godkännas eller redigeras av Adobe Experience Platform dokumentationsteam.

1. När du har sparat filen och överfört de önskade bilderna kan du öppna en pull-begäran (PR) för att sammanfoga din arbetsgren med den överordnad grenen i dokumentationsdatabasen för Adobe. Se till att grenen du arbetade med är markerad och väljer **Contribute > Öppna pull-begäran**.

![Skapa pull-begäran](../assets/docs-framework/ssd-create-pull-request-1.gif)

1. Kontrollera att bas- och jämförelsegrenarna är korrekta. Lägg till en anteckning till PR, som beskriver uppdateringen och välj **Skapa pull-begäran**. Då öppnas en PR som sammanfogar arbetsgrenen i din gaffel till den överordnad grenen i Adobe-databasen.

   >[!TIP]
   >
   >Lämna **Tillåt redigeringar av underhållare** kryssrutan markerad så att dokumentationsteamet på Adobe kan göra ändringar i PR.

   ![Skapa pull-begäran till Adobe-dokumentationsarkivet](../assets/docs-framework/ssd-create-pull-request-2.png)

1. Nu visas ett meddelande som uppmanar dig att signera Adobe Contributor License Agreement (CLA). Detta är ett obligatoriskt steg. När du har signerat CLA-avtalet uppdaterar du PR-sidan och skickar pull-begäran.

1. Du kan bekräfta att pull-begäran har skickats genom att granska **Dra in begäranden** tabba in `https://github.com/AdobeDocs/experience-platform.en`.

   ![PR lyckades](../assets/docs-framework/ssd-pr-successful.png)

1. Tack! Dokumentationsteamet på Adobe kommer att nå ut i PR om det skulle behövas ändringar och informera dig om när dokumentationen kommer att publiceras.

>[!TIP]
>
>Om du vill lägga till bilder och länkar till din dokumentation och om du vill ha andra frågor om Markdown läser du [Använda markering](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en) i Adobe samarbetsvägledning.
