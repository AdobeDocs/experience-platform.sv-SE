---
title: Frigöra ett tillägg
description: Lär dig hur du frigör ett taggtillägg privat eller offentligt i Adobe Experience Platform.
exl-id: a5eb6902-4b0f-4717-a431-a290c50fb5a6
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---

# Frigöra ett tillägg

När testningen och dokumentationen är klara är tillägget klart för release. Det finns för närvarande två typer av releaser som du kan utföra:

- **Privat release**: Det slutförda tillägget är tillgängligt för alla egenskaper i ditt företag, men inte för några andra företag i Adobe Experience Platform.
- **Offentlig version**: Det slutförda tillägget är tillgängligt på den offentliga marknadsplatsen för alla Adobe Experience Platform-användare.

>[!NOTE]
>
>När du har släppt tillägget kan du inte längre ändra det och du kan inte ta bort det.  När de släppts utförs felkorrigeringar och funktionstillägg genom att `POST`en ny version av tilläggspaketet skapas och ovanstående test- och releasesteg för den nya versionen följs.

Du måste först släppa tillägget som ett privat tillägg innan det kan släppas offentligt.

## Privat release

Det enklaste sättet att frigöra tillägget med privat tillgänglighet är att använda [taggtilläggsreleasen](https://www.npmjs.com/package/@adobe/reactor-releaser).

```bash
npx @adobe/reactor-releaser
```

Med `npx` kan du hämta och köra ett npm-paket utan att installera det på datorn. Det här är det enklaste sättet att köra releaser.

>[!NOTE]
> Som standard förväntar sig releaser att Adobe I/O-autentiseringsuppgifter används för ett server-till-server-Oauth-flöde. De gamla `jwt-auth`-autentiseringsuppgifterna
> kan användas genom att köra `npx @adobe/reactor-releaser@v3.1.3` tills borttagningen är den 1 januari 2025. De parametrar som krävs
> för att köra `jwt-auth`-versionen finns [här](https://github.com/adobe/reactor-releaser/tree/9ea66aa2c683fe7da0cca50ff5c9b9372f183bb5).

Du behöver bara ange några få uppgifter i releasern. `clientId` och `clientSecret` kan hämtas från Adobe I/O-konsolen. Navigera till [integreringssidan](https://console.adobe.io/integrations) i I/O-konsolen. Välj rätt organisation i listrutan, hitta rätt integrering och välj **[!UICONTROL View]**.

- Vad är din `clientId`? Kopiera och klistra in det här från I/O-konsolen.
- Vad är din `clientSecret`? Kopiera och klistra in det här från I/O-konsolen.

Releaseraren läser fälten `name` och `platform` från ditt tilläggsmanifest och frågar API efter ett matchande tilläggspaket i Development-tillgänglighet.
Releaser kommer sedan att be dig bekräfta att det har hittat rätt tilläggspaket som du vill frisläppa till privat tillgänglighet.

Om du vill frigöra tillägget med privat tillgänglighet med API:t direkt kan du läsa exempelanropet för [privat släppning av ett tilläggspaket](/help/tags/api/endpoints/extension-packages.md#private-release) i API-dokumenten för mer information.

## Offentlig release

När du har slutfört den privata versionen kan du be Adobe att publicera den offentligt.  Tillägget blir då tillgängligt i den offentliga katalogen. Alla användare av datainsamlingen kan installera tillägget på alla egenskaper.

Fyll i det [offentliga begärandeformuläret ](https://www.feedbackprogram.adobe.com/c/r/DCExtensionReleaseRequest) för att starta versionsprocessen.
