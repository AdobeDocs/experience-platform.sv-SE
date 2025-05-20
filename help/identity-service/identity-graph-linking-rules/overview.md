---
title: Länkningsregler för identitetsdiagram
description: Lär dig mer om länkningsregler för identitetsdiagram i identitetstjänsten.
exl-id: 317df52a-d3ae-4c21-bcac-802dceed4e53
source-git-commit: 0aefcfbbbed675a08d9e3023b9f667ec59874e46
workflow-type: tm+mt
source-wordcount: '1547'
ht-degree: 0%

---

# [!DNL Identity Graph Linking Rules] översikt {#identity-graph-linking-rules-overview}

>[!CONTEXTUALHELP]
>id="platform_identities_linkingrules_overview"
>title="Länkningsregler för identitetsdiagram"
>abstract="För att förhindra dessa oönskade sammanfogningar kan du använda konfigurationer som tillhandahålls via länkningsregler för identitetsdiagram och tillåta korrekt personalisering för dina användare."

>[!IMPORTANT]
>
>Kontakta Adobe-kontoteamet om du har en befintlig sandlåda som kräver att komprimerade diagram inte är komprimerade (&quot;fasta&quot;) när du har aktiverat identitetsinställningarna.

Med Adobe Experience Platform Identity Service och Real-Time Customer Profile är det enkelt att anta att dina data är perfekt insamlade och att alla sammanfogade profiler representerar en enskild person via en personidentifierare, till exempel ett CRMID. Det finns emellertid möjliga scenarier där vissa data kan försöka sammanfoga flera olika profiler till en enda profil (&quot;komprimera diagram&quot;). För att förhindra dessa oönskade sammanfogningar kan du använda konfigurationer som tillhandahålls via [!DNL Identity Graph Linking Rules] och tillåta korrekt personalisering för dina användare.

## Kom igång

Följande dokument är viktiga för att förstå [!DNL Identity Graph Linking Rules].

* [Optimeringsalgoritm för identitet](./identity-optimization-algorithm.md)
* [Implementeringsguide](./implementation-guide.md)
* [Exempel på diagramkonfigurationer](./example-configurations.md)
* [Felsökning och vanliga frågor](./troubleshooting.md)
* [Namnområdesprioritet](./namespace-priority.md)
* [Gränssnitt för diagramsimulering](./graph-simulation.md)
* [Användargränssnitt för identitetsinställningar](./identity-settings-ui.md)

## Videobibliotek

Titta på följande videofilmer för att lära dig mer om några av de grundläggande aspekterna i Länkningsregler för identitetsdiagram.

<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Identity Graph Linking Rules: Overview">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="https://video.tv.adobe.com/v/3448250/?learn=on&enablevpops" title="Länkningsregler för identitetsdiagram: Översikt" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3429845/?format=jpeg&nocache=1732633205780" alt="Länkningsregler för identitetsdiagram: Översikt"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="https://video.tv.adobe.com/v/3448250/?learn=on&enablevpops" target="_blank" rel="referrer" title="Länkningsregler för identitetsdiagram: Översikt">Länkningsregler för identitetsdiagram: Översikt</a>
                    </p>
                    <p class="is-size-6">I den här videon visas en översikt över länkningsregler för identitetsdiagram. Du lär dig hur du kan använda den här funktionen för att förhindra komprimering av diagram.</p>
                </div>
                <div style="display: flex; flex-direction; row;">
                  <a href="https://video.tv.adobe.com/v/3448250/?learn=on&enablevpops" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                      <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Bevakning</span>
                  </a>
                  <a href="./overview.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="margin-top: 1rem; margin-left: 0.5rem;">
                      <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Läs</span>
                  </a>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Identity Graph Linking Rules: Identity Settings">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="https://video.tv.adobe.com/v/3458487/?learn=on&enablevpops" title="Länkningsregler för identitetsdiagram: identitetsinställningar" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3441066/?format=jpeg&nocache=1732633205785" alt="Länkningsregler för identitetsdiagram: identitetsinställningar"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="https://video.tv.adobe.com/v/3458487/?learn=on&enablevpops" target="_blank" rel="referrer" title="Länkningsregler för identitetsdiagram: identitetsinställningar">Länkningsregler för identitetsdiagram: Identitetsinställningar</a>
                    </p>
                    <p class="is-size-6">I den här videon får du lära dig hur du konfigurerar dina identitetsinställningar och skapar högkvalitativa identitetsdiagram och kundprofiler för Adobe Experience Platform-program som Real-Time CDP, Adobe Journey Optimizer och Customer Journey Analytics.</p>
                </div>
                <div style="display: flex; flex-direction: row;">
                  <a href="https://video.tv.adobe.com/v/3458487/?learn=on&enablevpops" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                      <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Bevakning</span>
                  </a>
                  <a href="identity-settings-ui.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="margin-top: 1rem; margin-left: 0.5rem;">
                      <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Läs</span>
                  </a>
                </div>            
            </div>
        </div>
    </div>
