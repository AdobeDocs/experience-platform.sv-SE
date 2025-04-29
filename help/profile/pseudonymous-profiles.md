---
keywords: Experience Platform;hem;populära ämnen;datauppsättning;datauppsättning;tid att leva;ttl;tid till live;pseudonymous;pseudonymous profiles;data expiration;expiration;
solution: Experience Platform
title: Pseudonymt utgångsdatum för profildata
description: Det här dokumentet innehåller allmän vägledning om hur du konfigurerar förfallodatum för pseudonyma profiler inom Adobe Experience Platform.
exl-id: e8d31718-0b50-44b5-a15b-17668a063a9c
source-git-commit: 07786ad7f43c66411e9e167c17daa2baf51a2661
workflow-type: tm+mt
source-wordcount: '1241'
ht-degree: 0%

---

# Förfallodatum för pseudonyma profiler

I Adobe Experience Platform kan du konfigurera förfallotider för pseudonyma profiler så att du automatiskt kan ta bort data från profilarkivet som inte längre är giltiga eller användbara för dina användningsfall.

## Pseudonym profil {#pseudonymous-profile}

>[!CONTEXTUALHELP]
>id="platform_profile_pseudonymousprofile"
>title="Vad är en pseudonym profil?"
>abstract="En pseudonym profil är en profil som har ett pseudonymt eller okänt identitetsnamnutrymme eller en profil som inte har haft någon aktivitet under en viss tid."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_profile_pseudonymousprofile_dataexpiration"
>title="Pseudonymt utgångsdatum för profildata"
>abstract="Förfallodatumet för pseudonyma profildata anger hur många dagar en pseudonym profil kommer att finnas kvar i Adobe Experience Platform innan den tas bort. Värdet måste vara minst 1. Observera att det kan ta upp till tre dagar innan den pseudonyma profilen tas bort."

En profil används för att pseudonyma data ska upphöra att gälla om den uppfyller följande villkor:

- Identitetsnamnutrymmena för den sammanfogade profilen matchar det som kunden har angett som ett pseudonymt eller okänt ID-namnutrymme.
   - Om till exempel profilens ID-namnområde är `ECID`, `GAID` eller `AAID`. Den sammanfogade profilen har inga ID:n från något annat identitetsnamnutrymme. I det här exemplet har en sammanfogad profil **inte** en e-postadress eller CRM-identitet.
- Ingen aktivitet har ägt rum inom en användardefinierad tidsperiod. Aktiviteten definieras antingen av de Experience Events-händelser som importeras eller av kundinitierade uppdateringar av profilattributen.
   - En ny sidvyhändelse eller uppdatering av åldersattribut betraktas till exempel som en aktivitet. En icke användarinitierad uppdatering av målgruppsmedlemskapet betraktas **inte** som en aktivitet. För närvarande baseras spårningen på en profilnivå på tidpunkten för händelsen för Experience Events och tidpunkten för intaget av profilattribut för att beräkna när data förfaller.

## Åtkomst {#access}

