---
keywords: Experience Platform;hem;populära ämnen;källor;kopplingar;källkopplingar;källor sdk;sdk;SDK
solution: Experience Platform
title: Använd GitHub-webbgränssnittet för att skapa en källdokumentationssida
description: Det här dokumentet innehåller anvisningar om hur du använder GitHub-webbgränssnittet för att skapa dokumentation och skicka en pull-begäran (PR).
exl-id: 84b4219c-b3b2-4d0a-9a65-f2d5cd989f95
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# Skapa en källdokumentationssida med GitHub-webbgränssnittet

Det här dokumentet innehåller anvisningar om hur du använder GitHub-webbgränssnittet för att skapa dokumentation och skicka en pull-begäran (PR).

>[!TIP]
>
>Följande dokument från Adobe bidragsguide kan användas som ytterligare stöd för din dokumentationsprocess: <ul><li>[Installera Git- och Markdown-redigeringsverktygen](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html)</li><li>[Konfigurera Git-databasen lokalt för dokumentation](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html)</li><li>[Arbetsflöde för GitHub-bidrag för större ändringar](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html)</li></ul>

## Konfigurera GitHub-miljön

Det första steget för att konfigurera GitHub-miljön är att navigera till [Adobe Experience Platform GitHub-databasen](https://github.com/AdobeDocs/experience-platform.en).

![platform-repo](../assets/platform-repo.png)

Välj sedan **Förgrening**.

![förgrening](../assets/fork.png)

När gaffeln är klar väljer du **master** och anger ett namn för den nya grenen i listrutan som visas. Se till att du anger ett beskrivande namn för din gren eftersom det används för ditt arbete och välj sedan **Skapa gren**.

![create-branch](../assets/create-branch.png)

Navigera till [`experience-platform.en/help/sources/tutorials/api/create/`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/tutorials/api/create) i mappstrukturen för GitHub i den förankrade databasen och välj sedan lämplig kategori för källan i listan. Om du till exempel skapar dokumentation för en ny CRM-källa väljer du **crm**.

>[!TIP]
>
>Om du skapar dokumentation för användargränssnittet går du till [`experience-platform.en/help/sources/tutorials/ui/create/`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/tutorials/ui/create) och väljer lämplig kategori för källan. Om du vill lägga till dina bilder går du till [`experience-platform.en/help/sources/images/tutorials/create/sdk`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/images/tutorials/create) och lägger sedan till skärmbilderna i mappen `sdk`.

![crm](../assets/crm.png)

En mapp med befintliga CRM-källor visas. Om du vill lägga till dokumentation för en ny källa väljer du **Lägg till fil** och sedan **Skapa ny fil** i listrutan som visas.

![create-new-file](../assets/create-new-file.png)

Ge källfilen namnet `YOURSOURCE.md` där YOURSOURCE är namnet på källan i Experience Platform. Om ditt företag till exempel är ACME CRM ska ditt filnamn vara `acme-crm.md`.

![git-interface](../assets/git-interface.png)

## Skriv dokumentationssidan för källan

Om du vill börja dokumentera den nya källan klistrar du in innehållet i dokumentationsmallen för [källor](./template.md) i GitHub-webbredigeraren. Du kan även hämta mallen [här](../assets/api-template.zip).

När mallen har kopierats till GitHub-webbredigeringsgränssnittet följer du instruktionerna som beskrivs i mallen och redigerar värdena som innehåller relevant information för källan.

![paste-template](../assets/paste-template.png)

När du är klar implementerar du filen i din gren.

![spara](../assets/commit.png)

## Skicka in din dokumentation för granskning

När filen har implementerats kan du öppna en pull-begäran (PR) för att sammanfoga din arbetsgren med huvudgrenen i Adobe dokumentationsdatabas. Kontrollera att grenen du har arbetat med är markerad och välj sedan **Jämför och dra in-begäran**.

![compare-pr](../assets/compare-pr.png)

Kontrollera att bas- och jämförelsegrenarna är korrekta. Lägg till en anteckning i PR, som beskriver uppdateringen och välj sedan **Skapa pull-begäran**. Då öppnas en PR som sammanfogar arbetsgrenen i ditt arbete med huvudgrenen i Adobe-databasen.

>[!TIP]
>
>Låt kryssrutan **Tillåt redigeringar av underhållare** vara markerad för att se till att Adobe dokumentationsteam kan göra ändringar i PR-dokumentet.

![create-pr](../assets/create-pr.png)

Nu visas ett meddelande som uppmanar dig att signera Adobe Contributor License Agreement (CLA). Detta är ett obligatoriskt steg. När du har signerat CLA-avtalet uppdaterar du PR-sidan och skickar pull-begäran.

Du kan bekräfta att pull-begäran har skickats genom att granska mottagarfliken i https://github.com/AdobeDocs/experience-platform.en.

![confirm-pr](../assets/confirm-pr.png)
