---
title: Översikt över accelererad butik
description: Lär dig hur du använder den accelererade butiken i Adobe Experience Platform för snabba, SQL-baserade insikter med hjälp av aggregerade data. På den här sidan beskrivs dess avsedda användning, begränsningar av identitets- och BI-data samt bästa praxis för att säkerställa att Adobe policyer för datastyrning följs.
source-git-commit: 5e8dccf91e8c83b4734b363539cfb911b5c2ae29
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---

# Översikt över accelererad butik

Den accelererade butiken i Adobe Experience Platform är ett prestandaoptimerat lagringsskikt som är tillgängligt via Data Distiller SKU. Den är utformad för att rymma föraggregerade datauppsättningar, vilket möjliggör snabb, SQL-baserad kunskap och instrumentpanelsåtergivning.

I det här dokumentet beskrivs hur du använder det accelererade arkivet på rätt sätt, varför aggregerade datauppsättningar är undantagna från standardprocesser för datahygien och det betonas att identitetsdata inte får lagras. Om du vill följa Adobe riktlinjer måste du följa de regler för datastyrning och användningsbegränsningar som beskrivs i det här dokumentet.

## Viktiga funktioner {#key-capabilities}

Den accelererade butiken är specialbyggd för prestanda och effektivitet. Det möjliggör smidiga arbetsflöden för frågor och rapportering genom att fokusera på aggregerade data. Listan nedan visar på dess kärnfunktioner:

- Hantera högpresterande instrumentpaneler och widgetar med SQL-frågor
- Lagra föraggregerade datauppsättningar som utformats för återkommande insikter
- Stöd för anpassad datamodell för rapportering av användningsfall

## Avsedd användning {#intended-use}

Det accelererade arkivet är utformat **enbart** för att lagra aggregerade data som möjliggör effektiv instrumentbordning och visualisering. Dess arkitektur är inte avsedd att stödja komplexa arbetsbelastningar, som bearbetning av affärsinformation eller datalagerhantering.

>[!IMPORTANT]
>
>Det accelererade arkivet ersätter inte datasjön eller en lagringslösning för allmänt bruk.

## Användningsbegränsningar {#usage-restrictions}

För att säkerställa att Adobe datastyrningsmodell och licensvillkor följs gäller följande begränsningar:

- **Lagra inte råa händelsedata**
- **Lagra inte identitetsdata**
- **Lagra inte personligt identifierbar information (PII)** som e-postadresser, vårddata eller kundidentifierare
- **Använd inte det accelererade arkivet för att replikera hela datasjön**

Endast aggregerade, icke-identifierbara data kan lagras i det accelererade arkivet. Aggregerade datauppsättningar kan inte bakåtkompileras för att avslöja originalkälldata, vilket gör dem undantagna från Experience Platform centraliserade datahygiprocesser.

## Styrning och efterlevnad {#governance-and-compliance}

Om du använder den accelererade butiken utanför det avsedda ändamålet kan det innebära en risk för att din organisation bryter mot Adobe licensavtal och gränser för datastyrning. Om datastyrningsincidenter inträffar på grund av användarmönster som inte stöds, tar din organisation det fulla ansvaret.

Adobe kan inte hållas ansvarigt för eventuella konsekvenser som uppstår till följd av felaktig användning av den här funktionen.

Mer information om hur du hanterar data på ett ansvarsfullt sätt i Experience Platform finns i [Styrning, sekretess och säkerhet i Experience Platform](../../../landing/governance-privacy-security/overview.md). På den här sidan beskrivs de tjänster och verktyg som hjälper dig att kontrollera dina upplevelsedata i enlighet med affärspolicyer, juridiska krav och utvecklingsstandarder. Länkar till mer detaljerad vägledning om användningsetiketter och policystyrning finns på [Data Governance overview](../../../data-governance/home.md).

## Bästa praxis {#best-practices}

Följ de rekommenderade bästa sätten för att se till att den accelererade butiken används på ett effektivt och korrekt sätt:

- Använd härledda datauppsättningar för att skapa föraggregerade tabeller som är särskilt anpassade efter dina instrumentpanelsbehov
- Undvik att använda det accelererade arkivet som en mellanlagrings- eller säkerhetskopieringsplats för rådatauppsättningar
- Granska regelbundet användningen för att säkerställa att den överensstämmer med Adobe rekommenderade skyddsräcken

## Nästa steg

Genom att läsa det här dokumentet har du lärt dig vad det accelererade arkivet är, dess avsedda användning för aggregerade data i rapporteringsscenarier och de styrningsregler som måste följas för att säkerställa regelefterlevnad. Utforska följande resurser för att fördjupa din förståelse och tillämpa dessa riktlinjer effektivt:

- [Översikt över SQL-insikter](./overview.md): Lär dig hur SQL-insikter möjliggör prestandaoptimerad rapportering med hjälp av aggregerade datauppsättningar.
- [Skicka accelererade frågor](./send-accelerated-queries.md): Lär dig hur du kör frågor mot det accelererade arkivet för att styra instrumentpaneler och widgetar.
- [Datastyrning och hygien](../../data-governance/overview.md): Granska Adobe policyer för datahygien och riktlinjer för datastyrning för att se till att de används på rätt sätt.
