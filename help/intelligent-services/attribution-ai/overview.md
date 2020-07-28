---
keywords: Experience Platform;attribution ai;overview;popular topics
solution: Experience Platform
title: Översikt över Attribution AI
topic: Attribution AI
translation-type: tm+mt
source-git-commit: 83e74ad93bdef056c8aef07c9d56313af6f4ddfd
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---


# Översikt över Attribution AI

Attribution AI, som en del av Intelligent Services är en flerkanalig algoritmisk attribueringstjänst som beräknar påverkan och inkrementell påverkan av kundinteraktioner i förhållande till angivna resultat. Med Attribution AI kan marknadsförarna mäta och optimera marknadsförings- och annonsutgifterna genom att förstå effekten av varje enskild kundinteraktion i varje fas av kundresan.

## Förstå Attribution AI

Attribution AI används för att attribuera krediter till kontaktytor som leder till konverteringshändelser. Detta kan användas av marknadsförare för att kvantifiera marknadsföringseffekten av varje enskild kontaktyta för marknadsföring över kundresor. Exempel på kontaktytor är visningar av webbannonser, e-postmeddelanden, e-postöppningar och betalda sökningar.

Utdata från Attribution AI kan delas upp i olika dimensioner och kan användas i olika faser av kundresan. Detta uppnås utan att man behöver översätta affärsbehoven till maskininlärningsproblem, plockalgoritmer, utbildning eller driftsättningsmodeller.

Data från Attribution AI kan komma från Adobe (t.ex. [!DNL Analytics]) eller andra datakällor än Adobe.

Attribution AI har stöd för två kategorier med poäng, algoritmiska och regelbaserade. Algoritmiska poäng inkluderar inkrementella och påverkade poäng. Regelbaserade resultat inkluderar First Touch, Last Touch, Linear, U-shaped och Time-Decay.

Följande video har utformats för att ge stöd för din förståelse av Attribution AI.

>[!VIDEO](https://video.tv.adobe.com/v/32667?learn=on&quality=12)

## Attribution AI algoritmisk poäng

Attribution AI har stöd för två kategorier av attribueringspoäng, algoritmiska och regelbaserade poäng.

Attribution AI ger två olika typer av algoritmiska poäng, inkrementellt och påverkat. En påverkad poäng är den del av konverteringen som varje marknadsföringskontaktyta ansvarar för. En inkrementell poäng är mängden marginell påverkan som direkt orsakas av kontaktytan för marknadsföring. Den största skillnaden mellan det stegvisa poängvärdet och det poängvärde som påverkas är att det stegvisa poängvärdet tar baslinjeeffekten i beaktande. Man utgår inte från att en konvertering enbart orsakas av de föregående kontaktytorna.

Se tabellen nedan för mer information om var och en av dessa attribueringspoäng:

| Attributionspoäng | Beskrivning |
| ----- | ----------- |
| Första beröring | Regelbaserat attribueringspoäng som tilldelar alla krediter till den första kontaktytan på en konverteringsbana. |
| Sista beröring | Regelbaserat attribueringspoäng som tilldelar all kredit till den kontaktyta som ligger närmast konverteringen. |
| Linjär | Regelbaserat attribueringspoäng som tilldelar varje kontaktyta samma poäng på en konverteringsbana. |
| U-formad | Regelbaserat attribueringspoäng som tilldelar 40 % av krediten till den första kontaktytan och 40 % av krediten till den sista kontaktytan, där de andra kontaktytorna delar upp de återstående 20 % jämnt. |
| Tidsminskning | Regelbaserat attribueringspoäng där kontaktytor som ligger närmare konverteringen får mer kredit än kontaktytor som ligger längre bort från konverteringen. |
| Influerad (algoritmisk) | Påverkade poäng är den del av konverteringen som varje kontaktyta för marknadsföring ansvarar för. |
| Inkrementell (algoritmisk) | Inkrementell poäng är mängden marginell påverkan som direkt orsakas av en kontaktyta för marknadsföring. |

## Exempel på användningsområden

Attribution AI kan användas som hjälp i följande exempel:

- **Verkställande rapportering**: Låt cheferna förstå den verkliga inkrementella effekten av marknadsföring, både som helhet och efter kanal, region, SKU osv.
- **Budgettilldelning**: Informera om budgetallokeringsbeslut i alla marknadsföringskanaler.
- **Kampanjoptimering**: I varje kanal kan du förstå vilka kampanjer, kreatörer och nyckelord som fungerar bättre för vilka SKU:er eller geos. På så sätt kan ni titta på varje kanal så att marknadsföringsteamet kan optimera taktikerna.
- **Fullständig attribuering**: Förstå hur marknadsföringen påverkar hela kundresan. Exempel: kostnadsfri kontoregistrering till betalkonvertering och vidare.
- **Partnerutvärderingar**: Utvärdera effektiviteten hos myndigheter och partners utifrån attribueringsresultaten.

### Ytterligare funktioner

Attribution AI erbjuder även integrering med andra Adobe-lösningar som [!DNL Adobe Analytics]. På så sätt kan ni använda dessa lösningar för att använda den anpassningsbara algoritmiska modellen för att utvärdera mediaprestanda och ge analytiska insikter.

## Nästa steg

Du kan börja med att följa guiden [Komma igång](./getting-started.md) . I den här guiden får du hjälp med att konfigurera alla nödvändiga förbegäranden för Attribution AI. Om du redan har dina uppgifter tillgängliga går du till [Attribution AI användarhandbok](./user-guide.md). I den här guiden får du hjälp med att skapa en instans och skicka in den för utbildning och poängsättning.