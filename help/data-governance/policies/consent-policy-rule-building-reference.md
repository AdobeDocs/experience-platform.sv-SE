---
title: Referens för skapande av regel för samtycke
description: Lär dig hur du använder XDM-datatyper, operatorer som stöds och avancerad logik för att skapa detaljerade policyregler för samtycke i Adobe Experience Platform användargränssnitt.
source-git-commit: 678220b14cefd4dd31ef7a12355d796575a77a50
workflow-type: tm+mt
source-wordcount: '1576'
ht-degree: 0%

---

# Referens för policyregelbygge för samtycke

Använd den här referensen för avancerad regellogik för att ange exakta, juridiskt giltiga regler i **[!UICONTROL Then]**-satsen i verktyget för samtycke i Adobe Experience Platform.

![Gränssnittet för principbyggaren för medgivande markerar avsnittet [!UICONTROL Then] , där användarna definierar regelvillkor.](../images/policies/multiple-rules.png)

Lär dig hur policyregler gäller för er samtyckesdatas struktur och typer så att ni kan tillämpa era preferenser för kundgodkännande korrekt.

Läs det här dokumentet för att lära dig hur du filtrerar profiler baserat på samtycke genom att navigera i behållarfält i XDM-schemat och välja ett primitivt fält. Använd sedan lämplig operator för att definiera exakt vilket värde en profil måste matcha.

## Förhandskrav

Innan du använder den här referensen måste du se till att din inställning av samtyckespolicy är fullständig och att du förstår grundbegreppen för Adobe Experience Platform dataarkitektur och styrningsramverk.

Kontrollera att du uppfyller följande krav:

