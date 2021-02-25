---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API
title: Exempel på PQL-uttryck för beräknade attribut
topic: guide
type: Dokumentation
description: Beräknade attribut är funktioner som används för att samla data på händelsenivå i attribut på profilnivå. Dessa funktioner kräver att giltiga PQL-uttryck (Profile Query Language) används. I den här guiden beskrivs några av de vanligaste PQL-uttrycken för beräknade attribut.
translation-type: tm+mt
source-git-commit: 92533f732cc14b57d2a0a34ce9afe99554f9af04
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 0%

---


# (Alfa) Exempel på PQL-uttryck för beräknade attribut

>[!IMPORTANT]
>
>Funktionen för beräknade attribut är för närvarande alfavärden och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

I Adobe Experience Platform är beräknade attribut funktioner som används för att samla data på händelsenivå i attribut på profilnivå. Funktionerna beräknas automatiskt så att de kan användas för segmentering, aktivering och personalisering. Varje beräknat attribut definieras med grundläggande information, t.ex. ett namn och en beskrivning, schemaklassen och sökvägen till fältet som värdet ska sparas i samt ett uttryck vars beräknade värde är det värde som du vill lagra i det beräknade attributet.

Uttrycken som används i beräknade attribut skapas med [!DNL Profile Query Language] (PQL), ett XDM-kompatibelt frågespråk (Experience Data Model) som är utformat för att stödja definition och körning av frågor för kundprofildata i realtid.

Beräknade attribut har för närvarande stöd för följande funktioner: sum, count, min, max och boolesk. I den här guiden beskrivs några av de vanligaste PQL-uttrycken som du kan använda när du definierar egna beräknade attribut för din organisation. Mer information om PQL och länkar till ytterligare formateringsriktlinjer och exempel på frågor som stöds finns i [PQL overview](../../segmentation/pql/overview.md).

## Direktuppspelningsuttryck

Följande tabell innehåller information om de vanligaste frågeuttrycken som stöds i direktuppspelningsläge.

