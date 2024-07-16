---
title: Skapa en måldokumentationssida med GitHub-webbgränssnittet
description: Instruktionerna på den här sidan visar hur du använder GitHub-webbgränssnittet för att skapa en dokumentationssida för ditt Experience Platform-mål och skicka den för granskning.
exl-id: 4780e05e-3d1d-4f1b-8441-df28d09c1a88
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 0%

---

# Skapa en måldokumentationssida med GitHub-webbgränssnittet {#github-interface}

Instruktionerna nedan visar hur du använder GitHub-webbgränssnittet för att skapa dokumentation och skicka en pull-begäran (PR). Innan du går igenom de steg som anges här bör du läsa [Dokumentera ditt mål i Adobe Experience Platform Destinations](./documentation-instructions.md).

>[!TIP]
>
>Se även supportdokumentationen i Adobe Contributor Guide:
>* [Installera Git- och Markdown-redigeringsverktygen](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html)
>* [Konfigurera Git-databasen lokalt för dokumentation](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html)
>* [Arbetsflöde för GitHub-bidrag för större ändringar](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html).

## Konfigurera din GitHub-redigeringsmiljö {#set-up-environment}

1. Navigera till `https://github.com/AdobeDocs/experience-platform.en` i webbläsaren.
2. Om du vill [förgrena](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html#fork-the-repository) databasen klickar du på **Förgrening** enligt nedan. Detta skapar en kopia av databasen Experience Platform i ditt eget GitHub-konto.

   ![Fork Adobe-dokumentationsdatabas](../assets/docs-framework/ssd-fork-repository.gif)

3. Skapa en ny gren för ditt projekt i databasens gaffel, så som visas nedan. Använd den här nya grenen för ditt arbete.

   ![Skapa ny GitHub-gren](../assets/docs-framework/new-branch-github.gif)

4. Navigera till `experience-platform.en/help/destinations/catalog/[...]` i mappstrukturen GitHub för den förankrade databasen, där `[...]` är den önskade kategorin för ditt mål. Om du till exempel lägger till ett anpassningsmål i Experience Platform väljer du kategorin `personalization`. Välj **Lägg till fil > Skapa ny fil**.

   ![Lägg till ny fil](../assets/docs-framework/github-navigate-and-create-file.gif)

5. Ange namnet `YOURDESTINATION.md` där YOURDESTINATION är namnet på målet i Adobe Experience Platform. Om ditt företag till exempel heter Moviestar skulle du kalla din fil `moviestar.md`.

## Skriv dokumentationssidan för ditt mål {#author-documentation}

1. Du skapar innehållet på målsidan baserat på [dokumentationsmallen för självbetjäning](./self-service-template.md). **[Hämta](../assets/docs-framework/yourdestination-template.zip)** mallen och zippa upp den för att extrahera `.md`-filmallen.
2. Klistra in och redigera innehållet i mallen med relevant information om målet i en markeringsredigerare online, till exempel [dillinger.io](https://dillinger.io/). Följ instruktionerna i mallen för mer information om vad du ska fylla i och vilka stycken som kan tas bort.

   >[!TIP]
   >
   >Du kan när som helst stänga webbläsarfönstret och öppna det igen senare. Ditt arbete sparas automatiskt och väntar på dig när du öppnar webbläsaren igen.
3. Kopiera innehållet från markeringsredigeraren till den nya filen i GitHub.
4. För skärmbilder eller bilder som du tänker använda använder du GitHub-gränssnittet för att överföra filerna till `experience-platform.en/help/destinations/assets/catalog/[...]`, där `[...]` är den önskade kategorin för målet. Om du till exempel lägger till ett anpassningsmål i Experience Platform väljer du kategorin `personalization`. Du måste länka till bilderna från sidan som du redigerar. Se [instruktioner om hur du länkar till bilder](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html#link-to-images).

   ![Överför bild till GitHub](../assets/docs-framework/upload-image.gif)

5. När du är klar sparar du filen i din gren.

![Bekräfta skapande av fil](../assets/docs-framework/ssd-confirm-file-creation.png)

## Skicka in din dokumentation för granskning {#submit-review}

>[!TIP]
>
>Observera att det inte finns något du kan bryta här. Genom att följa instruktionerna i det här avsnittet föreslår du bara en uppdatering av dokumentationen. Den föreslagna uppdateringen kommer att godkännas eller redigeras av Adobe Experience Platform dokumentationsteam.

1. När du har sparat filen och överfört de önskade bilderna kan du öppna en pull-begäran (PR) för att sammanfoga din arbetsgren med huvudgrenen i dokumentationsdatabasen för Adobe. Kontrollera att grenen du arbetade med är markerad och välj **Contribute > Öppna pull-begäran**.

![Skapa pull-begäran](../assets/docs-framework/ssd-create-pull-request-1.gif)

1. Kontrollera att bas- och jämförelsegrenarna är korrekta. Lägg till en anteckning i PR, som beskriver uppdateringen och välj **Skapa pull-begäran**. Då öppnas en PR som sammanfogar arbetsgrenen i din gaffel med huvudgrenen i Adobe-databasen.

   >[!TIP]
   >
   >Låt kryssrutan **Tillåt redigeringar av underhållare** vara markerad så att dokumentationsteamet på Adobe kan göra ändringar i PR-dokumentet.

   ![Skapa pull-begäran till Adobe-dokumentationsdatabasen](../assets/docs-framework/ssd-create-pull-request-2.png)

1. Nu visas ett meddelande som uppmanar dig att signera Adobe Contributor License Agreement (CLA). Detta är ett obligatoriskt steg. När du har signerat CLA-avtalet uppdaterar du PR-sidan och skickar pull-begäran.

1. Du kan bekräfta att pull-begäran har skickats genom att granska fliken **Pull-begäranden** i `https://github.com/AdobeDocs/experience-platform.en`.

   ![PR lyckades](../assets/docs-framework/ssd-pr-successful.png)

1. Tack! Dokumentationsteamet på Adobe kommer att nå ut i PR om det skulle behövas ändringar och informera dig om när dokumentationen kommer att publiceras.

>[!TIP]
>
>Om du vill lägga till bilder och länkar i din dokumentation och om du har frågor om Markdown kan du läsa [Använda Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html) i Adobe SAMARE-handbok.
