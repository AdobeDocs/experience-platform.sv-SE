---
title: Bästa tillvägagångssätt
description: Lär dig vilka regler och tips du bör följa när du skapar en dokumentationssida för målet, så att du kan vara säker på att den uppfyller Adobe Experience Platform kvalitetsstandarder för dokumentation.
exl-id: b12059f1-6635-41cd-acc5-6ff471111164
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---

# Bästa tillvägagångssätt

## Översikt {#overview}

Den här sidan beskriver regler som du bör följa när du redigerar sidan för måldokumentation](./documentation-instructions.md), för att se till att den uppfyller kvalitetsstandarderna för Adobe Experience Platform-dokumentation.[

## Allmän vägledning {#general-guidance}

* När du fyller i [mallen](./self-service-template.md) för måldokumentationen läser du i handboken för Adobe Contributor om du vill ha information om [länkning](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html), [tabeller](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html#tables), den [kodningssyntax som stöds](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html), [skrivande vägledning](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html) med mera.
* Ta inte med observationer och uppskattningar i produktdokumentationen.
* I Experience Platform-dokumentationen använder Adobe-skrivare **fet formatering** för att referera till gränssnittskontroller, enligt följande:
   * Gå till **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** och välj fliken **[!UICONTROL Catalog]**. Visa ett exempel på hur användargränssnittskontroller dokumenteras i en [målsjälvstudiekurs](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html#select-destination).

## Skrivstil

>[!IMPORTANT]
>
>Läs [Skrivvägledning för Adobe-dokumentation](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html) innan du börjar skapa måldokumentationssidan.

* Håll dina meningar korta och kom till saken snabbt. Om din mening är längre än 20 ord eller använder flera kommatecken kan du dela upp den i olika meningar. Meningar som är längre än 20 ord kan vara särskilt komplicerade för läsarna.
* Var inte överdrivet artig. Undvik att använda&quot;snälla&quot; eller&quot;snälla&quot; ...&quot; i den tekniska dokumentationen.

## Länkning {#linking}

Följ den angivna dokumentationsmallen och redigera inte de befintliga länkarna i mallen. När du inkluderar nya länkar kan du läsa [med hjälp av länkar i dokumentation](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html) i handboken för deltagare.

## Riktlinjer för varumärken {#branding}

* AEP är inte en godkänd offentlig term. Använd Adobe Experience Platform först, sedan Experience Platform och sedan Platform.
   * **Använd inte**: Innan du kan exportera data från AEP till YourDestination bör du kontrollera att du läser och slutför dessa krav.
   * **Använd**: Innan du kan exportera data från Adobe Experience Platform till din destination måste du läsa och slutföra dessa krav.

## Bilder och skärmbilder {#images-and-screenshots}

* Mer information om [hur du länkar till bilder](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html#images) finns i handboken för medverkande.
* När du använder skärmbilder måste du se till att skärmbilden fångar upp hela användargränssnittsskärmen för plattformen.
* När du markerar bilder för att markera en viss kontroll eller etikett på sidan, ska du följa den markeringsstil som används av dokumentationsteamet på Experience Platform. Observera hur Profilbaserad markeras i [den här skärmbilden](/help/destinations/catalog/cloud-storage/amazon-s3.md#export-type-frequency).
* Använd `png`-formatbilder.
* Använd inte numrerade skärmbilder som filnamn. Bildfilnamn ska vara beskrivande.
   * **Använd inte**: `1.png`, `2.png`, `3.png`
   * **Använd**: `yourdestination-authentication-details.png`, `yourdestination-destination-details.png`
* Använd alternativ text för alla bilder som du lägger till i dokumentationen och använd rätt grammatik i alternativ text.
   * **Använd inte**: Information om målanslutning
   * **Använd**: Bild av plattformsgränssnittet, med information om målanslutning ifylld.

## Process {#process}

* [dokumentationsmallen](./self-service-template.md) uppdateras sällan, baserat på feedback från partner. Innan du börjar skapa dokumentation för ditt mål måste du kontrollera att du har hämtat den [senaste versionen av mallen](../assets/docs-framework/yourdestination-template.zip).
* Skriv dokumentationen och skapa en begäran om hämtning av dokumentation (PR) från en gren i din förgrening *förutom huvudgrenen*. Gå till Skicka-målet för granskning när du redigerar i [GitHub-gränssnittet](./use-github-interface-to-create-documentation.md#submit-review) eller i [din lokala miljö](./work-in-local-environment.md#submit-review).
