---
keywords: Experience Platform;hem;populära ämnen;källor;kopplingar;källkopplingar;källor sdk;sdk;SDK
solution: Experience Platform
title: SDK-översikt för källor (beta)
topic-legacy: overview
description: Adobe Experience Platform Sources SDK är en uppsättning konfigurations-API:er som gör att du kan integrera en REST API-baserad källa med API:t för Flow Service för att överföra data till Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: bfe6be73ed05b494a4a3eb1153e53ee8b9864ecf
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# Översikt över SDK för källor (beta)

>[!IMPORTANT]
>
>SDK:n för källor är för närvarande i betaversion och din organisation har kanske inte åtkomst till den än. Funktionerna som beskrivs i den här dokumentationen kan komma att ändras.

Adobe Experience Platform Sources SDK är en uppsättning konfigurations-API:er som gör att du kan integrera en REST API-baserad källa med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) för att ta med data till Experience Platform.

Med Sources SDK kan du:

* Konfigurera en ny källa till plattformskatalogen, med funktioner för att skapa, läsa, uppdatera och ta bort med hjälp av [!DNL Flow Service] API.
* Definiera specifikationer för källan, inklusive information om vilka autentiseringstyper som stöds och hur resursdata hämtas.
* Skapa användarinriktad dokumentation för den nya källan.

I Sources SDK-dokumentationen finns anvisningar om hur du använder Adobe Experience Platform Sources SDK för att konfigurera, testa och släppa en REST API-baserad källintegrering med Platform, och få källan att bli en del av den ständigt växande källkatalogen.

![katalog](./assets/catalog.png)

## Om källor

Plattformen kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Mer information om källor och en lista över olika källor som för närvarande stöds på plattformen finns i [källöversikt](../home.md).

## Skapa en källa

Via Sources SDK kan du integrera din egen REST API-baserade källa och överföra data till plattformen med [!DNL Flow Service]. Med Sources SDK kan du integrera en ny källa med Platform genom att skapa och skicka en ny anslutningsspecifikation via [!DNL Flow Service] API.

Se guiden [skapa en ny anslutningsspecifikation](./api/overview.md) om du vill ha information om hur du integrerar en ny källa till plattform.

## Dokumentera källan

När du har skapat källan kan du se [handbok](./documentation/overview.md) för instruktioner om hur du dokumenterar källan via [!DNL GitHub] webbgränssnitt eller via din egen textredigerare.

## Högnivåprocess

Hur du konfigurerar källan i Experience Platform beskrivs nedan:

* Läs [Sources SDK API guide](./api/overview.md);
   * Läs [komma igång-guide](./api/getting-started.md);
   * Följ självstudiekursen på [skapa en ny anslutningsspecifikation](./api/create.md);
   * Följ självstudiekursen på [uppdatera anslutningsspecifikationen](./api/update-connection-specs.md);
   * Följ självstudiekursen på [lägga till ditt nya anslutningsspecifikation-ID i en flödesspecifikation](./api/update-flow-specs.md)
   * [Skicka din nya källa](./api/submit.md).
* Om du vill få en bättre förståelse för strukturen och egenskaperna för en anslutningsspecifikation kan du läsa guiden om [konfigurationsalternativ för SDK för källor](./config/config.md);
   * Se guiden [konfigurera dina autentiseringsspecifikationer](./config/authspec.md);
   * Se guiden [konfigurera dina källspecifikationer](./config/sourcespec.md);
   * Se guiden [konfigurera dina specifikationer](./config/explorespec.md);
* Information om hur du börjar dokumentera källan finns i [översikt över hur du skapar dokumentation för SDK för källor](./documentation/overview.md)
   * Du kan använda den här [dokumentationsmall för källor](./documentation/template.md) för att strukturera dokumentationen,
   * Se guiden [med GitHub-webbgränssnittet](./documentation/github.md) för steg om hur du skapar dokumentation med GitHub,
   * Se guiden [använda en textredigerare](./documentation/text-editor.md) för steg om hur du skapar dokumentation med din lokala dator.

