---
title: Översikt över regler för länkning av identitetsdiagram
description: Lär dig mer om länkningsregler för identitetsdiagram i identitetstjänsten.
hide: true
hidefromtoc: true
badge: Alfa
exl-id: 317df52a-d3ae-4c21-bcac-802dceed4e53
source-git-commit: 20b8433cee719329bce562069c328adb906697a0
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 0%

---

# Översikt över regler för länkning av identitetsdiagram

>[!IMPORTANT]
>
>Länkningsregler för identitetsdiagram finns för närvarande i Alpha. Funktionen och dokumentationen kan komma att ändras.

## Innehållsförteckning

* [Översikt](./overview.md)
* [Identitetsoptimeringsalgoritm](./identity-optimization-algorithm.md)
* [Exempel på scenarier](./example-scenarios.md)
* [Identitetstjänst och kundprofil i realtid](identity-and-profile.md)
* [Identitetslänkningslogik](./identity-linking-logic.md)

Med Adobe Experience Platform Identity Service och Real-Time Customer Profile är det enkelt att anta att dina data är perfekt insamlade och att alla sammanfogade profiler representerar en enskild person via en personidentifierare, till exempel ett CRM-ID. Det finns dock möjliga scenarier där vissa data kan försöka sammanfoga flera olika profiler till en enda profil (&quot;komprimera profil&quot;). För att förhindra dessa oönskade sammanfogningar kan du använda konfigurationer som tillhandahålls via länkningsregler för identitetsdiagram och tillåta korrekt personalisering för dina användare.

## Exempel på scenarier där profilkomprimering kan inträffa

* **Delad enhet**: Delad enhet avser enheter som används av flera personer. Exempel på delade enheter är surfplattor, biblioteksdatorer och kioskdatorer.
* **Felaktiga e-post- och telefonnummer**: Felaktiga e-postadresser och telefonnummer hänvisar till slutanvändare som registrerar ogiltig kontaktinformation, till exempel&quot;test&quot;<span>@test.com för e-post och +1-111-111-1111 för telefonnummer.
* **Felaktiga eller felaktiga identitetsvärden**: Felaktiga eller felaktiga identitetsvärden refererar till icke-unika identitetsvärden som kan sammanfoga CRM-ID:n. IDFA:er måste till exempel ha 36 tecken (32 alfanumeriska tecken och fyra bindestreck), men det finns scenarier där en IDFA med identitetsvärdet &quot;user_null&quot; kan importeras. Telefonnummer har på liknande sätt bara stöd för numeriska tecken, men ett telefonnamnutrymme med identitetsvärdet &quot;inte specificerat&quot; kan kapslas.

Mer information om användningsscenarier för länkningsregler för identitetsdiagram finns i dokumentet om [exempelscenarier](./example-scenarios.md).

## Mål för länkningsregler för identitetsdiagram

Med länkningsregler för identitetsdiagram kan du:

* Skapa ett enskilt identitetsdiagram/sammanfogad profil för varje användare genom att konfigurera unika namnutrymmen (gränser), vilket förhindrar att två olika personidentifierare sammanfogas i ett identitetsdiagram.
* Associera online-autentiserade händelser med personen genom att konfigurera prioriteringar

### Gränser

Ett unikt namnutrymme är en identifierare som representerar en individ, till exempel CRM-ID, inloggnings-ID och hashade e-post. Om ett namnutrymme har angetts som unikt kan ett diagram bara ha en identitet med det namnutrymmet (`limit=1`). Detta förhindrar sammanfogning av två olika personidentifierare i samma diagram.

* Om en gräns inte är konfigurerad kan det leda till oönskade diagramsammanfogningar, till exempel två identiteter med ett CRM ID-namnutrymme i ett diagram.
* Om ingen gräns är konfigurerad kan diagrammet lägga till så många namnutrymmen som behövs så länge diagrammet finns inom skyddsritningarna (50 identiteter/diagram).
* Om en gräns är konfigurerad ser identitetsoptimeringsalgoritmen till att gränsen upprätthålls.

