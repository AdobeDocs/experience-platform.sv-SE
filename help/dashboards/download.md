---
solution: Experience Platform
title: Ladda ned Experience Platform Dashboards till PDF
type: Documentation
description: Spara kopior av kontrollpanelsvisualiseringar med funktionen för nedladdning till PDF som finns i Experience Platform användargränssnitt.
exl-id: 838e98a0-ce2e-4dcd-8c8f-d28ef2cb8315
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 0%

---

# Hämta paneler till PDF

Instrumentpaneler i Adobe Experience Platform kan laddas ned till PDF från Experience Platform användargränssnitt för att underlätta informationsutbytet med medlemmar i organisationen.

Det här dokumentet innehåller en sammanfattning av hur du hämtar kontrollpaneler med Experience Platform-gränssnittet och sparar kontrollpanelen i PDF med standardutskriftsmenyn i webbläsaren.

>[!WARNING]
>
>Informationen som finns på kontrollpanelerna kan innehålla personligt identifierbar information (PII) om dina kunder eller känsliga data relaterade till din organisation. Alla dashboard-data som sparas till PDF ska hanteras på rätt sätt i enlighet med organisationens riktlinjer för datasekretess.

## Hämta instrumentpanel

Om du vill börja hämta en instrumentpanel går du till den instrumentpanel som du vill hämta (till exempel kontrollpanelen [!UICONTROL Profiles]) och väljer menyn med fler alternativ (**`...`**) i det övre högra hörnet av instrumentpanelen. Välj sedan **[!UICONTROL Download]**.

![Kontrollpanelen Experience Platform Profiles med ellipsen och listrutan Download (Hämta) markerad.](images/download/download-button.png)

## Förhandsgranska PDF

När du har valt **[!UICONTROL Download]** öppnas standardutskriftsmenyn för webbläsaren. I det här exemplet visas utskriftsmenyn i Google Chrome.

På utskriftsmenyn kan du förhandsgranska den PDF som ska sparas. PDF är en riktig representation av instrumentpanelswidgetarna så som de visas i Experience Platform-gränssnittet och storleken på PDF justeras automatiskt så att alla de instrumentpanelswidgetar som är synliga för tillfället visas på en enda sida.

![Profilöversikten visas på ett enda sidformat med panelen Utskriftsalternativ till höger.](images/download/download-chrome-print.png)

PDF innehåller ett automatiskt genererat huvud som innehåller Experience Platform-logotypen, namnet på kontrollpanelen, ditt namn samt datum och tid då kontrollpanelen hämtades. Informationen är skrivskyddad och kan inte redigeras i PDF.

![En närbild av förhandsvisningen med det automatiskt genererade huvudet markerat.](images/download/download-pdf.png)

## Spara som PDF

När du har förhandsgranskat PDF väljer du **Spara** för att välja den plats där du vill spara din PDF.

>[!NOTE]
>
>Om det behövs kan du använda listrutan **Mål** och välja **Spara som PDF** om det alternativet inte väljs automatiskt.

![Profilöversikten visas i ett ensidigt format med utskriftsalternativet Spara som PDF markerat i listrutan Mål.](images/download/download-chrome-print-destination.png)

## Anpassa PDF-filer på kontrollpanelen

Det genererade PDF-programmet matchar den kontrollpanel som du kan se i användargränssnittet och innehåller bara de widgetar som för närvarande visas på din instrumentpanel. Vissa instrumentpaneler kan anpassas för att ändra storlek och plats för widgetar eller för att lägga till och ta bort widgetar från vyn. När du anpassar utseendet på kontrollpanelen i Experience Platform-gränssnittet ändras även utseendet på den PDF som genereras.

Du kan till exempel ändra utseendet på din profilkontrollpanel så att den innehåller flera widgetar med full bredd som är staplade över tre standardwidgetar.

![Profilinstrumentpanelen som visar utdragen widget.](images/download/download-modify.png)

Om du väljer att hämta den uppdaterade kontrollpanelen får du en ny PDF-förhandsvisning som matchar utseendet på den anpassade profilkontrollpanelen. Den justerar också automatiskt storleken på PDF så att alla synliga widgetar inkluderas i en PDF på en sida.

![Profilöversikten visas på ett enda sidformat med panelen Utskriftsalternativ till höger.](images/download/download-chrome-print-modified.png)

Om du vill veta mer om hur du anpassar kontrollpaneler börjar du med att läsa [översikten över anpassning av kontrollpanelen](customize/overview.md).

## Nästa steg

Nu när du har hämtat din kontrollpanel och sparat den som en PDF kan du upprepa de här stegen för att hämta ytterligare kontrollpaneler eller dela PDF med medlemmar i organisationen.
