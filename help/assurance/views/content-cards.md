---
title: Vyn Innehållskort
description: Den här vägledningen innehåller information om vyn Innehållskort i Adobe Experience Platform Assurance.
source-git-commit: fa5dbbfcc0c178c8886000479f44afd5d63c8c34
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 0%

---

# Vyn Innehållskort i Assurance

Vyn Meddelanden i appen i Adobe Experience Platform Assurance gör det möjligt att validera din app, övervaka de innehållskort som levereras till din enhet och förhandsgranska kort.

## Innehållskort

Överst på fliken **[!UICONTROL Content Cards]** finns en **[!UICONTROL Content Card]**-listruta. Här listas alla innehållskort som har tagits emot i Assurance-sessionen. Om ett kort inte finns med i den här listan betyder det att appen aldrig har fått det.

![Listrutan Innehållskort som innehåller en lista med kort](./images/content-cards/dropdown.png)

Om du väljer ett innehållskort visas mycket information om kortet enligt beskrivningen i avsnitten nedan.

### Kortförhandsvisning

I den högra panelen visas en ruta på **[!UICONTROL Card Preview]** som visar hur ett kort återges i vanliga mallar - liten bild, stor bild och endast bild.

![Förhandsgranska det markerade innehållskortet](./images/content-cards/preview.png)

Använd växlingsknappen **[!UICONTROL Theme]** för att visa kortet i ljust eller mörkt läge.

![Förhandsgranska valt innehållskort med mörkt tema](./images/content-cards/preview-dark.png)

### Tillgängliga flikar

I det vänstra avsnittet beror de tillgängliga flikarna på det valda kortet. Om kortet innehåller regler visas tre flikar: **[!UICONTROL Info]**, **[!UICONTROL Interactions]** och **[!UICONTROL Analyze Rules]**.

![Tillgängliga flikar när det finns regler: Info, Interaktioner, Analysera regler ](./images/content-cards/tabs-with-rules.png)

Om kortet inte innehåller regler visas två flikar: **[!UICONTROL Info]** och **[!UICONTROL Interactions]**.

![Tillgängliga flikar när inga regler finns: Information och interaktioner](./images/content-cards/tabs-no-rules.png)

### Fliken Info

Fliken **[!UICONTROL Info]** visar **[!UICONTROL Card Properties]**-avsnittet högst upp, inklusive emblem för **[!UICONTROL Current State]** (utlösare, visning, stängning, diskvalificering) plus metainformation som **[!UICONTROL Template]** (Liten bild, Stor bild eller Endast bild), **[!UICONTROL Surface]** och anpassade nyckelvärdepar.

![Kortegenskaper som visar aktuella statusemblem, mall, yta och nyckelvärdepar](./images/content-cards/card-properties.png)

Under det avsnittet **[!UICONTROL Campaign Properties]** visas information som lästs in från Adobe Journey Optimizer (AJO).

Du kan också välja **[!UICONTROL View Campaign]** för att öppna kortet i AJO för kontroll eller redigering.

![Avsnittet Kampanjegenskaper med knappen Visa kampanj](./images/content-cards/campaign-properties.png)

### Fliken Interaktioner

Fliken **[!UICONTROL Interactions]** sammanfattar varje korts livscykel som en sekvens av emblem: den börjar alltid med **[!UICONTROL trigger]**, följt av resultatet som reglerna skapade -**[!UICONTROL display]**, **[!UICONTROL dismiss]** eller **[!UICONTROL disqualify]**.

![Interaktionstabell som visar livscykelmärken från utlösare till visning, stängning eller diskvalificering](./images/content-cards/interactions-tab.png)

### Fliken Analysera regler

Fliken **[!UICONTROL Analyze]** visar en händelsetabell med upp till tre regelkolumner - **[!UICONTROL Display]**, **[!UICONTROL Dismiss]** och **[!UICONTROL Disqualify]** - baserat på kortets regler. Om kortet bara definierar en regel, visas bara den kolumnen.

Varje rad representerar en sessionshändelse och varje kolumn anger om kortets regel matchar villkoren för den händelsen. Ett poängvärde på 0 % betyder att inga villkor matchar. 100 % är en fullständig matchning (regeln startar).

Om händelsen matchar ett villkor visas en grön bockmarkering. Om händelsen inte matchar visas en röd ikon.

![Analysera flikhändelsetabell med kolumnerna Visa, Stäng och Disvalidera regel ](./images/content-cards/rules-tab.png)

Använd skjutreglaget **[!UICONTROL Match Threshold]** för att filtrera händelser efter lägsta matchningsprocent.

![Matcha tröskelvärde för att filtrera händelser efter minsta matchningsprocent](./images/content-cards/match-threshold.png)

När du väljer en händelse öppnas en informationspanel till höger med ett dragspel som listar de tre reglerna: **[!UICONTROL Display]**, **[!UICONTROL Dismiss]** och **[!UICONTROL Disqualify]**.

![Panelen Händelseinformation med en lista över regler för att visa, avvisa och diskvalificera ](./images/content-cards/rules-panel.png)

Expandera valfritt avsnitt för att se regelns villkor, vilka villkor som matchar, och den beräknade matchningsprocenten för det resultatet.

![Utökat regeldragspel som visar matchade villkor och matchande procent](./images/content-cards/expanded-accordion.png)

## Fliken Förfrågningar

Fliken **[!UICONTROL Requests]** visar vilka innehållskort som begärdes och på vilken yta.

Fliken ![Förfrågningar som visar innehållskortbegäranden](./images/content-cards/requests-tab.png)

Använd knappen **[!UICONTROL View Card]** för att gå tillbaka till informationsfliken för ett visst innehållskort.

## Fliken Händelselista

Fliken **[!UICONTROL Event List]** visar sessionshändelser som är relevanta för innehållskort, inklusive AJO förslagsbegäranden/svar, kortets livscykelhändelser och interaktionsspårning. Du kan söka efter, filtrera, sortera och anpassa kolumner samt exportera resultat.

Om du väljer en händelse öppnas en informationspanel på höger sida med oformaterad nyttolast och nyckelattribut. Du kan också flagga händelser för uppföljning. Den här vyn är användbar för korrelerande förfrågningar, regelresultat och interaktioner under hela sessionen.

![Fliken Händelselista med sökbara, filterbara sessionshändelser för innehållskort](./images/content-cards/event-list.png)

## Fliken Validering

Fliken **[!UICONTROL Validation]** kör valideringar mot din aktuella session och kontrollerar om appen har konfigurerats för meddelanden korrekt:

![Kontrollerar konfigurationen för meddelanden för den aktuella sessionen på fliken Validering](./images/content-cards/validation.png)
