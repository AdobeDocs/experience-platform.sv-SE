---
title: Datastyrning i frågetjänst
description: Den här översikten täcker de viktigaste elementen i datastyrningen i Experience Platform Query Service.
source-git-commit: d81ef9b9b6fdf7612d2afead13e925c8a9daf902
workflow-type: tm+mt
source-wordcount: '2659'
ht-degree: 0%

---

# Datastyrning i frågetjänsten

Adobe Experience Platform sammanför data från olika affärssystem och gör det möjligt att städa, forma, manipulera och berika data med Query Service efter behov. På så sätt kan marknadsförarna identifiera, förstå och engagera kunderna på ett bättre sätt. Tillräcklig datastyrning är en viktig aspekt när det gäller att hantera personuppgifter, eftersom vissa uppgifter kan omfattas av användningsbegränsningar som bygger på organisatoriska policyer och rättsliga bestämmelser. Det är viktigt att se till att inmatade data och relaterade åtgärder är kompatibla med de definierade dataanvändningsprinciperna.

Med hjälp av datastyrning i Query Service kan ni hantera kunddata och se till att regler, begränsningar och policyer som gäller för dataanvändning följs. Detta spelar en viktig roll när det gäller att säkerställa att användarprofilerna har tillämpats i enlighet med de regler som företaget har definierat.

Organisationer som rutinmässigt utför databehandling rekommenderas att utforma, öva och tillämpa dessa riktlinjer för att skapa en sekretessmedveten miljö för alla användare.

Följande kategorier är avgörande när det gäller att följa regler för datakompatibilitet när frågetjänsten används:

1. Säkerhet
1. Granskning
1. Dataanvändning
1. Sekretess
<!-- 1. Data hygiene -->

I det här dokumentet behandlas de olika styrområdena och det visas hur du kan underlätta datakompatibiliteten när du använder frågetjänsten. Se [styrning, integritet och säkerhet - översikt](../../landing/governance-privacy-security/overview.md) för mer omfattande information om hur Experience Platform kan hantera kunddata och säkerställa regelefterlevnad.

## Säkerhet

Datasäkerhet är processen att skydda data från obehörig åtkomst och säkerställa säker åtkomst under hela dess livscykel. Säker åtkomst upprätthålls i Experience Platform genom användning av roller och behörigheter, med funktioner som rollbaserad åtkomstkontroll och attributbaserad åtkomstkontroll. Autentiseringsuppgifter, SSL och datakryptering används också för att skydda data på olika plattformar.

Säkerheten med avseende på frågetjänsten är indelad i följande kategorier:

