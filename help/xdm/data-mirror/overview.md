---
keywords: Experience Platform;dataspegling;modellbaserat schema;relationsschema;registrering av ändringsdata;databassynkronisering;primärnyckel;relationer
solution: Experience Platform
title: Data Mirror - översikt
description: Läs om hur Data Mirror möjliggör redigering på radnivå från externa databaser till Adobe Experience Platform med hjälp av modellbaserade scheman med tvingande unikhet, relationer och versionshantering.
badge: Begränsad tillgänglighet
source-git-commit: 6ce214073f625a253fcc5bb14dfdb6a4a61e6e7b
workflow-type: tm+mt
source-wordcount: '1355'
ht-degree: 0%

---

# Data Mirror - översikt

>[!AVAILABILITY]
>
>Data Mirror och modellbaserade scheman är tillgängliga för innehavare av Adobe Journey Optimizer **samordnade kampanjer**. De är också tillgängliga som en **begränsad version** för Customer Journey Analytics-användare, beroende på din licens och aktivering av funktioner. Kontakta din Adobe-representant för att få åtkomst.

Data Mirror är en Adobe Experience Platform-funktion som gör det möjligt att ändra på radnivå från externa databaser till datasjön med hjälp av modellbaserade scheman. Den bevarar datarelationer, tillämpar unikt utseende och stöder versionshantering utan att kräva extraherings-, transformerings- och inläsningsprocesser (ETL) uppströms.

Använd Data Mirror för att synkronisera infogningar, uppdateringar och borttagningar (ändringsbara data) från externa system som [!DNL Snowflake], [!DNL Databricks] eller [!DNL BigQuery] direkt till Experience Platform. Detta hjälper dig att bevara den befintliga databasmodellstrukturen och dataintegriteten när du överför data till plattformen.

## Funktioner och fördelar

Data Mirror har följande viktiga funktioner för databassynkronisering:

* **Tillämpning av primärnyckel**: Ser till att datauppsättningar är unika och förhindrar dubblettposter vid förtäring.
* **Ändringsförslag på radnivå**: Stöder detaljerade dataändringar, inklusive överföringar och borttagningar med precisionskontroll.
* **Schemarelationer**: Aktiverar externa och primära nyckelrelationer mellan datauppsättningar via beskrivningar.
* **Obeständig händelsehantering**: Bearbetar ändringshändelser med hjälp av versions- och tidsstämpelbeskrivare, även när de inte kommer i sekvens.
* **Integrering av direkt lagerställe**: Ansluter till molndatalager som stöds för nästan synkronisering av ändringar i realtid.

Använd Data Mirror för att importera ändringar direkt från era källsystem, tillämpa schemaintegriteten och göra data tillgängliga för analyser, resesamordning och arbetsflöden för regelefterlevnad. Data Mirror eliminerar komplexa ETL-processer i tidigare led och snabbar upp implementeringen genom att möjliggöra direkt spegling av befintliga databasmodeller.

Planera för raderings- och datahygien när du implementerar modellbaserade scheman med Data Mirror. Alla program måste beakta hur borttagningar påverkar relaterade datauppsättningar, arbetsflöden för regelefterlevnad och processer i senare led före distributionen.

## Förhandskrav {#prerequisites}

Innan du börjar bör du förstå följande komponenter i Experience Platform och kontrollera att din miljö uppfyller de tekniska och strukturella kraven:

