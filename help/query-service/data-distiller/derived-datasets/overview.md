---
title: Härledda datauppsättningar
description: Härledda datauppsättningar är ett praktiskt sätt att generera datauppsättningar som du kan uppdatera vid valfri tidpunkt och som kan publiceras i kundprofildata i realtid. Det här dokumentet innehåller en översikt över hur du använder frågetjänsten för att skapa härledda datauppsättningar som kan användas med dina profildata.
exl-id: 5d52b268-e2a3-411c-8242-3aa32e759937
source-git-commit: 7364da23c261d83681af605047a7cd7539f4a83f
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---

# Härledda datauppsättningar

Funktionen för härledda datauppsättningar är ett praktiskt sätt att generera datauppsättningar utifrån annan information som finns i sjön. Dessa datauppsättningar kan uppdateras med valfri mellanrum och eventuellt publiceras i kundprofildata i realtid. Härledda datauppsättningar åtgärdar behovet av att skapa komplexa datauppsättningar som decile, percentile och quartile över enklare datamängder som max, count och means. Dessa datauppsättningar kan beräknas specifikt för en enskild användare eller för en affärsenhet. Detta gör att du kan härleda datauppsättningar som kan vara direkt ackrediterade för en identifierare, till exempel e-postadresser, enhets-ID:n och telefonnummer, och även härleda datauppsättningar som är indirekt kopplade till den användar- eller affärsprofilen.

Härledda datauppsättningar behövs för en rad olika användningsfall när data analyseras på sjön. Dessa data kan sedan markeras för användning i kundprofilen i realtid och användas i senare led, t.ex. för att skapa högt fokuserade målgrupper. Exempel på användningsområden för den här funktionen kan vara:

* Identifiera de lägsta 10 % av prenumeranterna baserat på tittarupplevelsen per kanal. Detta skulle göra det möjligt för marknadsförarna att inrikta sig på en viss målgrupp och sälja ett nytt prenumerationspaket.
* Identifiera en målgrupp som befinner sig i de tio största flygbolagen baserat på den totala tillryggalagda sträckan och som har statusen&quot;Flyer&quot;. Den här målgruppen kan användas för att selektivt rikta sig till försäljningen av ett nytt kreditkortserbjudande.
* Fastställ bortfallsfrekvensen baserat på prenumeration.
* Identifiera de 1 % viktigaste hushållsinkomsterna i en provins eller stat och ge ett mått på antalet individer som har flyttat ut ur den kollektiva gruppen under de senaste n-månaderna.

## Komplexa härledda datauppsättningar

Om du vill skapa en rankning baserad på en eller flera mätvärden (som intäkt, visningstid o.s.v.) för en viss dimension (kategori) krävs komplexa härledda datauppsättningar. Deciles, quartiles, and percentiles allow flexibility and precision when ranking data with derived datasets.

En decile är en metod för att dela upp en uppsättning rankade data i 10 lika stora delar. När data delas upp i decilar tilldelas varje rad i datauppsättningen en decimalrankning. Detta gör att data kan sorteras i fallande eller stigande ordning.

Med decimalrangordning ordnas data i ordning från det lägsta till det högsta och görs på en skala från 1 till 10 där varje successiv siffra motsvarar en ökning på 10 procentenheter.

Lövbucklar representerar antalet rankade grupper och används för att tilldela en rankning till en dimension (kategori) i datauppsättningen. Bucket kan vara ett tal eller ett uttryck som utvärderas till ett positivt heltalsvärde för varje partition. Bucketerna får inte ha ett null-värde.

Kvartilarna används för att dividera fördelningen med fyra och percentiler med 100.

## Analysbaserade härledda datauppsättningar

Frågetjänsten tillhandahåller inbyggda funktioner som sessioner och senaste beröring, bland annat, som du kan tillämpa på alla tidsseriedata för att generera affärsrelaterade härledda datauppsättningar. Du kan basera dessa analytiska härledda datauppsättningar på en eller flera identiteter och eventuellt publicera data i kundprofilen i realtid om det behövs.

Exempel på användningsområden för den här typen av härlett attribut kan vara:

* Spåra produkter som skannats under en användarsession och som inte fanns i lager.
* Spåra populära mätvärden som storlek, färg eller produktkategori för de produkter du bläddrar bland eller köper.
* Spåra den plattformskälla som ledde till en produkthandling eller ett köp.
* Spåra det senast bläddrade objektet efter en identitet.
* Spåra mätvärden som genomsnittligt antal artiklar i en kundvagn, övergivna varukorgar eller genomsnittlig inköpsfrekvens.

## Andra härledda datauppsättningar

Du kan också beräkna affärsvärden som ett härlett attribut och använda dem tillsammans med enkla datauppsättningar som zip-kod eller ett aggregerat mått som till exempel totalt antal. Exempel: ett totalt antal som baseras på en stad eller provins, eller totalt antal som baseras på en affärskategori och en stad/provins.

## Nästa steg och användningsexempel

Genom att läsa det här dokumentet får du en bättre förståelse för hur frågetjänstens härledda datauppsättningar underlättar komplexa användningsfall för att maximera dataanvändningen. I nästa exempel ska du läsa [decimalbaserat användningsfall för härlett attribut](../../use-cases/deciles-use-case.md) om du vill se hur den här funktionen används i ett verkligt scenario.
