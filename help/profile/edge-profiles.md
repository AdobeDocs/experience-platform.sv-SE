---
title: Edge-profiler
description: Lär dig mer om kantprofiler, och relaterad terminologi, tillgängliga områden för kantprofiler samt tillgängliga tjänster för kantprofiler.
exl-id: dcae267f-1d5a-4e90-b634-afd42b0d4edc
source-git-commit: 16e49628df73d5ce97ef890dbc0a6f2c8e7de346
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---

# Edge-profiler

I Adobe Experience Platform är kundprofilen i realtid den enda källan till sanning för entitetsdata. Profildata ligger i ett centralt nav och tar hänsyn till fall där era data är fullständiga och går att använda. I mer realtidssituationer, där tidskänslighet är viktigare, är dock kantprofiler det bästa alternativet. Edge-profiler är enkla profiler som sitter på kanterna och hjälper till i realtidspersonalisering.

Adobe-program som Adobe Target, Custom Personalization Destination och Adobe Campaign använder kanter för att leverera personaliserade kundupplevelser i realtid. Data dirigeras till en kant med en projektion, med en projektionsdestination som definierar den kant till vilken data ska skickas och en projektionskonfiguration som definierar den specifika information som ska göras tillgänglig på kanten.

## Terminologi {#terminology}

När du arbetar med kanter måste du känna till följande koncept:

- **Kant**: En kant är en geografiskt placerad server som lagrar data och som gör den lättillgänglig för program.
- **Projektionskonfiguration**: En projektionskonfiguration beskriver hur en viss enhet ska replikeras till kanterna för en viss kund och under vilka förhållanden. För Luma (en exempelkund) bör till exempel bara fälten ålder och kön från datauppsättningen efter profilschemat spridas till kanterna.
- **Kantprojektion**: En kantprojektion är en tillämpning av en projektionskonfiguration på en viss kant på en datadel med ett unikt ID som överensstämmer med ett givet schema för en viss kund. En entitet som till exempel respekterar profilschemat med ID `CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8`, besökare på Lumas webbplats, replikerad till datacentret VA6, som innehåller fälten `age = 35` och `gender = male`.

Med andra ord slussas data till en kant med en projektion, med **projektionsmål** definiera **som** den kant som data skickas till och **projektionskonfiguration** definiera **vad** data skickas till angiven kant.

## Tillgängliga regioner {#regions}

Följande områden kan användas med kant:

- VA6
- ELLER2
- IRL1
- AUS3
- SGP3
- JPN3
- IND1

Alla dessa områden är giltiga alternativ för profiler att landa i.

## Tillgängliga tjänster {#services}

Följande tjänster är aktiverade för profilsökning på kant:

- [Konfiguration av Edge Profile Service](#edge-profile-configuration-service)
- [Projektionsarbetare](#mepw)
- [Express Profile Service](#xps)

### Konfiguration av Edge Profile Service {#edge-profile-configuration-service}

Konfigurationstjänsten för Edge Profile visar API:er för lösningar och program längre fram i kedjan för att skapa projektionskonfigurationer. Du kan använda dessa API:er för att ange attribut och målgrupper för en profil som ska skickas till kanterna, samt de kantområden där projektionen ska skickas. Nu kan du ange **alla** för kantområdena för projektioner.

### Projektionsarbetare {#mepw}

Tjänsten Projection Worker (MEPW) övervakar förändringar som sker i profiler på navet. När du har granskat ändringarna i konfigurationerna förbereder den här tjänsten prognoserna och skickar dem till de tidigare angivna gränsområdena. Dessutom bearbetar den här tjänsten företagets begäranden om uppdatering och skickar de nödvändiga projektionerna till de nödvändiga regionerna. Entitetsuppdateringar används för att säkerställa att entiteten är tillgänglig.

### Express Profile Service {#xps}

Express Profile Service (XPS) hämtar profilerna i olika kanter. Den här tjänsten tar emot förfrågningar från nedströmslösningar, som Adobe Target eller Custom Personalization-mål, och söker upp profilerna från databaserna vid kanterna och skickar den begärda profilen till den begärande lösningen. Om profilen inte hittas skickas en uppdateringsbegäran till det associerade navet.

## Nästa steg

När du har läst den här guiden bör du ha en grundläggande förståelse för kantprofiler, inklusive information om tillgängliga områden och tjänster för kantprofiler. Mer information om Adobe Experience Edge finns i [Edge Network - översikt](../web-sdk/home.md).

## Bilaga

I följande avsnitt visas vanliga frågor om kantprofiler:

### Vilka områden kan kantprofilerna landa i?

Kantprofiler kan landa i olika områden beroende på den aktuella situationen.

För projektionskonfigurationer kommer alla ändringar av profilen att spridas till alla regioner som nämns i profilkonfigurationen.

Dessutom har varje edge-profil ett schemaattribut som kallas användaraktivitetsregion (UAR). Alla kanter som den här profilen har besökt under de senaste 14 dagarna visas i det här profilattributet. När det här attributet finns i en profil skickas därför alla ändringar i profilen också till alla regioner som finns i den övre gränsen för användargränssnittet.

### Hur fungerar utgångsdatum med kantprofiler?

För kantprofiler avgör dataförfallodatumet hur länge profilen ska vara kvar innan den tas bort. Utgångsdatum är **rullande**, vilket innebär att varje gång profilen öppnas på kanten återställs datans förfallotid. Som standard är utgångsdatumet 14 dagar.