* [Skapa scheman i Experience Platform UI](../ui/resources/schemas.md) eller [API](../api/schemas.md)
* [Konfigurera molnkällanslutningar](../../sources/home.md#cloud-storage)
* [Använd begrepp för datainhämtning](../../sources/tutorials/api/change-data-capture.md) (överför, tar bort)
* Skilj mellan [standard](../schema/composition.md) och [modellbaserade scheman](../schema/model-based.md)
* [Definiera strukturella relationer med beskrivningar](../api/descriptors.md)

### Implementeringskrav

Plattformsinstansen och källdata måste uppfylla specifika krav för att Data Mirror ska fungera korrekt. Data Mirror kräver **modellbaserade scheman**, som är flexibla datastrukturer med tvingande begränsningar. För närvarande arbetar Data Mirror främst med modellbaserade scheman, men integrering med vanliga XDM-scheman stöds av kommande funktioner för anpassade B2B-objekt (planeras i oktober 2025).

Inkludera en **primärnyckel och versionsbeskrivning** i alla scheman. Om du arbetar med ett tidsserieschema krävs även en **tidsstämpelbeskrivning**.

Den externa databasen måste ha stöd för datainhämtning eller innehålla metadata som identifierar infogningar, uppdateringar och borttagningar. Source-data måste innehålla **unika identifierare**, antingen ett enskilt fält eller en sammansatt primärnyckel och **versionsinformation** så att systemet kan tillämpa uppdateringar i rätt ordning.

Om du vill identifiera borttagningar lägger du till en `_change_request_type`-kolumn som anger om varje post är en upsert eller en delete.

## Implementera Data Mirror {#implementation-workflow}

Till skillnad från vanliga ingrepp bevarar Data Mirror databasmodellstrukturen inom Experience Platform datasjön. Denna datastrukturkonsekvens eliminerar behovet av extern förbehandling. Här följer ett högnivåarbetsflöde för implementering av Data Mirror. Välj implementeringsmetod baserat på teamets arbetsflöde och källsystem.

### Definiera schemastrukturen

Skapa [modellbaserade scheman](../schema/model-based.md) med obligatoriska beskrivningar (metadata som definierar schemabeteende och begränsningar). Välj en metod som passar teamets arbetsflöde, antingen via gränssnittet eller direkt via API:t.

* **Gränssnittsmetod**: [Skapa modellbaserade scheman i Schemaredigeraren](../ui/resources/schemas.md#create-model-based-schema)
* **API-inflygning**: [Skapa scheman via API:t för schemaregister](../api/schemas.md#create-model-based-schema)

### Mappa relationer och definiera datahantering

Definiera anslutningar mellan datauppsättningar med hjälp av relationsbeskrivare. Hantera relationer och bibehåll datakvaliteten i alla datauppsättningar. Dessa uppgifter säkerställer enhetliga kopplingar och uppfyller kraven på datahygien.

* **Schemarelationer**: [Definiera relationer mellan datauppsättningar med hjälp av beskrivningar](../api/descriptors.md)
* **Posthygien**: [Hantera precisionspostborttagningar](../../hygiene/ui/record-delete.md#model-based-record-delete)

### Konfigurera källanslutningen

Välj en matningsmetod som baseras på källsystemet och använd skiftläge. Varje alternativ har stöd för olika nivåer av automatisering, omformning och skalbarhet.

* [**Konfigurera molnkällanslutningar**](../../sources/home.md#cloud-storage)
* **SQL-import**: Använd Data Distiller för att skriva till relationsdatauppsättningar
* [**Filöverföring**](../ui/resources/schemas.md#upload-ddl-file): Överför filer manuellt för batch- eller engångsinmatning

### Aktivera inhämtning av ändringsdata

Konfigurera anslutningar för registrering av ändringsdata med molndatalager som stöds. Infoga ändringar på radnivå samtidigt som unika inställningar bevaras och uppdateringar tillämpas i rätt ordning.

* **Ändra datainhämtning**: [Aktivera inhämtning av ändringsdata i källanslutningar](../../sources/tutorials/api/change-data-capture.md)

## Vanliga användningsfall {#use-cases}

Läs vad som är vanligt: Data Mirror har stöd för exakt datasynkronisering och relationsbevarande. Varje scenario visar hur Data Mirror stöder vanliga affärsbehov inom analys, samordning och regelefterlevnad.

### Relationsdatamodellering

Använd [modellbaserade scheman](../schema/model-based.md) (även kallade relationsscheman) i Data Mirror för att representera entiteter, bearbeta infogningar, uppdateringar och borttagningar på radnivå och för att underhålla primära och externa nyckelrelationer som finns i dina datakällor. Detta tillvägagångssätt ger Experience Platform relationsbaserade datamodelleringsprinciper och säkerställer strukturell enhetlighet mellan datauppsättningar.

### Synkronisering mellan lager och sjöar

Spegla händelsedata, kundinteraktionsloggar, kampanjhändelser och hjälpdata från molndatalager som stöds till Experience Platform. Detta ger stöd för kampanjberättigande, målinriktning och sekvensering av meddelanden. Journey Optimizer och Real-Time CDP B2B förlitar sig på detta för nästan realtidssamordning.

### Integrering med Customer Journey Analytics

Synkronisera tidsseriehändelser som webbklick, produktvisningar, inköp och supportinteraktioner från system som callcenters eller chattloggar. En komplett ändringshistorik stöder korrekt trendanalys och beteendesegmentering. Experience Platform Data Mirror för Customer Journey Analytics använder detta för att spegla uppdateringar och borttagningar från källsystem.

### B2B-relationsmodellering

Bevara relationer som hierarkier av typen konto-till-kontakt, prenumeration-till-konto eller kontakt-till-region. Dessa har stöd för segmentering, poängsättning av leads, uppföljning av affärsmöjligheter och flerkanalskoordinering. Till skillnad från standardredigering som förenklar relationer, underhåller Data Mirror dem internt med hjälp av beskrivningar för mer korrekt modellering.

### Prenumerationshantering

Spåra händelser som förnyelser, uppsägningar, uppgraderingar, nedgraderingar och planändringar med hjälp av en komplett versionshistorik. Detta stöder kvarhållningskampanjer, omprövningsprognoser och livscykelbaserad segmentering. Full historik möjliggör beteendeinsikter och exakt målinriktning.

### Datahygien

Använd datainhämtning för att möjliggöra exakt borttagning på postnivå för att uppfylla kraven (t.ex. reglerade branscher) och rensa upp arbetsflöden. Data Mirror tillämpar borttagningar korrekt samtidigt som relaterade data bevaras i alla anslutna datauppsättningar.

## Viktiga överväganden {#considerations}

Granska dessa viktiga aspekter för att se till att implementeringen är anpassad efter schemabeteenden som stöds, intag-metoder och relationsmönster. Korrekt planering hjälper till att undvika integreringsproblem och säkerställer korrekt datamodellering.

### Krav på radering av data och hygien

Alla program som använder modellbaserade scheman och Data Mirror måste förstå vad det innebär att ta bort data. Modellbaserade scheman möjliggör exakt borttagning på postnivå som kan påverka relaterade data över sammankopplade datamängder. Dessa borttagningsfunktioner påverkar dataintegritet, regelefterlevnad och programbeteende längre fram i kedjan, oavsett vilket användningsfall du har. Granska [datahygien](../../hygiene/ui/record-delete.md#model-based-record-delete) och planera för borttagningsscenarier innan implementering.

### Val av schemabeteende

Modellbaserade scheman är som standard **postbeteende**, som hämtar enhetstillstånd (kunder, konton osv.). Om du behöver **tidsseriebeteende** för händelsespårning måste du konfigurera det explicit.

### Jämförelse av försäljningsmetod

Använd den här jämförelsetabellen om du vill välja den bästa metoden för inhämtning av data, oavsett om du behöver realtidssynkronisering, SQL-baserad omvandling eller manuella filöverföringar.

| Inmatningsmetod | Användningsfall |
| ----------------------- | -------------------------------------------------------------- |
| **Ändra datainhämtning** | Synkronisering i realtid från molnlager som stöds |
| **Data Distiller** | SQL-baserade arbetsflöden för import och transformering |
| **Filöverföring** | Batch-/manuell förtäring när källintegration inte är tillgänglig |

### Relationsbegränsningar

Data Mirror har stöd för **1:1- och** många-till-1 **-relationer med hjälp av beskrivningar.** **Många-till-många**-relationer kräver ytterligare modellering och stöds inte direkt.

## Nästa steg

När du har granskat den här översikten bör du kunna avgöra om Data Mirror passar ditt användningssätt och förstå implementeringskraven. Så här kommer du igång:

1. **Dataarkitekterna** bör utvärdera din datamodell för att se till att den har stöd för primärnycklar, versionshantering och ändringsspårningsfunktioner.
2. **Affärsintressenter** bör bekräfta att din licens innehåller modellbaserat schemastöd och nödvändiga Experience Platform-utgåvor.
3. **Schemadesigners** bör planera din schemastruktur för att identifiera nödvändiga beskrivningar, fältrelationer och datastyrningsbehov.
4. **Implementeringsteamen** bör välja en inmatningsmetod som baseras på dina källsystem, realtidskrav och arbetsflöden.

Implementeringsinformation finns i [modellbaserad schemadokumentation](../schema/model-based.md).
