---
title: Publicera om ett bibliotek
description: Lär dig hur du publicerar om ett tidigare taggbibliotek i Adobe Experience Platform.
exl-id: 026b01f2-a93d-4e8a-9ed2-47c4f011e70f
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---

# Publicera om ett bibliotek

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

De fem senaste biblioteken som har publicerats i produktionsmiljön på en webbegenskap är tillgängliga för senare hämtning. Den här funktionen är användbar när du hittar ett fel i ditt produktionsbibliotek och behöver återställa till ett känt bra läge omedelbart.

Hämtningsprocessen beror på dina miljöinställningar när biblioteket ursprungligen publicerades. Detta är viktigt eftersom hämtning av ett arkiverat bibliotek inte ändrar någonting på den publicerade webbplatsen, medan hämtning av ett vanligt bibliotek gör det.

Följande alternativ är tillgängliga:

* **Värd: Hanteras av Adobe, Archive: Av:** Om du använder Hanteras av Adobe och inte arkiverar ditt bibliotek kan du publicera om dessa äldre bibliotek.

* **Värd: Hanteras av Adobe, Archive: På:** Om du använder Hanteras av Adobe och arkiverar ditt bibliotek kan du hämta dessa äldre bibliotek.

* **Värd: SFTP, arkiv: På eller av:** Om du använder SFTP-värden antas du ha egna arkiveringsstrategier och inga hämtningsalternativ är tillgängliga.

Det finns ännu inga hämtningsalternativ för mobila egenskaper.

## Publicera igen

Varje taggmiljö innehåller en länk till en biblioteksfil. Alla bibliotek som du skapar i den miljön kan refereras till med den länken.

När du bygger till en utvecklings- eller staging-miljö rensas den gamla versionen och den nya versionen distribueras. För produktionsmiljön uppdateras länken så att den pekar på den senaste versionen, men de fem senaste byggen behålls innan de rensas.

Dessa fem senaste byggen i din produktionsmiljö är de som är tillgängliga för hämtning.

När du publicerar om ett äldre bibliotek uppdaterar Platform miljölänken så att den pekar på en av dessa äldre versioner som ännu inte har rensats.  Plattformen skickar också en rensningsbegäran till CDN-kantnodcachen för att ange att biblioteket har uppdaterats och att en ny kopia ska hämtas från ursprungsläget.

Det innebär att när du publicerar om ett äldre bibliotek:

* Inga ändringar görs i någon av resurserna (eller tidigare revideringar) i taggegenskapen

* Det sätt på vilket utvecklings- och mellanlagringsmiljöer beräknar vad som är uppströms förändras inte

Tänk på scenariot när du återställer på grund av ett problem med en viss regel. Regelrevisionen som nu är i produktion kan till exempel vara tre versioner gammal.  När du visar den regeln i användargränssnittet för att åtgärda den, återspeglas den fortfarande de senaste ändringarna som har sparats i stället för de som är under produktion.

Därför meddelar Platform dig om att en egenskap är i ett återpublicerat läge som en påminnelse om att det du ser i användargränssnittet för datainsamling är lite mer borttaget från Production än vanligt. Det här meddelandet kan inte visas och visas en gång per webbläsarsession första gången du visar egenskapen.

### Publicera om ett äldre bibliotek

![Publicera om ett bibliotek](images/retrieve_republish.png)

Från publiceringsskärmen:

1. Leta reda på biblioteket i kolumnen Publicerad som du vill publicera igen.
1. Markera ellipsen (`...`) i det övre högra hörnet av bibliotekskortet.
1. Välj **[!UICONTROL Republish]**.

## Hämta

Det är enklare att hämta ett arkiverat bibliotek. Du refererar inte direkt till de här ZIP-filerna någonstans, så du kan bara hämta det äldre biblioteket till datorn och köra din vanliga process.

### Hämta ett äldre bibliotek

![Hämta ett bibliotek](images/retrieve_download.png)

Från publiceringsskärmen:

1. Leta reda på det bibliotek i kolumnen Publicerad som du vill hämta.
1. Markera ellipsen (`...`) i det övre högra hörnet av bibliotekskortet.
1. Välj **[!UICONTROL Download]**.