</div>

## Diagramkomprimeringsscenarier {#graph-collapse-scenarios}

>[!CONTEXTUALHELP]
>id="platform_identities_graphcollapsescenarios"
>title="Diagram, komprimera scenarier"
>abstract="Det finns flera orsaker till varför diagram kan&quot;komprimera&quot; eller representera flera personenheter."

I det här avsnittet beskrivs exempelscenarier som du kan överväga när du konfigurerar [!DNL Identity Graph Linking Rules].

### Delad enhet

Det finns instanser där flera inloggningar kan förekomma på en enda enhet:

| Delad enhet | Beskrivning |
| --- | --- |
| Familjedatorer och surfplattor | Man och hustru loggar båda in på sina respektive bankkonton. |
| Publik kiosk | Resenärer på en flygplats som loggar in med sitt lojalitets-ID för att checka in väskor och skriva ut boardingkort. |
| Callcenter | Anställda på kundtjänst loggar in på en enda enhet för kunder som ringer kundsupport för att lösa problem. |

![Ett diagram över vissa delade enheter.](../images/identity-settings/shared-devices.png)

I dessa fall kommer ett enda ECID att länkas till flera CRMID från en diagramsynvinkel utan att några gränser är aktiverade.

Med [!DNL Identity Graph Linking Rules] kan du:

* Konfigurera det ID som används för inloggning som unik identifierare. Du kan t.ex. begränsa ett diagram så att bara en identitet lagras med ett CRMID-namnutrymme och därmed definiera det CRMID:t som den unika identifieraren för en delad enhet.
   * På så sätt kan du se till att CRMID inte sammanfogas med ECID.

### Ogiltiga e-post-/telefonscenarier

Det finns även instanser av användare som anger falska värden som telefonnummer och/eller e-postadresser när de registrerar sig. I dessa fall, om begränsningar inte är aktiverade, kommer telefon-/e-postrelaterade identiteter att länkas till flera olika CRMID:n.

![Ett diagram som representerar ogiltiga e-post- eller telefonscenarier.](../images/identity-settings/invalid-email-phone.png)

Med [!DNL Identity Graph Linking Rules] kan du:

* Konfigurera antingen CRMID, telefonnummer eller e-postadress som unik identifierare och begränsa därmed en person till endast ett CRMID, telefonnummer och/eller e-postadress som är kopplad till deras konto.

### Felaktiga eller felaktiga identitetsvärden

Det finns fall där icke-unika, felaktiga identitetsvärden är inkapslade i systemet, oavsett namnutrymme. Exempel:

* IDFA-namnutrymme med identitetsvärdet &quot;user_null&quot;.
   * IDFA-identitetsvärden ska innehålla 36 tecken: 32 alfanumeriska tecken och fyra bindestreck.
