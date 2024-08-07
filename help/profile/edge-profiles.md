---
title: Edge-profiler
description: Lär dig mer om kantprofiler, och relaterad terminologi, tillgängliga områden för kantprofiler samt tillgängliga tjänster för kantprofiler.
exl-id: dcae267f-1d5a-4e90-b634-afd42b0d4edc
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---

# Edge profiler

I Adobe Experience Platform är kundprofilen i realtid den enda källan till sanning för entitetsdata. Profildata ligger i ett centralt nav och tar hänsyn till fall där era data är fullständiga och går att använda. I mer realtidssituationer, där tidskänslighet är viktigare, är dock kantprofiler det bästa alternativet. Edge-profiler är enkla profiler som sitter på kanterna och hjälper till i realtidspersonalisering.

Adobe-program som Adobe Target, Custom Personalization Destination och Adobe Campaign använder kanter för att skapa personaliserade kundupplevelser i realtid. Data dirigeras till en kant med en projektion, där en projektionsdestination definierar den kant till vilken data ska skickas.

## Terminologi {#terminology}

När du arbetar med kanter måste du känna till följande koncept:

- **Edge**: En kant är en geografiskt placerad server som lagrar data och gör dem tillgängliga för program.
- **Edge-projektion**: En kantprojektion är systemprojektionsvyn för en profil på en viss kant för att representera profildata med ett unikt ID som överensstämmer med ett givet schema för en viss kund. En entitet som till exempel respekterar profilschemat med ID `CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8`, besökare på Luma-webbplatsen, replikerad till VA6-datacentret, som innehåller fälten `age = 35` och `gender = male`.

Med andra ord dirigeras data till en kant med en projektion, där **projektionsmålet** definierar **vilken** kant data ska skickas till.

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

- [Projektionsarbetare](#mepw)
- [Express Profile Service](#xps)

### Projektionsarbetare {#mepw}

Tjänsten Projection Worker (MEPW) övervakar förändringar som sker i profiler på navet. När du har granskat ändringarna i konfigurationerna förbereder den här tjänsten prognoserna och skickar dem till de tidigare angivna gränsområdena. Dessutom bearbetar den här tjänsten företagets begäranden om uppdatering och skickar de nödvändiga projektionerna till de nödvändiga regionerna. Entitetsuppdateringar används för att säkerställa att entiteten är tillgänglig.

### Express Profile Service {#xps}

Express Profile Service (XPS) hämtar profilerna i olika kanter. Den här tjänsten tar emot förfrågningar från nedströmslösningar, som Adobe Target eller anpassade Personalization-destinationer, och söker upp profilerna från databaserna vid kanterna och skickar den begärda profilen till den begärande lösningen. Om profilen inte hittas skickas en uppdateringsbegäran till det associerade navet.

## Nästa steg

När du har läst den här guiden bör du ha en grundläggande förståelse för kantprofiler, inklusive information om tillgängliga områden och tjänster för kantprofiler. Mer information om Adobe Experience Edge finns i översikten [Edge Network](../web-sdk/home.md#edge-network).

## Bilaga

I följande avsnitt visas vanliga frågor om kantprofiler:

### Vilka områden kan kantprofilerna landa i?

Edge-profiler kan landa i olika regioner beroende på situationen.

Dessutom har varje edge-profil ett schemaattribut som kallas användaraktivitetsregion (UAR). Alla kanter som den här profilen har besökt under de senaste 14 dagarna visas i det här profilattributet. När det här attributet finns i en profil skickas därför alla ändringar i profilen också till alla regioner som finns i den övre gränsen för användargränssnittet.

### Hur fungerar utgångsdatum med kantprofiler?

För kantprofiler avgör dataförfallodatumet hur länge profilen ska vara kvar innan den tas bort. Utgångsdatumet för data är **rullande**, vilket innebär att varje gång profilen nås på kanten återställs dataförfallotiden. Som standard är utgångsdatumet 14 dagar.

### Vilka data lagras i kantprofilen?

Edge Profile lagrar profilattributen, profil-ID:n och kvalificerade målgrupps-ID:n. Som standard är utgångsdatumet 14 dagar.