>[!AVAILABILITY]
>
>Du måste ha följande behörigheter för att kunna använda den här funktionen:
>
>- Hantera profilinställningar
>- Visa profiler
>
>Med behörigheten **Hantera profilinställningar** kan du ange förfallodatum för data, och med behörigheten **Visa profiler** kan du visa förfallodatum för data.
>
>Mer information om behörigheter i Experience Platform finns i [åtkomstkontrollsöversikten](../access-control/home.md#permissions).

Om du vill lägga till Pseudonymous profile data expiration till din organisation går du till profilkontrollpanelen och väljer **[!UICONTROL Settings]**.

![Knappen Inställningar på profilkontrollpanelen är markerad.](./images/pseudonymous-profiles/profile-settings.png)

[!UICONTROL Profile settings]-pekaren visas. På den här drivrutinen kan du ange antalet dagar för förfallodatum för pseudonyma profildata samt det identitetsnamnutrymme som används för förfallodatum för data.

För produktionssandlådor är standardvärdet för pseudonyma profildata 14 dagar, med det lägsta värdet 1 dag och det högsta värdet 365 dagar. För utvecklingssandlådor är standardvärdet för pseudonyma profildata 3 dagar, med minst 1 dag och högst 365 dagar.

Välj **[!UICONTROL Apply]** om du vill spara dina förfalloinställningar för data.

![Möjligheten att lägga till förfallodatum för pseudonyma profildata i din organisations profiler. Knappen Använd är markerad.](./images/pseudonymous-profiles/profile-settings-data-expiry.png){width="800" zoomable="yes"}

## Vanliga frågor och svar {#faq}

I följande avsnitt visas vanliga frågor om förfallodatum för pseudonyma profiler:

### Hur skiljer sig förfallodatum för pseudonyma profildata från utgångsdatum för Experience Event-data?

+++ Svar

Förfallodatum för pseudonyma profildata och utgångsdatum för upplevelsehändelsedata är komplementära funktioner.

#### Kornighet

Pseudonym förfallotid för profildata fungerar på en **sandbox**-nivå. Därför kommer förfallodatumet för data att påverka alla profiler i sandlådan.

Utgångsdatumet för händelsens data fungerar på en **datamängd**-nivå. Därför kan varje datauppsättning ha olika förfalloinställningar för data.

#### Identitetstyper

Pseudonyma profildata som förfaller **endast** hanterar profiler som har identitetsdiagram som innehåller identitetsnamnutrymmen som valts av kunden, t.ex. `ECID`, `AAID` eller andra typer av cookies. Om profilen innehåller **valfri** ytterligare identitetsnamnrymd som **inte** fanns i kundens lista tas profilen **inte** bort.

Utgångsdatum för Experience Event-data tar bort händelserna **only** baserat på händelsepostens tidsstämpel. Identitetsnamnutrymmena som ingår **ignoreras** i förfallosyfte.

#### Borttagna objekt

Pseudonym förfallotid för profildata tar bort **både** händelse- och profilposter. Detta innebär att även profilklassdata tas bort.

Experience Event-data förfaller **endast** och händelser tas **inte** bort profilklassdata. Profilklassdata tas bara bort när alla data har tagits bort från **alla** datauppsättningar och det finns **inga** profilklassposter kvar för profilen.

+++

### Hur kan pseudonyma profildata som förfaller användas tillsammans med Experience Event-data som förfaller?

+++ Svar

Pseudonyma utgångsdatum för profildata och utgångsdatum för upplevelsehändelsedata kan användas som komplement till varandra.

Du bör **alltid** konfigurera förfallodatum för Experience Event-data i dina datauppsättningar, baserat på dina behov av att lagra data om dina kända kunder. När Experience Event-data har förfallit kan du använda pseudonyma profildata som förfaller för att automatiskt ta bort pseudonyma profiler. Vanligtvis är utgångsdatumet för pseudonyma profiler kortare än utgångsdatumet för Experience Events.

I ett typiskt fall kan du ange att dina Experience Event-data ska upphöra att gälla baserat på värdena för dina kända användardata, och du kan ange att dina pseudonyma profildata ska upphöra att gälla mycket kortare tid för att begränsa effekten av pseudonyma profiler på din Experience Platform licensefterlevnad.

+++

### Vilken typ av användning ska jag använda för att använda pseudonyma profiler som ska förfalla?

+++ Svar

- Om du använder Web SDK för att skicka data direkt till Experience Platform.
- Om du har en webbplats som skickar oautentiserade kunder i stor skala.
- Om du har ett stort antal profiler i datauppsättningarna och har bekräftat att det här stora antalet profiler beror på anonym cookie-baserad ID-namnrymd.
   - För att avgöra detta bör du använda överlappningsrapporten för identitetsnamnutrymme. Mer information om den här rapporten finns i [rapporten om identitetsöverlappning](./api/preview-sample-status.md#identity-overlap-report) i API-handboken för förhandsgranskning av exempelstatus.

+++

### Vad är några kavattar du bör vara medveten om innan du använder pseudonyma profildata?

+++ Svar

- Pseudonym förfallotid för profildata körs på en **sandbox**-nivå. Du kan välja att ha olika konfigurationer för produktions- och utvecklingssandlådor.
- När du har aktiverat den här funktionen är borttagningen av profiler **permanent**. Det finns **inget** sätt att återställa eller återställa de borttagna profilerna.
- Detta är **inte** ett engångsrensningsjobb. Förfallodatum för pseudonyma profildata kommer att köras en gång per dag och profiler som matchar kundens indata tas bort.
- **Alla**-profiler som är definierade som pseudonyma profiler påverkas av att pseudonyma profildata förfaller. Det spelar **ingen** roll om profilen bara är Experience Event eller om den bara innehåller profilattribut.
- Den här rensningen kommer att **endast** ske i profilen. Identitetstjänsten kan fortsätta att visa de borttagna identiteterna i diagrammet efter rensningen om profilen har två eller flera associerade pseudonyma identiteter (till exempel `AAID` och `ECID`). Denna diskrepans kommer att åtgärdas inom den närmaste framtiden.
- Förfallodatum för pseudonyma profildata körs **inte** omedelbart och kan ta upp till tre dagar att bearbeta.

+++

### Hur interagerar Pseudonymous profiler med utgångsdatum för data som skyddas av identitetstjänstdata?

+++ Svar

- Identitetstjänsten [ första-i-och-ut-systemet ](../identity-service/guardrails.md) kan ta bort ECID:n från identitetsdiagrammet, som lagras i identitetstjänsten.
- Om raderingsbeteendet resulterar i att en ECID-profil lagras i kundprofilen i realtid (profilarkivet), kommer pseudonym utgångsinformation att ta bort profilen från profilarkivet.

+++

## Nästa steg

När du har läst den här guiden kan du visa och skapa pseudonyma utgångsdatum för profildata. Mer information om datahantering för Experience Platform som helhet finns i [Handboken ](../landing/license-usage-and-guardrails/data-management-best-practices.md) om god praxis för tillstånd för datahanteringslicenser.
