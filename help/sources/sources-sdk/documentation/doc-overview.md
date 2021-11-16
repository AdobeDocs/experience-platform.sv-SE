---
keywords: Experience Platform;hem;populära ämnen;källor;kopplingar;källkopplingar;källor sdk;sdk;SDK
solution: Experience Platform
title: Dokumentera källan
topic-legacy: overview
description: Det sista steget innan den nya källan kan publiceras i Adobe Experience Platform är att dokumentera den nya källan.
hide: true
hidefromtoc: true
source-git-commit: ae1a1139c24fd80e9f689e4c637897c905004c5f
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# Dokumentera källan

>[!IMPORTANT]
>
>SDK:n för källor är för närvarande i betaversion och din organisation har kanske inte åtkomst till den än. Funktionerna som beskrivs i den här dokumentationen kan komma att ändras.

Det sista steget innan den nya källan kan publiceras i Adobe Experience Platform är att dokumentera den nya källan.

Den här handboken innehåller följande:

* En självstudiekurs som du kan följa för att skapa en dokumentationssida för den nya källan;
* En dokumentationsmall där du kan fylla i för den nya källan;
* [Instruktioner om hur du använder Markdown för att skriva teknisk dokumentation](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en);
* [Instruktioner om hur du förstår Adobe Markdown-smak](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#custom-markdown-extensions).

## Förutsättningar

Följande objekt krävs innan du kan börja dokumentera den nya källan:

* **Ett giltigt GitHub-användarkonto**: Om du inte har något befintligt GitHub-konto måste du skapa ett via [Registreringssida för GitHub](https://github.com/);
* **Åtkomst till GitHub Desktop**: Du måste använda [GitHub-skrivbordsapp](https://desktop.github.com/) för att skapa källdokumentation i din lokala miljö,
* Din integrering med Adobe måste vara i en testfas med din källa driftsatt i en staging-miljö i Platform.

## Instruktioner på hög nivå för att skapa dokumentation för källan i Platform

Om du vill skapa dokumentation för din källa måste du på en hög nivå skapa en gaffel i plattformens dokumentationsarkiv och redigera den tillhandahållna dokumentationsmallen i en ny gren. Använd mallen som tillhandahålls av Adobe för att skapa en ny källsida och öppna en pull-begäran (PR) när du är klar. Anvisningar om hur du gör detta finns nedan, i steg för att skapa en ny källsida.

## Dokumentationsmall

Du kan använda en förfylld injektionspenna. [dokumentmall](./template.md) som hjälper dig att skapa dokumentation för källan. Nedan finns instruktioner om hur du redigerar mallen och öppnar en pull-begäran. Dokumentation som skickas till den nya källan granskas och publiceras av dokumentationsteamet på Adobe.

Du kan även hämta [dokumentmall här](../assets/template.zip).

## Skapa en ny källsida

Du kan använda GitHub-webbgränssnittet eller din lokala miljö för att skapa dokumentation för den nya källan i Platform. Sök efter instruktioner för båda alternativen i länkarna nedan:

* [Använd GitHub-webbgränssnittet för att skapa en källdokumentationssida](./github.md)
* [Använda en textredigerare i den lokala miljön för att skapa en källdokumentationssida](./text-editor.md)