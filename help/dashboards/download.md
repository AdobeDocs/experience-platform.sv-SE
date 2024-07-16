---
solution: Experience Platform
title: Hämta instrumentpaneler för Experience Platform till PDF
type: Documentation
description: Spara kopior av kontrollpanelsvisualiseringar med funktionen för nedladdning till PDF som finns i användargränssnittet för Experience Platform.
exl-id: 838e98a0-ce2e-4dcd-8c8f-d28ef2cb8315
source-git-commit: 5d9428c4323e65c2605fd116160e160af7d9086d
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# Hämta instrumentpaneler till PDF

Kontrollpaneler i Adobe Experience Platform kan laddas ned till PDF från användargränssnittet för att underlätta informationsutbytet med medlemmar i organisationen.

Det här dokumentet innehåller en sammanfattning av hur du hämtar instrumentpaneler med hjälp av plattformsgränssnittet och sparar instrumentpanelen i PDF med webbläsarens standardutskriftsmeny.

>[!WARNING]
>
>Informationen som finns på kontrollpanelerna kan innehålla personligt identifierbar information (PII) om dina kunder eller känsliga data relaterade till din organisation. Instrumentpanelsdata som sparats på PDF ska hanteras på rätt sätt i enlighet med organisationens riktlinjer för datasekretess.

## Hämta instrumentpanel

Om du vill börja hämta en instrumentpanel går du till den instrumentpanel som du vill hämta (till exempel kontrollpanelen [!UICONTROL Profiles]) och väljer menyn med fler alternativ (**`...`**) i det övre högra hörnet av instrumentpanelen. Välj sedan **[!UICONTROL Download]**.

![Kontrollpanelen Experience Platform Profiles med ellipsen och listrutan Download (Hämta) markerad.](images/download/download-button.png)

## Förhandsgranska PDF

När du har valt **[!UICONTROL Download]** öppnas standardutskriftsmenyn för webbläsaren. I det här exemplet visas utskriftsmenyn i Google Chrome.

På utskriftsmenyn kan du förhandsgranska PDF som ska sparas. PDF är en sann representation av instrumentpanelswidgetarna så som de visas i plattformsgränssnittet och storleken på PDF justeras automatiskt så att alla instrumentpanelswidgetar som visas för tillfället visas på en enda sida visas.

![Profilöversikten visas på ett enda sidformat med panelen Utskriftsalternativ till höger.](images/download/download-chrome-print.png)

PDF innehåller ett automatiskt genererat huvud som innehåller Experience Platform-logotypen, namnet på kontrollpanelen, ditt namn samt datum och tid då kontrollpanelen hämtades. Informationen är skrivskyddad och kan inte redigeras i PDF.

![En närbild av förhandsvisningen med det automatiskt genererade huvudet markerat.](images/download/download-pdf.png)

## Spara som PDF

När du har förhandsgranskat PDF väljer du **Spara** för att välja den plats där du vill spara PDF.

>[!NOTE]
>
>Om det behövs kan du använda listrutan **Mål** och välja **Spara som PDF** om det alternativet inte väljs automatiskt.

![Profilöversikten visas i ett ensidigt format med utskriftsalternativet Spara som PDF i listrutan Mål markerat.](images/download/download-chrome-print-destination.png)

## Anpassa PDF för kontrollpanel

PDF som genereras matchar den instrumentpanel som du kan se i användargränssnittet och innehåller bara de widgetar som för närvarande visas på din instrumentpanel. Vissa instrumentpaneler kan anpassas för att ändra storlek och plats för widgetar eller för att lägga till och ta bort widgetar från vyn. När du anpassar utseendet på kontrollpanelen i användargränssnittet för plattformen ändras även utseendet på PDF som genereras.

Du kan till exempel ändra utseendet på din profilkontrollpanel så att den innehåller flera widgetar med full bredd som är staplade över tre standardwidgetar.

![Profilinstrumentpanelen som visar utdragen widget.](images/download/download-modify.png)

Om du väljer att hämta den uppdaterade kontrollpanelen får du en ny förhandsvisning i PDF som matchar utseendet på den anpassade profilkontrollpanelen. Det justerar också automatiskt storleken på PDF för att säkerställa att alla synliga widgetar inkluderas i en enkelsidig PDF.

![Profilöversikten visas på ett enda sidformat med panelen Utskriftsalternativ till höger.](images/download/download-chrome-print-modified.png)

Om du vill veta mer om hur du anpassar kontrollpaneler börjar du med att läsa [översikten över anpassning av kontrollpanelen](customize/overview.md).

## Nästa steg

Nu när du har hämtat din kontrollpanel och sparat den som PDF kan du upprepa de här stegen för att hämta ytterligare kontrollpaneler eller dela PDF med medlemmar i organisationen.
