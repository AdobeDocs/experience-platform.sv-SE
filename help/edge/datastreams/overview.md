---
title: Översikt över dataströmmar
description: Koppla samman integreringen av SDK för Experience Platform på klientsidan med Adobe-produkter och tredjepartsdestinationer.
keywords: konfiguration;datastreams;datastreamId;edge;datastream id;Environment Settings;edgeConfigId;identity;id sync enabled;ID Sync Container ID;Sandbox;Streaming Inlet;Event Dataset;target;client code;Property Token;Target Environment ID;Cookie Destination;url Destinations;Analytics Settings Blockreport suite;Data Prep för datainsamling;Data Prep;Mapper;XDM Mapper;Mapper on Edge;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 2cec87d3f45b1b774925a9b669b53a958e65e57a
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 1%

---

# Översikt över datastreams

En datastream representerar konfigurationen på serversidan när Adobe Experience Platform Web och Mobile SDK implementeras. Med [konfigurera, kommando](../fundamentals/configuring-the-sdk.md) i SDK styr saker som måste hanteras på klienten (till exempel `edgeDomain`) hanterar datastreams alla andra konfigurationer för SDK. När en begäran skickas till Adobe Experience Platform Edge Network `edgeConfigId` används för att referera till datastream. På så sätt kan du uppdatera konfigurationen på serversidan utan att behöva göra kodändringar på webbplatsen.

Du kan skapa och hantera datastreams genom att välja **[!UICONTROL Datastreams]** i den vänstra navigeringen i Adobe Experience Platform användargränssnitt eller användargränssnittet för datainsamling.

![Fliken Datastreams i användargränssnittet](../assets/datastreams/overview/datastreams-tab.png)

Mer information om hur du konfigurerar ett datastream i användargränssnittet finns i [konfigurationsguide](./configure.md).

## Hantera känsliga data i datastreams {#sensitive}

>[!IMPORTANT]
>
>Innehållet i detta dokument är inte juridisk rådgivning och är inte avsett att ersätta juridisk rådgivning. Rådfråga företagets juridiska avdelning om råd angående hanteringen av känsliga uppgifter.

Regler och krav för datahantering på företag ökar restriktionerna för hur känsliga kunddata kan samlas in, behandlas och användas. Detta innefattar insamling, behandling och användning av data om skyddad hälsa (PHI), som omfattas av bestämmelser som HIPAA (Health Insurance Portability and Accounability Act).

Datastreams erbjuder tre metoder som hjälper dig att hantera känsliga data på ett säkert sätt:

* [Förbättrad kryptering](#encryption)
* [Datastyrning](#governance)
* [Granskningsloggar](#audit-logs)

### Förbättrad kryptering {#encryption}

Alla data som överförs genom Edge Network utförs via säkra, krypterade anslutningar med [HTTPS TLS 1.2](https://datatracker.ietf.org/doc/html/rfc5246). Om datastream hämtar in data till Experience Platform krypteras data sedan i vila i Experience Platform datasjön. Visa dokumentet på [datakryptering i Experience Platform](../../landing/governance-privacy-security/encryption.md) för mer information.

### Datastyrning {#governance}

Datastreams utnyttjar Experience Platform inbyggda funktioner för datastyrning för att förhindra att känsliga data skickas till icke-HIPAA-klara tjänster. Genom att etikettera specifika fält som innehåller känsliga data i dina datastream-scheman kan du få detaljkontroll över vilka datafält som kan användas för särskilda ändamål.

I följande video visas en kort översikt över hur dataanvändningsbegränsningar konfigureras och används för datastreams i användargränssnittet:

>[!VIDEO](https://video.tv.adobe.com/v/3409588/?quality=12&learn=on&speedcontrol=on)

I Experience Platform kan du använda [etiketter för känslig dataanvändning](../../data-governance/labels/reference.md#sensitive) till scheman och fält som innehåller data som din organisation anser vara känsliga. Till exempel `RHD` Etiketten används för att beteckna Skyddad hälsoinformation (PHI) och `S1` label representerar geopositioneringsdata.

>[!NOTE]
>
>Mer information om hur du använder dataetiketter i [!UICONTROL Schemas] -fliken i användargränssnittet eller användargränssnittet för datainsamling i Experience Platform finns i [självstudiekurs om schemamärkning](../../xdm/tutorials/labels.md).

När du skapar en ny datastream kan datastream bara konfigureras för att skicka data till HIPAA-klara mål om det valda schemat innehåller etiketter för känslig dataanvändning. För närvarande är Adobe Experience Platform den enda HIPAA-klara destinationen som stöds av datastreams. Andra destinationstjänster som Adobe Target, Adobe Analytics, Adobe Audience Manager, händelsevidarebefordran och edge-mål är inaktiverade för datastreams som innehåller etiketter för känslig dataanvändning.

Om ett schema används i en befintlig datastam med tjänster som inte är HIPAA-förberedda, kommer ett försök att lägga till en känslig dataanvändningsetikett till schemat att resultera i ett principbrytningsmeddelande och åtgärden förhindras. Meddelandet anger vilken datastream som utlöste överträdelsen och föreslår att alla tjänster som inte är HIPAA-klara tas bort från datastream för att lösa problemet.

### Granskningsloggar

I Experience Platform kan datastream-aktiviteter övervakas i form av granskningsloggar. En granskningslogg anger **som** utförd **vad** och **när**, tillsammans med andra kontextuella data som kan hjälpa er att felsöka problem som rör datastreams för att hjälpa ert företag att följa företagets policyer för datahantering och lagstadgade krav.

Varje gång en användare skapar, uppdaterar eller tar bort ett dataflöde skapas en granskningslogg för att spela in åtgärden. Samma sak händer när en användare skapar, uppdaterar eller tar bort en mappning via [Dataförberedelse för datainsamling](./data-prep.md). Oavsett om det var en datastream eller en mappning som uppdaterades, kategoriseras den resulterande granskningsloggen under [!UICONTROL Datastreams] resurstyp.

Läs dokumentationen om [granskningsloggar](../../landing/governance-privacy-security/audit-logs/overview.md) om du vill ha mer information om hur du tolkar loggar från datastreams och andra tjänster som stöds.

## Nästa steg

Den här guiden ger en översikt på hög nivå över datastreams och deras användning i datainsamling och bearbetning av känsliga data. Anvisningar om hur du konfigurerar ett nytt datastream finns i [konfigurationsguide för datastream](./configure.md).
