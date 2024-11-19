---
keywords: Experience Platform;home;IAB;IAB 2.0;medgivande;Samtycke
solution: Experience Platform
title: Stöd för IAB TCF 2.0 i Experience Platform
description: Lär dig hur du konfigurerar dataåtgärder och scheman för att förmedla val av kundsamtycke när du aktiverar segment till mål i Adobe Experience Platform.
role: Developer
feature: Consent
exl-id: af787adf-b46e-43cf-84ac-dfb0bc274025
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '2477'
ht-degree: 0%

---

# Stöd för IAB TCF 2.0 i Experience Platform

[!DNL Transparency & Consent Framework] (TCF), som beskrivs av IAB ([!DNL Interactive Advertising Bureau]), är en öppen teknisk ram som är avsedd att göra det möjligt för organisationer att få, registrera och uppdatera konsumentens samtycke till att deras personuppgifter behandlas, i enlighet med Europeiska unionens [!DNL General Data Protection Regulation] (GDPR). Den andra versionen av ramverket, TCF 2.0, ger större flexibilitet för hur konsumenter kan ge eller vägra samtycke, inklusive om och hur leverantörer kan använda vissa funktioner för databearbetning, till exempel exakt positionering.

>[!NOTE]
>
>Mer information om TCF 2.0 finns på webbplatsen [IAB Europe](https://iabeurope.eu/), inklusive supportmaterial och tekniska specifikationer.

Adobe Experience Platform ingår i den registrerade [IAB TCF 2.0-leverantörslistan](https://iabeurope.eu/vendor-list-tcf/), under ID **565**. I enlighet med kraven för TCF 2.0 kan du med hjälp av Platform samla in data om kundernas samtycke och integrera dessa i era lagrade kundprofiler. Dessa data om samtycke kan sedan beaktas för att avgöra om profiler ska inkluderas i exporterade målgruppssegment, beroende på hur de används.

>[!IMPORTANT]
>
>Plattformen kan bara uppfylla version 2.0 av TCF (eller senare). Tidigare versioner av TCF stöds inte.

Det här dokumentet innehåller en översikt över hur du konfigurerar dataåtgärder och profilscheman för att acceptera data om kundgodkännande som genererats av din CMP (Consent Management Platform). Det handlar också om hur Platform förmedlar val av användarsamtycke vid export av segment.

## Förhandskrav

Om du vill följa med i den här guiden måste du använda en CMP, antingen kommersiell eller egen, som är integrerad och kompatibel med IAB TCF. Mer information finns i [listan över kompatibla CMP](https://iabeurope.eu/cmp-list/).

>[!IMPORTANT]
>
>Om ditt CMP-ID är ogiltigt fortsätter Platform att bearbeta dina data som de är. Om du vill använda TCF 2.0 måste du bekräfta att din CMP har ett giltigt ID som har registrerats med IAB TCF 2.0 innan du skickar data till plattformen.

Handboken kräver även en fungerande förståelse av följande plattformstjänster:

* [Experience Data Model (XDM)](/help/xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
* [Adobe Experience Platform identitetstjänst](/help/identity-service/home.md): Lös den grundläggande utmaning som en fragmentering av kundupplevelsedata innebär genom att överbrygga identiteter mellan olika enheter och system.
* [Kundprofil i realtid](/help/profile/home.md): Använder [!DNL Identity Service] för att skapa detaljerade kundprofiler från dina datauppsättningar i realtid. [!DNL Real-Time Customer Profile] hämtar data från datasjön och behåller kundprofiler i sitt eget separata datalager.
* [Adobe Experience Platform Web SDK](/help/web-sdk/home.md): Ett JavaScript-bibliotek på klientsidan som gör att du kan integrera olika plattformstjänster i kundens webbplats.
   * [SDK-medgivandekommandon](../../../../web-sdk/commands/setconsent.md): En översikt över de medgivanderelaterade SDK-kommandona som visas i den här handboken.
* [Adobe Experience Platform segmenteringstjänst](/help/segmentation/home.md): Gör att du kan dela in [!DNL Real-Time Customer Profile]-data i grupper med individer som delar liknande egenskaper och svarar på liknande sätt som marknadsföringsstrategier.

Utöver de plattformstjänster som anges ovan bör du även känna till [mål](/help/data-governance/home.md) och deras roll i plattformens ekosystem.

## Sammanfattning av kundens godkännandeflöde {#summary}

I följande avsnitt beskrivs hur data om samtycke samlas in och används efter att systemet har konfigurerats korrekt.

### Samling av data för samtycke

Plattformen gör att ni kan samla in data om kundens samtycke genom följande process:

1. En kund ger sitt samtycke till datainsamling via en dialogruta på er webbplats.
1. Din CMP identifierar ändringen av medgivandeinställningen och genererar TCF-medgivandedata i enlighet med detta.
1. Med Platform Web SDK skickas genererade data om samtycke (returneras av CMP) till Adobe Experience Platform.
1. De insamlade medgivandedata är inkapslade i en [!DNL Profile]-aktiverad datauppsättning vars schema innehåller TCF-medgivandefält.

Förutom SDK-kommandon som aktiveras av CMP-kodekar för avtalsändringar kan data även flöda in i Experience Platform via alla kundgenererade XDM-data som överförs direkt till en [!DNL Profile]-aktiverad datauppsättning.

Alla segment som delas med Platform av Adobe Audience Manager (via [!DNL Audience Manager]-källkopplingen eller på annat sätt) kan också innehålla data om samtycke om rätt fält har tillämpats på dessa segment via [!DNL Experience Cloud Identity Service]. Mer information om hur du samlar in medgivandedata i [!DNL Audience Manager] finns i dokumentet om [Adobe Audience Manager-plugin-programmet för IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html).

### Efterföljande av samtycke

När TCF-medgivandedata har importerats, utförs följande processer i efterföljande plattformstjänster:

1. [!DNL Real-Time Customer Profile] uppdaterar lagrade medgivandedata för den kundens profil.
1. Plattformen behandlar endast kund-ID:n om leverantörsbehörigheten för Platform (565) anges för varje ID i ett kluster.
1. När du exporterar segment till mål som tillhör medlemmar i leverantörslistan för TCF 2.0, innehåller plattformen bara profiler om leverantörsbehörigheterna för både plattformen (565) *och* anges för varje ID i ett kluster.

Övriga avsnitt i det här dokumentet innehåller riktlinjer för hur du konfigurerar plattformen och dina dataåtgärder så att de uppfyller de krav på insamling och verkställighet som beskrivs ovan.

## Bestäm hur ni genererar data om kundsamtycke i er CMP {#consent-data}

Eftersom varje CMP-system är unikt måste ni fastställa det bästa sättet för kunderna att ge sitt samtycke när de interagerar med tjänsten. En dialog om cookie-samtycke är ett vanligt sätt att få kunden att ge sitt samtycke. Ett exempel på en CMP-dialogruta visas nedan.

![Ett exempel på en dialogruta för plattform för hantering av samtycke.](../../../images/governance-privacy-security/consent/iab/overview/cmp-dialog.png)

Den här dialogrutan måste göra det möjligt för kunden att välja att inte göra något av följande:

| Medgivandealternativ | Beskrivning |
| --- | --- |
| **Syften** | Ändamålen definierar vilka reklamsyften ett varumärke kan använda kundens data för. Följande syften måste väljas för att Platform ska kunna behandla kund-ID: <ul><li>**Syfte 1**: Lagra och/eller få åtkomst till information på en enhet</li><li>**Syfte 10**: Utveckla och förbättra produkter</li></ul> |
| **Leverantörsbehörigheter** | Utöver annonseringsteknologiska ändamål måste dialogen också göra det möjligt för kunden att välja att inte få sina data använda av specifika leverantörer, inklusive Adobe Experience Platform (565). |

### Samtyckessträngar {#consent-strings}

Oavsett vilken metod du använder för att samla in data, är målet att generera ett strängvärde baserat på de alternativ för samtycke som kunden valt, vilket kallas godkännandesträng.

I TCF-specifikationen används medgivandesträngar för att koda relevant information om en kunds medgivandeinställningar, i termer av specifika marknadsföringssyften som definieras av policyer och leverantörer. Plattformen använder dessa strängar för att lagra medgivandeinställningarna för varje kund, och därför måste en ny medgivandesträng skapas varje gång inställningarna ändras.

Samtyckessträngar kan bara skapas av en CMP som är registrerad med IAB TCF. Mer information om hur du skapar medgivandesträngar med din CMP finns i [bekräftelsesträngformateringsguiden](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) i IAB TCF GitHub-repo.

## Skapa datauppsättningar med TCF-medgivandefält {#datasets}

Data om kundsamtycke måste skickas till datauppsättningar vars scheman innehåller TCF-medgivandefält. Se självstudiekursen [Skapa datauppsättningar för att hämta TCF 2.0-medgivande](./dataset.md) för hur du skapar den profildatauppsättning som krävs (och en valfri Experience Event-datauppsättning) innan du fortsätter med den här guiden.

## Uppdatera sammanfogningsprinciper för [!DNL Profile] så att de innehåller medgivandedata {#merge-policies}

När du har skapat en [!DNL Profile]-aktiverad datauppsättning för insamling av medgivandedata måste du se till att dina sammanfogningsprinciper har konfigurerats så att de alltid innehåller TCF-medgivandefält i dina kundprofiler. Detta innebär att ange datauppsättningens prioritet så att din sambandsuppsättning prioriteras framför andra datauppsättningar som kan vara i konflikt.

Mer information om hur du arbetar med sammanfogningsprinciper finns i [översikten över sammanfogningsprinciper](/help/profile/merge-policies/overview.md). När du konfigurerar dina sammanfogningsprinciper måste du se till att dina segment innehåller alla nödvändiga medgivandeattribut som tillhandahålls av [XDM-sekretesschemafältgruppen](./dataset.md#privacy-field-group), enligt anvisningarna i guiden om datauppsättningsförberedelse.

## Integrera Experience Platform Web SDK för att samla in data om kundernas samtycke {#sdk}

>[!NOTE]
>
>Det krävs att Experience Platform Web SDK används för att bearbeta data om samtycke direkt i Adobe Experience Platform. [!DNL Experience Cloud Identity Service] stöds inte.
>
>[!DNL Experience Cloud Identity Service] stöds fortfarande för godkännandebearbetning i Adobe Audience Manager, och kompatibilitet med TCF 2.0 kräver bara att biblioteket uppdateras till [version 5.0](https://github.com/Adobe-Marketing-Cloud/id-service/releases).

När du har konfigurerat din CMP för att generera medgivandesträngar måste du integrera Experience Platform Web SDK för att samla in strängarna och skicka dem till Platform. Plattforms-SDK innehåller två kommandon som kan användas för att skicka TCF-medgivandedata till plattformen (förklaras i underavsnitten nedan). Dessa kommandon bör användas när en kund ger sitt medgivande för första gången och därefter när som helst när detta medgivande ändras.

**SDK:n samverkar inte med några CMP:er i rutan**. Det är upp till dig att bestämma hur du ska integrera SDK i din webbplats, lyssna efter medgivandeändringar i CMP och anropa lämpligt kommando.

### Skapa ett datastream

För att SDK ska kunna skicka data till Experience Platform måste du först skapa ett datastream för Platform. Specifika steg för hur du skapar ett datastam finns i [SDK-dokumentationen](/help/datastreams/overview.md).

När du har angett ett unikt namn för datastream väljer du växlingsknappen bredvid **[!UICONTROL Adobe Experience Platform]**. Använd sedan följande värden för att fylla i resten av formuläret:

| Datastream-fält | Värde |
| --- | --- |
| [!UICONTROL Sandbox] | Namnet på plattformen [sandlådan](/help/sandboxes/home.md) som innehåller den nödvändiga direktuppspelningsanslutningen och de datauppsättningar som krävs för att konfigurera dataströmmen. |
| [!UICONTROL Streaming Inlet] | En giltig direktuppspelningsanslutning för Experience Platform. Se självstudiekursen [Skapa en direktuppspelningsanslutning](/help/ingestion/tutorials/create-streaming-connection-ui.md) om du inte har ett befintligt direktuppspelningsinlopp. |
| [!UICONTROL Event Dataset] | Markera datauppsättningen [!DNL XDM ExperienceEvent] som skapades i [föregående steg](#datasets). Om du inkluderade fältgruppen [[!UICONTROL IAB TCF 2.0 Consent] ](/help/xdm/field-groups/event/iab.md) i datasetens schema kan du spåra händelser för ändring av samtycke över tiden med kommandot [`sendEvent`](#sendEvent) och lagra data i den här datauppsättningen. Kom ihåg att de medgivandevärden som lagras i den här datauppsättningen **inte** används i automatiska arbetsflöden för verkställighet. |
| [!UICONTROL Profile Dataset] | Markera datauppsättningen [!DNL XDM Individual Profile] som skapades i [föregående steg](#datasets). När du svarar på CMP-krokar för ändring av samtycke med kommandot [`setConsent`](#setConsent) lagras insamlade data i den här datauppsättningen. Eftersom den här datauppsättningen är profilaktiverad respekteras de medgivandevärden som lagras i den här datauppsättningen under automatiska arbetsflöden för verkställighet. |

![](../../../images/governance-privacy-security/consent/iab/overview/edge-config.png)

När du är klar väljer du **[!UICONTROL Save]** längst ned på skärmen och fortsätter att följa eventuella ytterligare uppmaningar för att slutföra konfigurationen.

### Kommandon för att ändra samtycke

När du har skapat dataströmmen som beskrivs i föregående avsnitt kan du börja använda SDK-kommandon för att skicka data om samtycke till plattformen. Avsnitten nedan innehåller exempel på hur varje SDK-kommando kan användas i olika scenarier.

#### Använda CMP-krokar för ändring av samtycke {#setConsent}

Många CMP-modeller har färdiga kopplingar som lyssnar på händelser om samtycke. När dessa händelser inträffar kan du använda kommandot [`setConsent`](/help/web-sdk/commands/setconsent.md) för att uppdatera kundens medgivandedata.

Kommandot `setConsent` förväntar sig två argument:

1. En sträng som anger kommandotypen (i det här fallet &quot;setConsent&quot;).
1. En nyttolast som innehåller en `consent`-matris. Arrayen måste innehålla minst ett objekt som innehåller de obligatoriska medgivandefälten.

Kommandot `setConsent` visas nedan:

```js
alloy("setConsent", {
  consent: [{
    standard: "IAB TCF",
    version: "2.0",
    value: "CLcVDxRMWfGmWAVAHCENAXCkAKDAADnAABRgA5mdfCKZuYJez-NQm0TBMYA4oCAAGQYIAAAAAAEAIAEgAA.argAC0gAAAAAAAAAAAA",
    gdprApplies: "true"
  }]
});
```

| Nyttolastegenskap | Beskrivning |
| --- | --- |
| `standard` | Den standard för samtycke som används. Värdet måste anges till `IAB` för TCF 2.0-godkännandebearbetning. |
| `version` | Versionsnumret för den medgivandestandard som anges under `standard`. Värdet måste anges till `2.0` för TCF 2.0-godkännandebearbetning. |
| `value` | Den bas-64-kodade medgivandesträngen som genererats av CMP. |
| `gdprApplies` | Ett booleskt värde som anger om GDPR gäller för den inloggade kunden. För att TCF 2.0 ska framtvingas för den här kunden måste värdet anges till `true`. Standardvärdet är `true` om inte definierat. |

Kommandot `setConsent` ska användas som en del av en CMP-krok som upptäcker ändringar i medgivandeinställningarna. Följande JavaScript innehåller ett exempel på hur kommandot `setConsent` kan användas för OneTrust-kroken `OnConsentChanged`:

```js
OneTrust.OnConsentChanged(function () {
  // Retrieve the TCF 2.0 consent data generated by the CMP, and pass it to Alloy. 
  __tcfapi("getTCData", 2, function (data, success) {
    if (success) {
      var tcString = data.tcString;
      var gdpr = data.gdprApplies;

      alloy("setConsent", {
        consent: [{
          standard: "IAB TCF",
          version: "2.0",
          value: tcString,
          gdprApplies: gdpr
        }]
      });
    }
  });
});
```

#### Använda händelser {#sendEvent}

Du kan också samla in TCF 2.0-medgivandedata för varje händelse som utlöses i Platform med kommandot `sendEvent`.

>[!NOTE]
>
>Om du vill använda den här metoden måste du ha lagt till fältgruppen Experience Event Privacy i ditt [!DNL Profile]-aktiverade [!DNL XDM ExperienceEvent]-schema. I avsnittet [Uppdatera ExperienceEvent-schemat](./dataset.md#event-schema) i guiden för datauppsättningsförberedelser finns mer information om hur du konfigurerar det här.

Kommandot `sendEvent` bör användas som återanrop i lämpliga händelseavlyssnare på webbplatsen. Kommandot förväntar sig två argument: (1) en sträng som anger kommandotypen (i det här fallet `sendEvent`) och (2) en nyttolast som innehåller ett `xdm` -objekt som tillhandahåller obligatoriska medgivandefält som JSON:

```js
alloy("sendEvent", {
  xdm: {
    "consentStrings": [{
      "consentStandard": "IAB TCF",
      "consentStandardVersion": "2.0",
      "consentStringValue": "CLcVDxRMWfGmWAVAHCENAXCkAKDAADnAABRgA5mdfCKZuYJez-NQm0TBMYA4oCAAGQYIAAAAAAEAIAEgAA.argAC0gAAAAAAAAAAAA",
      "gdprApplies": true
    }]
  }
});
```

| Nyttolastegenskap | Beskrivning |
| --- | --- |
| `xdm.consentStrings` | En array som måste innehålla minst ett objekt som innehåller obligatoriska fält för samtycke. |
| `consentStandard` | Den standard för samtycke som används. Värdet måste anges till `IAB` för TCF 2.0-godkännandebearbetning. |
| `consentStandardVersion` | Versionsnumret för den medgivandestandard som anges under `standard`. Värdet måste anges till `2.0` för TCF 2.0-godkännandebearbetning. |
| `consentStringValue` | Den bas-64-kodade medgivandesträngen som genererats av CMP. |
| `gdprApplies` | Ett booleskt värde som anger om GDPR gäller för den inloggade kunden. För att TCF 2.0 ska framtvingas för den här kunden måste värdet anges till `true`. Standardvärdet är `true` om inte definierat. |

### Hantera SDK-svar

Många Web SDK-kommandon returnerar löften som anger om anropet lyckades eller misslyckades. Du kan sedan använda dessa svar för ytterligare logik, till exempel för att visa bekräftelsemeddelanden för kunden. Mer information finns i [Kommandosvar](/help/web-sdk/commands/command-responses.md).

## Exportera segment {#export}

>[!NOTE]
>
>Innan du börjar exportera segment måste du se till att dina segment innehåller alla obligatoriska fält för samtycke. Mer information finns i avsnittet [Konfigurera sammanfogningsprinciper](#merge-policies).

När ni har samlat in kundens medgivandedata och skapat målgruppssegment som innehåller de obligatoriska medgivandeattributen, kan ni tillämpa TCF 2.0-kompatibilitet när ni exporterar dessa segment till efterföljande destinationer.

Om medgivandeinställningen `gdprApplies` är `true` för en uppsättning kundprofiler filtreras alla data från de profiler som exporteras till underordnade mål baserat på inställningarna för TCF-samtycke för varje profil. Alla profiler som inte uppfyller de obligatoriska medgivandeinställningarna hoppas över under exportprocessen.

Kunder måste godkänna följande syften (enligt riktlinjerna i [TCF 2.0-profiler](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions)) för att deras profiler ska kunna inkluderas i segment som exporteras till mål:

* **Syfte 1**: Lagra och/eller få åtkomst till information på en enhet
* **Syfte 10**: Utveckla och förbättra produkter

TCF 2.0 kräver också att datakällan måste kontrollera målets leverantörsbehörighet innan data skickas till det målet. Plattformen kontrollerar därför om målets leverantörsbehörighet har valts för alla ID:n i klustret innan data som är bundna till målet inkluderas.

>[!NOTE]
>
>Alla segment som delas med Adobe Audience Manager innehåller samma TCF 2.0-medgivandevärden som deras plattformsmotsvarigheter. Eftersom [!DNL Audience Manager] delar samma leverantörs-ID som Platform (565) krävs samma syften och leverantörsbehörighet. Mer information finns i dokumentet om [Adobe Audience Manager-plugin-programmet för IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html).

## Testa implementeringen {#test-implementation}

När du har konfigurerat implementeringen av TCF 2.0 och exporterat segment till destinationer, kommer data som inte uppfyller kraven för samtycke inte att exporteras. Om du vill se om rätt kundprofiler filtrerades under exporten måste du kontrollera datalagret på dina destinationer manuellt för att se om samtycke har använts på rätt sätt.

>[!IMPORTANT]
>
>Om flera ID:n utgör ett kluster och TCF 2.0 tillämpas, utesluts hela klustret om inte ens ett enda ID innehåller rätt syften och leverantörsbehörighet(er).

## Nästa steg

I det här dokumentet beskrivs hur du konfigurerar plattformsdataåtgärder för att uppfylla dina affärsskyldigheter enligt TCF 2.0. Se översikten om [styrning, sekretess och säkerhet](../../overview.md) för mer information om plattformens sekretessrelaterade funktioner.
