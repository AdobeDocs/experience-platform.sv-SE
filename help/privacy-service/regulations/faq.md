---
keywords: Experience Platform;hemmabas;populära ämnen;GDPR;gdpr;CCPA;ccpa;PDPA;pdpa;LGPD;lgpd;faq;FAQ;Regulation;Regulation;Regulations;Regulations;privacy;Privacy;Privacy;
solution: Experience Platform
title: Frågor och svar om sekretessregler
description: Det här dokumentet innehåller svar på vanliga frågor om vilka sekretessregler som stöds och hur de implementeras i Adobe Experience Cloud.
exl-id: ec553e53-664b-4e18-abb1-4e4063fdd2c9
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1599'
ht-degree: 0%

---

# Frågor och svar om sekretessbestämmelser

Det här dokumentet innehåller svar på vanliga frågor om vilka sekretessregler som stöds och hur de implementeras i Adobe Experience Cloud.

>[!NOTE]
>
>Definitioner för de olika termer som används i det här dokumentet finns i [sekretessreglerande terminologi](terminology.md) guide.

## Allmänna frågor

Följande frågor rör alla sekretessbestämmelser som stöds av Experience Cloud.

### Vilka påverkar de sekretessbestämmelser som stöds?

The [sekretessbestämmelser som stöds av Experience Cloud](./overview.md) gäller för alla organisationer som lagrar och behandlar personuppgifter för medborgare inom de olika jurisdiktionerna, oavsett var organisationen befinner sig.

### Vad är personuppgifter?

Personuppgifter är varje information som rör en fysisk person eller en registrerad som kan användas för att direkt eller indirekt identifiera personen. Det kan vara vad som helst från ett namn, ett foto, en e-postadress, bankinformation, inlägg på sociala nätverksplatser, medicinsk information eller en IP-adress till en dator.

Följande identifierare används ofta i Experience Cloud och kan omfattas av sekretesskrav:

* Namn
* Postadress
* Unik personlig identifierare
* Online-ID
* IP-adress
* E-postadress
* Kontonamn

Personlig information kan också omfatta information om internetaktiviteter eller andra aktiviteter i elektroniska nätverk. Detta omfattar, men är inte begränsat till:

* Webbhistorik
* Sökhistorik
* Information om en kunds interaktion med en webbplats, tillämpning eller annons

Även om sekretessbestämmelserna omfattar en mängd personuppgifter, innebär Adobe standardavtalsvillkor att känslig personlig information (som SSN, körkortsinformation, ekonomisk kontoinformation och biometriska data) i allmänhet inte får importeras och användas i Experience Cloud-tillämpningar.

### Vad är skillnaden mellan en personuppgiftsansvarig och en personuppgiftsbiträde?

A **datastyrenhet** är den enhet som fastställer syften, villkor och sätt att behandla personuppgifter, medan **dataprocessor** är en enhet som behandlar personuppgifter för den personuppgiftsansvariges räkning.

A **datastyrenhet** är den person eller organisation som har befogenhet och ansvar att fatta beslut om insamling, användning eller utlämnande av personuppgifter. A **dataprocessor** är den person eller organisation som är verksam i samband med insamling, användning eller utlämnande av personuppgifter och den registeransvariges riktning.

### Vad är skillnaden mellan uttryckligt och otvetydigt samtycke från registrerade?

**Explicit samtycke** hänvisar till en standard för samtycke som inbegriper en specifik, informerad och otvetydig indikation om den registrerades önskemål i oral eller skriftlig form. Enkelt uttryckt måste den registrerade bokstavligen och uttryckligen säga&quot;Jag godkänner&quot; eller&quot;Jag godkänner&quot; för att samtycke ska kunna anses vara explicit. Dessutom måste det vara lika enkelt att dra tillbaka sitt samtycke som att ge det.

**Tvetydigt (underförstått) samtycke** avser samtycke som inte uttryckligen gavs av den registrerade, men som ändå är entydigt till sin natur. Exempel: under registreringsprocessen för ett företags webbplats får man ett meddelande om att den registrerade genom att ange en e-postadress samtycker till att ta emot e-post om specialerbjudanden. Om den registrerade läser meddelandet är den positiva åtgärden att ange sin e-postadress tillräckligt för att betraktas som otvetydigt samtycke.

