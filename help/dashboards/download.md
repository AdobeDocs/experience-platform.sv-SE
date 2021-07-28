---
solution: Experience Platform
title: Hämta Experience Platform Dashboards till PDF
type: Documentation
description: Spara kopior av kontrollpanelsvisualiseringar med funktionen för att ladda ned till PDF som finns i användargränssnittet i Experience Platform.
source-git-commit: a95f77d048b5bb9562507122d249f592e68a1bcf
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# Hämta instrumentpaneler till PDF

Instrumentpaneler i Adobe Experience Platform kan laddas ned till PDF från användargränssnittet för att underlätta informationsutbytet med medlemmar i organisationen.

Det här dokumentet innehåller en sammanfattning av hur du hämtar instrumentpaneler med hjälp av plattformsgränssnittet och sparar instrumentpanelen i PDF-format med webbläsarens standardutskriftsmeny.

>[!WARNING]
>
>Informationen som finns på kontrollpanelerna kan innehålla personligt identifierbar information (PII) om dina kunder eller känsliga data relaterade till din organisation. Alla dashboard-data som sparas i PDF-filen ska hanteras på rätt sätt enligt organisationens riktlinjer för datasekretess.

## Hämta instrumentpanel

Börja hämta en kontrollpanel genom att navigera till den kontrollpanel som du vill hämta (till exempel kontrollpanelen [!UICONTROL Profiles]) och sedan välja menyn med fler alternativ (**`...`**) längst upp till höger på kontrollpanelen. Välj sedan **[!UICONTROL Download]**.

![](images/download/download-button.png)

## Förhandsgranska PDF

När du har valt **[!UICONTROL Download]** öppnas standardutskriftsmenyn för webbläsaren. I det här exemplet visas utskriftsmenyn för Google Chrome.

På menyn Skriv ut kan du förhandsgranska den PDF-fil som ska sparas. PDF-filen är en riktig representation av instrumentpanelswidgetarna så som de visas i plattformsgränssnittet, och storleken på PDF-filen justeras automatiskt så att alla de instrumentpanelswidgetar som är synliga för tillfället visas på en enda sida.

![](images/download/download-chrome-print.png)

PDF-filen innehåller ett automatiskt genererat huvud som innehåller Experience Platform-logotypen, namnet på kontrollpanelen, ditt namn samt datum och tid då kontrollpanelen hämtades. Den här informationen är skrivskyddad och kan inte redigeras i PDF-filen.

![](images/download/download-pdf.png)

## Spara som PDF

När du har förhandsgranskat PDF-filen väljer du **Spara** och väljer sedan den plats där du vill spara PDF-filen.

>[!NOTE]
>
>Om det behövs kan du använda listrutan **Mål** för att välja **Spara som PDF** om det alternativet inte väljs automatiskt.

![](images/download/download-chrome-print-destination.png)

## Anpassa PDF-filer på kontrollpanelen

PDF-filen som skapas matchar den kontrollpanel som du kan se i användargränssnittet och innehåller bara de widgetar som är synliga på din instrumentpanel. Vissa instrumentpaneler kan anpassas för att ändra storlek och plats för widgetar eller för att lägga till och ta bort widgetar från vyn. Om du anpassar utseendet på kontrollpanelen i användargränssnittet för plattformen ändras även utseendet på PDF-filen som genereras.

Du kan till exempel ändra utseendet på din profilkontrollpanel så att den innehåller flera widgetar med full bredd som är staplade över tre standardwidgetar.

![](images/download/download-modify.png)

Om du väljer att hämta den uppdaterade kontrollpanelen får du en ny PDF-förhandsgranskning som matchar utseendet på den anpassade profilkontrollpanelen. Det justerar också automatiskt storleken på PDF-filen för att säkerställa att alla synliga widgetar inkluderas i en PDF-fil på en sida.

![](images/download/download-chrome-print-modified.png)

Om du vill veta mer om hur du anpassar kontrollpaneler börjar du med att läsa [översikten över anpassning av kontrollpanelen](customize/overview.md).

## Nästa steg

Nu när du har laddat ned kontrollpanelen och sparat den som en PDF-fil kan du upprepa de här stegen för att ladda ned fler kontrollpaneler eller dela PDF-filen med medlemmar i organisationen.