---
title: Frigöra ett tillägg
description: Lär dig hur du frigör ett taggtillägg privat eller offentligt i Adobe Experience Platform.
exl-id: a5eb6902-4b0f-4717-a431-a290c50fb5a6
source-git-commit: 60d88be5d710314cdc6900f4b63643c740b91fa6
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# Frigöra ett tillägg

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. I följande [dokument](../../term-updates.md) finns en konsoliderad referens till de ändrade terminologin.

När testningen och dokumentationen är klara är tillägget klart för release. Det finns för närvarande två typer av releaser som du kan utföra:

- **Privat release**: Det slutförda tillägget är tillgängligt för alla egenskaper i ditt företag, men inte för några andra företag i Adobe Experience Platform.
- **Offentlig version**: Det slutförda tillägget är tillgängligt på den offentliga marknadsplatsen för alla Adobe Experience Platform-användare.

>[!NOTE]
>
>När du har släppt tillägget kan du inte längre ändra det och du kan inte ta bort det.  När de släppts utförs felkorrigeringar och funktionstillägg genom att `POST`en ny version av tilläggspaketet skapas och ovanstående test- och releasesteg för den nya versionen följs.

Du måste frigöra tillägget som ett privat tillägg innan du kan frigöra det offentligt.

## Privat release

Det enklaste sättet att frigöra tillägget med privat tillgänglighet är att använda [taggtilläggsreleasen](https://www.npmjs.com/package/@adobe/reactor-releaser). Fler instruktioner finns i dokumentationen.

Om du vill frigöra tillägget med privat tillgänglighet med API:t direkt kan du läsa exempelanropet för [privat släppning av ett tilläggspaket](../../api/endpoints/extension-packages.md/#private-release) i API-dokumenten för mer information.

## Offentlig release

När du har slutfört den privata releasen kan du be Adobe att publicera den offentligt.  Tillägget blir då tillgängligt i den offentliga katalogen. Alla användare av datainsamlingen kan installera tillägget på alla egenskaper.

Fyll i det [offentliga begärandeformuläret ](https://www.feedbackprogram.adobe.com/c/r/DCExtensionReleaseRequest) för att starta versionsprocessen.
