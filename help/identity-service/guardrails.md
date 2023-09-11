---
keywords: Experience Platform;identitet;identitetstjänst;felsökning;skyddsräcken;riktlinjer;gräns;
title: Gardrutor för identitetstjänsten
description: Det här dokumentet innehåller information om användning och hastighetsgränser för identitetstjänstens data som hjälper dig att optimera din användning av identitetsdiagrammet.
exl-id: bd86d8bf-53fd-4d76-ad01-da473a1999ab
source-git-commit: 87138cbf041e40bfc6b42edffb16f5b8a8f5b365
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 1%

---

# Guardrails för [!DNL Identity Service] data

Det här dokumentet innehåller information om användning och hastighetsbegränsningar för [!DNL Identity Service] data som hjälper dig att optimera användningen av identitetsdiagrammet. När du granskar följande skyddsutkast förutsätts det att du har modellerat data korrekt. Om du har frågor om hur du modellerar data kan du kontakta kundtjänstrepresentanten.

## Komma igång

Följande Experience Platform-tjänster är involverade i modellering av identitetsdata:

* [Identiteter](home.md): Bridge-identiteter från olika datakällor när de hämtas till Platform.
* [[!DNL Real-Time Customer Profile]](../profile/home.md): Skapa enhetliga konsumentprofiler med data från flera källor.

## Begränsningar för datamodell

Tabellerna nedan innehåller riktlinjer för skyddsförslag för statiska gränser samt valideringsregler för identitetsnamnutrymmen.

### Statiska gränser

I följande tabell visas statiska gränser för identitetsdata.