För många förordningar som GDPR krävs explicit samtycke för att behandla känsliga personuppgifter, där det inte räcker med&quot;deltagande&quot;. För icke-känsliga uppgifter kan dock entydigt (underförstått) samtycke användas.

### Kan registrerade under en viss ålder ge sitt samtycke?

Många integritetsbestämmelser föreskriver att om en registrerad är under en viss ålder kan de inte lagligen ge sitt samtycke till insamling av deras personuppgifter. Enligt vissa bestämmelser kan den som har föräldraansvar för den registrerade i dessa fall ge sitt samtycke, men inte alla. I följande tabell anges den lägsta ålder som de registrerade måste ge sitt eget samtycke till varje förordning, med anmärkningar för ytterligare information:

| Förordning | Ålder för samtycke | Anteckningar |
| --- | --- | --- |
| CCPA (Kalifornien) | 16 | <ul><li>Föräldratillstånd kan endast ges till registrerade personer som är 13 år eller äldre.</li><li>Insamling av personuppgifter från personer under 13 års ålder är strängt förbjuden.</li></ul> |
| GDPR (Europeiska unionen) | 16 | <ul><li>Vissa av EU:s medlemsstater kan för detta ändamål införa en lag om en lägre ålder, dock inte lägre än 13 år.</li><li>Föräldrar måste ge sitt samtycke till alla registrerade under åldersgränsen.</li></ul> |
| LGPD (Brasilien) | 13 | <ul><li>Föräldrar måste ge sitt samtycke till alla registrerade under åldersgränsen.</li><li>En fysisk person som är 13 till 18 år får ge sitt samtycke så länge som behandlingen av deras personuppgifter sker i deras bästa intresse.</li></ul> |
| PDPA (Thailand) | 10 | <ul><li>Föräldrar måste ge sitt samtycke till alla registrerade under åldersgränsen.</li></ul> |

<!-- | New Zealand [!DNL Privacy Act] | 16 | <ul><li>Parental consent must be provided for all data subjects below the age limit in cases where consent is required.</li></ul> | -->

### Hur många dagar måste ett företag svara på en konsumentförfrågan om att få tillgång till eller ta bort personlig information?

Om man utgår ifrån att företaget har samlat in personuppgifter och att det kan autentisera eller verifiera en viss kunds identitet, kan sekretessreglerna medge ett visst tidsintervall för när en konsumentförfrågan kan utföras. I följande tabell visas de tillämpliga tidsintervallen för varje regel, med anmärkningar om några undantag:

| Förordning | Efterlevnadsfönster | Anteckningar |
| --- | --- | --- |
| CCPA (Kalifornien) | 45 dagar |  |
| GDPR (Europeiska unionen) | 30 dagar | Om begäran är komplex, eller om flera förfrågningar har gjorts av samma registrerade, kan begäran förlängas till 60 dagar. |
| LGPD (Brasilien) | 15 dagar |  |
| PDPA (Thailand) | 30 dagar | Om ett företag inte kan besvara en begäran från en registrerad inom efterlevnadsperioden, kommer företaget att ha ytterligare 30 dagar från den dag då de inte kunde besvara en skriftlig begäran till den registrerade. |

<!-- | New Zealand [!DNL Privacy Act] | 20 working days | | -->

### Måste mitt företag utse en dataskyddsombud?

Om din organisations dataåtgärder faller under jurisdiktionerna för GDPR, LGPD eller PDPA måste du utse en dataskyddsombud i följande fall:

* Din organisation är en offentlig myndighet
* Organisationen deltar i storskalig systematisk övervakning
* Din organisation arbetar med storskalig behandling av känsliga personuppgifter.

>[!IMPORTANT]
>
>Till skillnad från andra bestämmelser anger CCPA detta som ett krav. Det rekommenderas dock i allmänhet att ett företag måste ha en kvalificerad individuell datainsamling och lagring av konsumentdata samt svara på kundförfrågningar för att upprätthålla integritetsefterlevnad.

