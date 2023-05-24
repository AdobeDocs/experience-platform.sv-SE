---
title: Stöd för sluttaggar i Internet Explorer 10 och 11
description: Adobe Experience Platform tillhandahåller inte längre uppdateringsstöd för taggar i Internet Explorer 10 och 11.
exl-id: 35491c80-2a8a-4e07-baa7-a5db373b6852
source-git-commit: 44e056407f5089c927752f00cc6bf173d7640b83
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# Stöd för sluttaggar i Internet Explorer 10 och 11

I takt med att det digitala upplevelselandskapet utvecklas fortsätter Adobe inte längre att investera resurser för att stödja taggar i Adobe Experience Platform för Internet Explorer 10 (IE10) och Internet Explorer 11 (IE11). Även om Adobe inte aktivt tar bort stöd för IE10 och IE11, kommer effekten av dessa webbläsare på nya funktioner inte längre att beaktas i framtida uppdateringar.

## Varför stöds inte IE10 och IE11 längre?

Det finns fyra orsaker till varför taggar inte längre stöder IE10 och IE11:

* **Microsoft upphör med stödet för IE10 och IE11**: Från och med januari 2020 [Microsoft slutade stödja IE10](https://docs.microsoft.com/en-us/lifecycle/announcements/internet-explorer-10-end-of-support) för säkerhetsuppdateringar och icke-säkerhetsuppdateringar. Från och med juni 2022 [Microsoft slutade stödja IE11](https://docs.microsoft.com/en-us/lifecycle/announcements/internet-explorer-11-end-of-support) i vissa versioner av Windows.
* **Bredare branscher upphör med stödet för IE10 och IE11**: I takt med att den bredare branschen minskar stödet för IE10 och IE11 blir förmågan att använda taggar för att bibehålla bakåtkompatibiliteten med dessa tekniker allt svårare.
* **Modern teknik stöder inte IE10 och IE11**: För att taggar ska ha fortsatt stöd för den senaste tekniken måste stödet för IE10 och IE11 ha upphört, eftersom dessa moderna tekniker inte är kompatibla med dessa webbläsare.
* **Stöd för IE10 och IE11 gör att den övergripande funktionsutvecklingen går långsammare**: Många nya funktioner som släpps för taggar kräver noggrann övervakning av IE10 och IE11. Detta resulterar i timtals ytterligare arbetsmoment för att skaffa svårsökbara testverktyg som fungerar med IE10 och IE11, lägga till ytterligare kod för att få funktioner att fungera med IE10 och IE11 som inte har inbyggt stöd, samt för att kontrollera att funktionen fungerar som förväntat. Genom att stoppa stödet för IE10 och IE11 kan Adobe leverera nya funktioner snabbare.

## Effekter av borttagning av IE10 och IE11

När stödet är inaktuellt utförs följande effekter:

* Nya funktioner kanske inte stöder IE10 och IE11.
* Testningen av det aktuella och nya funktionsstödet med IE10 och IE11 upphör.
* Funktioner som tidigare hade stöd för IE10 och IE11 kanske inte längre har stöd för dessa webbläsare.
