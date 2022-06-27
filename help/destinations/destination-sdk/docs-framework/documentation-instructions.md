---
title: Dokumentera destinationen i Adobe Experience Platform
description: Stegvisa instruktioner om hur du skapar en dokumentationssida för destinationen i Adobe Experience Platform
exl-id: 6cc9c758-44bb-463b-941a-06b1a22ee8f3
source-git-commit: dd4a150351b5e0c41586cf663324aeb345a896e4
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# Dokumentera destinationen i Adobe Experience Platform

>[!IMPORTANT]
>
>Processen som beskrivs här krävs endast för partners som skickar producerade (offentliga) destinationer. Om du skapar ett privat mål för egen användning behöver du inte skapa och publicera någon dokumentation för destinationen.

## Översikt {#overview}

Välkommen till Adobe Experience Platform!
Att dokumentera destinationen är det sista steget innan det kan göras live i Adobe Experience Platform.

I det här dokumentationsavsnittet ingår:

* Stegvisa instruktioner för att skapa en dokumentationssida för det nya målet;
* En mall som du kan fylla i för din destination;
* [Allmänna instruktioner om hur du använder Markering](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en);
* [Specifika anvisningar för Adobe Markdown-aromen](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#custom-markdown-extensions) (Adobe Markdown-aromen påminner mycket om vanlig Markdown).
* A [sida med bästa praxis](./authoring-best-practices.md) för att hjälpa dig att skapa en dokumentationssida för målsidan som uppfyller kvalitetsstandarderna för Experience Platform-dokumentationen.

## Förutsättningar {#prerequisites}

Om du vill skapa dokumentation för destinationen enligt instruktionerna i den här artikeln behöver du följande objekt:

* **Ett GitHub-konto**. Registrera dig för [GitHub](https://github.com/) om du inte har något konto än.
* **GitHub Desktop**. Om du väljer att [skapa dokumentationen i den lokala miljön](./work-in-local-environment.md)måste du använda [GitHub Desktop](https://desktop.github.com/).
* Din integrering med Adobe måste vara i en testfas med ditt mål som distribueras i en testmiljö i Adobe Experience Platform.

## Instruktioner på hög nivå för att skapa dokumentation för destinationen i Adobe Experience Platform {#high-level-instructions}

Om du vill skapa dokumentation för destinationen måste du [skapa en gaffel](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository) av Adobe Experience Platform dokumentationsarkiv och redigera [tillhandahållen dokumentationsmall](./self-service-template.md) i en ny gren. Använd mallen som tillhandahålls av Adobe för att skapa en ny målsida. Öppna en pull-begäran (PR) när du är klar. Instruktioner för att göra detta finns nedan, i [Steg för att skapa en ny målsida](./documentation-instructions.md#steps-to-create-docs-page).

<!--

* In the table of contents (TOC.md) `/help/rtcdp/TOC.md`, add a link to your new destination page. Place it within the category where your destination resides in the Adobe Experience Platform user interface (for example: mobile, social, advertising). 
* In the overview page for the respective category, add a link to your new destination page. For example, for cloud storage destinations, you would add a link to [this page](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-cat/cloud-storage/cloud-storage-destinations.html). 

-->

## Dokumentationsmall {#documentation-template}

Adobe har fyllt i en [dokumentmall](./self-service-template.md) för dig. Nedan finns instruktioner om hur du redigerar mallen och öppnar en pull-begäran. Dokumentationsteamet på Adobe granskar och publicerar dokumentationen för ditt nya mål.

[Hämta mallen här](assets/yourdestination-template.zip) och zippa upp filen för att extrahera `yourdestination.md` -fil.

Instruktioner om hur du använder mallen för att skapa dokumentationssidan finns nedan.

## Steg för att skapa en ny målsida {#steps-to-create-docs-page}

Du kan använda GitHub-webbgränssnittet eller din lokala miljö för att skapa dokumentation för ditt nya mål i Adobe Experience Platform. Sök efter instruktioner för båda alternativen i länkarna nedan:

* [Använd GitHub-webbgränssnittet för att skapa en måldokumentationssida](./use-github-interface-to-create-documentation.md)
* [Skapa en måldokumentationssida med en textredigerare i den lokala miljön](./work-in-local-environment.md)

## God praxis {#best-practices}

Granska [god praxis](/help/destinations/destination-sdk/docs-framework/authoring-best-practices.md) innan och medan du skapar måldokumentationssidan. Se även till att läsa [Skriftlig vägledning för Adobe-dokumentation](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en) för fler skrivtips som Adobe dokumentationsteamet använder när de skriver dokumentation.