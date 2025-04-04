---
title: Självvärdande bibliotek
description: Lär dig hur du implementerar självvärdtjänster för dina kodbiblioteksbyggen i Adobe Experience Platform.
exl-id: 8c3bf202-de7a-46e0-801f-0cede24865fd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 9%

---

# Självvärdande bibliotek

>[!NOTE]
>
>Adobe Experience Platform Launch har omprofilerats till en serie tekniker för datainsamling i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar genomförts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad referens av terminologiändringarna.

Taggar i Adobe Experience Platform tillåter produktion av en uppsättning filer som kallas [build](../builds.md). Den här uppsättningen filer styr programmets beteende vid körning.

Byggnader måste ligga någonstans så att klientenheterna kan hämta dem vid körning efter behov.

Experience Platform kan antingen hantera värdtjänsten för dessa filer åt dig eller göra det själv.

## Hanteras av Adobe {#managed-by-adobe}

Adobe använder inte webbhotell. Om du väljer att låta Adobe hantera värdtjänsten levereras dina byggen till ett tredjepartsnätverk för innehållsleverans (CDN) som vi har ett kontrakt med.

För närvarande är den primära CDN-leverantören Akamai. Filer på Akamai har domänen `assets.adobedtm.com`.

### Varför använda hanterade värdtjänster?

Det främsta skälet till att använda hanterade värdtjänster är bekvämlighet. Det är enklare att skapa den värddator som krävs, och du behöver inte bekymra dig om underhåll.

## Självvärdande

Om du inte vill att Adobe ska hantera dina värdbaserade filer måste du själv vara värd för dem. För att kunna lagra dina filer måste du få de färdiga byggnaderna från Experience Platform och vara ansvarig för att få filerna via företagets releasecykel på företagshanterade servrar.

### Varför använda självbetjäning?

Det finns många skäl att välja att ha egna byggfiler.

* Vissa webbläsare blockerar domänen assets.adobedtm.com baserat på de sekretessinställningar som slutanvändaren har konfigurerat
* Självvärdande minskar det antal DNS-sökningar som krävs
* Du har specifika rubriker som du måste ange för dokumentskydd
* Kraven för cachekontroll skiljer sig från standardinställningarna för Adobe
* Du vill ha större kontroll över placeringen av kantnoder
* Din organisation har säkerhetskrav och juridiska krav som hindrar dig från att använda det Adobe-hanterade alternativet

### Självvärd

Det finns två metoder som du kan använda för att hämta färdiga byggen så att du kan vara värd för dem själv.

* Ladda ned
* Direktleverans

#### Ladda ned

Byggnaderna kan levereras som en paketerad ZIP-fil (kryptering är valfritt). Du kan sedan packa upp paketet och infoga innehållet i releasecykeln för att placera dem på dina egna servrar.

Använd en [hanterad av Adobe](self-hosting-libraries.md)-värd och välj alternativet [Arkiv](../environments.md) i din miljö. Miljön innehåller en nedladdningslänk. När du skapar en version kan du hämta den från miljöns nedladdningslänk.

#### Direktleverans

Byggnaderna kan också levereras direkt till en SFTP-server som du har skapat. Du tar ansvar för att få in de här fälten i releasecykeln och göra dem tillgängliga.

Om du vill utföra en direktleverans bör du skapa en [SFTP-värd](sftp-host.md) och tilldela den värden till din miljö. När du skapar ett bibliotek i den miljön levereras filerna till din SFTP-server.
