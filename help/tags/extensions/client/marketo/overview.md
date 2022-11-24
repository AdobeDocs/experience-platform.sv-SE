---
title: Marketo Munchkin Extension - översikt
description: Läs om taggtillägget Marketo Munchkin i Adobe Experience Platform.
exl-id: 8efc5203-91fc-4e89-be8f-74bf1aeeee5f
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Marketo Munchkin-tillägg - översikt

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

Använd det här tillägget för att integrera [!DNL Marketo Munchkin] JavaScript-spårningskod med din egenskap. [!DNL Marketo Munchkin] JavaScript gör det möjligt att följa upp besök på slutanvändarens sidor och navigerar till Marketo landningssidor och externa webbsidor.

## Installera Marketo Munchkin-tillägg

If [!DNL Marketo Munchkin] tillägget är inte installerat ännu, öppna egenskapen och välj **[!UICONTROL Extensions > Catalog]**, hovra över [!DNL Marketo Munchkin] och markera **[!UICONTROL Install]**.

Tillägget har ingen nödvändig konfiguration.

## Åtgärdstyper för Marketo Munchkin-tillägg

I det här avsnittet beskrivs de tillgängliga åtgärdstyperna i [!DNL Marketo Munchkin] tillägg.

### Initiera

![](../../../images/munchkin-Init.png)

**Munchkin-ID: (obligatoriskt)** Munchkins konto-ID finns under Admin > Integration > Munchkin-menyn.

**Konfigurationer:** Alla konfigurerbara parametrar dokumenteras [här](https://developers.marketo.com/javascript-api/lead-tracking/configuration/)

### Besök webbsidan

![](../../../images/munchkin-visit-page.png)

**url: (obligatoriskt)** Den URL-filsökväg som används för att registrera ett sidbesök.

**parametrar:** En frågesträng med de parametrar som ska registreras.

**namn:** Det anpassade namnet på webbsidesresursen.

### Klicka på länken

![](../../../images/munchkin-click-link.png)

**href: (obligatoriskt)** Den URL-filsökväg som används för att spela in ett länkval.
