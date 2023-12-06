---
title: Översikt över datastreams
description: Lär dig hur datastreams hjälper dig att koppla samman din integrering med Experience Platform SDK på klientsidan med Adobe-produkter och tredjepartsmål.
source-git-commit: 68174928d3b005d1e5a31b17f3f287e475b5dc86
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 0%

---


# Översikt över datastreams

En datastream representerar konfigurationen på serversidan när Adobe Experience Platform Web och Mobile SDK implementeras. Med [konfigurera](../edge/fundamentals/configuring-the-sdk.md) -kommandot i SDK styr saker som måste hanteras på klienten (till exempel `edgeDomain`) hanterar datastreams alla andra konfigurationer för SDK. När en begäran skickas till Adobe Experience Platform Edge Network `edgeConfigId` används för att referera till datastream. På så sätt kan du uppdatera konfigurationen på serversidan utan att behöva göra kodändringar på webbplatsen.

Du kan skapa och hantera datastreams genom att välja **[!UICONTROL Datastreams]** i den vänstra navigeringen i Adobe Experience Platform användargränssnitt eller användargränssnittet för datainsamling.

![Fliken Datastreams i användargränssnittet](assets/overview/datastreams-tab.png)

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

Alla data som överförs genom Edge Network utförs via säkra, krypterade anslutningar med [HTTPS TLS 1.2](https://datatracker.ietf.org/doc/html/rfc5246). Om datastream hämtar in data till Experience Platform krypteras data sedan i vila i Experience Platform datasjön. Visa dokumentet på [datakryptering i Experience Platform](../landing/governance-privacy-security/encryption.md) för mer information.

### Datastyrning {#governance}

Datastreams använder de inbyggda datastyrningsfunktionerna i Experience Platform för att förhindra att känsliga data skickas till icke-HIPAA-klara tjänster. Genom att etikettera specifika fält som innehåller känsliga data i dina datastream-scheman kan du få detaljkontroll över vilka datafält som kan användas för särskilda ändamål.

I följande video visas en kort översikt över hur dataanvändningsbegränsningar konfigureras och används för datastreams i användargränssnittet:

>[!VIDEO](https://video.tv.adobe.com/v/3409588/?quality=12&learn=on&speedcontrol=on)

I Experience Platform kan du använda [etiketter för känslig dataanvändning](../data-governance/labels/reference.md#sensitive) till scheman och fält som innehåller data som din organisation anser vara känsliga. Till exempel `RHD` Etiketten används för att beteckna Skyddad hälsoinformation (PHI) och `S1` label representerar geopositioneringsdata.

>[!NOTE]
>
>Mer information om hur du använder dataetiketter i [!UICONTROL Schemas] -fliken i användargränssnittet eller användargränssnittet för datainsamling i Experience Platform finns i [självstudiekurs om schemamärkning](../xdm/tutorials/labels.md).

När du skapar en datastream, och det markerade schemat innehåller etiketter för känslig dataanvändning, kan du bara konfigurera datastream så att data skickas till HIPAA-klara mål. För närvarande är Adobe Experience Platform den enda HIPAA-klara destinationen som stöds av datastreams. Andra destinationstjänster som Adobe Target, Adobe Analytics, Adobe Audience Manager, händelsevidarebefordran och edge-mål är inaktiverade för datastreams som innehåller etiketter för känslig dataanvändning.

Om ett schema används i en befintlig datastam med tjänster som inte är HIPAA-förberedda, kommer ett försök att lägga till en känslig dataanvändningsetikett till schemat att resultera i ett principbrytningsmeddelande och åtgärden förhindras. Meddelandet anger vilken datastream som utlöste överträdelsen och föreslår att alla tjänster som inte är HIPAA-klara tas bort från datastream för att lösa problemet.

### Granskningsloggar

I Experience Platform kan datastream-aktiviteter övervakas i form av granskningsloggar. Granskningsloggar indikerar **som** utförd **vad** och **när**, tillsammans med andra kontextuella data som kan hjälpa er att felsöka problem som rör datastreams för att hjälpa ert företag att följa företagets policyer för datahantering och lagstadgade krav.

Varje gång en användare skapar, uppdaterar eller tar bort ett dataflöde skapas en granskningslogg för att spela in åtgärden. Samma sak händer när en användare skapar, uppdaterar eller tar bort en mappning via [Dataförberedelse för datainsamling](./data-prep.md). Oavsett om det var en datastream eller en mappning som uppdaterades, kategoriseras den resulterande granskningsloggen under [!UICONTROL Datastreams] resurstyp.

Läs dokumentationen om [granskningsloggar](../landing/governance-privacy-security/audit-logs/overview.md) för mer information om hur du tolkar loggar från datastreams och andra tjänster som stöds.

## Nästa steg

Den här guiden ger en översikt på hög nivå över datastreams och deras användning i datainsamling och bearbetning av känsliga data. Anvisningar om hur du konfigurerar ett nytt datastream finns i [konfigurationsguide för datastream](./configure.md).
