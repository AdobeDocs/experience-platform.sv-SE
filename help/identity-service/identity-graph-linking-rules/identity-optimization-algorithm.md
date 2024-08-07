---
title: Identitetsoptimeringsalgoritm
description: Lär dig mer om algoritm för identitetsoptimering i identitetstjänsten.
badge: Beta
exl-id: 5545bf35-3f23-4206-9658-e1c33e668c98
source-git-commit: 7daa9191f2e095f01c7c09f02f87aa8724e2e325
workflow-type: tm+mt
source-wordcount: '1565'
ht-degree: 0%

---

# Identitetsoptimeringsalgoritm

>[!AVAILABILITY]
>
>Länkningsregler för identitetsdiagram finns för närvarande i betaversionen. Kontakta ditt Adobe-kontoteam för att få information om deltagandekriterierna. Funktionen och dokumentationen kan komma att ändras.

Identitetsoptimeringsalgoritmen är en diagramalgoritm i identitetstjänsten som hjälper till att säkerställa att ett identitetsdiagram är representativt för en enskild person och därför förhindrar oönskad sammanslagning av identiteter i kundprofilen i realtid.

## Indataparametrar {#input-parameters}

I det här avsnittet finns information om unika namnutrymmen och namnområdesprioritet. Dessa två koncept fungerar som indataparametrar som krävs av identitetsoptimeringsalgoritmen.

### Unikt namnutrymme {#unique-namespace}

Ett unikt namnutrymme avgör vilka länkar som tas bort om diagramkomprimering inträffar.

En sammanfogad profil och dess motsvarande identitetsdiagram ska representera en enskild person (personenhet). En enskild person representeras vanligtvis av CRM-ID:n och/eller inloggnings-ID:n. Förväntningen är att inga två personer (CRM-ID:n) sammanfogas till en enda profil eller diagram.

Du måste ange vilka namnutrymmen som representerar en personenhet i identitetstjänsten med hjälp av algoritmen för identitetsoptimering. Om en CRM-databas till exempel definierar ett användarkonto som ska kopplas till ett enda CRM-ID och en enda e-postadress ser identitetsinställningarna för den här sandlådan ut så här:

* CRM ID-namnområde = unikt
* Namnutrymme för e-post = unikt

Ett namnutrymme som du deklarerar som unikt kommer automatiskt att konfigureras så att det har en maxgräns på ett inom ett givet identitetsdiagram. Om du till exempel deklarerar ett CRM ID-namnutrymme som unikt kan ett identitetsdiagram bara ha en identitet som innehåller ett CRM ID-namnutrymme. Om du inte deklarerar ett namnutrymme som unikt kan diagrammet innehålla mer än en identitet med det namnutrymmet.

>[!NOTE]
>
>* Hushållens representationer (hushållsdiagram) stöds för närvarande inte.
>
>* Alla namnutrymmen som är personidentifierare och som används i sandlådan för att generera identitetsdiagram måste markeras som ett unikt namnutrymme. I annat fall kan du se oönskade länkningsresultat.

### Namnområdesprioritet {#namespace-priority}

Namnområdesprioriteten avgör hur identitetsoptimeringsalgoritmen tar bort länkar.

Namnutrymmen i identitetstjänsten har en implicit relativ prioritetsordning. Tänk dig ett diagram som är strukturerat som en pyramid. Det finns en nod i det övre lagret, två noder i det mellersta lagret och fyra noder i det nedre lagret. Namnområdesprioriteten måste återspegla den här relativa ordningen för att säkerställa att en personentitet representeras korrekt.

Om du vill ha mer information om namnområdesprioritet och dess fullständiga funktioner och användningsområden läser du [prioritetsguiden för namnutrymme](./namespace-priority.md).

![diagramlager och namnområdesprioritet](../images/namespace-priority/graph-layers.png)

## Process {#process}

När nya identiteter hämtas kontrollerar identitetstjänsten om de nya identiteterna och deras motsvarande namnutrymmen följer unika namnutrymmeskonfigurationer. Om konfigurationerna följs fortsätter intaget och de nya identiteterna länkas till diagrammet. Om konfigurationerna inte följs kommer dock identitetsoptimeringsalgoritmen att:

