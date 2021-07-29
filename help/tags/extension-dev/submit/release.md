---
title: Frigöra ett tillägg
description: Lär dig hur du frigör ett taggtillägg privat eller offentligt i Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# Släpp ett tillägg

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad referens till terminologiska ändringar.

När testningen och dokumentationen är klara är tillägget klart för release. Det finns för närvarande två typer av releaser som du kan utföra:

- **Privat release**: Det färdiga tillägget är tillgängligt för alla fastigheter på ditt företag, men inte för några andra företag i Adobe Experience Platform.
- **Offentlig version**: Det färdiga tillägget är tillgängligt på den offentliga marknaden för alla Adobe Experience Platform-användare.

>[!NOTE]
>
>När du har släppt tillägget kan du inte längre ändra det och du kan inte ta bort det.  När de släppts utförs felkorrigeringar och funktionstillägg genom att `POST`en ny version av tilläggspaketet följer ovanstående test- och releasesteg för den nya versionen.

Du måste frigöra tillägget som ett privat tillägg innan du kan frigöra det offentligt.

## Privat release

Det enklaste sättet att frigöra tillägget med privat tillgänglighet är att använda [taggtilläggsreleaser](https://www.npmjs.com/package/@adobe/reactor-releaser). Fler instruktioner finns i dokumentationen.

Om du vill frigöra tillägget med privat tillgänglighet via API:t direkt kan du läsa exempelanropet för [privat släppande ett tilläggspaket](https://developer.adobelaunch.com/api/reference/1.0/extension_packages/release_private/) i API-dokumenten för mer information.

## Offentlig release

När du har slutfört den privata versionen kan du be Adobe att publicera den offentligt.  Tillägget blir då tillgängligt i den offentliga katalogen. Alla användare av datainsamlingen kan installera tillägget på vilken egenskap som helst.

Fyll i [formuläret för begäran om offentlig release](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=7DRB5U) för att starta versionsprocessen.
