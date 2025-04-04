---
title: Versionsinformation om Adobe Experience Platform – februari 2023
description: Versionsinformationen för Adobe Experience Platform från februari 2023.
exl-id: 1c30a646-d9f8-4749-ac25-40bc48365a40
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1218'
ht-degree: 29%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 22 februari 2023**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Datainsamling](#data-collection)
- [[!DNL Destinations]](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Frågetjänst](#query-service)
- [Real-Time Customer Data Platform B2B-utgåva](#b2b)
- [Källor](#sources)

## Datainsamling {#data-collection}

Adobe Experience Platform tillhandahåller en uppsättning tekniker som gör att du kan samla in kundupplevelsedata på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omvandlas och distribueras till mål inom eller utanför Adobe.

### Assurance {#assurance}

Med Adobe Assurance kan ni inspektera, bevisa, simulera och validera hur ni samlar in data eller levererar upplevelser i er mobilapp.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Offentliga API:er | Adobe Assurance API:er är nu tillgängliga. Assurance API:er är en samling API:er som gör det möjligt för användare att testa och felsöka sina egna webb- och mobilappar när de är utrustade med Adobe Assurance-tillägget med Mobile SDK. Mer information om Assurance API:er finns i [Assurance API-översikt](https://developer.adobe.com/adobe-assurance-public-apis/). |

{style="table-layout:auto"}

Mer information om Assurance finns i [Assurance-dokumentationen](https://developer.adobe.com/client-sdks/documentation/platform-assurance/).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Adobe Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Nya eller uppdaterade funktioner** {#destinations-new-updated-features}

| Funktion | Beskrivning |
| ----------- | ----------- |
| [Förbättrad sambandsprincip](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) för integrering med [filbaserade (batch) mål](/help/destinations/destination-types.md#file-based) | <p> När profiler inte längre är kvalificerade för en samtyckespolicy meddelar Experience Platform nu aktivt sin policy att avsluta sina filbaserade mål. Detta följer [versionen i februari 2023](/help/release-notes/2023/january-2023.md#destinations-new-updated-functionality) av samma funktionalitet för direktuppspelningsmål. </p> <p> <b>Obs!</b>: Den här funktionen är bara tillgänglig för kunder med **[!UICONTROL Privacy and Security Shield]** och för **[!UICONTROL Healthcare Shield]**. </p> |

{style="table-layout:auto"}

**Ny eller uppdaterad dokumentation** {#destinations-new-updated-documentation}

| Dokumentation | Beskrivning |
| ----------- | ----------- |
| Dokumentation om hur destinationer fungerar | <p>Vi har publicerat tre nya artiklar om hur destinationer fungerar, baserat på vanliga frågor från användarna:</p> <p><ul><li>[Konfigurerbara och gemensamma exportinställningar i mål](/help/destinations/how-destinations-work/destinations-configurations.md)</li><li>[Profilexportbeteende för olika måltyper](/help/destinations/how-destinations-work/profile-export-behavior.md)</li><li>[Identitetshantering i arbetsflödet för målaktivering](/help/destinations/how-destinations-work/identity-handling.md)</li></p> |

Mer allmän information om destinationer finns i [målöversikten](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM är en specifikation med öppen källkod som tillhandahåller gemensamma strukturer och definitioner (scheman) för data som förs in i Adobe Experience Platform. Genom att följa XDM-standarder kan all data om kundupplevelsen införlivas i en gemensam representation för att leverera insikter på ett snabbare och mer integrerat sätt. Du kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut för personalisering.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Borttagning av fält via användargränssnittet | Du kan nu [ta bort fält från dina scheman efter att data har importerats](../../xdm/tutorials/field-deprecation-ui.md). Med XDM-fältborttagning kan du ta bort fält från användargränssnittsvyn samtidigt som du behåller dem för användning. Du kan visa inaktuella fält igen om det behövs, och eventuella segment, frågor eller lösningar längre ned som refererar till fälten kommer att köras som vanligt. |

{style="table-layout:auto"}

**Nya XDM-komponenter**

| Komponenttyp | Namn | Beskrivning |
| --- | --- | --- |
| Klass | [[!UICONTROL XDM Individual Prospect Profile]](https://github.com/adobe/xdm/pull/1669/files) | Klassen XDM Individual Prospect Profile innehåller ID:n som tillhandahålls av partner. |

{style="table-layout:auto"}

**Uppdaterade XDM-komponenter**

| Komponenttyp | Namn | Beskrivning |
| --- | --- | --- |
| Fältgrupp | [!UICONTROL Frequency Capping Constraints] | Fältgruppen [!UICONTROL Frequency Capping Constraints] har [uppdaterats för att stödja upprepningar och anpassade händelser](https://github.com/adobe/xdm/pull/1641/files). |
| Datatyp | [!UICONTROL Web referrer] | Egenskaperna för webbreferenten har [uppdaterats så att de inkluderar `xdm:linkName` och `xdm:linkRegion`](https://github.com/adobe/xdm/pull/1666/files). Detta är namnet och regionen för det HTML-element som markerades på föregående sida. |
| Fältgrupp | [!UICONTROL Adobe CJM ExperienceEvent - Message interaction details] | [Fältet [!UICONTROL Tracker URL] lades till ](https://github.com/adobe/xdm/pull/1665/files) i [!UICONTROL Adobe CJM ExperienceEvent]. Denna spårare tillhandahåller den URL som användaren har valt. |
| Fältgrupp | [!UICONTROL Adobe CJM ExperienceEvent - Message interaction detail] | [Den tomma egenskapen `meta:enum` togs bort](https://github.com/adobe/xdm/pull/1668/files) från fältet URL [!UICONTROL Tracking Type]. |
| Datatyp | [!UICONTROL Media information] | [Regex-mönstret från egenskapen `videoSegment` i datatypen [!UICONTROL Media information] har tagits bort](https://github.com/adobe/xdm/pull/1667/files). |

{style="table-layout:auto"}

Mer information om XDM i Experience Platform finns i [XDM-systemöversikt](../../xdm/home.md). &#x200B;

## Frågetjänst {#query-service}

Med frågetjänsten kan du använda standard SQL för att söka efter data i Adobe Experience Platform [!DNL Data Lake]. Du kan koppla samman alla datauppsättningar från datasjön och fånga upp sökresultaten som en ny datauppsättning för användning i rapportering, arbetsyta för datavetenskap eller för inmatning i kundprofil i realtid.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Aktivera datauppsättningar för profil med SQL | [Använd ETIKETTER i CTAS-frågor för att göra datauppsättningen &#39;profile enabled&#39;](../../query-service/sql/syntax.md#create-table-as-select), eller använd ALTER för att uppdatera befintliga datauppsättningar som ska aktiveras för profilen. Du kan använda den här utökade SQL-konstruktionen för att ge sömlös support för härledda datauppsättningar för dina affärssituationer med kundprofiler i realtid. Mer information finns i [Sömlöst SQL-flöde för härledda datauppsättningsdokument](../../query-service/data-distiller/derived-datasets/create-derived-datasets-with-sql.md). |
| Övervaka schemalagda frågor | Använd fliken [Schemalagda frågor](../../query-service/ui/monitor-queries.md) för att hitta viktig information om frågekörningar och prenumerera på aviseringar. Övervaka frågor för schemainformation, status och felmeddelanden/koder om de misslyckas. |
| Funktionen Komplettera automatiskt | Ta bort vissa metadatakommandon och förbättra bearbetningstiden genom att [växla funktionen för automatisk komplettering av frågeredigeraren](../../query-service/ui/user-guide.md#auto-complete). Den här funktionen föreslår automatiskt möjliga SQL-nyckelord och tabelldetaljer för frågan när du skriver den. |
| Datauppsättningsexempel | Ange en samplingsfrekvens i din fråga och [använd datauppsättningsexempel för att skapa ett enhetligt slumpmässigt urval](../../query-service/key-concepts/dataset-samples.md), eller skapa villkorsstyrda exempel baserat på specifika villkor. |

{style="table-layout:auto"}

Mer information om frågetjänster finns i [översikten över frågetjänster](../../query-service/home.md).


## Real-Time Customer Data Platform B2B-utgåva {#b2b}

Real-Time CDP B2B edition bygger på Real-Time Customer Data Platform (Real-Time CDP) och är utformat för marknadsförare som arbetar i en affärs-till-affärstjänstmodell. Den sammanför data från flera källor och kombinerar dem i en enda vy över personer och kontoprofiler. Tack vare dessa enhetliga data kan marknadsförarna inrikta sig exakt på specifika målgrupper och engagera dessa målgrupper i alla tillgängliga kanaler.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Aktivera tjänsten för relaterade konton | Med den nya växlingsfunktionen kan du aktivera den relaterade kontotjänsten på ditt konto. Mer information finns i guiden om att [aktivera den relaterade kontotjänsten](../../rtcdp/b2b-ai-ml-services/related-accounts.md#enable). |

{style="table-layout:auto"}

Läs [Real-Time CDP B2B edition overview](../../rtcdp/overview.md) om du vill veta mer om Real-Time CDP B2B edition.

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och göra det möjligt att strukturera, etikettera och förbättra dessa data med hjälp av Experience Platform tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Ange åtkomst på prenumerationsnivå med [!DNL Google PubSub] | Du kan nu definiera åtkomst till en specifik ämnesprenumeration när du använder källan [!DNL Google PubSub] genom att ange prenumerations-ID:t när du autentiserar. Mer information finns i självstudiekursen [!DNL Google PubSub] om autentisering [med API:t för Flow Service ](../../sources/tutorials/api/create/cloud-storage/google-pubsub.md) eller [Experience Platform UI](../../sources/tutorials/ui/create/cloud-storage/google-pubsub.md). |
| Infoga anpassade aktivitetsdata från [!DNL Marketo] | Du kan nu hämta anpassade aktivitetsdata från din [!DNL Marketo]-instans till Experience Platform. Om du vill importera anpassade aktivitetsdata måste du skapa anpassade aktivitetsfältgrupper i B2B-aktivitetsschemat och skapa ett dataflöde med aktivitetsdatauppsättningen. När dataflödet är klart innehåller den inkapslade datauppsättningen både standardaktiviteter och anpassade aktiviteter från din [!DNL Marketo]-instans. Du kan sedan använda [frågetjänsten](../../query-service/home.md) för att komma åt dina anpassade aktivitetsposter på Experience Platform. Mer information finns i guiden om att [skapa ett dataflöde för anpassade aktivitetsdata](../../sources/tutorials/ui/create/adobe-applications/marketo-custom-activities.md). |
| Exkludera ej begärda konton från [!DNL Marketo] | Du kan nu konfigurera om du vill exkludera eller ta med ej ianspråktagna konton från inmatningen när du skapar ett dataflöde för företagsdata. Mer information finns i guiden om att [skapa en källanslutning och ett dataflöde för  [!DNL Marketo]](../../sources/tutorials/ui/create/adobe-applications/marketo.md). |

{style="table-layout:auto"}

Mer information om källor finns i [översikten över källor](../../sources/home.md).
