---
title: Tilläggskonfiguration
description: Lär dig hur du konfigurerar ett taggtillägg för att samla in globala inställningar från en användare i användargränssnittet för datainsamling i Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# Tilläggskonfiguration

>[!NOTE]
>
>Adobe Experience Platform Launch omdöms till en serie datainsamlingstekniker i Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../term-updates.md) för en konsoliderad referens till terminologiska ändringar.

Tilläggskonfiguration är det sätt som ett tillägg samlar in globala inställningar från en användare. Ta till exempel ett tillägg som gör att användaren kan skicka en fyr med en Skicka fyr-åtgärd, och fyren måste alltid innehålla ett konto-ID. Vi vill inte besvära användare genom att fråga dem om konto-ID varje gång de konfigurerar en Skicka Beacon-åtgärd. Tillägget ska i stället be om konto-ID en gång från tilläggskonfigurationsvyn. Varje gång en beacon ska skickas kan åtgärdsbiblioteksmodulen Skicka beacon hämta konto-ID:t från tilläggskonfigurationen och lägga till det i beacon.

När användare installerar ett tillägg till en taggegenskap i Adobe Experience Platform visas tilläggskonfigurationsvyn som tillägget tillhandahåller. De kan inte slutföra installationen av tillägget utan att slutföra tilläggskonfigurationen. Läs dokumentet på [vyer](./web/views.md) om du vill veta mer om hur du skapar en vy för tilläggskonfiguration.

När inställningarna har sparats från en tilläggskonfigurationsvy skickas de från taggens körtidsbibliotek. Du kan sedan komma åt dessa inställningar från tilläggsbiblioteksmodulerna genom att ringa [`turbine.getExtensionSettings()`](./turbine.md#get-extension-settings).

Tilläggskonfigurationen är en valfri funktion som du kan välja att inte använda.
