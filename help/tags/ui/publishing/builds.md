---
title: Bygger
description: Lär dig mer om byggkoncept och hur de fungerar i Adobe Experience Platform.
exl-id: af899282-aa2d-4395-8dbd-18d91be3f041
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 5%

---

# Bygger

>[!NOTE]
>
>Adobe Experience Platform Launch har omprofilerats till en serie tekniker för datainsamling i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar genomförts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad referens av terminologiändringarna.

Ett bygge är den uppsättning filer som innehåller all kod som körs på klientenheten.

Det är en sammansatt av de ändringar som du har angett i ditt bibliotek samt allt som har skickats, godkänts eller publicerats före det.

Bygget består av kodfiler på klientsidan som refererar till varandra. Dessa filer levereras till din värdplats med den miljö och värd som du har valt för biblioteket. Koden som du distribuerar på platsen pekar på samma plats så att filerna kan läsas in när en användare kommer åt platsen eller programmet.

## Filinnehåll

Ett bibliotek definierar en diskret uppsättning taggresurser (tillägg, regler och dataelement) som ska inkluderas i biblioteket.

Ett bygge innehåller all modulkod (tillhandahålls av tilläggsutvecklarna) och den konfiguration (anges av dig) som behövs för att driva resurserna i biblioteket. Om ett tillägg t.ex. innehåller åtgärder som inte används i reglerna finns koden som utför åtgärderna inte i bygget.

Byggnader delas upp i huvudbiblioteksfilen och kan vara många mindre filer. Huvudbiblioteksfilen refereras i inbäddningskoden och läses in på sidan vid körning. Den innehåller:

* Regelmotorn
* All tilläggskonfiguration
* All dataelementkod och konfiguration
* All regelhändelsekod och konfiguration
* All villkorskod och konfiguration
* Händelsekod och konfiguration för alla regler som har Library Loaded eller Page Bottom som händelse (eftersom vi vet att vi behöver det direkt).

De mindre filerna innehåller kod och konfiguration för enskilda åtgärder som läses in på sidan efter behov. När en regel aktiveras och dess villkor utvärderas så att åtgärderna måste utföras, hämtas den nödvändiga koden och konfigurationen för den specifika åtgärden från en av de mindre filerna. Det innebär att bara den kod som behövs för att utföra de nödvändiga åtgärderna har lästs in på sidan, vilket gör huvudbiblioteket så litet som möjligt.

## Filformat

Standardfilformatet för byggen är ett paket med filer som innehåller all kod som krävs för att dina tillägg, dataelement och regler ska kunna köras på det sätt som du vill.

I vissa fall kanske du föredrar ett ZIP-arkiv av filerna i stället för den körbara kodfilen på klientsidan. Du kan till exempel skapa ett arkiv om du själv är värd för ditt bygge och vill använda bygget i en annan distribution. Om du anger något i den självhanterade sökvägen till biblioteksfältet kan du spara din miljö. Tillsammans med den nya koden blir en länk till den arkiverade nedladdningen tillgänglig. När biblioteket har byggts kan du distribuera en ZIP-fil till Akamai och hämta den från `assets.adobedtm.com/...`.

>[!NOTE]
>
>Det finns ingenting på den platsen förrän du skapar ett bygge.

Oavsett filformat levereras bygget alltid till den plats som anges av värden.

Om du vill slutföra ett bygge markerar du ett bibliotek och väljer alternativet Skapa som är tillgängligt på den nivån i publiceringsprocessen (Build for Development, Build for Staging osv.).

## Miniatyr

Minimering minskar bandbreddskostnaderna och förbättrar hastigheten genom att radera data som inte behövs för att köras från en fil.

För att få bättre prestanda minimerar Experience Platform allt, inklusive:

* Huvudtaggbiblioteket
* Modulkod från tilläggsutvecklare som en del av ett tillägg
* Anpassad kod från Experience Platform-användare

>[!NOTE]
>
>Om modulkoden och den anpassade koden redan är miniatyrbilder miniatyriserar Experience Platform den igen. Den andra miniatyrversionen ger inga ytterligare fördelar, men den orsakar inga skador och gör Experience Platform mindre komplext och enklare att underhålla.

All kod på klientsidan pekar mot den minifierade versionen av koden. Detta visas i filnamnen som följer standardnamnkonventionen för minifierade filer:

`launch-%environment_id%.min.js`

Om du vill se den ominifierade koden tar du bort .min från filnamnet:

`launch-%environment_id%.js`

Om en tilläggsutvecklare tillhandahåller minifierad kod med sitt tillägg, tillhandahåller Experience Platform inte icke-minifierad kod i den icke-minifierade versionen. På samma sätt gäller att om en Experience Platform-användare placerar minierad kod i en anpassad kodruta så är koden fortfarande minifierad i icke-minifierade byggen. Experience Platform tar inte bort någonting.

Mer information om miniatyrbilder finns i [den här artikeln om stackbanor](https://blog.stackpath.com/glossary/minification/).

När du skapar en version skapas det ominifierade biblioteket först och sedan minimeras hela biblioteket samtidigt.
