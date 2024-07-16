---
keywords: Experience Platform;hem;populära ämnen;källor;kopplingar;källkopplingar;källor sdk;sdk;SDK
solution: Experience Platform
title: Dokumentera din Source
description: Det sista steget innan den nya källan kan publiceras i Adobe Experience Platform är att dokumentera den nya källan.
exl-id: 80daadb1-127f-4f42-8bc9-fb89a7898462
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# Dokumentera källan

Det sista steget innan den nya källan kan publiceras i Adobe Experience Platform är att dokumentera den nya källan.

Den här handboken innehåller följande:

* En självstudiekurs som du kan följa för att skapa en dokumentationssida för den nya källan;
* En dokumentationsmall där du kan fylla i för den nya källan;
* [Instruktioner om hur du använder Markdown för att skriva teknisk dokumentation](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html);
* [Instruktioner för att förstå Adobe Markdown-smak](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html#custom-markdown-extensions).

## Förhandskrav

Följande objekt krävs innan du kan börja dokumentera den nya källan:

* **Ett giltigt GitHub-användarkonto**: Om du inte har något befintligt GitHub-konto måste du skapa ett via [GitHub-registreringssidan](https://github.com/);
* **Åtkomst till GitHub Desktop**: Du måste använda [GitHub-skrivbordsappen](https://desktop.github.com/) för att kunna skapa källdokumentation i din lokala miljö;
* Din integrering med Adobe måste vara i en testfas med din källa driftsatt i en staging-miljö i Platform.

## Instruktioner på hög nivå för att skapa dokumentation för källan i Platform

Om du vill skapa dokumentation för din källa måste du på en hög nivå skapa en gaffel i plattformens dokumentationsarkiv och redigera den tillhandahållna dokumentationsmallen i en ny gren. Använd mallen som tillhandahålls av Adobe för att skapa en ny källsida och öppna en pull-begäran (PR) när du är klar. Anvisningar om hur du gör detta finns nedan, i steg för att skapa en ny källsida.

## Dokumentationsmall

Du kan använda en förfylld [dokumentationsmall](./template.md) för att skapa dokumentation för källan. Nedan finns instruktioner om hur du redigerar mallen och öppnar en pull-begäran. Dokumentation som skickas till den nya källan granskas och publiceras av dokumentationsteamet på Adobe.

Du kan även hämta dokumentationsmallarna nedan:

* [API-dokumentationsmall](../assets/api-template.zip)
* [Dokumentationsmall för användargränssnitt](../assets/ui-template.zip)

## Skapa en ny källsida

Du kan använda GitHub-webbgränssnittet eller din lokala miljö för att skapa dokumentation för den nya källan i Platform. Sök efter instruktioner för båda alternativen i länkarna nedan:

* [Skapa en källdokumentationssida med GitHub-webbgränssnittet](./github.md)
* [Använda en textredigerare i den lokala miljön för att skapa en källdokumentationssida](./text-editor.md)
