---
title: Självvärdande bibliotek
description: Lär dig hur du implementerar värdtjänster för dina taggbiblioteksbyggen i Adobe Experience Platform.
exl-id: 8c3bf202-de7a-46e0-801f-0cede24865fd
source-git-commit: 91b28fc284344b42020b0e49b64ac023e492d572
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 1%

---

# Självvärdande bibliotek

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

Taggar i Adobe Experience Platform gör det möjligt att producera en uppsättning filer som kallas [bygga](../builds.md). Den här uppsättningen filer styr programmets beteende vid körning.

Byggnader måste ligga någonstans så att klientenheterna kan hämta dem vid körning efter behov.

Plattformen kan antingen hantera värdtjänsten för dessa filer åt dig eller så kan du göra det själv.

## Hanteras av Adobe {#managed-by-adobe}

Adobe är inte webbhotell. Om du väljer att låta Adobe hantera värdtjänsten levereras dina byggen till ett tredjepartsnätverk för innehållsleverans (CDN) som vi har ett kontrakt med.

För närvarande är den primära CDN-leverantören Akamai. Filer som lagras på Akamai har domänen `assets.adobedtm.com`.

### Varför använda hanterade värdtjänster?

Det främsta skälet till att använda hanterade värdtjänster är att det är bekvämt. Det är enklare att skapa den värddator som krävs, och du behöver inte bekymra dig om underhåll.

## Självvärdande

Om du inte vill att Adobe ska hantera dina värdbaserade filer måste du själv vara värd för dem. Om du vill ha dina filer som värd måste du skaffa de färdiga byggnaderna från Platform och vara ansvarig för att få filerna via företagets releasecykel till företagshanterade servrar.

### Varför använda självbetjäning?

Det finns många skäl att välja att ha egna byggfiler.

* Vissa webbläsare blockerar domänen assets.adobedtm.com baserat på de sekretessinställningar som slutanvändaren har konfigurerat
* Självvärdande minskar antalet DNS-sökningar som krävs
* Du har specifika rubriker som du måste ange för dokumentskydd
* Kraven för cachekontroll skiljer sig från standardinställningarna för Adobe
* Du vill ha större kontroll över kantnodernas placering
* Din organisation har säkerhetskrav och juridiska krav som hindrar dig från att använda det alternativ som hanteras av Adobe

### Självvärd

Det finns två metoder som du kan använda för att hämta färdiga byggen så att du kan vara värd för dem själv.

* Hämta
* Direktleverans

#### Hämta

Byggnaderna kan levereras som en paketerad ZIP-fil (kryptering är valfritt). Du kan sedan packa upp paketet och infoga innehållet i releasecykeln för att placera dem på dina egna servrar.

Använd en [Hanteras av Adobe](self-hosting-libraries.md) värddator och välj [Arkiv](../environments.md) i din miljö. Miljön innehåller en nedladdningslänk. När du skapar en version kan du hämta den från miljöns nedladdningslänk.

#### Direktleverans

Byggnaderna kan också levereras direkt till en SFTP-server som du har skapat. Du tar ansvar för att få in de här fälten i releasecykeln och göra dem tillgängliga.

Om du vill utföra en direktleverans måste du skapa en [SFTP-värd](sftp-host.md) och tilldela värden till din miljö. När du skapar ett bibliotek i den miljön levereras filerna till din SFTP-server.