* [Åtkomstkontroll](#access-control): Åtkomsten styrs via roller och behörigheter, inklusive datauppsättningar och behörigheter på kolumnnivå.
* Skydda data genom [anslutning](#connectivity): Data skyddas med hjälp av plattformsklienter och externa klienter genom att en begränsad anslutning upprättas med utgångsdatum eller ej utgångsdatum.
* Skydda data genom [krypterings- och systemnivånycklar](#encryption): Datasäkerheten säkerställs genom kryptering när data ligger kvar.

<!-- * Securing data through [encryption and customer-managed keys (CMK)](#encryption-and-customer-managed-keys): Access controlled through encryption when data is at rest. -->

### Åtkomstkontroll {#access-control}

Med åtkomstkontrollen i Adobe Experience Platform kan du använda [Adobe Admin Console](https://adminconsole.adobe.com/) för att hantera åtkomst till funktioner i frågetjänsten med rollbaserade behörigheter. På samma sätt kan du styra åtkomsten till specifika dataattribut genom etiketthantering för scheman och datafält.

I det här avsnittet beskrivs de nödvändiga behörigheterna för åtkomstkontroll som en användare måste ha för att kunna utnyttja funktionerna i frågetjänsten fullt ut. Se dokumenten på [hantera behörigheter](../../access-control/ui/permissions.md) och [hantera användare](../../access-control/ui/users.md) om du vill ha detaljerade anvisningar om hur du tilldelar åtkomst till en produktprofil.

#### Relevanta behörigheter

Behörigheterna för åtkomstkontroll definieras i tabellerna nedan utifrån deras omfattning.

**Behörigheter för frågekörning**

Om du vill köra frågor i frågetjänsten måste användaren tilldelas en roll med följande behörighet:

| Behörighet | Beskrivning |
|---|---|
| [!UICONTROL Manage Queries] | Med den här behörigheten kan användare utföra datautforskande och gruppfrågor, som antingen kan läsa en befintlig datauppsättning eller skriva data på datauppsättningar. Detta inkluderar båda `CREATE TABLE AS SELECT` (`CTAS`) och `INSERT INTO AS SELECT` (`ITAS`) frågor. |

**Datauppsättningsbehörigheter**

Det här avsnittet är en guide för den resursbaserade åtkomst som krävs för att få åtkomst till datauppsättningar när data hämtas via frågetjänsten.

Via behörighetsgränssnittet kan du definiera resursbaserad åtkomstkontroll för en datauppsättning och ett schema med följande behörigheter:

| Behörighet | Beskrivning |
|---|---|
| [!UICONTROL Manage Datasets] | Den här behörigheten ger skrivskyddad åtkomst till scheman och ger åtkomst till att läsa, skapa, redigera och ta bort datauppsättningar för användning med frågetjänsten. |
| [!UICONTROL View Datasets] | Den här behörigheten tillåter skrivskyddad åtkomst för datauppsättningar och scheman som kan användas med frågetjänsten. |

#### Åtkomstkontroll för kolumner/fält

Med den attributbaserade åtkomstkontrollfunktionen kan användare av frågetjänsten begränsa åtkomsten till viktiga användardata. Åtkomst kan beviljas eller begränsas baserat på de behörigheter som tilldelats en roll. Användaråtkomst till enskilda kolumner styrs av de relevanta dataanvändningsetiketterna och de behörighetsgrupper som används för rollerna som tilldelats användare.

När du taggar schemafältgrupper och klasser med dataanvändningsetiketter tillämpas dataanvändningsbegränsningar på alla scheman med samma fältgrupper och klasser. Se översikten på [attributbaserad åtkomstkontroll](../../access-control/abac/overview.md) för utförlig information om den här funktionen.

Med den här funktionen kan du ge åtkomsträttigheter för konfidentiella kolumner till de användargrupper som du väljer. Åtkomstkontroll för en kolumn kan begränsa både läs- och skrivfunktionerna för en viss typ av användare.

Åtkomstkontroll för kolumner kan tillämpas på schemanivå för både standard- och ad hoc-scheman. Använd dataanvändningsetiketter på XDM-scheman för att begränsa åtkomsten till en eller flera kolumner. Dataetiketteringen tillämpas konsekvent, även för datauppsättningar som skapats via Query Service med ett fördefinierat schema eller ett ad hoc-schema som genererats som en del av CTAS-åtgärden.

När rätt åtkomstnivå har tillämpats med etiketter och roller inträffar följande systembeteende när en användare försöker få åtkomst till data som inte är tillgängliga:

1. Om en användare har nekats åtkomst till en av kolumnerna i ett schema nekas användaren även behörighet att läsa eller skriva i den begränsade kolumnen. Detta gäller följande vanliga scenarier:

   * **Fall 1**: När en användare försöker köra en fråga som bara påverkar en begränsad kolumn, genereras ett fel om att kolumnen inte finns.
   * **Fall 2**: När en användare försöker köra en fråga med flera kolumner, inklusive en begränsad kolumn, returnerar systemet endast utdata för alla kolumner som inte är begränsade.

1. Om en användare försöker få åtkomst till ett beräkningsfält måste användaren ha åtkomst till alla fält som används i kompositionen, eller systemet nekar även åtkomst till beräkningsfältet.

#### Åtkomstkontroller för vyer

Med frågetjänsten kan du använda ANSI SQL av standardtyp för [`CREATE VIEW`](../sql/syntax.md#create-view) -programsatser. För mycket känsliga arbetsflöden med data måste du använda lämpliga kontroller när du skapar vyer.

The `CREATE VIEW` nyckelordet definierar en vy av en fråga, men vyn materialiseras inte fysiskt. I stället körs frågan varje gång vyn refereras i en fråga. När en användare skapar en vy från en datauppsättning är de rollbaserade och attributbaserade åtkomstkontrollreglerna för den överordnade datauppsättningen **not** hierarkiskt tillämpad. Därför måste du uttryckligen ange behörigheter för var och en av kolumnerna när en vy skapas.

### Anslutningar {#connectivity}

Frågetjänsten kan nås via plattformsgränssnittet eller genom att en anslutning skapas med externa kompatibla klienter. Åtkomsten till alla tillgängliga fronter styrs av en uppsättning autentiseringsuppgifter.

#### Anslutning via externa klienter

Åtkomst till frågetjänsten med en tredjepartsklient kräver autentiseringsuppgifter för auktorisering. Dessa autentiseringsuppgifter är obligatoriska för att få åtkomst till frågetjänsten med någon av de kompatibla externa klienterna. Du kan ansluta till externa klienter genom att använda antingen [förfallodatum för inloggningsuppgifter](#expiring-credentials) eller [ej förfallande autentiseringsuppgifter](#non-expiring-credentials).

#### Begränsad anslutningstid via utgångsdatum {#expiring-credentials}

[Utgående autentiseringsuppgifter](../ui/credentials.md) tillåter användare att skapa en tillfällig anslutning med en extern klient. Den här uppsättningen autentiseringsuppgifter är bara giltig i 24 timmar. När den här typen av autentiseringsuppgifter har upphört att gälla visas även fliken Autentiseringsuppgifter på kontrollpanelen för frågetjänsten.

![Fliken Autentiseringsuppgifter i arbetsytan för frågetjänsten med utgångsdatum markerat.](../images/data-governance/overview/expiring-credentials.png)

#### Giltiga autentiseringsuppgifter {#non-expiring-credentials}

[Giltiga autentiseringsuppgifter](../ui/credentials.md#non-expiring-credentials) gör att du kan skapa en permanent anslutning till en extern klient, vilket gör det enklare att ansluta till frågetjänsten utan att behöva ett manuellt lösenord.

Om du vill aktivera alternativet att generera autentiseringsuppgifter som inte upphör att gälla måste du följa riktlinjerna [arbetsflöde som kräver krav](../ui/credentials.md#prerequisites). Som en del av den här processen måste din organisationsadministratör konfigurera behörigheter för produktprofilen och ge administratören kontroll över vilka konton som har åtkomst till autentiseringsuppgifter som inte upphör att gälla.

Tekniska användarkonton som tillåts med ej utgångsdatum kan tilldelas roller för att säkerställa lämplig datastyrning genom att definiera omfattningen av deras läs- och skrivåtkomst baserat på deras ansvar och behov. Se det tidigare avsnittet om [använda rollbaserade behörigheter via åtkomstkontroll](#access-control) för att hantera åtkomst till frågetjänsten.

När det obligatoriska arbetsflödet har slutförts kan behöriga användare nu [generera de anslutningsreferenser som krävs](../ui/credentials.md#generate-credentials).

#### SSL-datakryptering

För ökad säkerhet tillhandahåller Query Service inbyggt stöd för SSL-anslutningar för kryptering av kommunikationen mellan klient och server. Plattformen har stöd för olika SSL-alternativ som passar dina datasäkerhetsbehov och som balanserar bearbetningskostnaderna för kryptering och nyckelutbyte.

Se guiden för [SSL-alternativ för klientanslutningar från tredje part till frågetjänsten](../clients/ssl-modes.md) för mer information, inklusive hur du ansluter med `verify-full` SSL-parametervärde.

### Kryptering {#encryption}

<!-- Commented out lines to be included when customer-managed keys is released. Link out to the new document. -->

<!-- ### Encryption and customer-managed keys (CMK) {#encryption-and-customer-managed-keys} -->

Kryptering är användning av en algoritmisk process för att omvandla data till kodad och oläslig text för att säkerställa att informationen skyddas och inte är tillgänglig utan en dekrypteringsnyckel.

Med datakompatibiliteten för frågetjänsten säkerställs att data alltid krypteras. Data-in-Transition är alltid HTTPS-kompatibel och data-i-rest krypteras i ett Azure Data Lake-arkiv med nycklar på systemnivå. Läs dokumentationen om [hur data krypteras i Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/encryption.html) för mer information. Mer information om hur vilande data krypteras i Azure Data Lake Storage finns i [officiell Azure-dokumentation](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption).

<!-- Data-in-transit is always HTTPS compliant and similarly when the data is at rest in the data lake, the encryption is done with Customer Management Key (CMK), which is already supported by Data Lake Management. The currently supported version is TLS1.2. -->

## Granskning {#audit}

Frågetjänsten registrerar användaraktivitet och kategoriserar aktiviteten i olika loggtyper. Information om loggar på **som** utförd **vad** och **när**. Varje åtgärd som registreras i en logg innehåller metadata som anger åtgärdstyp, datum och tid, e-post-ID för användaren som utförde åtgärden samt ytterligare attribut som är relevanta för åtgärdstypen.

Alla loggkategorier kan begäras av en plattformsanvändare. I det här avsnittet finns information om vilken typ av information som har hämtats för frågetjänsten och var informationen finns.

### Frågeloggar {#query-logs}

Med frågeloggarnas användargränssnitt kan du övervaka och granska körningsinformation för alla frågor som har körts antingen via Frågeredigeraren eller API:t för frågetjänsten. Detta ger genomskinlighet till frågetjänstaktiviteter, vilket gör att du kan kontrollera metadata för **alla** de frågor som har körts mellan frågetjänsterna. Den innehåller alla typer av frågor, vare sig det är en undersökande, gruppfråga eller en schemalagd fråga.

Du kan komma åt frågeloggar via plattformsgränssnittet i [!UICONTROL Logs] -fliken i [!UICONTROL Queries] arbetsyta.

![Fliken Frågogg med informationspanelen markerad.](../images/data-governance/overview/queries-log.png)

### Granskningsloggar {#audit-logs}

Granskningsloggarna innehåller mer detaljerad information än frågeloggar och gör det möjligt att filtrera loggar baserat på attribut som användare, datum, typ av fråga osv. Förutom informationen i frågeloggens användargränssnitt lagrar granskningsloggar information om enskilda användare tillsammans med sessionsdata eller anslutning till en tredjepartsklient.

Genom att ge en exakt beskrivning av användaråtgärder kan en verifieringskedja hjälpa till med felsökningsproblem och hjälpa ert företag att effektivt följa företagets policyer för datahantering och lagstadgade krav. Granskningsloggarna innehåller en förteckning över alla plattformsaktiviteter. Med granskningsloggar kan du granska användaråtgärder som rör frågekörning, mallar och schemalagda frågor för att öka genomskinligheten och synligheten för åtgärder som utförs av användare i frågetjänsten.

Följande tabell visar de frågekategorier som har hämtats av granskningsloggar och de åtgärdstyper som de registrerar:

| Kategori | Åtgärdstyp |
|---|---|
| Fråga | Kör |
| Frågemall | Skapa, ta bort, uppdatera |
| Schemalagd fråga | Skapa, ta bort, uppdatera |

Nedan finns en lista med tre utökade serverloggar som innehåller mer information än de som finns i frågeloggarna. De utökade loggarna finns i frågekategorierna för granskningsloggar:

1. **Meta query logs**: När en fråga körs, utförs olika tillhörande underfrågor i serverdelen (som parsing). Dessa typer av frågor kallas för metadatafrågor. Deras relevanta information finns i granskningsloggarna.
1. **Sessionsloggar**: Systemet skapar en sessionslogg för en användare när han/hon loggar in på frågetjänsten oavsett om han/hon kör en fråga eller inte.
1. **Anslutningsloggar för klienter från tredje part**: En anslutningsgranskningslogg skapas när en användare ansluter frågetjänsten till en tredjepartsklient.

Se [granskningsloggar - översikt](../../landing/governance-privacy-security/audit-logs/overview.md) om du vill ha mer information om hur granskningsloggar kan hjälpa er organisation att hantera datakompatibiliteten.

## Dataanvändning {#data-usage}

Datastyrningsramverket i Platform erbjuder ett enhetligt sätt att på ett ansvarsfullt sätt använda data på alla Adobe-lösningar, -tjänster och -plattformar. Den koordinerar systemmetoden för att hämta in, kommunicera och använda metadata i hela Adobe Experience Cloud. Detta hjälper i sin tur de registeransvariga att märka data i enlighet med de marknadsföringsåtgärder som behövs och de begränsningar som gäller för dessa data från de planerade marknadsföringsåtgärderna. Se översikten på [etiketter för dataanvändning](../../data-governance/labels/overview.md) om du vill ha mer information om hur datastyrning gör att du kan använda dataanvändningsetiketter på datauppsättningar och fält.

Det är bästa sättet att arbeta för att uppfylla alla data i varje skede av dataresan. Därför bör härledda datauppsättningar som använder ad hoc-scheman märkas på lämpligt sätt som en del av ramverket för datastyrning. Det finns två typer av härledda datauppsättningar som har formats av Query Service: datauppsättningar som använder ett standardschema och datauppsättningar som använder ett ad hoc-schema.

>[!NOTE]
>
>Datauppsättningar som skapas med frågetjänsten kallas för härledda datauppsättningar.

När ad hoc-scheman skapas av en enskild användare för ett specifikt ändamål namnges XDM-schemafälten för den aktuella datamängden och är inte avsedda att användas i olika datamängder. Därför visas inte ad hoc-scheman som standard i användargränssnittet för Experience Platform. Även om det inte finns någon skillnad i hur dataanvändningsetiketter används mellan både standard- och ad hoc-scheman, måste man först göra ad hoc-scheman som skapats av Query Service för etikettering synliga i plattformens användargränssnitt. Se guiden [identifiera ad hoc-scheman inom plattformsgränssnittet](./ad-hoc-schema-labels.md#discover-ad-hoc-schemas) för mer information.

När du har öppnat schemat kan du [använda etiketter på enskilda fält](../../xdm/tutorials/labels.md). När ett schema har etiketterats ärver alla datauppsättningar som härleds från det schemat dessa etiketter. Härifrån kan du ange dataanvändningsprinciper som kan begränsa dataanvändning med vissa etiketter från att aktiveras till vissa mål. Mer information finns i översikten på [dataanvändningsprinciper](../../data-governance/policies/overview.md).

## Sekretess {#privacy}

[Privacy Service](../../privacy-service/home.md) hjälper er att hantera kundförfrågningar om att få tillgång till och ta bort deras data i enlighet med juridiska sekretessbestämmelser. Det gör man genom att söka efter befintliga identifierare i data och antingen få åtkomst till eller ta bort dessa data beroende på vilket sekretessjobb som begärts. Data måste vara korrekt märkta för att tjänsten ska kunna avgöra vilka fält som ska användas eller tas bort under sekretessjobb. Uppgifter som omfattas av sekretessförfrågningar måste innehålla kundidentitetsinformation för att kunna koppla de olika uppgifterna till den person som sekretessförfrågningen gäller för. Frågetjänsten kan berika de data som används med en unik identifierare för att uppfylla sekretessjobb.

Sekretessförfrågningar kan skickas till datasjön eller profildatalagret. Poster som tas bort från datasjön leder inte till att profiler som gjorts från dessa poster tas bort. Ett sekretessjobb som tar bort personuppgifter från datasjön tar inte bort deras profil, så all information (som innehåller det profil-ID:t) som har infogats efter slutförandet av sekretessjobbet uppdaterar den profilen som vanligt. Detta bekräftar behovet av att korrekt identifiera data som används i särskilda scheman.

Mer information om Privacy Service finns i dokumentationen [identitetsdata för sekretessförfrågningar](../../privacy-service/identity-data.md) och hur ni konfigurerar era dataåtgärder och utnyttjar Adobe-tekniker för att effektivt hämta in lämplig identitetsinformation för kundsekretessförfrågningar.

Frågetjänstfunktioner för datastyrning förenklar och effektiviserar processen för kategorisering av data och efterlevnad av regler för dataanvändning. När data har identifierats kan du med Query Service tilldela den primära identiteten till alla utdatamängder. Du **måste** lägga till identiteter i datauppsättningen för att underlätta förfrågningar om datasekretess och arbeta för att uppfylla datakraven.

Schemadatafält kan anges som ett identitetsfält via användargränssnittet för plattformen och frågetjänsten gör det även möjligt att [markera de primära identiteterna med SQL-kommandot&quot;ALTER TABLE&quot;](../sql/syntax.md#alter-table). Ställa in en identitet med `ALTER TABLE` Kommandot är särskilt användbart när datauppsättningar skapas med SQL i stället för direkt från ett schema via plattformsgränssnittet. I dokumentationen finns instruktioner om hur du [definiera identitetsfält i användargränssnittet](../../xdm/ui/fields/identity.md) när du använder standardscheman.

<!-- COMMENTING OUT DATA HYGEINE SECTION TEMPORARILY UNTIL IT IS GA. currently it is in Beta only.

## Data hygiene 

"Data hygiene" refers to the process of repairing or removing data that may be outdated, inaccurate, incorrectly formatted, duplicated, or incomplete. It is important to ensure adequate data hygiene along every step of the data's journey and even from the initial data storage location. In Query Service, this is either the data lake or the data warehouse.

It is necessary to assign an identity to a derived dataset to allow their management by the [!DNL Data Hygiene] service. Conversely, when you create aggregated data on an accelerated data store, the aggregated data cannot be used to derive the original data. As a result of this data aggregation, the need to raise data hygiene requests is eliminated. == THIS APPEARS TO BE A PRIVACY USE CASE NAD NOT DATA HYGEINE ++  this is confusing.

An exception to this scenario is the case of deletion. If a data hygiene deletion is requested on a dataset and before the deletion is completed, another derived dataset query is executed, then the derived dataset will capture information from the original dataset. In this case, you must be mindful that if a request to delete a dataset has been sent, you must not execute any new derived dataset queries using the same dataset source. 

See the [data hygiene overview](../../hygiene/home.md) for more information on data hygiene in Adobe Experience Platform. -->
