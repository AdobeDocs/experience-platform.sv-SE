---
title: Oautentiserad återmarknadsföring på serversidan
description: Lär dig hur du omdirigerar oautentiserade användare med hjälp av ECID
feature: Use Cases, Customer Acquisition
exl-id: 008f4534-29e7-49b9-b0be-9e0c3962ee21
source-git-commit: ba2154e84f24ddf4ec270121bdcbb6dd5d3dff42
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---

# Oautentiserad återmarknadsföring på serversidan {#unauthenticated-retargeting}

I takt med att cookies från tredje part blir mindre effektiva övergår företagen till cookie-lösa lösningar för personaliserat engagemang och återmarknadsföring. Med återmarknadsföring utomhus kan företag nå målmedvetna användare baserat på deras tidigare interaktioner, utan att vara beroende av JavaScript på klientsidan.

## Varför ska man återannonsera oautentiserade besökare? {#why-use-case}

Genom att integrera Adobe Experience Platform Web SDK och händelsevidarebefordran på serversidan kan du effektivisera händelseströmning och datavidarebefordran. Detta gör det möjligt att omdirigera oautentiserade användare på ett smidigt sätt med hjälp av ECID:n (Experience Cloud ID), vilket ger ett konsekvent engagemang på olika plattformar. Med den här lösningen kan ni öka konverteringsmöjligheterna genom att effektivt återannonsera oautentiserade användare baserat på deras tidigare interaktioner.

## Förutsättningar och planering {#prerequisites-and-planning}

Innan du fortsätter med distributionen av Web SDK och konfigurationen av händelsevidarebefordran bör du kontrollera följande:

1. **Adobe med Web SDK-konfiguration**: Adobe Web SDK måste implementeras för att underlätta händelseinsamling och datavidarebefordran.

2. **Adobe Experience Platform Edge Network-konfiguration**: Kontrollera att Edge Network har konfigurerats för stöd för händelsevidarebefordran i realtid för återmarknadsföring utanför webbplatsen.

3. **ECID-synkronisering**: Kontrollera att ECID:n är synkroniserade mellan plattformar för att aktivera sömlös målgruppsmatchning.

## Så här återannonserar du webbplatser {#achieve-offsite-retargeting}

1. **Distribuera Web SDK**: Implementera Adobe Web SDK på din webbplats för att hämta händelsedata i realtid, inklusive användarinteraktioner som sidvisningar, klickningar och andra beteenden.

2. **Aktivera vidarebefordran av händelser**: Konfigurera vidarebefordran av händelser inom plattformen för att skicka insamlade användardata, vilket säkerställer effektiv dataöverföring för målgruppsaktivering.

3. **Konfigurera aktivering på serversidan**: Använd Adobe serversidesfunktioner för att aktivera återmarknadsföring av målgrupper baserat på ECID:n, för att säkerställa korrekt målgruppsanpassning över olika plattformar.

4. **Skapa återmarknadsförda målgrupper**: Använd plattformens målgruppssegmenteringsverktyg för att definiera fokuserade målgrupper baserat på användarbeteende, till exempel vyer, interaktioner eller övergivna kundvagnar.

5. **Aktivera målgrupper**: När målgrupperna har skapats på nytt kan du aktivera dem för att leverera personaliserat innehåll och se till att användarna är engagerade på nytt baserat på deras tidigare interaktioner med webbplatsen.

## Skapa en målgrupp med det beräknade attributet {#create-audience}

För att effektivt återannonsera målgrupper med hög återgivning kan du skapa målgrupper baserat på deras tidigare interaktioner med er webbplats. Använd Platform för att segmentera användare med beräknade attribut.

1. **Identifiera nyckelbeteenden**: Välj användaråtgärder att spåra, till exempel sidvyer eller klick.

2. **Skapa målgrupper**: Använd målgruppssegmenteringsverktyg för att gruppera användare baserat på beteenden.

3. **Synkronisera ECID**: Kontrollera att ECID:n är synkroniserade mellan plattformar för korrekt målgruppsmatchning.

## Aktivera er målgrupp {#activate-audience}

När ni har skapat er målgrupp kan ni aktivera den på olika plattformar för att engagera användarna.

1. **Granska målgrupper**: Se till att målgruppssegmenten återspeglar rätt beteenden.

2. **Skapa aktiveringsregler**: Ange villkor för när och hur användare ska aktiveras baserat på åtgärder.

3. **Push to Platform**: Aktivera målgruppen.

4. **Bildskärmsprestanda**: Spåra målgruppsprestanda och justera efter behov.

## Konfigurera tillägget för omdirigering utanför webbplatsen {#configure-extension}

### Installera SDK för webben

Se till att Adobe Web SDK är ordentligt integrerat i er webbplats. Med denna SDK kan man samla in händelsedata i realtid, vilket är avgörande för en effektiv återmarknadsföring.

### Aktivera vidarebefordran av händelser

Konfigurera en händelsevidarebefordring inom Platform för att skicka insamlade användarbeteendedata till återmarknadsföringsplattformar. Vidarebefordran av händelser säkerställer att data överförs effektivt, vilket gör det möjligt för företag att rikta sig till användare med hög återgivning utan att förlita sig på cookies.

### Koppla till återmarknadsföringsregel

Kontrollera att tillägget för omdirigering utanför webbplatsen är kopplat till en giltig händelseregel i Adobe Experience Platform Data Collection. Vanligtvis bör en global regel skapas för att aktiveras för nyckelåtgärder, som `page load` eller specifika användarinteraktioner.

Mer information om hur du konfigurerar tillägget finns i dokumentationen om [vidarebefordran av händelser](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/getting-started).

## Andra användningsområden {#other-use-cases}

I det här dokumentet finns en översikt över viktiga användningsexempel och tekniska aspekter för att kunna utveckla och använda Web SDK och konfigurationen för händelsevidarebefordran. Genom att följa de beskrivna procedurerna och se till att de nödvändiga förutsättningarna uppfylls kan ni förbättra deras funktioner för dataspårning och -analys avsevärt.

Du kan utforska fler användningsfall som aktiveras via partnerdatasupport i Real-Time CDP:

- [Engagera och skaffa nya kunder](./prospecting.md) med partnerdata.
- [Anpassa upplevelser på plats](./offsite-retargeting.md) med partnerstödd besökarigenkänning.
- [Komplettera förstapartsprofiler](./supplement-first-party-profiles.md) med attribut som tillhandahålls av partner.
