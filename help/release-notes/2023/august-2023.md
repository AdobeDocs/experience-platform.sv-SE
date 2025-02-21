---
title: Versionsinformation om Adobe Experience Platform från augusti 2023
description: Versionsinformation för augusti 2023 för Adobe Experience Platform.
exl-id: c67dca3a-eccb-427e-8ab3-b69c51b57938
source-git-commit: 4afb2c76f2022423e8f1fa29c91d02b43447ba90
workflow-type: tm+mt
source-wordcount: '1715'
ht-degree: 40%

---

# Versionsinformation om Adobe Experience Platform

**Releasedatum: 23 augusti 2023**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Plattform för kunddata i realtid](#rtcdp)
- [Attributbaserad åtkomstkontroll](#abac)
- [Kontrollpaneler](#dashboards)
- [Datainsamling](#data-collection)
- [Datainmatning](#data-ingestion)
- [Dataförberedelse](#data-prep)
- [Mål](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Identitetstjänst](#identity-service)
- [Segmenteringstjänst](#segmentation)
- [Källor](#sources)

## Plattform för kunddata i realtid {#rtcdp}

Real-Time Customer Data Platform ([!DNL Real-Time CDP]) bygger på Experience Platform och hjälper företag att sammanföra kända och okända data för att aktivera kundprofiler med intelligent beslutsfattande under hela kundresan.

[!DNL Real-Time CDP] kombinerar flera datakällor från företag för att skapa kundprofiler i realtid. Segment som byggs upp utifrån dessa profiler kan sedan skickas till mål i senare led för att ge personliga kundupplevelser i alla kanaler och på alla enheter.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Handbok för användning av intelligent återanvändning | I [Handboken om intelligent återanvändning](../../rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md) finns information om hur du återengagerar kunder som har avbrutit en konvertering innan de slutför den på ett intelligent och ansvarsfullt sätt. I den här guiden används följande exempel på resor för att återengagera kunder: <ul><li>Återengagemangsresa - Rikta in dig på kunder som inte längre surfar.</li><li>Övergiven kundvagnsresa - Rikta in dig på kunder som har lagt produkter i vagnen men ännu inte slutfört köpet.</li><li>Beställningsbekräftelseresa - Fokusera på produktinköp</li></ul> Använd den detaljerade länken för feedbackalternativ längst ned i [fallguiden ](../../rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md) för intelligent återanvändning för att ge feedback. |
| Stöd för partnerdata | Utför marknadsföring i Real-Time CDP, med profiler för potentiella kunder och partner-ID:n från våra partners, för att nå nya kunder och berika era egna data: <ul><li>Kundvärvning och adresserbarhet: Dra nytta av cookiefria identifierare och hashas-PII från valfria datapartner för att nå nya nettokunder och minska beroendet av cookies från tredje part.</li><li>Fullständig trattmarknadsföring i ett enda system: Self-serve-segmentering, målgruppsurval och inbyggd aktivering för potentiella och kända kunder i ett enda system.</li><li>Grunden för förtroende: Styrd partnerdata och -profiler med patenterad dataanvändning, märkning, åtkomstkontroll och mycket mer på marknaden på ett ansvarsfullt sätt. Mer information finns i följande fallhandböcker: Handböckerna för prospektering finns nu tillgängliga. Läs fallhandböckerna om prospektering för att lära dig hur ni engagerar och förvärvar nya kunder genom prospekteringsexempel:<ul><li>[Prospektering](../../rtcdp/partner-data/prospecting.md)</li><li>[Personalisering på plats](../../rtcdp/partner-data/onsite-personalization.md)</li><li>[Komplettera förstapartsprofiler](../../rtcdp/partner-data/supplement-first-party-profiles.md)</li><li>[Aktivera potentiella målgrupper](../../destinations/ui/activate-prospect-audiences.md)</li></ul> |

{style="table-layout:auto"}

Mer information finns i [Real-Time CDP-översikten](../../rtcdp/overview.md).

## Attributbaserad åtkomstkontroll {#abac}

Attributbaserad åtkomstkontroll är en funktion hos Adobe Experience Platform som ger sekretessmedvetna varumärken större flexibilitet att hantera användaråtkomst. Enskilda objekt som schemafält och segment kan tilldelas användarroller. Med den här funktionen kan du bevilja eller återkalla åtkomst till enskilda objekt för specifika plattformsanvändare i organisationen.

Tack vare attributbaserad åtkomstkontroll kan administratören styra användarnas åtkomst till känsliga personuppgifter (SPD), personligt identifierbar information (PII) och andra anpassade typer av data i alla plattformsarbetsflöden och resurser. Administratörer kan definiera användarroller som bara har åtkomst till specifika fält och data som motsvarar dessa fält.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Sandlådekonfiguration för behörighetsprincip | Med den nya funktionen [behörighetsprincipsandlådekonfiguration](../../access-control/abac/ui/policies.md) kan du tillämpa en attributbaserad åtkomstkontrollprincip på alla eller ett visst antal sandlådor, beroende på dina behov och krav. |

{style="table-layout:auto"}

Mer information om attributbaserad åtkomstkontroll finns i [översikt över attributbaserad åtkomstkontroll](../../access-control/abac/overview.md). En utförlig guide om det attributbaserade arbetsflödet för åtkomstkontroll finns i [heltäckande attributbaserad åtkomstkontroll](../../access-control/abac/end-to-end-guide.md).

## Kontrollpaneler {#dashboards}

Adobe Experience Platform tillhandahåller flera instrumentpaneler där du kan visa viktiga insikter om organisationens data, som fångas upp under dagliga ögonblicksbilder.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Användningsfall för analys och uppföljning av samtycke | Lär dig hur du skapar en kontrollpanel för godkännande för olika användningsfall för marknadsföring för Real-Time CDP-data med [dokumentet för analys av samtycke och spårning](../../dashboards/insights-use-cases/consent-analysis.md). Här beskrivs hur du skapar en målgrupp med rätt attribut för dina affärsbehov och sedan kan du få insikter genom att använda förkonfigurerade widgetar i Adobe Experience Platform användargränssnitt. Den innehåller även anvisningar om hur du skapar en egen anpassad widget med den användardefinierade funktionen för instrumentpaneler. Dokumentet omfattar användningsfall för samtyckestrender och samtycke överlappar varandra. |

{style="table-layout:auto"}

Mer information om kontrollpaneler, inklusive hur du ger åtkomstbehörigheter och skapar anpassade widgetar, får du genom att läsa [översikten för kontrollpaneler](../../dashboards/home.md).

## Datainsamling {#data-collection}

Adobe Experience Platform tillhandahåller en uppsättning tekniker som gör att du kan samla in kundupplevelsedata på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omvandlas och distribueras till mål inom eller utanför Adobe.

**Nya eller uppdaterade funktioner**

| Typ | Funktion | Beskrivning |
| --- | --- | --- |
| Taggar och vidarebefordran av händelser | [Experience Platform-taggar (Kina)](/help/tags/ui/publishing/premium-cdn.md) | Den nya funktionen Experience Platform Tags (China) förbättrar webbplatsens tillförlitlighet och latens, vilket ger kortare svarstider för kunder som använder taggar på webbplatser i Kina. Kunder kan nu använda JavaScript-koden i taggbiblioteket när de implementerar webbplatser i Kina. Den här funktionen har också lagts till i UPP-protokollet (Unified Provisioning Protocol), vilket gör att produktdistributionen kan automatiseras efter köpet. |

{style="table-layout:auto"}

Mer information finns i [översikten över datainsamlingar](../../tags/home.md).

## Datainmatning {#data-ingestion}

Adobe Experience Platform har en omfattande uppsättning funktioner för att mata in alla typer av data med alla fördröjningar. Du kan mata in med grupp- eller strömnings-API:er, med Adobe-byggda källor, partners för dataintegration eller Adobe Experience Platform-gränssnittet.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Ändringar i arbetsflöden för dataöverföring | Rader med data som innehåller värden som är större än den angivna datatypen (t.ex. långa data som skickas som heltalsdatatyp) kommer nu att refuseras och felmeddelanden rapporteras. Tidigare avvisades dessa rader utan varning. |

Mer information finns i [översikten över dataöverföring](../../ingestion/home.md).

## Dataförberedelse {#data-prep}

Med dataförberedelse kan utvecklare mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för filtrering av sekundära identiteter | Du kan nu använda Data Prep för att filtrera bort identiteter som kommer från Adobe Analytics, till exempel AAID och AACUSTOMID. Om de filtreras bort blir dessa identiteter inte inkapslade i kundprofilen i realtid. Ofiltrerade data kommer även i fortsättningen att förtäras i datasjön. |

{style="table-layout:auto"}

Mer information finns i [översikten över dataförberedelser](../../data-prep/home.md).

## Mål {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Adobe Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Ny eller uppdaterad funktion** {#destinations-new-updated-functionality}

- Du kan nu [aktivera potentiella målgrupper](../../destinations/ui/activate-prospect-audiences.md) till molnlagringsmål.
- Det allmänna [aktiveringsskyddet](../../destinations/guardrails.md#general-activation-guardrails) för högst 100 mål per sandlåda har uppdaterats till att vara en _hård gräns_.

Mer allmän information om destinationer finns i [målöversikten](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM är en specifikation med öppen källkod som tillhandahåller gemensamma strukturer och definitioner (scheman) för data som förs in i Adobe Experience Platform. Genom att följa XDM-standarder kan all data om kundupplevelsen införlivas i en gemensam representation för att leverera insikter på ett snabbare och mer integrerat sätt. Du kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut för personalisering.

**Nya XDM-komponenter**

| Komponenttyp | Namn | Beskrivning |
| --- | --- | --- |
| Klass | [[!UICONTROL XDM Individual Prospect Profile]](https://github.com/adobe/xdm/pull/1758/files) | Använd den här klassen för att ta in profiler för potentiella kunder som har hämtats från dataleverantörers toppmoderna kundvärvningsexempel. Se exempel och läs mer i [[!UICONTROL XDM Individual Prospect Profile]](../../xdm/classes/prospect.md)-dokumentationen. |

{style="table-layout:auto"}

**Uppdaterade XDM-komponenter**

| Komponenttyp | Namn | Uppdatera beskrivning |
| --- | --- | --- |
| Tillägg ([!UICONTROL Adobe Analytics ExperienceEvent Full Extension]) | [[!UICONTROL Context Data]](https://github.com/adobe/xdm/pull/1761/files) | [!UICONTROL Context Data]-mappningsobjekt har lagts till i [!UICONTROL Adobe Analytics ExperienceEvent Full Extension] för att tillhandahålla kontextdata för Adobe Analytics. |
| Fältgrupp | Flera | Flera fält har lagts till i [[!UICONTROL Enriched Event Segment Details]](https://github.com/adobe/xdm/pull/1760/files). |

{style="table-layout:auto"}

Mer information finns i [XDM-systemöversikt](../../xdm/home.md).

## Identitetstjänst {#identity-service}

Adobe Experience Platforms identitetstjänst ger dig en heltäckande bild av dina kunder och deras beteende genom att koppla samman identiteter mellan enheter och system så att du kan leverera effektiva, personliga digitala upplevelser i realtid.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Ändringar av begränsningar för identitetsdiagram | I slutet av september kommer identitetsdiagrammet att ändras till 50 identiteter per diagram och den senaste identiteten kommer att importeras. Den äldsta identiteten kommer därför att tas bort baserat på tidsstämpeln för inmatningen och identitetstypen, och cookie-identitetstyperna tas bort först. I dag har identitetsdiagram en gräns på 150 identiteter per diagram, och när gränsen har nåtts uppdateras inte längre diagram. Kontakta din kontorepresentant för att begära en ändring av identitetstypen om din produktionssandlåda innehåller: <ul><li>ett anpassat namnutrymme där personidentifierarna (t.ex. CRM-ID:n) är konfigurerade som cookie/enhetsidentitetstyp.</li><li>ett anpassat namnutrymme där cookie-/enhetsidentifierare har konfigurerats som identitetstyp för olika enheter.</li></ul> Dessa förfrågningar behandlas manuellt av Adobe Engineering. Mer information finns i [skyddsjournalerna för identitetstjänstens data](../../identity-service/guardrails.md). |

Mer information finns i [Översikt över identitetstjänsten](../../identity-service/home.md).

## Segmenteringstjänst {#segmentation}

Med [!DNL Segmentation Service] kan du segmentera data som lagras i [!DNL Experience Platform] och som relaterar till individer (t.ex. kunder, potentiella kunder, användare eller organisationer) till målgrupper. Du kan skapa målgrupper med hjälp av segmentdefinitioner eller andra källor från dina [!DNL Real-Time Customer Profile]-data. Dessa målgrupper är centralt konfigurerade och underhållna på [!DNL Platform] och är tillgängliga för alla Adobe-lösningar.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Målgrupper som ser likadana ut (begränsad tillgänglighet) | Målgrupper som ser likadana ut ger intelligenta insikter om var och en av era målgrupper och utnyttjar maskininlärningsbaserade insikter för att identifiera och inrikta er på värdefulla kunder med era marknadsföringskampanjer. Med lookalike-målgrupper kan ni skapa expanderade målgrupper som riktar sig till kunder som liknar era högpresterande målgrupper eller målgrupper som liknar tidigare konverterade målgrupper. Mer information om lookalike-målgrupper finns i översikten [Look-alike-målgrupper](../../segmentation/types/account-audiences.md). |

{style="table-layout:auto"}

Mer information finns i [Segmenteringsöversikt](../../segmentation/home.md).

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Allmän tillgänglighet för [!DNL SugarCRM] | [!DNL SugarCRM] källor är nu tillgängliga. Använd källorna [!DNL SugarCRM Accounts & Contacts] och [!DNL SugarCRM Events] för att hämta data från ditt [!DNL SugarCRM]-konto till Experience Platform. Mer information finns i [[!DNL SugarCRM] översikten](../../sources/connectors/crm/sugarcrm.md). |
| Stöd för on-demand-inmatning för källdataflöden i användargränssnittet | Nu kan du skapa flödeskörningar på begäran för ett befintligt källdataflöde i användargränssnittet. Mer information finns i guiden om att [skapa ett on demand-flöde för källor med användargränssnittet](../../sources/tutorials/ui/on-demand-ingestion.md). |
| Stöd för det nya fältet `correlationID` för Adobe Analytics | Fältet `_experience.decisioning.propositions.scopeDetails.correlationID` är nu tillgängligt i Adobe Analytics källanslutningsschema. Det här fältet används som stöd för A4T-klassificeringar och kommer att fyllas i från och med september 2023. |

{style="table-layout:auto"}

Mer information finns i [källöversikten](../../sources/home.md).
