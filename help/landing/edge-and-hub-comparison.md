---
solution: Experience Platform
title: Jämförelse mellan Edge Network och Hub
description: Lär dig mer om de olika bearbetningssökvägarna som är tillgängliga för Adobe Experience Platform.
exl-id: 3e9c63d2-c798-44b4-870d-bf1551f29690
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 2%

---

# Jämförelse mellan Edge Network och Hub

Adobe Experience Platform är det mest kraftfulla, flexibla och öppna systemet på marknaden för att bygga och hantera kompletta lösningar som ger en bättre kundupplevelse. Med Experience Platform kan ni centralisera och standardisera kunddata och innehåll från alla system och tillämpa datavetenskap och maskininlärning för att dramatiskt förbättra utformningen och leveransen av avancerade, personaliserade upplevelser. Därför har Experience Platform flera olika sätt att behandla data, vilket gör att du kan utvärdera dina data på bästa sätt.

## Servertyper

I Experience Platform kan data bearbetas på två olika sätt: Adobe Experience Platform nav för batch- och direktuppspelningsarbetsflöden och Edge Network för realtidsupplevelser.

### Adobe Experience Platform nav

Hub är ett huvuddatacenter som är centralt placerat och innehåller alla historiska data och omfattande profilsammanhang som har samlats in i Adobe Experience Platform. På så sätt kan ni skicka och ta emot mer robusta och fullständiga data till era tjänster längre fram i kedjan. Därför bör navet användas i scenarier där datas **noggrannhet** är viktigare.

Följande tjänster finns på navet:

- Gruppsegmentering
- Direktuppspelningssegmentering
- Profiler
- Mål
- Identitetsdiagram
- Data Distiller - frågetjänst
- Source-anslutningar

### Experience Platform Edge Network

Edge Network är en server som fysiskt finns närmare olika geografiska platser. Dessa datacenter bearbetar alla data som samlas in via SDK-tilläggen och Edge Network API:er. De enda data som finns på Edge Network är målgruppsmedlemskap, profilidentiteter och attribut som krävs för personalisering.

Med Edge Network kan ni skicka och ta emot data till era kunder snabbare på grund av deras närhet till slutanvändaren. Dessutom kan du använda Edge Network för att bearbeta begäranden om vidarebefordran av händelser och tagghantering. Edge Network bearbetar emellertid bara **beteendemässiga** data. Därför bör Edge Network användas i scenarier där datans **hastighet** är viktigare.

Följande tjänster är tillgängliga på Edge Network:

- Edge segmentering
- Edge profiler
- Edge destinationer
- Datainsamling
- SDK-tillägg

## Platser

I följande avsnitt visas platserna för både nav och Edge Network.

![Ett diagram som visar de olika platserna för både nav- och Edge Network-servrar.](./images/servers/platform-server-locations.png)

**Hubb**

- VA7 (Virginia, USA)
- NLD2 (Nederländerna)
- AUS5 (Australien)
- CAN2 (Kanada)
- GBR9 (Storbritannien)
- IND1 (Indien)

**Edge Network**

- OR2 (Oregon, USA)
- VA6 (Virginia, USA)
- IRL1 (Irland)
- IND1 (Indien)
- SGP3 (Singapore)
- AUS3 (Australien)
- JPN3 (Japan)

Mer detaljerad information om de tillgängliga serverplatserna finns i [flermolnöversikten](./multi-cloud.md#available-cloud-regions).

## Nästa steg

När du har läst den här översikten förstår du nu skillnaderna mellan databearbetning på Adobe Experience Platform nav och Adobe Experience Platform Edge Network.

## Bilaga

I följande avsnitt visas ytterligare information om databearbetning på Adobe Experience Platform.

### Vanliga frågor och svar

I följande avsnitt visas vanliga frågor om hubben och Edge Network:

#### Vilka scenarier passar bäst för navet?

Hubben passar bäst i scenarier där **noggrannheten** för data är viktigare. Låt oss till exempel säga att ni vill skapa en marknadsföringskampanj som riktar sig till alla kunder som har övergett kundvagnar. I så fall kan du använda gruppsegmentering för att skapa en målgrupp som matchar de övergivna kundvagnarna och exportera den till en gruppdestination.

#### Vilka scenarier passar bäst för Edge Network?

Edge Network passar bäst för scenarier där **hastighet** av data är viktigare. Låt oss till exempel säga att du behöver skapa en begränsad Flash-försäljning för att rikta dig till en kund som surfar på din webbplats med en produkt i kundvagnen. I så fall kan du använda kantsegmentering, så att du omedelbart kan rikta in dig på och skicka ett personligt meddelande till användare med en produkt i kundvagnen med en&quot;blixtförsäljning&quot;.

#### Vilka data skickas från navet till Edge Network?

Endast data som behövs för att leverera upplevelser i realtid är inlästa från navet till Edge Network. Dessa data skickas automatiskt från navet till Edge Network för att så småningom hålla dem konsekventa, och lagras endast i upp till 14 dagar. Detta innebär dock **inte** att data hålls perfekt synkroniserade med data i navet. Det kan därför finnas skillnader i tillgängliga data mellan hubben och Edge Network.
