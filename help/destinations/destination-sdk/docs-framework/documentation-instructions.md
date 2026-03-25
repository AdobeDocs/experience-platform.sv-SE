---
title: Dokumentera destinationen i Adobe Experience Platform
description: Stegvisa instruktioner om hur du skapar en dokumentationssida för destinationen i Adobe Experience Platform
exl-id: 6cc9c758-44bb-463b-941a-06b1a22ee8f3
source-git-commit: d946d3dbb09c1fe0163fba3a892b4c0f1b331f87
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 0%

---

# Dokumentera ditt mål i [!DNL Adobe Experience Platform]

>[!IMPORTANT]
>
>Processen som beskrivs här krävs endast för partners som skickar producerade (offentliga) destinationer. Om du skapar ett privat mål för egen användning behöver du inte skapa och publicera någon dokumentation för destinationen.

## Översikt {#overview}

Välkommen till [!DNL Adobe Experience Platform], bra att ha dig här!
Att dokumentera ditt mål är det sista steget innan det kan anges live i [!DNL Adobe Experience Platform].

I det här dokumentationsavsnittet ingår:

* Stegvisa instruktioner för att skapa en dokumentationssida för det nya målet;
* En mall som du kan fylla i för din destination;
* [Allmänna instruktioner om hur du använder Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html);
* [Specifika instruktioner för Adobe Markdown-aromen](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html#custom-markdown-extensions) (Adobe Markdown-aromen liknar den för vanlig Markdown).
* En [sida för bästa praxis](./authoring-best-practices.md) som hjälper dig att skapa en dokumentationssida för målsidan, som uppfyller Experience Platform kvalitetsstandarder för dokumentation.

## Förutsättningar {#prerequisites}

Om du vill skapa dokumentation för destinationen enligt instruktionerna i den här artikeln behöver du följande objekt:

* **Ett GitHub-konto**. Registrera dig för [GitHub](https://github.com/) om du inte har något konto än.
* **GitHub Desktop**. Om du väljer att [skapa dokumentationen i din lokala miljö](./work-in-local-environment.md) måste du använda [GitHub Desktop](https://desktop.github.com/).
* Din integrering med Adobe måste vara i en testfas med ditt mål som är distribuerat i en testmiljö i [!DNL Adobe Experience Platform].

## Instruktioner på hög nivå för att skapa dokumentation för ditt mål i [!DNL Adobe Experience Platform] {#high-level-instructions}

Om du på en hög nivå vill skapa dokumentation för ditt mål måste du [skapa en gaffel](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html#fork-the-repository) i dokumentationsdatabasen för [!DNL Adobe Experience Platform] och redigera den [tillhandahållna dokumentationsmallen](./self-service-template.md) i en ny gren. Använd mallen som tillhandahålls av Adobe för att skapa en ny målsida. Öppna en pull-begäran (PR) när du är klar. Instruktioner om hur du gör detta finns nedan, i [steg för att skapa din nya målsida](./documentation-instructions.md#steps-to-create-docs-page).

<!--

* In the table of contents (TOC.md) `/help/rtcdp/TOC.md`, add a link to your new destination page. Place it within the category where your destination resides in the Adobe Experience Platform user interface (for example: mobile, social, advertising). 
* In the overview page for the respective category, add a link to your new destination page. For example, for cloud storage destinations, you would add a link to [this page](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-cat/cloud-storage/cloud-storage-destinations.html). 

-->

## Dokumentationsmall {#documentation-template}

Adobe har förfyllt en [dokumentationsmall](./self-service-template.md) åt dig så att du enklare kan skapa din dokumentationssida. Nedan finns instruktioner om hur du redigerar mallen och öppnar en pull-begäran. Adobe dokumentationsteam granskar och publicerar dokumentationen för ditt nya mål.

[Hämta mallen här](../assets/docs-framework/yourdestination-template.zip) och packa upp filen för att extrahera `yourdestination.md`-filen.

Instruktioner om hur du använder mallen för att skapa dokumentationssidan finns nedan.

## Steg för att skapa en ny målsida {#steps-to-create-docs-page}

Du kan använda GitHub-webbgränssnittet eller den lokala miljön för att skapa dokumentation för det nya målet i [!DNL Adobe Experience Platform]. Sök efter instruktioner för båda alternativen i länkarna nedan:

* [Skapa en måldokumentationssida med GitHub-webbgränssnittet](./use-github-interface-to-create-documentation.md)
* [Skapa en måldokumentationssida med en textredigerare i den lokala miljön](./work-in-local-environment.md)

## Bästa praxis {#best-practices}

Granska de [bästa sätten att skapa ](/help/destinations/destination-sdk/docs-framework/authoring-best-practices.md) innan och medan du skapar måldokumentationssidan. Läs även [handledningen för skrivande av Adobe-dokumentation](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html) om du vill ha mer skrivande tips som Adobe dokumentationsteam använder när de skapar dokumentation.