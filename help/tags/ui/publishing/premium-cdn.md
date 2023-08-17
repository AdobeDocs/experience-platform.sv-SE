---
title: Experience Platform-taggar (Kina)
description: Lär dig mer om taggar för Experience Platform (Kina) och hur de kan användas för att leverera innehåll i flera geografiska regioner.
exl-id: 33e36d3b-9e21-44a8-8498-32a5fc20b46b
source-git-commit: 9c39fd5d0353cc171230818d79ac213ce200dc1e
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# Experience Platform-taggar (Kina)

När du använder en [värddator som hanteras av Adobe](./hosts/managed-by-adobe-host.md) för att kunna leverera dina Adobe Experience Platform-taggar på din webbplats, distribueras dessa resurser till olika leveransnätverk runt om i världen för att ge snabbast nedladdningshastighet. Det finns dock vissa regioner som kräver att alla webbplatsresurser ska replikeras och lagras på en server i den regionen.

För att ta hänsyn till detta har taggar i Experience Platform en funktion för Experience Platform-taggar (Kina) som gör att du kan leverera innehåll till dessa specialregioner.

Stöd för Experience Platform-taggar (Kina) är en betalfunktion och måste köpas av din organisation för att kunna aktivera och använda den. I den här guiden beskrivs hur du konfigurerar och använder funktionen i användargränssnittet för Experience Platform eller datainsamling när du har köpt den.

## Aktivera Experience Platform-taggar (Kina) för din organisation

Experience Platform-taggar (Kina) är aktiverade på företagsnivå. När din organisation har köpt funktionen Experience Platform-taggar (Kina) aktiverar en Adobe-administratör funktionen i användargränssnittet för ditt företag.

## Återskapa och installera taggbibliotek med uppdaterade inbäddningskoder

När taggar för Experience Platform (Kina) har aktiverats innebär det inte att dina taggresurser omedelbart replikeras och är klara att användas i de nya regionerna. Det betyder bara att du nu kan välja när du vill använda den här funktionen.

>[!IMPORTANT]
>
>Bibliotek som byggts innan du aktiverat taggar i Kina fortsätter att fungera som de gör idag. Detta gäller även bibliotek som inte hanteras av Adobe, eftersom [arkiverade miljöer](./environments.md#archive) Använd bara relativa URL:er för sina resurssökvägar. När du har aktiverat Experience Platform-taggar (Kina) fungerar alla bibliotek som du skapar och som inte hanteras av Adobe som om taggarna i Kina inte är aktiverade.

När du har aktiverat taggar i Kina och återskapat bibliotek som du vill använda från de nya värdregionerna, kan du hämta de nya inbäddningskoderna för värdregioner som du vill lägga till på dina webbplatser.

>[!NOTE]
>
>Bibliotekets inbäddningskod som visas under [!UICONTROL Standard] Värdregionen kommer att fortsätta fungera som den är, liksom alla inbäddningskoder för Sidbörjan eller Sidslutet som redan finns på dina webbplatser.

Besök **[!UICONTROL Environments]** eller visa installationsanvisningarna för miljön från bibliotekets redigeringsskärm för att hitta de nya inbäddningskoderna. Varje nytt värdregion som stöds visas efter [!UICONTROL Standard] värdregion (används för områden i världen som stöds utan Experience Platform-taggar (Kina)). På skärmbilden nedan visas en inbäddningskod för regionen Kina som använder `.cn` som toppnivådomän (TLD).

![Bädda in kod för regionen Kina](../../images/ui/publishing/premium-cdn/embed-codes.png)

Välj lämplig inbäddningskod för webbsidan och klistra in den i `<head>` -taggen i dokumentet. Mer information om hur du använder inbäddningskoder för att installera taggbibliotek finns i [användargränssnittsguide för miljöer](./environments.md#installation).

## Nästa steg

I den här guiden beskrivs hur du aktiverar och installerar funktionen Experience Platform Tags (China) för taggimplementeringen. Mer information om hur du installerar och testar taggbibliotek på dina webb- och mobilegenskaper finns i [publicera översikt](./overview.md).
