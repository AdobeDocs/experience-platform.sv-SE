---
title: Tilläggskonfiguration
description: Lär dig hur du konfigurerar ett taggtillägg för att samla in globala inställningar från en användare i användargränssnittet för Adobe Experience Platform eller användargränssnittet för datainsamling.
exl-id: 2bf33617-1398-499f-8325-3849dbdb1f97
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# Tilläggskonfiguration

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

Tilläggskonfiguration är det sätt som ett tillägg samlar in globala inställningar från en användare. Ta till exempel ett tillägg som gör att användaren kan skicka en fyr med en Skicka fyr-åtgärd, och fyren måste alltid innehålla ett konto-ID. Vi vill inte besvära användare genom att fråga dem om konto-ID varje gång de konfigurerar en Skicka Beacon-åtgärd. Tillägget ska i stället be om konto-ID en gång från tilläggskonfigurationsvyn. Varje gång en beacon ska skickas kan åtgärdsbiblioteksmodulen Skicka beacon hämta konto-ID:t från tilläggskonfigurationen och lägga till det i beacon.

När användare installerar ett tillägg till en taggegenskap i Adobe Experience Platform visas tilläggskonfigurationsvyn som tillägget tillhandahåller. De kan inte slutföra installationen av tillägget utan att slutföra tilläggskonfigurationen. Visa dokumentet på [vyer](./web/views.md) om du vill lära dig hur du skapar en vy för tilläggskonfiguration.

När inställningarna har sparats från en tilläggskonfigurationsvy skickas de från taggens körtidsbibliotek. Sedan kan du få åtkomst till inställningarna från tilläggsbiblioteksmodulerna genom att ringa [`turbine.getExtensionSettings()`](./turbine.md#get-extension-settings).

Tilläggskonfigurationen är en valfri funktion som du kan välja att inte använda.
