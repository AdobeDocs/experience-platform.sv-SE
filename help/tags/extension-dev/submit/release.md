---
title: Frigöra ett tillägg
description: Lär dig hur du frigör ett taggtillägg privat eller offentligt i Adobe Experience Platform.
exl-id: a5eb6902-4b0f-4717-a431-a290c50fb5a6
source-git-commit: 8862a911f09d47c3a2260faba045f3c79826b52c
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# Släpp ett tillägg

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

När testningen och dokumentationen är klara är tillägget klart för release. Det finns för närvarande två typer av releaser som du kan utföra:

- **Privat release**: Det färdiga tillägget är tillgängligt för alla fastigheter på ditt företag, men inte för några andra företag i Adobe Experience Platform.
- **Offentlig release**: Det färdiga tillägget är tillgängligt på den offentliga marknaden för alla Adobe Experience Platform-användare.

>[!NOTE]
>
>När du har släppt tillägget kan du inte längre ändra det och du kan inte ta bort det.  När de släppts utförs felkorrigeringar och funktionstillägg av `POST`som en ny version av tilläggspaketet och följer ovanstående test- och releasesteg för den nya versionen.

Du måste frigöra tillägget som ett privat tillägg innan du kan frigöra det offentligt.

## Privat release

Det enklaste sättet att släppa tillägget med privat tillgänglighet är att använda [frisläppa taggtillägg](https://www.npmjs.com/package/@adobe/reactor-releaser). Fler instruktioner finns i dokumentationen.

Om du vill frigöra tillägget med privat tillgänglighet via API:t direkt, se exempelanropet för [frigöra ett tilläggspaket privat](https://developer.adobelaunch.com/api/reference/1.0/extension_packages/release_private/) i API-dokumenten för mer information.

## Offentlig release

När du har slutfört den privata versionen kan du be Adobe att publicera den offentligt.  Tillägget blir då tillgängligt i den offentliga katalogen. Alla användare av datainsamlingen kan installera tillägget på vilken egenskap som helst.

Fyll i [blankett för begäran om offentliggörande](https://experiencecloudpanel.adobe.com/c/r/DCExtensionReleaseRequest) för att starta releaseprocessen.
