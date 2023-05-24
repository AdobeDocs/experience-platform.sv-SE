---
title: Versionsinformation om Adobe Experience Platform, februari 2023
description: Versionsinformation från februari 2023 för Adobe Experience Platform.
exl-id: 1c30a646-d9f8-4749-ac25-40bc48365a40
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1252'
ht-degree: 3%

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

Adobe Experience Platform erbjuder en serie teknologier som gör att ni kan samla in kundupplevelsedata på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omformas och distribueras till Adobe eller andra destinationer än Adobe.

### Säkerhet {#assurance}

Med Adobe Assurance kan ni inspektera, bevisa, simulera och validera hur ni samlar in data eller levererar upplevelser i er mobilapp.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Offentliga API:er | API:erna för Adobe Assurance är nu tillgängliga. Assurance-API:erna är en samling API:er som gör det möjligt för användare att testa och felsöka sina egna webb- och mobilappar när de är utrustade med Adobe Assurance-tillägget med Mobile SDK. Läs mer om API:erna för försäkringar i [Översikt över Assurance API](https://developer.adobe.com/adobe-assurance-public-apis/). |

{style="table-layout:auto"}

Mer information om Assurance finns i [Assurance-dokumentation](https://developer.adobe.com/client-sdks/documentation/platform-assurance/).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

**Nya eller uppdaterade funktioner** {#destinations-new-updated-features}

| Funktion | Beskrivning |
| ----------- | ----------- |
| [Förbättrad profil för samtycke](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) för integrering med [filbaserade (batch) mål](/help/destinations/destination-types.md#file-based) | <p> När profiler inte längre är kvalificerade för en samtyckespolicy meddelar Experience Platform nu aktivt sin policy att avsluta sina filbaserade destinationer. Detta följer [från februari 2023](/help/release-notes/2023/january-2023.md#destinations-new-updated-functionality) av samma funktionalitet för direktuppspelningsdestinationer. </p> <p> <b>Anteckning</b>: Den här funktionen är endast tillgänglig för kunder som har **[!UICONTROL Privacy and Security Shield]** och **[!UICONTROL Healthcare Shield]**. </p> |

{style="table-layout:auto"}

**Ny eller uppdaterad dokumentation** {#destinations-new-updated-documentation}

| Dokumentation | Beskrivning |
| ----------- | ----------- |
| Dokumentation om hur destinationer fungerar | <p>Vi har publicerat tre nya artiklar om hur destinationer fungerar, baserat på vanliga frågor från användarna:</p> <p><ul><li>[Konfigurerbara och gemensamma exportinställningar för destinationer](/help/destinations/how-destinations-work/destinations-configurations.md)</li><li>[Profilexportbeteende för olika måltyper](/help/destinations/how-destinations-work/profile-export-behavior.md)</li><li>[Identitetshantering i arbetsflödet för målaktivering](/help/destinations/how-destinations-work/identity-handling.md)</li></p> |

Mer allmän information om destinationer finns i [destinationer, översikt](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM är en öppen källkodsspecifikation som innehåller gemensamma strukturer och definitioner (scheman) för data som hämtas till Adobe Experience Platform. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation för att ge insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut i personaliseringssyfte.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Borttagning av fält via användargränssnittet | Nu kan du [ta bort fält från scheman efter att data har importerats](../../xdm/tutorials/field-deprecation-ui.md). Med XDM-fältborttagning kan du ta bort fält från användargränssnittsvyn samtidigt som du behåller dem för användning. Du kan visa inaktuella fält igen om det behövs, och eventuella segment, frågor eller lösningar längre fram i kedjan som refererar till fälten kommer att fungera som vanligt. |

{style="table-layout:auto"}

**Nya XDM-komponenter**

| Komponenttyp | Namn | Beskrivning |
| --- | --- | --- |
| Klass | [[!UICONTROL XDM Individual Prospect Profile]](https://github.com/adobe/xdm/pull/1669/files) | Klassen XDM Individual Prospect Profile innehåller ID:n som tillhandahålls av partner. |

{style="table-layout:auto"}

**Uppdaterade XDM-komponenter**

| Komponenttyp | Namn | Beskrivning |
| --- | --- | --- |
| Fältgrupp | [!UICONTROL Frequency Capping Constraints] | The [!UICONTROL Frequency Capping Constraints] fältgruppen har [uppdaterat för att stödja upprepningar och anpassade händelser](https://github.com/adobe/xdm/pull/1641/files). |
| Datatyp | [!UICONTROL Web referrer] | Egenskaper för webbreferenten har [uppdaterat för att inkludera `xdm:linkName` och `xdm:linkRegion`](https://github.com/adobe/xdm/pull/1666/files). Det här är namnet och regionen för det HTML-element som markerades på föregående sida. |
| Fältgrupp | [!UICONTROL Adobe CJM ExperienceEvent - Message interaction details] | [The [!UICONTROL Tracker URL] fältet lades till](https://github.com/adobe/xdm/pull/1665/files) till [!UICONTROL Adobe CJM ExperienceEvent]. Denna spårare tillhandahåller den URL som användaren har valt. |
| Fältgrupp | [!UICONTROL Adobe CJM ExperienceEvent - Message interaction detail] | [De tomma `meta:enum` egenskapen togs bort](https://github.com/adobe/xdm/pull/1668/files) från URL:en [!UICONTROL Tracking Type] fält. |
| Datatyp | [!UICONTROL Media information] | [Regex-mönstret från `videoSegment` egenskap i [!UICONTROL Media information] datatypen har tagits bort](https://github.com/adobe/xdm/pull/1667/files). |

{style="table-layout:auto"}

Mer information om XDM in Platform finns i [XDM - systemöversikt](../../xdm/home.md). &#x200B;

## Frågetjänst {#query-service}

Med frågetjänsten kan du använda standard-SQL för att fråga data i Adobe Experience Platform [!DNL Data Lake]. Du kan ansluta alla datauppsättningar från datasjön och samla in frågeresultaten som en ny datauppsättning som kan användas i rapporter, Data Science Workspace eller för att matas in i kundprofilen i realtid.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Aktivera datauppsättningar för profil med SQL | [Använd ETIKETTER i CTAS-frågor för att göra datauppsättningen &#39;profile enabled&#39;](../../query-service/sql/syntax.md#create-table-as-select)eller använd ALTER för att uppdatera befintliga datauppsättningar som ska aktiveras för profilen. Du kan använda den här utökade SQL-konstruktionen för att tillhandahålla sömlöst stöd för härledda attribut för dina affärssituationer med kundprofiler i realtid. Se [Sömlöst SQL-flöde för härledda attributdokument](../../query-service/data-distiller/derived-attributes/seamless-sql-flow.md) för mer information. |
| Övervaka schemalagda frågor | Använd [Fliken Schemalagda frågor](../../query-service/ui/monitor-queries.md) om du vill hitta viktig information om frågekörningar och prenumerera på aviseringar. Övervaka frågor för schemainformation, status och felmeddelanden/koder om de misslyckas. |
| Funktionen Komplettera automatiskt | Eliminera vissa metadatakommandon och förbättra bearbetningstiden med [växla funktionen för automatisk komplettering av frågeredigeraren](../../query-service/ui/user-guide.md#auto-complete). Den här funktionen föreslår automatiskt möjliga SQL-nyckelord och tabelldetaljer för frågan när du skriver den. |
| Datauppsättningsexempel | Ange en samplingsfrekvens i din fråga och [använda datauppsättningsexempel för att skapa ett enhetligt slumpmässigt urval](../../query-service/essential-concepts/dataset-samples.md)eller skapa villkorliga exempel baserat på specifika villkor. |

{style="table-layout:auto"}

Mer information om frågetjänster finns i [Översikt över frågetjänsten](../../query-service/home.md).


## Real-Time Customer Data Platform B2B-utgåva {#b2b}

Real-Time CDP B2B Edition bygger på Real-time Customer Data Platform (Real-Time CDP) och är särskilt framtagen för marknadsförare som använder en tjänstmodell som bygger på business-to-business. Den sammanför data från flera källor och kombinerar dem i en enda vy över personer och kontoprofiler. Tack vare dessa enhetliga data kan marknadsförarna inrikta sig exakt på specifika målgrupper och engagera dessa målgrupper i alla tillgängliga kanaler.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Aktivera tjänsten för relaterade konton | Med den nya växlingsfunktionen kan du aktivera den relaterade kontotjänsten på ditt konto. Mer information finns i guiden [aktivera tjänsten för relaterade konton](../../rtcdp/b2b-ai-ml-services/related-accounts.md#enable). |

{style="table-layout:auto"}

Läs mer om Real-Time CDP B2B Edition i [Real-Time CDP B2B Edition - översikt](../../rtcdp/overview.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och göra det möjligt att strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Ange åtkomst på prenumerationsnivå med [!DNL Google PubSub] | Nu kan du definiera åtkomst till en specifik ämnesprenumeration när du använder [!DNL Google PubSub] genom att ange prenumerations-ID vid autentisering. Mer information finns i [!DNL Google PubSub] självstudiekurs om autentisering [med API:t för Flow Service](../../sources/tutorials/api/create/cloud-storage/google-pubsub.md) eller [Plattformsgränssnitt](../../sources/tutorials/ui/create/cloud-storage/google-pubsub.md). |
| Infoga anpassade aktivitetsdata från [!DNL Marketo] | Nu kan du hämta anpassade aktivitetsdata från [!DNL Marketo] -instans till Experience Platform. Om du vill importera anpassade aktivitetsdata måste du skapa anpassade aktivitetsfältgrupper i B2B-aktivitetsschemat och skapa ett dataflöde med aktivitetsdatauppsättningen. När dataflödet är klart innehåller den inkapslade datauppsättningen både standardaktiviteter och anpassade aktiviteter från din [!DNL Marketo] -instans. Du kan sedan använda [Frågetjänst](../../query-service/home.md) för att få tillgång till dina anpassade aktivitetsposter på Platform. Mer information finns i guiden [skapa ett dataflöde för anpassade aktivitetsdata](../../sources/tutorials/ui/create/adobe-applications/marketo-custom-activities.md). |
| Exkludera ej begärda konton från [!DNL Marketo] | Du kan nu konfigurera om du vill exkludera eller ta med ej ianspråktagna konton från inmatningen när du skapar ett dataflöde för företagsdata. Mer information finns i guiden [skapa en källanslutning och ett dataflöde för [!DNL Marketo]](../../sources/tutorials/ui/create/adobe-applications/marketo.md). |

{style="table-layout:auto"}

Läs mer om källor i [källöversikt](../../sources/home.md).