### Hur kan jag stödja konsumentförfrågningar om jag upprätthåller data som omfattas av sekretesslagstiftningen?

När ni har vidtagit de åtgärder som krävs för att autentisera konsumenter som omfattas av lämplig juridisk behörighet, kan ni med Adobe Experience Platform Privacy Service skicka in förfrågningar om konsumentintegritet till kompatibla Experience Cloud-program. Se [[!DNL Privacy Service] översikt](../home.md) för mer information. Mer information om hur dina Experience Cloud-program kan uppfylla sekretesskrav finns i handboken om [Privacy Service och Experience Cloud](../experience-cloud-apps.md).

>[!NOTE]
>
>Ytterligare vägledning från den kaliforniska tillsynsmyndigheten ges fortfarande om vilka typer av uppgifter som kan omfattas av konsumentsekretesskrav.

## CCPA-frågor

Följande frågor gäller specifikt CCPA.

### Hur gäller CCPA:s olika roller och ansvarsområden för Experience Cloud?

Enligt CCPA gäller följande roller Adobe och dess kunder:

* Kunder i Adobe (den part som begär insamling och användning av personuppgifter från personer bosatta i Kalifornien) skulle anses vara en **Företag**.
* Adobe, i sin roll att tillhandahålla tjänsten, skulle anses vara **Tjänsteleverantör**.

Som tjänsteleverantör samlar Adobe in och behandlar personuppgifter för företagets räkning och är enligt avtal bundet att använda dessa uppgifter endast för de särskilda ändamål som anges i avtalet.

Med tanke på detta förhållande och Adobe avtalsspråk skulle utlämnande av information till Adobe sannolikt inte betraktas som en&quot;försäljning&quot; som företag skulle behöva lämna besked om och begära samtycke till.

Adobes tjänster kan dock användas för att möjliggöra viss datadelning och överföring till tredje part. Dessa överföringar från tredje part kan betraktas som&quot;försäljning&quot; och kräver rättsligt utlämnande och samtycke. Kunderna bör samarbeta med sin juridiska rådgivare för att utvärdera specifika användningsfall för att bedöma tillämpliga krav.

### Erbjuder Adobe andra verktyg som kan vara till hjälp för att tillgodose CCPA-kraven?

Adobe Experience Cloud-programmen har funktioner för datahantering och styrning som kan vara till hjälp för företagens integritetsbehov. Bland dessa verktyg finns etikettering av dataanvändning, rollbaserade åtkomstkontroller, IP-förfalskning och hash-funktioner.

Adobe har fått olika certifieringar av sin sekretess- och säkerhetspraxis, till exempel en ISO 27001-certifiering och en TrustArc GDPR-validering.

## GDPR-frågor

Följande frågor gäller specifikt den allmänna dataskyddsförordningen.

### Vad är skillnaden mellan en förordning och ett direktiv?

A **reglering** är en bindande lagstiftningsakt och måste tillämpas i sin helhet i hela EU. A **direktiv** är en lagstiftningsakt som fastställer ett mål som alla EU-länder måste uppnå, men det är de enskilda länderna som bestämmer hur.

Det är viktigt att notera att den allmänna dataskyddsförordningen är en förordning, i motsats till den tidigare lagstiftningen (dataskyddsdirektivet), som är ett direktiv.

### Hur påverkar GDPR policyn kring dataintrång?

Föreslagna förordningar om dataintrång gäller i första hand de delgivningspolicyer som tillämpas av företag som har överträtts. Dataintrång som kan utgöra en risk för enskilda personer måste anmälas till dataskyddsmyndigheten inom 72 timmar och till berörda personer utan onödigt dröjsmål.

## PDPA-frågor

Följande frågor gäller specifikt PDPA.

### Vad är känsliga personuppgifter?

PDF-dokumentet innehåller strikta krav för insamling och lagring av känsliga personuppgifter som omfattar personuppgifter som gäller Ras eller etnisk tillhörighet, politiska åsikter, religiös eller filosofisk övertygelse, kriminalregister, fackliga medlemskap, genetiska uppgifter, biometriska uppgifter, hälsoregister, sexuell läggning eller preferenser.
