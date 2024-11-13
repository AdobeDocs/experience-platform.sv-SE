---
title: Översikt över datastreams
description: Lär dig hur datastreams hjälper dig att koppla samman din integrering med Experience Platform SDK på klientsidan med Adobe-produkter och tredjepartsmål.
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: e3768a3f695abeedc9a3ce2fef591c6ecae9a897
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 0%

---

# Översikt över datastreams

En datastream representerar serversideskonfigurationen för Adobe Experience Platform Web och Mobile SDK. Medan kommandot [`configure`](/help/web-sdk/commands/configure/overview.md) i SDK hanterar klientinställningar (till exempel `edgeDomain`) hanterar datastreams alla andra konfigurationer.

När du skickar en begäran till Edge Network refererar `datastreamId` till datastream där data skickas. På så sätt kan du uppdatera konfigurationen på serversidan utan att ändra webbplatsens kod.

Du kan skapa och hantera datastölar genom att välja **[!UICONTROL Datastreams]** i den vänstra navigeringen i användargränssnittet för Adobe Experience Platform eller datainsamling.

![Fliken Datastreams i användargränssnittet](assets/overview/datastreams-tab.png)

Mer information om hur du konfigurerar ett datastam i användargränssnittet finns i [konfigurationsguiden](./configure.md).

## Hantera känsliga data i datastreams {#sensitive}

>[!IMPORTANT]
>
>Innehållet i detta dokument är inte juridisk rådgivning och är inte avsett att ersätta juridisk rådgivning. Rådfråga företagets juridiska avdelning om råd angående hanteringen av känsliga uppgifter.

Regler och krav för datahantering på företag ökar restriktionerna för hur känsliga kunddata kan samlas in, behandlas och användas. Detta innefattar insamling, behandling och användning av data om skyddad hälsa (PHI), som omfattas av bestämmelser som HIPAA (Health Insurance Portability and Accounability Act).

Datastreams erbjuder tre metoder som hjälper dig att hantera känsliga data på ett säkert sätt:

* [Förbättrad kryptering](#encryption)
* [Dataförvaltning](#governance)
* [Granskningsloggar](#audit-logs)

### Förbättrad kryptering {#encryption}

Alla data som överförs genom Edge Network utförs via säkra, krypterade anslutningar med [HTTPS TLS 1.2](https://datatracker.ietf.org/doc/html/rfc5246). Om datastream hämtar in data till Experience Platform krypteras data sedan i vila i Experience Platform datasjön. Mer information finns i dokumentet om [datakryptering i Experience Platform](../landing/governance-privacy-security/encryption.md).

### Dataförvaltning {#governance}

Datastreams använder de inbyggda datastyrningsfunktionerna i Experience Platform för att förhindra att känsliga data skickas till icke-HIPAA-klara tjänster. Genom att etikettera specifika fält som innehåller känsliga data i dina datastream-scheman kan du få detaljkontroll över vilka datafält som kan användas för särskilda ändamål.

I följande video visas en kort översikt över hur dataanvändningsbegränsningar konfigureras och används för datastreams i användargränssnittet:

>[!VIDEO](https://video.tv.adobe.com/v/3409588/?quality=12&learn=on&speedcontrol=on)

I Experience Platform kan du använda [känsliga dataanvändningsetiketter](../data-governance/labels/reference.md#sensitive) på scheman och fält som innehåller data som din organisation anser vara känsliga. Etiketten `RHD` används till exempel för att beteckna PHI (Protected Health Information) och etiketten `S1` representerar data för geopositionering.

>[!NOTE]
>
>Mer information om hur du använder dataanvändningsetiketter på fliken [!UICONTROL Schemas] i användargränssnittet för Experience Platform och datainsamling finns i [schemaetikettsjälvstudiekursen](../xdm/tutorials/labels.md).

När du skapar en datastream, och det markerade schemat innehåller etiketter för känslig dataanvändning, kan du bara konfigurera datastream så att data skickas till HIPAA-klara mål. För närvarande är Adobe Experience Platform den enda HIPAA-klara destinationen som stöds av datastreams. Andra destinationstjänster som Adobe Target, Adobe Analytics, Adobe Audience Manager, händelsevidarebefordran och edge-mål är inaktiverade för datastreams som innehåller etiketter för känslig dataanvändning.

Om ett schema används i en befintlig datastam med tjänster som inte är HIPAA-förberedda, kommer ett försök att lägga till en känslig dataanvändningsetikett till schemat att resultera i ett principbrytningsmeddelande och åtgärden förhindras. Meddelandet anger vilken datastream som utlöste överträdelsen och föreslår att alla tjänster som inte är HIPAA-klara tas bort från datastream för att lösa problemet.

### Granskningsloggar

I Experience Platform kan datastream-aktiviteter övervakas i form av granskningsloggar. Granskningsloggarna anger **vem** utförde **vad**-åtgärden och **när**, tillsammans med andra kontextuella data som kan hjälpa dig att felsöka problem som rör datastreams för att hjälpa ditt företag att följa företagets policyer för datahantering och lagstadgade krav.

Varje gång en användare skapar, uppdaterar eller tar bort ett dataflöde skapas en granskningslogg för att spela in åtgärden. Samma sak händer när en användare skapar, uppdaterar eller tar bort en mappning via [Dataprep för datainsamling](./data-prep.md). Oavsett om det var en datastream eller en mappning som uppdaterades, kategoriseras den resulterande granskningsloggen under resurstypen [!UICONTROL Datastreams].

Mer information om hur du tolkar loggar från dataströmmar och andra tjänster som stöds finns i dokumentationen om [granskningsloggar](../landing/governance-privacy-security/audit-logs/overview.md).

## Nästa steg

Den här guiden ger en översikt på hög nivå över datastreams och deras användning i datainsamling och bearbetning av känsliga data. Anvisningar om hur du konfigurerar ett nytt datastream finns i [konfigurationsguiden för datastream](./configure.md).