| Guardrail | Gräns | Anteckningar |
| --- | --- | --- |
| (Aktuellt beteende) Antal identiteter i ett diagram | 150 | Gränsen tillämpas på sandlådenivå. När antalet identiteter har nått 150 eller fler kommer inga nya identiteter att läggas till och identitetsdiagrammet uppdateras inte. Diagram kan visa identiteter som är större än 150 som ett resultat av länkning av ett eller flera diagram med mindre än 150 identiteter. **Anteckning**: Det maximala antalet identiteter i ett identitetsdiagram **för en enskild sammanfogad profil** är 50. Sammanfogade profiler som baseras på identitetsdiagram med fler än 50 identiteter ingår inte i kundprofilen i realtid. Mer information finns i guiden [skyddsutkast för profildata](../profile/guardrails.md). |
| (Kommande beteende) Antal identiteter i ett diagram [!BADGE Beta]{type=Informative} | 50 | När ett diagram med 50 länkade identiteter uppdateras kommer identitetstjänsten att använda en&quot;första-in-ut-mekanism&quot; och tar bort den äldsta identiteten för att skapa utrymme för den senaste identiteten. Borttagningen baseras på identitetstyp och tidsstämpel. Gränsen tillämpas på sandlådenivå. Läs [appendix](#appendix) för mer information om hur identitetstjänsten tar bort identiteter när gränsen har nåtts. |
| Antal identiteter i en XDM-post | 20 | Det minsta antalet XDM-poster som krävs är två. |
| Antal anpassade namnutrymmen | Ingen | Det finns inga gränser för hur många anpassade namnutrymmen du kan skapa. |
| Antal tecken för ett namnområdes visningsnamn eller identitetssymbol | Ingen | Det finns inga gränser för hur många tecken ett namnområdes visningsnamn eller identitetssymbol får innehålla. |

### Validering av identitetsvärde

Följande tabell visar befintliga regler som du måste följa för att identitetsvärdet ska kunna valideras korrekt.

| Namnutrymme | Valideringsregel | Systembeteende när regeln bryts |
| --- | --- | --- |
| ECID | <ul><li>Identitetsvärdet för ett ECID måste vara exakt 38 tecken.</li><li>Identitetsvärdet för ett ECID får endast bestå av siffror.</li></ul> | <ul><li>Om identitetsvärdet för ECID inte är exakt 38 tecken hoppas posten över.</li><li>Om identitetsvärdet för ECID innehåller icke-numeriska tecken hoppas posten över.</li></ul> |
| Ej ECID | Identitetsvärdet får inte vara längre än 1 024 tecken. | Om identitetsvärdet är längre än 1 024 tecken hoppas posten över. |

### Inläsning av namnområde för identitet

Från och med 31 mars 2023 blockerar identitetstjänsten intag av Adobe Analytics ID (AAID) för nya kunder. Den här identiteten hämtas vanligtvis via [Adobe Analytics-källa](../sources/connectors/adobe-applications/analytics.md) och [Adobe Audience Manager-källa](../sources//connectors/adobe-applications/audience-manager.md) och är redundant eftersom ECID representerar samma webbläsare. Om du vill ändra den här standardkonfigurationen kontaktar du ditt Adobe-kontoteam.

## Nästa steg

Mer information om [!DNL Identity Service]:

* [[!DNL Identity Service] översikt](home.md)
* [Identitetsdiagramvisningsprogram](ui/identity-graph-viewer.md)


## Bilaga {#appendix}

Följande avsnitt innehåller ytterligare information om skyddsförslag för identitetstjänsten.

### [!BADGE Beta]{type=Informative} Om borttagningslogiken när ett identitetsdiagram med kapacitet uppdateras {#deletion-logic}

>[!IMPORTANT]
>
>Följande borttagningslogik är ett kommande beteende för identitetstjänsten. Kontakta din kontorepresentant för att begära en ändring av identitetstypen om din produktionssandlåda innehåller:
>
> * Ett anpassat namnutrymme där personidentifierarna (t.ex. CRM-ID:n) är konfigurerade som cookie/enhetsidentitetstyp.
> * Ett anpassat namnutrymme där cookie-/enhetsidentifierare har konfigurerats som identitetstyp för olika enheter.
>
>När den här funktionen är tillgänglig kommer diagram som överskrider gränsen på 50 identiteter att minskas ned till 50 identiteter. För CDP B2C Edition i realtid kan detta resultera i en minimal ökning av antalet profiler som kvalificerar för en målgrupp, eftersom dessa profiler tidigare ignorerades från segmentering och aktivering.

När ett fullständigt identitetsdiagram uppdateras, tar identitetstjänsten bort den äldsta identiteten i diagrammet innan den senaste identiteten läggs till. Detta är för att identitetsdata ska vara korrekta och relevanta. Den här borttagningsprocessen följer två huvudregler:

#### Borttagning av regel 1 prioriteras baserat på identitetstypen för ett namnutrymme

Borttagningsprioriteten är följande:

1. Cookie-ID
2. Enhets-ID
3. Enhets-ID, e-post och telefon

#### Regel 2 Borttagning baseras på den tidsstämpel som finns lagrad i identiteten

Varje identitet som länkas i ett diagram har en egen motsvarande tidsstämpel. När ett fullständigt diagram uppdateras tar identitetstjänsten bort identiteten med den äldsta tidsstämpeln.

När ett fullständigt diagram uppdateras med en ny identitet, fungerar dessa två regler tillsammans för att ange vilken äldre identitet som ska tas bort. Identitetstjänsten tar först bort det äldsta cookie-ID:t, sedan det äldsta enhets-ID:t och slutligen det äldsta korsenhets-ID:t/e-postadressen/telefonen.

>[!NOTE]
>
>Om den identitet som ska tas bort är länkad till flera andra identiteter i diagrammet, tas även länkarna som förbinder den identiteten bort.

>[!BEGINSHADEBOX]

**En visuell representation av borttagningslogiken**

![Ett exempel på den äldsta identiteten som tas bort för den senaste identiteten](./images/graph-limits-v3.png)

*Diagramanteckningar:*

* `t` = tidsstämpel.
* Värdet för en tidsstämpel motsvarar nyheten för en viss identitet. Till exempel: `t1` representerar den första länkade identiteten (äldst) och `t51` representerar den senaste länkade identiteten.

I det här exemplet tar identitetstjänsten först bort den befintliga identiteten med den äldsta tidsstämpeln innan diagrammet till vänster kan uppdateras med en ny identitet. Men eftersom den äldsta identiteten är ett enhets-ID, hoppar identitetstjänsten över den identiteten tills den kommer till namnutrymmet med en typ som är högre i listan över borttagningsprioriteter, vilket i det här fallet är `ecid-3`. När den äldsta identiteten med en högre prioritetstyp för borttagning har tagits bort uppdateras diagrammet med en ny länk, `ecid-51`.

* I det sällsynta fallet att det finns två identiteter med samma tidsstämpel och identitetstyp sorteras ID:n baserat på [XID](./api/list-native-id.md) och genomföra radering.

>[!ENDSHADEBOX]

Borttagning sker endast med data i identitetstjänsten och inte med kundprofilen i realtid.

* Detta beteende kan följaktligen skapa fler profiler med ett enda ECID, eftersom ECID inte längre är en del av identitetsdiagrammet.
* För att du ska kunna hålla dig inom de adresserbara målgruppernas berättigandenummer rekommenderar vi att du aktiverar [pseudonymt utgångsdatum för profildata](../profile/pseudonymous-profiles.md) för att ta bort dina gamla profiler.