* **Principinstallationen har slutförts**: Du har skapat eller börjat skapa en medgivandeprincip i Adobe Experience Platform-gränssnittet. Detaljerade steg finns i användarhandboken för [dataanvändningsprinciper](user-guide.md#consent-policy).

* **Bekanta dig med datastrukturer**: Den här referensen kräver att du har kunskap om följande grundläggande begrepp:
   * **XDM och unionsschema**: Förstå hur Experience Data Model definierar datarelationer och hur unionsschemat representerar enhetliga kundprofiler. Mer information finns i [översikten över XDM-systemet](../../xdm/home.md).
   * **Datastyrningsramverk**: Se hur Adobe Experience Platform tillämpar dataanvändningsprinciper och styrningsregler. Mer information finns i [Översikt över datastyrning](../home.md).
   * **Bearbetning av kundsamtycke**: Förstå hur data om samtycke samlas in, lagras och används i arbetsflöden för kundupplevelser. Se översikten över [godkännandebearbetning](../../landing/governance-privacy-security/consent/adobe/overview.md).

## Grundbegrepp: primitiva fält och behållarfält

Läs det här avsnittet för att lära dig hur regler för medgivandeprinciper använder olika fälttyper i XDM-scheman. Genom att förstå skillnaden mellan behållar- och primitiva fält kan du välja rätt fält och operator när du definierar policyvillkor.

### Fälttyper och regellogik som stöds

Samtyckesprinciper har stöd för flera fälttyper, där var och en har specifika operatorer för att skapa regelvillkor. Fälttyper grupperas i två kategorier: **behållartyper** och **primitiva typer**.

### Behållartyper (schemanavigering)

Behållartyper organiserar medgivandedata men kan inte användas direkt i policyvillkor. De fungerar som navigeringssökvägar för att nå de primitiva fält som innehåller faktiska värden.

| Behållartyp | Beskrivning |
|----------------|-------------|
| **Objekt** | En behållare med ett fast schema som innehåller flera fält av olika typer. |
| **Array** | En behållare som innehåller flera värden av samma typ. |
| **Karta** | En behållare med dynamiska nycklar som kan innehålla objekt eller andra fälttyper. |

>[!IMPORTANT]
>
>Behållarfält kan inte väljas direkt i villkoren för medgivandeprincipen. Du måste navigera i behållare för att kunna välja **primitiva fält** (till exempel sträng, tal eller booleskt) för regelgenerering. Behållaroperatorer används bara för schemavigering, inte för att ange principvillkor.

### Primitiva typer (regelvillkor)

Primitiva fält innehåller de faktiska värdena för data för medgivande (till exempel `true` eller `"weekly"`) och är de enda fälttyperna som kan användas för att definiera policyvillkor.

Tabellen nedan beskriver alla primitiva typer som stöds och de tillgängliga operatorerna.

| Primitiv typ | Operatorer som stöds | Beskrivning |
|----------------|---------------------|-------------|
| **Sträng** | `is equal to`, `is not equal to`, `exists`, `does not exist` | Textbaserade medgivandeattribut. |
| **Number** | `is equal to`, `is not equal to`, `is greater than`, `is less than`, `exists`, `does not exist` | Numeriska medgivandeattribut. |
| **Boolean** | `is equal to`, `is not equal to` | Sant eller falskt medgivandevärde. |
| **Datum** | `is equal to`, `is not equal to`, `exists`, `does not exist` | Datumbaserade medgivandeattribut. |


## Arbeta med komplexa datastrukturer

Läs det här avsnittet för att lära dig hur du navigerar i kapslade behållare i ditt medgivandeschema för att nå primitiva fält. Här presenteras vanliga schemamönster och förklarar hur djupare strukturer möjliggör mer detaljerad godkännandelogik.

### Hantera kapslade och komplexa schemastrukturer

Komplexa medgivandescheman innehåller ofta kapslade behållarstrukturer som stöder flexibel och skalbar datahantering. Eftersom principregler bara kan referera till primitiva fält måste du navigera genom behållarhierarkier för att nå de fält som kan användas i villkoren för medgivandeprincipen. Djupare kapsling möjliggör mer detaljerad och specifik regelanpassning.

Vanliga kapslade behållarmönster:

* **Karta över karta** - Dynamiska nycklar som innehåller andra kartor.
* **Karta över objekt** - Dynamiska nycklar som innehåller objekt med fasta scheman.
* **Matris med karta** - Matriser som innehåller kartor med dynamiska nycklar.
* **Array med objekt** - arrayer som innehåller objekt med fasta scheman.
* **Objekt med mappnings- eller matrisegenskaper** - Objekt som innehåller mappnings- eller matrisfält.

### Exempel på fältstruktur

Följande struktur fungerar som visuell referens för regelexempel i den här handboken.

```
consent.marketing (Object)
├── email (Boolean)
├── sms (Boolean)
├── preferences (Map with dynamic keys)
│   ├── "email_preferences" (Object)
│   │   ├── frequency (String)
│   │   └── channels (Array of Strings)
│   ├── "sms_preferences" (Object)
│   │   ├── frequency (String)
│   │   └── opt_in_time (Date)
│   └── "push_preferences" (Object)
│       ├── frequency (String)
│       └── categories (Array of Strings)
└── lastUpdated (Date)
```

## Avancerad regeluppbyggnad efter fälttyp

I det här avsnittet finns detaljerade riktlinjer om hur du skapar regler för samtycke baserat på fälttyp. Du får lära dig hur du konfigurerar regellogik för booleska operatorer, kartor, objekt och arrayer för att få exakta villkor för samtycke.

### Regelbyggandekomponenter och -steg

För att skapa effektiva policyregler för samtycke måste du förstå hur du navigerar i schemastrukturen och använder rätt operatorer för varje fälttyp. Varje regel följer samma grundläggande tillvägagångssätt: navigera till ett primitivt fält, välj lämplig operator och definiera det villkor som måste uppfyllas.

Så här skapar du en regel:

1. **Välj ett fält** - Navigera genom behållarfälten för att nå ett primitivt fält.
2. **Välj en operator** - Välj den operator som stöds av fälttypen.
   ![Den hierarkiska schemanavigeringspanelen, som visar en användare som expanderar en behållare för att nå ett primitivt fält.](../images/policies/consent-policy-map-field.png)
3. **Ange ett värde** - Definiera det värde eller villkor som ska matchas.
4. **Matcha kartnycklar** - Välj om du vill ange en specifik nyckel eller matchning för alla nycklar på en karta.
5. **Lägg till villkor** - Kombinera flera regler med AND eller OR-logik efter behov.

### Arbeta med booleska fält (implicit medgivandelogik)

Booleska fält lagrar sanna eller falska medgivandevärden och representerar de vanligaste medgivandeattributen. Operatorn `is not equal to` gör att du kan inkludera profiler som inte uttryckligen har avanmält sig, som stöder implicita scenarier för samtycke.

**Booleska operatorer och resultat**

| Operatör | Värde | Resultat |
|----------|-------|--------|
| `is equal to` | `true` | Inkluderar profiler med explicit samtycke (`true`). |
| `is equal to` | `false` | Inkluderar profiler med explicit avanmälan (`false`). |
| `is not equal to` | `true` | Inkluderar profiler utan explicit samtycke (`false` eller saknas). |
| `is not equal to` | `false` | Innehåller profiler som inte uttryckligen har avanmält sig (`true` eller saknas). |

**Exempel: Implicit e-postmedgivande**

```
Field: consent.marketing.email (boolean)
Operator: is not equal to
Value: false
Result: Includes profiles who have not explicitly opted out of email marketing (includes both true and missing/null values).
```

### Arbeta med kartfält (dynamiska inställningar)

Kartfält lagrar nyckelvärdepar med dynamiska nycklar, till skillnad från objekt med fasta scheman. Kartor används ofta i inställningscenter där nya kategorier kan läggas till utan schemauppdateringar. Du kan ange specifika tangenter som mål eller använda jokerteckenmatchning för alla tangenter.

**Specifik nyckelmatchning**

Använd det här sättet för att ange en specifik inställningskategori som mål.

```
Field: consent.preferences["email_preferences"].frequency (string) - navigated to from the map container
Operator: is equal to
Value: "weekly"
Result: Includes profiles who set the email frequency to weekly (for the "email_preferences" key)
```

**Valfri nyckelmatchning**

Använd kryssrutealternativet **[!UICONTROL find any matching item]** om du vill matcha alla dynamiska nycklar på en karta.

![Principregelbyggaren visar kryssrutan Sök efter matchande objekt för kartfält, som används för att matcha värden för alla dynamiska nycklar.](../images/policies/find-any-matching-item.png)

```
Field: consent.preferences.*.frequency (string)
Operator: is equal to
Value: "weekly"
Result: Includes profiles who set frequency to weekly in ANY preference category (for example, email_preferences, sms_preferences, or push_preferences)
```

### Arbeta med objektfält (fast navigering)

Objektfält fungerar som behållare med fasta scheman. De används bara för navigering och kan inte refereras direkt i principvillkor.

**Exempel på navigering**

```
consent.marketing (object) → consent.marketing.email (boolean)
```

**Exempel på användningsfall:**

```
Field: consent.marketing.email (Boolean) - navigated to from the object
Operator: is equal to
Value: true
Result: Include profiles who have explicitly consented to marketing emails
```


### Arbeta med arrayfält (flera värden)

Matrisfält innehåller flera värden av samma typ och kräver olika hantering beroende på om de lagrar primitiva värden eller objekt. Navigerings- och operatoralternativen varierar beroende på arraytyp.

**Exempel på matris med primitiva värden**

Använd operatorn `contains` för att identifiera profiler baserat på specifika värden i en array.

```
Field: consent.communication_channels (array of strings)
Operator: contains
Value: "email"
Result: Include profiles who have consented to email communication
```

**Exempel på array med objekt**

Navigera till arrayen för att komma åt primitiva fält i kapslade objekt.

```
Field: consent.preferences["email_preferences"].categories[].type - navigated to from the array
Operator: is equal to
Value: "promotional"
Result: Include profiles where any email category is "promotional"
```

## Kombinera regler med komplex logik

I det här avsnittet beskrivs hur du kombinerar flera regelvillkor med AND eller OR-logik. Du får lära dig hur logiska operatorer arbetar tillsammans för att definiera avancerade policyer för godkännande av flera villkor.

### Kombinera flera villkor (OCH eller OR-logik)

Du kan kombinera flera regelvillkor med AND eller OR-logik för att skapa mer sofistikerade medgivandeprinciper som riktar sig till specifika profilsegment.\
**AND-logik** kräver att alla villkor är sanna, vilket ger snävare målgruppsmatchningar.\
**OR-logik** tillåter alla villkor att vara sanna, vilket utökar målgruppens räckvidd.

I gränssnittet för principen för samtycke använder du den logikväljare som visas mellan regelvillkoren för att växla mellan AND och OR-logik.

### Exempel på allmän, komplex regel

I följande exempel kombineras grundläggande medgivandestatus med inställningsfrekvens för att skapa ett riktat segment.

```
Field: consent.marketing.email
Operator: is equal to true
AND
Field: consent.preferences.frequency
Operator: is not equal to "daily"
Result: Include profiles who consent to email marketing but not to a daily frequency
```

### Avancerad logik för arrayer med objekt

När du kombinerar villkor i arrayer med objekt beror beteendet på om du använder AND eller OR-logik mellan villkoren.

**Exempel: Array med objekt med AND-villkor**

Använd AND-logik när alla villkor måste gälla för arrayelementet *same*.

```
Field: consent.preferences["email_preferences"].categories[].enabled (boolean)
Operator: is equal to
Value: true
AND
Field: consent.preferences["email_preferences"].categories[].type (string)
Operator: is equal to
Value: "promotional"
Result: Includes profiles where the same category entry has both enabled=true and type="promotional".
Note: AND conditions apply to the same array entry. Using OR logic would include profiles if any array entry matches any of the conditions.
```

>[!TIP]
>
>**God praxis för AND-logik**
>
>Tänk på följande när du skapar OCH-baserade matrisförhållanden:
>
>* Använd AND-logik när alla villkor måste gälla för **samma arrayelement**.
>* Kom ihåg att AND skapar restriktiv målinriktning (färre profiler matchar).
>* Förvänta dig inte att AND-logik ska matcha flera matrisposter. Den gäller för varje post.
>* Undvik att använda AND-logik när du behöver flexibel matchning mellan poster.

>[!IMPORTANT]
>
>Med AND-logik måste varje matrispost uppfylla alla angivna villkor samtidigt. Det här beteendet är idealiskt när du behöver matcha kombinerade attribut, till exempel kategorier som både är aktiverade och kampanjanpassade.

>[!NOTE]
>
>AND-logik gäller för samma arraypost **endast för arrayer av objekt.**\
>För primitiva arrayer utvärderas AND-logik på fältnivå i hela arrayen.

**Exempel: Array med objekt med ELLER-villkor**

Använd ELLER-logik för att skapa heltäckande målgruppsmatchningar genom att tillåta att alla villkor är sanna över matrisposter.

```
Field: consent.preferences["email_preferences"].categories[].enabled (boolean)
Operator: is equal to
Value: true
OR
Field: consent.preferences["email_preferences"].categories[].type (string)
Operator: is equal to
Value: "newsletter"
Result: Includes profiles where any category entry has enabled=true or any entry has type="newsletter".
Note: OR logic allows matching across different array entries. One entry can meet the first condition while another meets the second.
```

### Nästa steg

När du har skapat och förfinat dina regler för samtyckespolicyn använder du följande resurser för att slutföra konfigurationen, validera policytillämpning och granska underliggande datamodeller.

* **Arbetsflöde för att skapa principer**: Implementera de regler som du definierade i användargränssnittet för principbyggaren med [Användargränssnittshandboken för principen för samtycke](user-guide.md#consent-policy.md)
* **Samtyckesprinciputvärdering och -tillämpning**: Verifiera hur den aktiverade principen påverkar målgruppsaktivering och användning av profildata. Mer information finns i [handboken om automatisk policytillämpning](../enforcement/auto-enforcement.md)
* **Datatyper för XDM-samtycke**: Referera till specifika schemastrukturer och fältdefinitioner för medgivandeattribut som används i dina principregler. Se guiden [XDM-datatypen Consents and Preferences](../../xdm/data-types/consents.md).