* Infoga den senaste händelsen, med namnområdesprioritet i åtanke.
* Ta bort länken som skulle sammanfoga två personenheter från rätt diagramlager.

## Information om algoritm för identitetsoptimering

När den unika namnutrymmesbegränsningen bryts kommer identitetsoptimeringsalgoritmen att&quot;spela upp&quot; länkarna igen och återskapa diagrammet från början.

* Länkarna sorteras i följande ordning:
   * Senaste händelse.
   * Tidsstämpla med summan av namnområdesprioriteten (lägre summa = högre ordning).
* Diagrammet återskapas baserat på ovanstående ordning. Om länken bryter mot begränsningsbegränsningen (diagrammet innehåller två eller flera identiteter med ett unikt namnutrymme) tas länkarna bort.
* Det resulterande diagrammet kommer sedan att vara kompatibelt med den unika namnutrymmesbegränsningen som du konfigurerade.

![Ett diagram som visualiserar algoritmen för identitetsoptimering.](../images/ido.png)

## Exempelscenarier för algoritm för identitetsoptimering

I följande avsnitt beskrivs hur identitetsoptimeringsalgoritmen fungerar, i scenarier som delad enhet eller inmatning av data med samma tidsstämpel.

### Delad enhet

En delad enhet avser en enhet som används av mer än en person. En delad enhet kan till exempel vara en bärbar dator eller en surfplatta som du delar med en partner eller familjemedlem, en biblioteksdator eller en offentlig kioskdator.

>[!BEGINTABS]

>[!TAB Exempel: ]

| Namnutrymme | Unikt namnutrymme |
| --- | --- |
| CRM-ID | Ja |
| E-post | Ja |
| ECID | Nej |

I det här exemplet anges både CRM-ID och E-post som unika namnutrymmen. På `timestamp=0` kapslas en CRM-postdatauppsättning in och två olika diagram skapas på grund av den unika namnområdeskonfigurationen. Varje diagram innehåller ett CRM-ID och ett e-postnamnutrymme.

* `timestamp=1`: Jane loggar in på din e-handelswebbplats med en bärbar dator. Jane representeras av sitt CRM-ID och sin e-postadress, medan webbläsaren på sin bärbara dator representeras av ett ECID.
* `timestamp=2`: John loggar in på din e-handelswebbplats med samma bärbara dator. John representeras av sitt CRM-ID och sin e-postadress, medan webbläsaren han använde redan representeras av ett ECID. Eftersom samma ECID är länkat till två olika diagram kan identitetstjänsten känna till att den här enheten (den bärbara datorn) är en delad enhet.
* Men på grund av den unika namnområdeskonfigurationen som anger högst ett CRM ID-namnutrymme och ett e-postnamnutrymme per diagram, delas grafen upp i två.
   * Slutligen, eftersom John är den sista autentiserade användaren, förblir det ECID som representerar den bärbara datorn länkat till hans diagram i stället för Jane.

![delat skiftläge för en enhet](../images/identity-settings/shared-device-case-one.png)

>[!TAB Exempel två]

| Namnutrymme | Unikt namnutrymme |
| --- | --- |
| CRM-ID | Ja |
| ECID | Nej |

I det här exemplet är CRM ID-namnutrymmet angivet som ett unikt namnutrymme.

* `timestamp=1`: Jane loggar in på din e-handelswebbplats med en bärbar dator. Hon representeras av sitt CRM-ID och webbläsaren på den bärbara datorn representeras av ECID.
* `timestamp=2`: John loggar in på din e-handelswebbplats med samma bärbara dator. Han representeras av sitt CRM-ID och webbläsaren han använder representeras av samma ECID.
   * Den här händelsen länkar två oberoende CRM-ID:n till samma ECID, vilket överskrider den konfigurerade gränsen för ett CRM-ID.
   * Därför tar identitetsoptimeringsalgoritmen bort den äldre länken, som i det här fallet är Jane CRM-ID som länkades `timestamp=1`.
   * Även om Jane CRM ID inte längre finns som diagram i identitetstjänsten finns det fortfarande som profil i kundprofilen i realtid. Detta beror på att ett identitetsdiagram måste innehålla minst två länkade identiteter, och som ett resultat av att länkarna tas bort har Jane CRM-ID inte längre någon annan identitet att länka till.

