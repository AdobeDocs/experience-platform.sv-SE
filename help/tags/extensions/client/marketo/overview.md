---
title: Marketo Munchkin Extension - översikt
description: Läs om taggtillägget Marketo Munchkin i Adobe Experience Platform.
exl-id: 8efc5203-91fc-4e89-be8f-74bf1aeeee5f
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---

# Översikt över tillägget Marketo Munchkin

Använd det här tillägget om du vill integrera JavaScript-spårningskoden [!DNL Marketo Munchkin] med din egenskap. [!DNL Marketo Munchkin] JavaScript gör det möjligt att spåra besök på slutanvändarsidor och navigerar till Marketo landningssidor och externa webbsidor.

## Installera Marketo Munchkin-tillägg

Om tillägget [!DNL Marketo Munchkin] inte har installerats än öppnar du egenskapen, väljer **[!UICONTROL Extensions > Catalog]**, håller pekaren över tillägget [!DNL Marketo Munchkin] och väljer **[!UICONTROL Install]**.

Tillägget har ingen nödvändig konfiguration.

## Åtgärdstyper för Marketo Munchkin-tillägg

I det här avsnittet beskrivs de åtgärdstyper som är tillgängliga i tillägget [!DNL Marketo Munchkin].

### Initiera

![](../../../images/munchkin-Init.png)

**Munchkin-id: (obligatoriskt)** Munchkin konto-ID hittades under Admin > Integration > Munchkin-menyn.

**Konfigurationer:** Alla konfigurerbara parametrar beskrivs [här](https://developers.marketo.com/javascript-api/lead-tracking/configuration/)

### Besök webbsidan

![](../../../images/munchkin-visit-page.png)

**url: (obligatoriskt)** URL-filsökvägen som används för att registrera ett sidbesök.

**parametrar:** En frågesträng med de parametrar som ska registreras.

**namn:** Det anpassade namnet på webbsidesresursen.

### Klicka på länken

![](../../../images/munchkin-click-link.png)

**href: (obligatoriskt)** Den URL-filsökväg som används för att spela in ett länkval.
