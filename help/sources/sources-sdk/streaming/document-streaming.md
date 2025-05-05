---
title: Dokumentera din Source (Streaming SDK)
description: Det sista steget innan den nya källan kan publiceras i Adobe Experience Platform är att dokumentera den nya källan.
exl-id: 65ca7a4d-3e02-4f54-bf07-ea2c92b8dbf1
badge: Beta
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# Dokumentera källan (Streaming SDK)

>[!NOTE]
>
>Självbetjäning Källströmning SDK är en betaversion. Läs [källöversikten](../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade källor.

Det sista steget innan den nya källan kan publiceras i Adobe Experience Platform är att dokumentera den nya källan.

Den här handboken innehåller följande:

* En självstudiekurs som du kan följa för att skapa en dokumentationssida för den nya källan;
* En dokumentationsmall där du kan fylla i för den nya källan;
* [Instruktioner om hur du använder Markdown för att skriva teknisk dokumentation](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=sv-SE);
* [Instruktioner om hur du förstår Adobe Markdown-smak](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=sv-SE#custom-markdown-extensions).

## Förhandskrav

Följande objekt krävs innan du kan börja dokumentera den nya källan:

* **Ett giltigt GitHub-användarkonto**: Om du inte har något befintligt GitHub-konto måste du skapa ett via [GitHub-registreringssidan](https://github.com/);
* **Åtkomst till GitHub Desktop**: Du måste använda [GitHub-skrivbordsappen](https://desktop.github.com/) för att kunna skapa källdokumentation i din lokala miljö;
* Din integrering med Adobe måste vara i en testfas med din källa i en testmiljö i Experience Platform.

## Instruktioner på hög nivå för att skapa dokumentation för källan i Experience Platform

Om du vill skapa dokumentation för källan måste du skapa en gaffel i Experience Platform dokumentationsarkiv och redigera dokumentationsmallen i en ny gren. Använd mallen som tillhandahålls av Adobe för att skapa en ny källsida och öppna en pull-begäran (PR) när du är klar. Anvisningar om hur du gör detta finns nedan, i steg för att skapa en ny källsida.

## Dokumentationsmall

Du kan använda en förfylld [API-dokumentationsmall](streaming-template-api.md) eller [dokumentationsmallen för användargränssnittet](streaming-template-ui.md) för att skapa dokumentation för källan. Nedan finns instruktioner om hur du redigerar mallen och öppnar en pull-begäran. Dokumentation som skickas till den nya källan granskas och publiceras av Adobe dokumentationsteam.

Du kan även hämta dokumentationsmallarna nedan:

* [API-dokumentationsmall](../assets/streaming/streaming-template-api.zip)
* [Dokumentationsmall för användargränssnitt](../assets/streaming/streaming-template-ui.zip)

## Skapa en ny källsida

Du kan använda GitHub-webbgränssnittet eller din lokala miljö för att skapa dokumentation för den nya källan i Experience Platform. Sök efter instruktioner för båda alternativen i länkarna nedan:

* [Skapa en källdokumentationssida med GitHub-webbgränssnittet](../documentation/github.md)
* [Använda en textredigerare i den lokala miljön för att skapa en källdokumentationssida](../documentation/text-editor.md)
