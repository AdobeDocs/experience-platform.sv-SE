---
title: Bästa tillvägagångssätt
description: Lär dig vilka regler och tips du bör följa när du skapar en dokumentationssida för målet, så att du kan vara säker på att den uppfyller Adobe Experience Platform kvalitetsstandarder för dokumentation.
exl-id: b12059f1-6635-41cd-acc5-6ff471111164
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# Bästa tillvägagångssätt

## Översikt {#overview}

Den här sidan beskriver regler som du bör följa när [skapa din måldokumentation](./documentation-instructions.md) för att säkerställa att den uppfyller Adobe Experience Platform dokumentationskvalitetsstandarder.

## Allmän vägledning {#general-guidance}

* När du fyller i [mall](./self-service-template.md) om du vill ha mer information om destinationsdokumentationen läser du i handboken för medverkande på Adobe [länka](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html), [tabeller](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html#tables), [markeringssyntax som stöds](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html), [skrivande vägledning](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html), med mera.
* Ta inte med observationer och uppskattningar i produktdokumentationen.
* I Experience Platform-dokumentationen använder Adobe-skribenter **fet formatering** för att hänvisa till användargränssnittskontroller, så här:
   * Gå till **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** och väljer **[!UICONTROL Catalog]** -fliken. Visa ett exempel på hur gränssnittskontroller dokumenteras i en [mål, genomgång](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html#select-destination).

## Skrivstil

>[!IMPORTANT]
>
>Läs [Skriftlig vägledning för Adobe-dokumentation](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html) innan du börjar redigera måldokumentationssidan.

* Håll dina meningar korta och kom till saken snabbt. Om din mening är längre än 20 ord eller använder flera kommatecken kan du dela upp den i olika meningar. Meningar som är längre än 20 ord kan vara särskilt komplicerade för läsarna.
* Var inte överdrivet artig. Undvik att använda&quot;snälla&quot; eller&quot;snälla&quot; ...&quot; i den tekniska dokumentationen.

## Länkning {#linking}

Följ den angivna dokumentationsmallen och redigera inte de befintliga länkarna i mallen. När nya länkar tas med, läs [använda länkar i dokumentation](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html) i medverkarhandboken.

## Riktlinjer för varumärken {#branding}

* AEP är inte en godkänd offentlig term. Använd Adobe Experience Platform först, sedan Experience Platform och sedan Platform.
   * **Använd inte**: Innan du kan exportera data från AEP till YourDestination måste du läsa och slutföra dessa krav.
   * **Använd**: Innan du kan exportera data från Adobe Experience Platform till ditt mål måste du kontrollera att du har läst och fyllt i dessa krav.

## Bilder och skärmbilder {#images-and-screenshots}

* För information om [länka till bilder](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html#images), se medverkarhandboken.
* När du använder skärmbilder måste du se till att skärmbilden fångar upp hela användargränssnittsskärmen för plattformen.
* När du markerar bilder för att markera en viss kontroll eller etikett på sidan, ska du följa den markeringsstil som används av dokumentationsteamet på Experience Platform. Lägg märke till hur profilbaserad markeras i [den här skärmbilden](/help/destinations/catalog/cloud-storage/amazon-s3.md#export-type-frequency).
* Använd `png` formatera bilder.
* Använd inte numrerade skärmbilder som filnamn. Bildfilnamn ska vara beskrivande.
   * **Använd inte**: `1.png`, `2.png`, `3.png`
   * **Använd**: `yourdestination-authentication-details.png`, `yourdestination-destination-details.png`
* Använd alternativ text för alla bilder som du lägger till i dokumentationen och använd rätt grammatik i alternativ text.
   * **Använd inte**: Information om målanslutning
   * **Använd**: Bild av plattformsgränssnittet, med information om målanslutning ifylld.

## Process {#process}

* The [dokumentmall](./self-service-template.md) uppdateras sällan, baserat på feedback från partner. Innan du börjar skapa dokumentation för målet bör du kontrollera att du har hämtat [senaste versionen av mallen](../assets/docs-framework/yourdestination-template.zip).
* Skriv dokumentationen och skapa en begäran om dokumentationsinstruktion (PR) från en gren i ditt gaffel *annan än huvudgrenen*. Se Skicka-målet för granskning när du redigerar i dialogrutan [GitHub-gränssnitt](./use-github-interface-to-create-documentation.md#submit-review) eller in [din lokala miljö](./work-in-local-environment.md#submit-review).
