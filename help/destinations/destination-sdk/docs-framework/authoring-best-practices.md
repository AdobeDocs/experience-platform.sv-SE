---
title: Bästa tillvägagångssätt
description: Lär dig vilka regler och tips du bör följa när du skapar en dokumentationssida för målet, så att du kan vara säker på att den uppfyller Adobe Experience Platform kvalitetsstandarder för dokumentation.
source-git-commit: 35e5c388e9572a3b27ec4bce55e766725936eda4
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# Bästa tillvägagångssätt

## Översikt {#overview}

Den här sidan beskriver regler som du bör följa när [skapa din måldokumentation](./documentation-instructions.md) för att säkerställa att den uppfyller Adobe Experience Platform dokumentationskvalitetsstandarder.

## Allmän vägledning {#general-guidance}

* När du fyller i [mall](./self-service-template.md) om du vill ha mer information om destinationsdokumentationen läser du i handboken för medverkande på Adobe [länka](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en), [tabeller](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#tables), [markeringssyntax som stöds](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en), [skrivande vägledning](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en), med mera.
* Ta inte med observationer och uppskattningar i produktdokumentationen.
* I Experience Platform-dokumentationen använder Adobe-skribenter **fet formatering** för att hänvisa till användargränssnittskontroller, så här:
   * Gå till **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** och väljer **[!UICONTROL Catalog]** -fliken. Visa ett exempel på hur gränssnittskontroller dokumenteras i en [mål, genomgång](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#select-destination).

## Länkar {#linking}

Följ den angivna dokumentationsmallen och redigera inte de befintliga länkarna i mallen. När nya länkar tas med, läs [använda länkar i dokumentation](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en) i medverkarhandboken.

## Riktlinjer för varumärken {#branding}

* AEP är inte en godkänd offentlig term. Använd Adobe Experience Platform först, sedan Experience Platform och sedan Platform.
   * **Använd inte**: Innan du kan exportera data från AEP till YourDestination måste du läsa och slutföra dessa krav.
   * **Använd**: Innan du kan exportera data från Adobe Experience Platform till ditt mål måste du kontrollera att du har läst och fyllt i dessa krav.

## Bilder och skärmbilder {#images-and-screenshots}

* För information om [länka till bilder](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#images), se medverkarhandboken.
* När du använder skärmbilder måste du se till att skärmbilden fångar upp hela användargränssnittsskärmen för plattformen.
* När du markerar bilder för att markera en viss kontroll eller etikett på sidan, ska du följa den markeringsstil som används av dokumentationsteamet på Experience Platform. Lägg märke till hur profilbaserad markeras i [den här skärmbilden](/help/destinations/catalog/cloud-storage/amazon-s3.md#export-type-frequency).
* Använd `png` formatera bilder.
* Använd inte numrerade skärmbilder som filnamn. Bildfilnamn ska vara beskrivande.
   * **Använd inte**: `1.png`, `2.png`, `3.png`
   * **Använd**: `yourdestination-authentication-details.png`, `yourdestination-destination-details.png`
* Använd alternativ text för alla bilder som du lägger till i dokumentationen och använd rätt grammatik i alternativ text.
   * **Använd inte**: Information om målanslutning
   * **Använd**: Bild av plattformens användargränssnitt, med information om målanslutning ifylld.

## Process {#process}

* The [dokumentmall](./self-service-template.md) uppdateras sällan, baserat på feedback från partner. Innan du börjar skapa dokumentation för destinationen bör du kontrollera att du har laddat ned [senaste versionen av mallen](/help/destinations/destination-sdk/docs-framework/assets/yourdestination-template.zip).
* Skriv dokumentationen och skapa en begäran om dokumentationsinstruktion (PR) från en gren i ditt gaffel *annan än huvudgrenen*. Se Skicka-målet för granskning när du redigerar i [GitHub-gränssnitt](./use-github-interface-to-create-documentation.md#submit-review) eller in [din lokala miljö](./work-in-local-environment.md#submit-review).