| Beskrivning | PQL-uttryck | Indatatyp:<br/>Profil eller upplevelsehändelse (EE[]) | Resultattyp |
|---|---|---|---|
| Antal nedladdningar av bilder under de senaste 7 dagarna. | xEvent[(tidsstämpeln inträffar &lt; 7 dagar före nu) och eventType=&quot;download&quot; och contentType = &quot;image&quot;].count() | Profil och EE[] | Heltal |
| Summan av kundutgifterna för sportartiklar de senaste sju dagarna. | xEvent[(tidsstämpel inträffar &lt; 7 dagar före nu) och eventType=&quot;transaktion&quot; och kategori = &quot;sportartiklar&quot;].sum(commerce.order.priceTotal) | Profil och EE[] | Heltal eller Dubbel |
| De senaste sju dagarnas genomsnittliga kundutgifter för sportartiklar.<br/><br/>**Obs!** Kräver att tre beräknade attribut skapas. | **ca1:** xEvent[(tidsstämpeln inträffar  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.sum(commerce.order.priceTotal)<br/><br/>**ca2:** xEvent[(timestamp inträffar  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.count()<br/><br/>**ca3:** ca1 / ca2]] | Profil och EE[] | Dubbel |
| Har kunden spenderat mer än 100 dollar på sportartiklar de senaste sju dagarna?<br/><br/>**Obs!** Kräver att två beräknade attribut skapas. | **ca1:** xEvent[(tidsstämpeln inträffar  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.sum(commerce.order.priceTotal)<br/><br/>**ca2:** ca1 > 100] | Profil och EE[] | Boolean |
| Har kunden köpt något de senaste sju dagarna? | chain(xEvent, timestamp, [A: What(eventType = &quot;transaction&quot;) WHEN(&lt; 7 dagar före nu)]) | Profil och EE[] | Boolean |
| De senaste sju dagarnas låga användarutgifter för sportartiklar. | xEvent[(tidsstämpel inträffar &lt; 7 dagar före nu) och eventType=&quot;transaktion&quot; och kategori = &quot;sportartiklar&quot;].min(commerce.order.priceTotal) | Profil och EE[] | Heltal eller Dubbel |
| De senaste sju dagarnas största utgifter för sportartiklar. | xEvent[(tidsstämpel inträffar &lt; 7 dagar före nu) och eventType=&quot;transaktion&quot; och kategori = &quot;sportartiklar&quot;].max(commerce.order.priceTotal) | Profil och EE[] | Heltal eller Dubbel |
| Antal nedladdningar av varje nedladdad produkt under de senaste 7 dagarna, indexerade per produkt. | xEvent[(tidsstämpeln inträffar &lt; 7 dagar före nu) och eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.count())) | Profil och EE[] | Mappa[Sträng, Heltal] |
| Summan av numeriska egenskaper för nedladdning av varje nedladdad produkt under de senaste 7 dagarna, indexerade efter produkt. | xEvent[(tidsstämpeln inträffar &lt; 7 dagar före nu) och eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal))) | Profil och EE[] | Mappa[Sträng, Heltal] eller Karta[Sträng, Dubbel] |
| Genomsnittlig numerisk egenskap över nedladdningar av varje nedladdad produkt under de senaste 7 dagarna, indexerade efter produkt.<br/><br/>**Obs!** Kräver att tre beräknade attribut skapas. | **ca1:** xEvent[(tidsstämpeln inträffar  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal)))<br/><br/>**ca2:** xEvent[(tidsstämpeln inträffar  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.groupBy(product).map((K, G) => mapEntry(K, G.count())<br/><br/>**) ca3:** ca2 / ca1]] | Profil och EE[] | Mappa[Sträng, Dubbel] |
| Minsta numeriska värde för nedladdning av varje nedladdad produkt under de senaste 7 dagarna, indexerat efter produkt. | xEvent[(tidsstämpeln inträffar &lt; 7 dagar före nu) och eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.min(commerce.order.priceTotal)) | Profil och EE[] | Mappa[Sträng, Heltal] eller Karta[Sträng, Dubbel] |
| Maximalt antal numeriska egenskaper för nedladdningar av varje nedladdad produkt under de senaste 7 dagarna, indexerade efter produkt. | xEvent[(tidsstämpeln inträffar &lt; 7 dagar före nu) och eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.max(commerce.order.priceTotal))) | Profil och EE[] | Mappa[Sträng, Heltal] eller Karta[Sträng, Dubbel] |
| Numeriskt uttryck i profil, refererar inte till händelser. | if(person.kön = &quot;kvinna&quot;, 60, 65) | Profil | Heltal eller Dubbel |
| Booleskt uttryck i profil, refererar inte till händelser. | person.bornYear >= 2000 | Profil | Boolean |
| Stränguttryck i profil, refererar inte till händelser. | if(homeAddress.countryCode in [&quot;US&quot;,&quot;MX&quot;,&quot;CA&quot;], &quot;NA&quot;, &quot;ROW&quot;) | Profil | Sträng |

## Grupputtryck

Följande tabell innehåller information för frågeuttryck som bara är tillgängliga i gruppläge, vilket innebär att de inte är tillgängliga i direktuppspelning.

| Beskrivning | PQL-uttryck | Indatatyp:<br/>Profil eller upplevelsehändelse (EE[]) | Resultattyp |
|---|---|---|---|
| Om summan av numeriska uttryck över produktnedladdningar under de senaste 7 dagarna överstiger 100, indexerat efter produkt. | xEvent[(tidsstämpeln inträffar &lt; 7 dagar före nu) och eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal) > 100)) | Profil och EE[] | Mappa[Sträng, Boolean] |
| Anger om det genomsnittliga antalet numeriska uttryck över produktnedladdningar under de senaste 7 dagarna överskrider 100, indexerat efter produkt. | xEvent[(tidsstämpeln inträffar &lt; 7 dagar före nu) och eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.Average(commerce.order.priceTotal) > 100)) | Profil och EE[] | Mappa[Sträng, Boolean] |
| Ackumulering av olika mätvärden för varje nedladdad produkt de senaste sju dagarna, indexerade efter produkt. | xEvent[(tidsstämpeln inträffar &lt; 7 dagar före nu) och eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, {&quot;count&quot;: G.count(), &quot;sum&quot;: G.sum(commerce.order.priceTotal)}) | Profil och EE[] | Mappa[Sträng, Objekt] där Objektet är en anpassad XDM-typ |