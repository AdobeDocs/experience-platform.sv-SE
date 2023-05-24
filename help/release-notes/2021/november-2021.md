---
title: Versionsinformation om Adobe Experience Platform november 2021
description: Versionsinformation november 2021 för Adobe Experience Platform.
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 9%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 17 november 2021**

## Nya funktioner

Nya funktioner i Adobe Experience Platform:

- [Real-Time Customer Data Platform B2B-utgåva](#B2B)
- [(Beta) Aktivera målgruppssegment till batchmål via ad hoc-aktiverings-API](#ad-hoc-activation)

## Uppdateringar av befintliga funktioner

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Attribution AI](#attribution-ai)
- [Kund-AI](#customer-ai)

### Real-Time Customer Data Platform B2B-utgåva {#B2B}

**Releasedatum: 12 november 2021**

Real-Time CDP B2B Edition bygger på Real-time Customer Data Platform (Real-Time CDP) och är särskilt framtagen för marknadsförare som använder en tjänstmodell som bygger på business-to-business. Den sammanför data från flera källor och kombinerar dem i en enda vy över personer och kontoprofiler. Tack vare dessa enhetliga data kan marknadsförarna inrikta sig exakt på specifika målgrupper och engagera dessa målgrupper i alla tillgängliga kanaler.

Det finns förbättringar i en rad olika Adobe Experience Platform-funktioner som skiljer Real-Time CDP B2B Edition från B2C-motsvarigheten. De innehåller förbättringar av Experience Data Model (XDM) för B2B-användningsfall, uppgraderingar av identitetsupplösning och profilsegmentering samt en anpassad anslutning och destination för Marketo Engage. Tack vare Marketo Connector kan B2B-varumärken koppla sina branschledande B2B-interaktionsdata till beteendeinformation för att vårda leads och förbättra kontobaserade marknadsföringsaktiviteter.

-[Nya utgåvor av B2B och B2P](#editions)
-[Nya Marketo datakällor och målanslutningar](#marketo)
-[Standard B2B XDM](#XDM)

### Nya utgåvor av B2B och B2P {#editions}

Nya B2B- och B2P-utgåvor som ger både Real-Time CDP och Platform Activation-produkter B2B-data och -funktionalitet finns att köpa.

Mer information om Real-Time CDP B2B Edition finns i [översikt](../../rtcdp/overview.md).

### Nya Marketo datakällor och målanslutningar {#marketo}

Nya Marketo datakällor- och målanslutningar strömmar Marketo-data till målgrupper på olika plattformar tillbaka till Marketo. Tillgängligt för alla plattformsanvändare.

| Funktion | Beskrivning |
|----------|-------------|
| Marketo Engage-källanslutning | The [Marketo Engage-källanslutning](../../sources/connectors/adobe-applications/marketo/marketo.md) gör det möjligt för marknadsförare att smidigt importera data från en eller flera Marketo-instanser till sin Adobe Experience Platform-instans och erbjuder en komplett lösning för lead-hantering och B2B-marknadsförare. |
| Marketo Engage destination | The [Marketo](../../destinations/catalog/adobe/marketo-engage.md) Med kan marknadsförare skicka segment som skapats i Adobe Experience Platform till Marketo där de visas som statiska listor. |

### Standard B2B XDM {#XDM}

Standardklasser, fältgrupper och datatyper i B2B XDM är tillgängliga för alla plattformsanvändare.

| Funktion | Beskrivning |
|-----------|--------------|
| Standardklasser för B2B XDM | Real-time Customer Data Platform B2B Edition innehåller flera standard-XDM som samlar in information om viktiga B2B-datatabeller, som konton, möjligheter, kampanjer med mera. |

Se [Scheman i Real-time Customer Data Platform B2B Edition](../../rtcdp/schemas/b2b.md) dokumentation för att lära dig mer om att hämta B2B-datatabeller.

### (Beta) Aktivera målgruppssegment till batchmål via ad hoc-aktiverings-API {#ad-hoc-activation}

Med API:t för ad hoc-aktivering kan marknadsförare programmässigt aktivera målgruppssegment till destinationer på ett snabbt och effektivt sätt i situationer där omedelbar aktivering krävs. Ad hoc-målgruppsaktivering stöds endast av [gruppfilsbaserade mål](../../destinations/destination-types.md#file-based) och är för närvarande i betaversion. Mer information finns i [API-dokumentation för ad hoc-aktivering](../../destinations/api/ad-hoc-activation-api.md).

### Attribution AI {#attribution-ai}

Attribution AI används för att attribuera krediter till kontaktpunkter som leder till konverteringshändelser. Detta kan användas av marknadsförare för att kvantifiera marknadsföringseffekten av varje enskild kontaktpunkt för marknadsföring över kundresor.

| Funktion | Beskrivning |
|-----------|---------------|
| Stöd för flera datauppsättningar | Attribution AI kan nu enkelt importera flera datauppsättningar direkt i användargränssnittet utan att behöva mappa och sätta ihop varje datauppsättning. Denna nya tidsbesparande funktion ger kraftfullare och exaktare resultat med data från flera datauppsättningar. |
| Mappning av mediekanal och kampanjfält | Attribution AI har nu stöd för mappning av mediekanal- och kampanjfält. Mediekanalmappning mellan datauppsättningar förbättrar insikterna från Attribution AI och ger tydligare resultat som är enkla att tolka. |

Mer information om Attribution AI finns i [Attribution AI](../../intelligent-services/attribution-ai/overview.md).

### Kund-AI {#customer-ai}

Customer AI available in Real-time Customer Data Platform, is used to generate custom bensipensity scores such as churn and conversion for individual profiles at scale. Detta uppnås utan att man behöver omvandla affärsbehoven till maskininlärningsproblem, välja en algoritm, utbilda eller distribuera.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
|-----------|-------------|
| Stöd för flera datauppsättningar | Kunds-AI kan nu enkelt importera flera datauppsättningar direkt i användargränssnittet utan att behöva mappa och sätta ihop varje datauppsättning. Denna nya tidsbesparande funktion ger kraftfullare och exaktare resultat med data från flera datauppsättningar. |
| Anpassade profilattribut | Kund-AI har nu stöd för att definiera anpassade profildatauppsättningsfält (med tidsstämplar) i dina data utöver vanliga händelsefält. Om du använder det här alternativet kan du lägga till ytterligare profilattribut som du anser vara inflytelserika, vilket kan förbättra modellens kvalitet och ge mer korrekta resultat. |

Mer information om kundens AI finns i [AI-dokumentation för kund](../../intelligent-services/customer-ai/overview.md).