* Namnområde för telefonnummer med identitetsvärdet &quot;ej angivet&quot;.
   * Telefonnummer får inte innehålla några alfabet.

Dessa identiteter kan resultera i följande diagram, där flera CRMID sammanfogas med den felaktiga identiteten:

![Ett diagramexempel på identitetsdata med felaktiga eller felaktiga identitetsvärden.](../images/identity-settings/bad-data.png)

Med [!DNL Identity Graph Linking Rules] kan du konfigurera CRMID som den unika identifieraren för att förhindra att oönskade profiler komprimeras på grund av den här datatypen.

## [!DNL Identity Graph Linking Rules] {#identity-graph-linking-rules}

Med [!DNL Identity Graph Linking Rules] kan du:

* Skapa ett enskilt identitetsdiagram/sammanfogad profil för varje användare genom att konfigurera unika namnutrymmen, vilket förhindrar att två olika personidentifierare sammanfogas i ett identitetsdiagram.
* Associera online-autentiserade händelser med personen genom att konfigurera prioriteringar

### Terminologi {#terminology}

| Terminologi | Beskrivning |
| --- | --- |
| Unikt namnutrymme | Ett unikt namnutrymme är ett identitetsnamnutrymme som har ställts in för att vara distinkt i sammanhanget för ett identitetsdiagram. Du kan konfigurera ett namnutrymme så att det är unikt med användargränssnittet. När ett namnutrymme definieras som unikt kan ett diagram bara ha en identitet som innehåller det namnutrymmet. |
| Namnområdesprioritet | Namnområdesprioritet avser den relativa vikten av namnutrymmen jämfört med varandra. Namnområdesprioriteten kan konfigureras via användargränssnittet. Du kan rangordna namnutrymmen i ett givet identitetsdiagram. När den är aktiverad används namnprioritet i olika scenarier, t.ex. indata för algoritmen för identitetsoptimering och fastställande av primär identitet för händelsesegment för upplevelser. |
| Optimeringsalgoritm för identitet | Med algoritmen för identitetsoptimering säkerställs att riktlinjer som skapas genom att konfigurera en unik namnområdes- och namnområdesprioritet används i ett givet identitetsdiagram. |

### Unikt namnutrymme {#unique-namespace}

Du kan konfigurera ett namnutrymme så att det blir unikt med hjälp av arbetsytan för identitetsinställningar i användargränssnittet. Om du gör det informeras identitetsoptimeringsalgoritmen om att ett visst diagram bara kan ha en identitet som innehåller det unika namnutrymmet. Detta förhindrar sammanfogning av två olika personidentifierare i samma diagram.

Tänk på följande scenario:

* Scott använder en surfplatta och öppnar sin webbläsare Google Chrome för att gå till acme<span>.com, där han loggar in och bläddrar efter nya basketskor.
   * Bakom scenerna loggar det här scenariot följande identiteter:
      * Ett ECID-namnutrymme och -värde som representerar webbläsarens användning
      * Ett CRMID-namnutrymme och -värde som representerar den autentiserade användaren (Scott loggade in med sin kombination av användarnamn och lösenord).
* Hans son Peter använder sedan samma surfplatta och även Google Chrome för att åka till acme<span>.com, där han loggar in med sitt eget konto för att söka efter fotbollsutrustning.
   * Bakom scenerna loggar det här scenariot följande identiteter:
      * Samma ECID-namnutrymme och värde som representerar webbläsaren.
      * Ett nytt CRMID-namnutrymme och värde som representerar den autentiserade användaren.

Om CRMID har konfigurerats som ett unikt namnutrymme delas CRMID:n upp i två separata identitetsdiagram i identitetsoptimeringsalgoritmen, i stället för att sammanfoga dem.

Om du inte konfigurerar ett unikt namnutrymme kan du få oönskade diagramsammanfogningar, till exempel två identiteter med samma CRMID-namnutrymme, men olika identitetsvärden (scenarier som dessa representerar ofta två olika personenheter i samma diagram).

