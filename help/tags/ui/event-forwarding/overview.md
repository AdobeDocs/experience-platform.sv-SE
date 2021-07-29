---
title: Översikt över vidarebefordran av händelser
description: Lär dig mer om vidarebefordran av händelser i Adobe Experience Platform, där du kan använda Platform Edge Network för att utföra uppgifter utan att ändra taggimplementeringen.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 1%

---

# Översikt över vidarebefordran av händelser

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad referens till terminologiska ändringar.

Vidarebefordran av händelser i Adobe Experience Platform minskar webbsidans och appens vikt genom att använda Adobe Experience Platform Edge Network för att utföra åtgärder som normalt utförs på klienten. Regler för vidarebefordran av händelser kan transformera och skicka data till nya destinationer utan att implementeringarna på klientsidan ändras.

Vidarebefordran av händelser i kombination med Adobe Experience Platform Web och Mobile SDK gör det möjligt att:

* Gör ett enda anrop från sidan som innehåller en datanyttolast. Data federerar sedan serversidan för att minska nätverkstrafiken på klientsidan och ge kunderna en snabbare upplevelse.
* Minska den tid det tar för webbsidor att läsas in så att sajten uppfyller branschens bästa praxis när det gäller prestanda.
* Öka genomskinligheten och kontrollera vilka datatyper som skickas var i alla taggegenskaper.
* Skapa en regel för vidarebefordran av händelser om du vill skicka tidigare spårade data till ett nytt mål.

## Förbättrade prestanda

I en allt mer konkurrensutsatt miljö måste företagen prioritera resultat för att behålla och utöka sin marknadsandel. Vidarebefordran av händelser förbättrar prestanda för webbplatser och appar på mobila enheter, IoT- och OTT-enheter. Konverteringsgraden för webbplatser kan öka på grund av snabbare laddningstider, mobilappar tar inte batterierna lika snabbt och OTT-appar känner sig lika responsiva som de appar som körs på mobila enheter. I takt med att resultatet ökar är det också vanligt att konverteringsgraden ökar.

## Bättre datastyrning

När teknologin växer och data skickas till fler och fler destinationer blir det svårare att kontrollera vilka data som skickas där. Normaliseringen av bestämmelser som GDPR och CCPA tvingar företagen att få mer kontroll över ett dataproblem som blir allt svårare.

Med hjälp av händelsevidarebefordran kan marknadsföringsteamen utöka sin verksamhet samtidigt som de kontrollerar data. Det minskar antalet tekniker på klientsidan som marknadsförarna behöver för att nå sin målmarknad och skicka data till destinationer utanför Adobe. Detta gör det enklare för implementeringsteamen att hantera data som flödar från klienten till olika destinationer.

## Skillnader mellan händelsevidarebefordran och taggar

Det är viktigt att tänka på följande skillnader mellan händelsevidarebefordran och taggar:

* Tokenisering av dataelement

   * Taggar: I en regel tokeniseras dataelement med `%` i början och slutet av dataelementnamnet. Exempel, `%viewportHeight%`.

   * Vidarebefordran: I en regel tokeniseras dataelement med `{{` i början och `}}` i slutet av dataelementnamnet. Exempel, `{{viewportHeight}}`.

* Hur data refereras

   Om du vill referera till data från Edge-nätverket måste dataelementets sökväg vara `arc.event._<element>_`.

   `arc` står för Adobe Response Context.

   Exempel: `arc.event.xdm.web.webPageDetails.URL`

   >[!IMPORTANT]
   >
   >Om den här sökvägen anges felaktigt samlas inga data in.


* Regelåtgärdssekvens

   I åtgärdsavsnittet för en regel körs alltid regler för vidarebefordran av händelser sekventiellt. Kontrollera att åtgärdsordningen är korrekt när du sparar en regel. Den här körningssekvensen kan inte väljas på samma sätt som med taggar.

* Anpassad kod - JavaScript-versioner

   Taggar använder JavaScript-versionen es5. Vid vidarebefordran av händelser används version es6.

<!--doc Adobe Cloud Connector extension, get from Jon-->
