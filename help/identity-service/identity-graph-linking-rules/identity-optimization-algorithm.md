---
title: Identitetsoptimeringsalgoritm
description: Lär dig mer om algoritm för identitetsoptimering i identitetstjänsten.
hide: true
hidefromtoc: true
badge: Alfa
source-git-commit: 8f99dc633c87fa36cc0c5413d23b97b4fce7dbc3
workflow-type: tm+mt
source-wordcount: '1319'
ht-degree: 1%

---

# Identitetsoptimeringsalgoritm

>[!IMPORTANT]
>
>Identitetsoptimeringsalgoritmen finns i Alpha. Funktionen och dokumentationen kan komma att ändras.

Identitetsoptimeringsalgoritmen är en regel som hjälper till att säkerställa att ett identitetsdiagram är representativt för en enskild person och därför förhindrar oönskad sammanslagning av identiteter i kundprofilen i realtid.

## Indataparametrar

En sammanfogad profil och dess motsvarande identitetsdiagram ska representera en enskild person (personenhet). En enskild person representeras vanligtvis av CRM-ID:n och/eller inloggnings-ID:n. Förväntningen är att inga två personer (CRM-ID:n) sammanfogas till en enda profil eller diagram.

Du måste ange vilka namnutrymmen som representerar en personenhet i identitetstjänsten med hjälp av algoritmen för identitetsoptimering. Om en CRM-databas till exempel definierar ett användarkonto som ska kopplas till ett enda CRM-ID och en enda e-postadress ser identitetsinställningarna för den här sandlådan ut så här:

* CRM ID-namnområde = unikt
* Namnutrymme för e-post = unikt

Ett namnutrymme som du deklarerar som unikt kommer automatiskt att konfigureras så att det har en maxgräns på ett inom ett givet identitetsdiagram. Om du till exempel deklarerar ett CRM ID-namnutrymme som unikt kan ett identitetsdiagram bara ha en identitet som innehåller ett CRM ID-namnutrymme.

>[!NOTE]
>
>* För närvarande stöder algoritmen endast användning av en enda inloggningsidentifierare (ett inloggningsnamnutrymme). Flera inloggningsidentifierare (flera identitetsnamnutrymmen används för inloggning), diagram över hushållsenheter och hierarkiska diagramstrukturer stöds för närvarande inte.
>
>* Alla namnutrymmen som är personidentifierare och som används i sandlådan för att generera identitetsdiagram måste markeras som ett unikt namnutrymme. I annat fall kan du se oönskade länkningsresultat.

## Process

När nya identiteter har importerats kontrollerar identitetstjänsten om de nya identiteterna och deras motsvarande namnutrymmen kommer att resultera i att de konfigurerade gränserna överskrids. Om gränserna inte överskrids fortsätter importen av nya identiteter och dessa identiteter länkas till diagrammet. Om emellertid gränserna överskrids kommer identitetsoptimeringsalgoritmen att uppdatera diagrammet så att den senaste tidsstämpeln respekteras och de äldsta länkarna med de lägre prioriteternas namnutrymmen tas bort.

## Exempelscenarier för algoritm för identitetsoptimering

I följande avsnitt beskrivs hur identitetsoptimeringsalgoritmen fungerar, i scenarier som delad enhet eller inmatning av data med samma tidsstämpel.

### Delad enhet

En delad enhet avser en enhet som används av mer än en person. En delad enhet kan till exempel vara en bärbar dator eller en surfplatta som du delar med en partner eller familjemedlem, en biblioteksdator eller en offentlig kioskdator.

>[!BEGINTABS]

>[!TAB Exempel ett]

| Namnutrymme | Gräns |
| --- | --- |
| CRM-ID | 1 |
| E-post | 1 |
| ECID | Ej tillämpligt |

I det här exemplet anges både CRM-ID och E-post som unika namnutrymmen. At `timestamp=0`, är en CRM-postdatauppsättning inkapslad och två olika diagram skapas på grund av begränsningskonfigurationen. Varje diagram innehåller ett CRM-ID och ett e-postnamnutrymme.

* `timestamp=1`: Jane loggar in på din e-handelswebbplats med en bärbar dator. Jane representeras av sitt CRM-ID och sin e-postadress, medan webbläsaren på sin bärbara dator representeras av ett ECID.
* `timestamp=2`: John loggar in på din e-handelswebbplats med samma bärbara dator. John representeras av sitt CRM-ID och sin e-postadress, medan webbläsaren han använde redan representeras av ett ECID. Eftersom samma ECID är länkat till två olika diagram kan identitetstjänsten känna till att den här enheten (den bärbara datorn) är en delad enhet.
* På grund av begränsningskonfigurationen som anger högst ett CRM ID-namnutrymme och ett e-postnamnutrymme per diagram delar identitetsoptimeringsalgoritmen sedan diagrammet i två delar.
   * Slutligen, eftersom John är den sista autentiserade användaren, förblir det ECID som representerar den bärbara datorn länkat till hans diagram i stället för Jane.

![delat enhetsskiftläge ett](../images/identity-settings/shared-device-case-one.png)

>[!TAB Exempel två]

| Namnutrymme | Gräns |
| --- | --- |
| CRM-ID | 1 |
| ECID | Ej tillämpligt |