### Identitetsoptimeringsalgoritm

Identitetsoptimeringsalgoritmen är en regel som ser till att begränsningarna upprätthålls. Algoritmen respekterar de senaste länkarna och tar bort de äldsta länkarna för att säkerställa att ett visst diagram hålls inom de gränser som du har definierat.

Nedan följer en lista över algoritmens konsekvenser för hur anonyma händelser kopplas till kända identifierare:

* ECID kopplas till den senast autentiserade användaren om följande villkor uppfylls:
   * Om CRM-ID sammanfogas med ECID (delad enhet).
   * Om begränsningar bara är konfigurerade till ett CRM-ID.

Mer information finns i dokumentet om [algoritm för identitetsoptimering](./identity-optimization-algorithm.md).

### Prioritet

>[!IMPORTANT]
>
>Namnområdesprioriteter är för närvarande inte tillgängliga för alfa.

Du kan använda namnutrymmesprioritet för att definiera vilka namnutrymmen som är viktigare än andra. Den hierarki som du anger för dina namnutrymmen används sedan för att definiera primära identiteter och lagra profilfragment. Om prioritetsinställningar har konfigurerats kommer den primära identitetsinställningen på Web SDK inte längre att användas för att avgöra vilka profilfragment som lagras.

* Gränser och prioritet är oberoende konfigurationer och gör **not** påverka varandra:
   * Gränser är en konfiguration av identitetsdiagram i identitetstjänsten.
   * Prioritet är en profilfragmentskonfiguration i kundprofilen i realtid.
   * Prioritet gör **not** påverka säkerhetsstängningar för identitetsdiagramsystem.

>[!BEGINSHADEBOX]

**Exempel på namnområdesprioritet**

Anta att du har konfigurerat följande prioritet för dina namnutrymmen:

1. CRM-ID: Representerar en användare.
2. IDFA: Representerar en maskinvaruenhet från Apple, till exempel en iPhone och iPad.
3. GAID: Representerar en maskinvaruenhet från Google, till exempel Google Pixel.
4. ECID: Representerar en webbläsare, till exempel Firefox, Safari och Chrome.
5. AAID: Representerar en webbläsare.
Om ECID och AAID skickas samtidigt representerar båda identiteterna samma webbläsare (dubblett).

Om följande upplevelsehändelser är inkapslade i Experience Platform lagras profilfragmenten mot namnutrymmet med högre prioritet.

**Autentiserade händelser:**

* Om identitetskartan innehåller ett ECID, ett GAID och ett CRM ID, lagras händelseinformationen mot CRM ID:t (primär identitet).
   * GAID representerar en maskinvaruenhet från Google (t.ex. Google Pixel), ECID representerar en webbläsare (t.ex. Google Chrome) och CRM ID representerar en autentiserad användare.
   * Om identitetskartan innehåller ett CRM-ID, ett ECID och ett AAID, lagras händelseinformationen mot CRM-ID:t (primär identitet).

**Oautentiserade händelser:**

* Om identitetskartan innehåller ett ECID, IDFA och AAID, lagras händelseinformationen mot IDFA (primär identitet).
   * IDFA representerar en maskinvaruenhet från Apple (t.ex. iPhone), ECID och AAID representerar båda en webbläsare (Safari).

>[!ENDSHADEBOX]

## Nästa steg

Mer information om regler för länkning av identitetsdiagram finns i följande dokumentation:

* [Identitetsoptimeringsalgoritm](./identity-optimization-algorithm.md)
* [Exempelscenarier för konfiguration av länkningsregler för identitetsdiagram](./example-scenarios.md)
* [Identitetstjänst och kundprofil i realtid](identity-and-profile.md)
* [Identitetslänkningslogik](./identity-linking-logic.md)