![shared-device-case-two](../images/identity-settings/shared-device-case-two.png)

>[!ENDTABS]

### Felaktig e-post

Det finns instanser där en användare kan ange felaktiga värden för e-post och/eller telefonnummer.

| Namnutrymme | Unikt namnutrymme |
| --- | --- |
| CRM-ID | Ja |
| E-post | Ja |
| ECID | Nej |

I det här exemplet är namnutrymmena för CRM-ID och e-post unika. Tänk på scenariot att Jane och John har registrerat sig på din e-handelswebbplats med ett felaktigt e-postvärde (till exempel test<span>@test.com).

* `timestamp=1`: Jane loggar in på din e-handelswebbplats med Safari på sin iPhone, där hon upprättar sitt CRM-ID (inloggningsinformation) och sin ECID (webbläsare).
* `timestamp=2`: John loggar in på din e-handelswebbplats med Google Chrome på sin iPhone och upprättar sitt CRM-ID (inloggningsinformation) och ECID (webbläsare).
* `timestamp=3`: Din datatekniker importerade Jane CRM-post, vilket gör att hennes CRM-ID länkas till den felaktiga e-postadressen.
* `timestamp=4`: Din datatekniker importerar Johns CRM-post, vilket gör att hans CRM-ID länkas till den felaktiga e-postadressen.
   * Detta bryter sedan mot den unika namnområdeskonfigurationen eftersom ett diagram med två CRM ID-namnutrymmen skapas.
   * Som ett resultat av detta tar identitetsoptimeringsalgoritmen bort den äldre länken, som i det här fallet är länken mellan Jane identitet med CRM ID-namnrymden och identiteten med test<span>@test.

Med algoritmen för identitetsoptimering sprids inte felaktiga identitetsvärden som falska e-postmeddelanden eller telefonnummer över flera olika identitetsdiagram.

![felaktig-e-post](../images/identity-settings/bad-email.png)

### Anonym händelseassociation

ECID:n lagrar oautentiserade (anonyma) händelser medan CRM ID lagrar autentiserade händelser. När det gäller delade enheter kopplas ECID (hanterare av oautentiserade händelser) till den **senaste autentiserade användaren**.

Se bilden nedan för att få en bättre förståelse för hur anonym händelseassociation fungerar:

* Kevin och Nora delar en tablett.
   * `timestamp=1`: Kevin loggar in på en e-handelswebbplats med hjälp av sitt konto, vilket skapar hans CRM-ID (inloggningsinformation) och ett ECID (webbläsare). Kevin betraktas nu som den sista autentiserade användaren vid inloggningen.
   * `timestamp=2`: Nora loggar in på en e-handelswebbplats med hjälp av sitt konto och upprättar därmed sitt CRM-ID (inloggningsinformation) och samma ECID. Vid inloggning betraktas nu Nora som den senaste autentiserade användaren.
   * `timestamp=3`: Kevin använder surfplattan för att bläddra på e-handelswebbplatsen, men loggar inte in med sitt konto. Kevin&#39;s browsing activity are stored in the ECID, which in i sin tur is associated with Nora because her is the last authenticated user. Nora äger nu de anonyma händelserna.
      * Tills Kevin loggar in igen kopplas Noras sammanslagna profil till alla oautentiserade händelser som lagras mot ECID (där ECID är den primära identiteten).
   * `timestamp=4`: Kevin loggar in en andra gång. Nu blir han ännu en gång den sista autentiserade användaren och äger även de oautentiserade händelserna:
      * Före den första inloggningen före `timestamp=1`, och
      * Alla aktiviteter han eller Nora gjorde när han bläddrade anonymt mellan Kevin&#39;s första och andra inloggning.

![anon-event-association](../images/identity-settings/anon-event-association.png)


## Nästa steg

Mer information om regler för länkning av identitetsdiagram finns i följande dokumentation:

* [Översikt över regler för länkning av identitetsdiagram](./overview.md)
* [Namnområdesprioritet](./namespace-priority.md)
* [Exempelscenarier för konfiguration av länkningsregler för identitetsdiagram](./example-scenarios.md)
* [Identitetslänkningslogik](../features/identity-linking-logic.md)
* [Identitetstjänst och kundprofil i realtid](../identity-and-profile.md)
