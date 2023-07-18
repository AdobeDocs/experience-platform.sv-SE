---
keywords: Experience Platform;hem;populära ämnen;datauppsättning;datauppsättning;tid att leva;ttl;tid till live;pseudonymous;pseudonymous profiles;data expiration;expiration;
solution: Experience Platform
title: Förfallodatum för pseudonyma profildata
description: Det här dokumentet innehåller allmän vägledning om hur du konfigurerar förfallodatum för pseudonyma profiler inom Adobe Experience Platform.
exl-id: e8d31718-0b50-44b5-a15b-17668a063a9c
source-git-commit: 8ae18565937adca3596d8663f9c9e6d84b0ce95a
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---

# Förfallodatum för pseudonyma profiler

I Adobe Experience Platform kan du konfigurera förfallotider för pseudonyma profiler så att du automatiskt kan ta bort data från profilarkivet som inte längre är giltiga eller användbara i dina fall.

## Pseudonym profil {#pseudonymous-profile}

En profil används för att pseudonyma data ska upphöra att gälla om den uppfyller följande villkor:

- Identitetsnamnutrymmena för den sammanfogade profilen matchar det som kunden har angett som ett pseudonymt eller okänt ID-namnutrymme.
   - Om till exempel profilens ID-namnutrymme är `ECID`, `GAID`, eller `AAID`. Den sammanfogade profilen har inga ID:n från något annat identitetsnamnutrymme. I det här exemplet gör en sammanfogad profil **not** har antingen en e-postadress eller en CRM-identitet.
- Ingen aktivitet har ägt rum inom en användardefinierad tidsperiod. Aktiviteten definieras antingen av de Experience Events-händelser som importeras eller av kundinitierade uppdateringar av profilattributen.
   - En ny sidvyhändelse eller uppdatering av åldersattribut betraktas till exempel som en aktivitet. En uppdatering av ett målgruppsmedlemskap som inte initierats av användaren är dock **not** betraktas som en verksamhet. För närvarande baseras spårningen på en profilnivå på tidpunkten för händelsen för Experience Events och tidpunkten för intaget av profilattribut för att beräkna när data förfaller.

## Åtkomst {#access}

Det går inte att konfigurera förfallodatum för pseudonyma profildata via plattformens gränssnitt eller API:er. Om du vill aktivera den här funktionen måste du kontakta supporten. När du kontaktar supporten, inkludera följande information:

- De identitetsnamnutrymmen som ska användas för pseudonyma profiler tas bort.
   - Till exempel: `ECID` endast, `AAID` eller en kombination av `ECID` och `AAID`.
- Hur lång tid det tar att vänta innan en pseudonym profil tas bort. Standardrekommendationen för kunder är 14 dagar. Det här värdet kan dock variera beroende på ditt användningssätt.

## Frågor och svar {#faq}

I följande avsnitt visas vanliga frågor om förfallodatum för pseudonyma profiler:

### Hur skiljer sig Pseudonymous Profile Data från utgångsdatum från Experience Event data?

Förfallodatum för pseudonyma profildata och utgångsdatum för upplevelsedata är komplementära funktioner.

#### Kornighet

Förfallodatum för pseudonyma profildata fungerar på en **sandlåda** nivå. Därför kommer förfallodatumet för data att påverka alla profiler i sandlådan.

Förfallodatum för Experience Event fungerar på en **datauppsättning** nivå. Därför kan varje datauppsättning ha olika inställningar för när data förfaller.

#### Identitetstyper

Förfallodatum för pseudonyma profildata **endast** hanterar profiler som har identitetsdiagram som innehåller identitetsnamnutrymmen som valts av kunden, t.ex. `ECID`, `AAID`eller andra typer av cookies. Om profilen innehåller **alla** ytterligare ID-namnutrymme som **not** i kundens lista kommer profilen att **not** tas bort.

Utgångsdatum för Experience Event-data tar bort händelser **endast** baserat på händelsepostens tidsstämpel. De identitetsnamnutrymmen som ingår är **ignorerad** för utgångsändamål.

#### Borttagna objekt

Förfallodatum för pseudonyma profiler tar bort **båda** händelse- och profilposter. Detta innebär att även profilklassdata tas bort.

Utgångsdatum för Experience Event-data **endast** tar bort händelser och gör **not** ta bort profilklassdata. Profilklassdata tas bara bort när alla data tas bort från **alla** datauppsättningar och det finns **no** återstående profilklassposter för profilen.

### Hur kan Pseudonymous Profile data förfalla i samband med att Experience Event-data förfaller?

Pseudonyma utgångsdatum för profildata och utgångsdatum för Experience Event-data kan användas som komplement till varandra.

Du borde **alltid** konfigurera Experience Event-dataförfallodatum i era datauppsättningar, baserat på era behov av att lagra data om era kända kunder. När Experience Event-data har förfallit kan du använda Pseudonymous Profile data som förfaller för att automatiskt ta bort pseudonyma profiler. Vanligtvis är dataförfalloperioden för pseudonyma profiler kortare än dataförfalloperioden för Experience Events.

I ett typiskt fall kan du ange att Experience Event-data ska upphöra att gälla baserat på värdena för dina kända användardata, och du kan ange att Pseudonymous-profildata ska ha en mycket kortare varaktighet för att begränsa effekten av pseudonyma profiler på plattformslicensens efterlevnad.

### Vilka användare bör använda pseudonyma profiler när data förfaller?

- Om du använder Web SDK för att skicka data direkt till plattformen.
- Om du har en webbplats som skickar oautentiserade kunder i stor skala.
- Om du har ett stort antal profiler i datauppsättningarna och har bekräftat att det här stora antalet profiler beror på anonym cookie-baserad ID-namnrymd.
   - För att avgöra detta bör du använda överlappningsrapporten för identitetsnamnutrymme. Mer information om den här rapporten finns i [rapportavsnitt om identitetsöverlappning](./api/preview-sample-status.md#identity-overlap-report) av API-handboken för förhandsgranskning av exempelstatus.

### Vad är några kavattar du bör vara medveten om innan du använder pseudonyma profildata?

- Förfallodatum för pseudonyma profildata körs på en **sandlåda** nivå. Du kan välja att ha olika konfigurationer för produktions- och utvecklingssandlådor.
- När du har aktiverat den här funktionen är det **permanent**. Det finns **no** hur du återställer eller återställer borttagna profiler.
- Det här är **not** ett engångsrensningsjobb. Pseudonyma profildata upphör att gälla en gång om dagen och profiler som matchar kundens indata tas bort.
- **Alla** profiler som definieras som pseudonyma profiler påverkas av att pseudonyma profildata upphör att gälla. Det gör det **not** spelar någon roll om profilen bara är Experience Event eller om den bara innehåller profilattribut.
- Rensningen kommer att **endast** inträffar i profilen. Identitetstjänsten kan fortsätta att visa borttagna identiteter i diagrammet efter rensningen om profilen har två eller flera associerade pseudonyma identiteter (till exempel `AAID` och `ECID`). Denna diskrepans kommer att åtgärdas inom den närmaste framtiden.