Du måste konfigurera ett unikt namnutrymme för att informera algoritmen för identitetsoptimering om du vill tillämpa begränsningar för identitetsdata som är inkapslade i ett visst identitetsdiagram.

### Namnområdesprioritet {#namespace-priority}

Namnområdesprioritet avser den relativa vikten av namnutrymmen jämfört med varandra. Namnområdesprioriteten kan konfigureras via användargränssnittet och du kan rangordna namnutrymmen i ett givet identitetsdiagram.

Ett sätt som namnområdesprioriteten används på är att fastställa den primära identiteten för händelsefragment (användarbeteende) i kundprofilen i realtid. Om prioritetsinställningar har konfigurerats kommer den primära identitetsinställningen på Web SDK inte längre att användas för att avgöra vilka profilfragment som lagras.

Både unika namnutrymmen och namnområdesprioriteter kan konfigureras på arbetsytan för identitetsinställningar. Effekterna av deras konfigurationer är dock annorlunda:

| | Identitetstjänst | Kundprofil i realtid |
| --- | --- | --- |
| Unikt namnutrymme | I identitetstjänsten refererar algoritmen för identitetsoptimering till unika namnutrymmen för att fastställa vilka identitetsdata som är inkapslade i ett visst identitetsdiagram. | Unika namnutrymmen påverkar inte kundprofilen i realtid. |
| Namnområdesprioritet | I identitetstjänsten avgör namnområdesprioriteten att rätt länkar tas bort för diagram som har flera lager. | När en upplevelsehändelse kapslas in i en profil blir det namnutrymme som har högst prioritet den primära identiteten för profilfragmentet. |

* Namnområdesprioriteten påverkar inte diagrambeteendet när gränsen på 50 identiteter per diagram nås.
* **Namnområdesprioriteten är ett numeriskt värde** som tilldelats ett namnutrymme och anger dess relativa betydelse. Detta är en egenskap för ett namnutrymme.
* **Primär identitet är den identitet i vilken ett profilfragment lagras mot**. Ett profilfragment är en datapost som lagrar information om en viss användare: attribut (som vanligtvis hämtas via CRM-poster) eller händelser (som vanligtvis hämtas från upplevelsehändelser eller onlinedata).
* Namnområdesprioriteten avgör den primära identiteten för händelsesegment för upplevelser.
   * För profilposter kan du använda arbetsytan för scheman i Experience Platform-gränssnittet för att definiera identitetsfält, inklusive den primära identiteten. Mer information finns i guiden [Definiera identitetsfält i användargränssnittet](../../xdm/ui/fields/identity.md).
* Om en upplevelsehändelse har två eller flera identiteter med den högsta namnområdesprioriteten i identityMap, kommer den att nekas att matas in eftersom den betraktas som &quot;felaktiga data&quot;. Om identityMap till exempel innehåller `{ECID: 111, CRMID: John, CRMID: Jane}` kommer hela händelsen att avvisas som felaktiga data eftersom det betyder att händelsen är kopplad till både `CRMID: John` och `CRMID: Jane` samtidigt.

Mer information finns i handboken om [namnområdesprioritet](./namespace-priority.md).

## Nästa steg

Mer information om [!DNL Identity Graph Linking Rules] finns i följande dokumentation:

* [Optimeringsalgoritm för identitet](./identity-optimization-algorithm.md)
* [Implementeringsguide](./implementation-guide.md)
* [Exempel på diagramkonfigurationer](./example-configurations.md)
* [Felsökning och vanliga frågor](./troubleshooting.md)
* [Namnområdesprioritet](./namespace-priority.md)
* [Gränssnitt för diagramsimulering](./graph-simulation.md)
* [Användargränssnitt för identitetsinställningar](./identity-settings-ui.md)