I det här exemplet är CRM ID-namnutrymmet angivet som ett unikt namnutrymme.

* `timestamp=1`: Jane loggar in på din e-handelswebbplats med en bärbar dator. Hon representeras av sitt CRM-ID och webbläsaren på den bärbara datorn representeras av ECID.
* `timestamp=2`: John loggar in på din e-handelswebbplats med samma bärbara dator. Han representeras av sitt CRM-ID och webbläsaren han använder representeras av samma ECID.
   * Den här händelsen länkar två oberoende CRM-ID:n till samma ECID, vilket överskrider den konfigurerade gränsen för ett CRM-ID.
   * Därför tar identitetsoptimeringsalgoritmen bort den äldre länken, som i det här fallet är Jane CRM ID som länkades på `timestamp=1`.
   * Även om Jane CRM ID inte längre finns som diagram i identitetstjänsten finns det fortfarande som profil i kundprofilen i realtid. Detta beror på att ett identitetsdiagram måste innehålla minst två länkade identiteter, och som ett resultat av att länkarna tas bort har Jane CRM-ID inte längre någon annan identitet att länka till.

![shared-device-case-two](../images/identity-settings/shared-device-case-two.png)

>[!ENDTABS]

### Felaktig e-post

Det finns instanser där en användare kan ange felaktiga värden för e-post och/eller telefonnummer.

| Namnutrymme | Gräns |
| --- | --- |
| CRM-ID | 1 |
| E-post | 1 |
| ECID | Ej tillämpligt |

I det här exemplet är namnutrymmena för CRM-ID och e-post unika. Tänk på scenariot att Jane och John har registrerat sig för din e-handelswebbplats med ett dåligt e-postvärde (till exempel test<span>@test.com).

* `timestamp=1`: Jane loggar in på din e-handelswebbplats med Safari på sin iPhone och upprättar sitt CRM-ID (inloggningsinformation) och sin ECID (webbläsare).
* `timestamp=2`: John loggar in på din e-handelswebbplats med Google Chrome på sin iPhone och upprättar sitt CRM-ID (inloggningsinformation) och ECID (webbläsare).
* `timestamp=3`: Din datatekniker tar emot Jane CRM-post, vilket gör att hennes CRM-ID länkas till den felaktiga e-postadressen.
* `timestamp=4`: Din datatekniker inhämtar Johns CRM-post, vilket gör att hans CRM-ID länkas till den felaktiga e-postadressen.
   * Detta bryter sedan mot de konfigurerade gränserna eftersom ett diagram med två CRM ID-namnutrymmen skapas.
   * Som ett resultat av detta tar identitetsoptimeringsalgoritmen bort den äldre länken, som i det här fallet är länken mellan Jane identitet och CRM ID-namnutrymme och identiteten med test<span>@test.

Med algoritmen för identitetsoptimering sprids inte felaktiga identitetsvärden som falska e-postmeddelanden eller telefonnummer över flera olika identitetsdiagram.

![felaktig e-post](../images/identity-settings/bad-email.png)

### Anonym händelseassociation

ECID:n lagrar oautentiserade (anonyma) händelser medan CRM ID lagrar autentiserade händelser. När det gäller delade enheter kopplas ECID (innehavaren av ej autentiserade händelser) till **senaste autentiserade användare**.

Se bilden nedan för att få en bättre förståelse för hur anonym händelseassociation fungerar:

* Kevin och Nora delar en tablett.
   * `timestamp=1`: Kevin loggar in på en e-handelswebbplats med hjälp av sitt konto och upprättar därmed sitt CRM-ID (inloggningsinformation) och ett ECID (webbläsare). Kevin betraktas nu som den sista autentiserade användaren vid inloggningen.
   * `timestamp=2`: Nora loggar in på en e-handelswebbplats med hjälp av sitt konto och upprättar därmed sitt CRM-ID (inloggningsinformation) och samma ECID. Vid inloggning betraktas nu Nora som den senaste autentiserade användaren.
   * `timestamp=3`: Kevin använder surfplattan för att surfa på e-handelswebbplatsen, men loggar inte in med sitt konto. Kevin&#39;s browsing activity are stored in the ECID, which in i sin tur is associated with Nora because her is the last authenticated user. Nora äger nu de anonyma händelserna.
      * Tills Kevin loggar in igen kopplas Noras sammanslagna profil till alla oautentiserade händelser som lagras mot ECID (där ECID är den primära identiteten).
   * `timestamp=4`Kevin loggar in en andra gång. Nu blir han ännu en gång den sista autentiserade användaren och äger även de oautentiserade händelserna:
      * Före den första inloggningen före `timestamp=1`; och
      * Alla aktiviteter han eller Nora gjorde när han bläddrade anonymt mellan Kevin&#39;s första och andra inloggning.

![anon-event-association](../images/identity-settings/anon-event-association.png)


## Nästa steg

Mer information om regler för länkning av identitetsdiagram finns i följande dokumentation:

* [Översikt över regler för länkning av identitetsdiagram](./overview.md)
* [Exempelscenarier för konfiguration av länkningsregler för identitetsdiagram](./example-scenarios.md)
* [Identitetslänkningslogik](./identity-linking-logic.md)
* [Identitetstjänst och kundprofil i realtid](identity-and-profile.md)
