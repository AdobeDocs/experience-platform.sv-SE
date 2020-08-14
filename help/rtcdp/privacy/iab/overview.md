---
keywords: Experience Platform;home;IAB;IAB 2.0;
solution: Experience Platform
title: Stöd för IAB TCF 2.0 i kunddataplattformen i realtid
topic: privacy events
translation-type: tm+mt
source-git-commit: 28106d5db179e71f47b7e071b359ffe4934a3bbe
workflow-type: tm+mt
source-wordcount: '2377'
ht-degree: 1%

---


# Stöd för IAB TCF 2.0 i [!DNL Real-time Customer Data Platform]

Den [!DNL Transparency & Consent Framework] (TCF), som beskrivs av [!DNL Interactive Advertising Bureau] (IAB), är en öppen teknisk ram som är avsedd att göra det möjligt för organisationer att få, registrera och uppdatera konsumentens samtycke till behandlingen av deras personuppgifter, i enlighet med Europeiska unionens [!DNL General Data Protection Regulation] (GDPR). Den andra versionen av ramverket, TCF 2.0, ger större flexibilitet för hur konsumenter kan ge eller vägra samtycke, inklusive om och hur leverantörer kan använda vissa funktioner för databearbetning, till exempel exakt positionering.

>[!NOTE]
>
>Mer information om TCF 2.0 finns på [IAB Europe-webbplatsen](https://iabeurope.eu/tcf-2-0/), inklusive supportmaterial och tekniska specifikationer.

[!DNL Real-time Customer Data Platform (Real-time CDP)] ingår i den registrerade [IAB TCF 2.0-leverantörslistan](https://iabeurope.eu/vendor-list-tcf-v2-0/), under ID **565**. I enlighet med kraven för TCF 2.0 kan ni samla in data om kundernas samtycke och integrera dem i era lagrade kundprofiler. [!DNL Real-time CDP] Dessa data om samtycke kan sedan beaktas för att avgöra om profiler ska inkluderas i exporterade målgruppssegment, beroende på hur de används.

>[!IMPORTANT]
>
>[!DNL Real-time CDP] kan bara uppfylla version 2.0 av TCF (eller senare). Tidigare versioner av TCF stöds inte.

I det här dokumentet finns en översikt över hur du konfigurerar dataåtgärder och profilscheman för att acceptera kundmedgivandedata som genererats av din CMP samt hur du [!DNL Real-time CDP] anger val för användarsamtycke när du exporterar segment.

## Förutsättningar

För att kunna följa med i den här guiden måste du använda en CMP (Consent Management Platform), antingen kommersiell eller egen, som är integrerad och kompatibel med IAB TCF. Mer information finns i [listan över kompatibla CMP](https://iabeurope.eu/cmp-list/) .

>[!IMPORTANT]
>
>Om ID:t för din CMP är ogiltigt fortsätter [!DNL Real-time CDP] bearbetningen av dina data i befintligt skick. Om du vill använda TCF 2.0 måste du bekräfta att din CMP har ett giltigt ID som har registrerats med IAB TCF 2.0 innan du skickar data till [!DNL Experience Platform].

Handboken kräver även en fungerande förståelse av följande Adobe Experience Platform-tjänster:

* [Experience Data Model (XDM)](../../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata.
* [Adobe Experience Platform Identity Service](../../../identity-service/home.md): Lös den grundläggande utmaning som fragmenteringen av kundupplevelsedata innebär genom att överbrygga identiteter mellan olika enheter och system.
* [Kundprofil](../../../profile/home.md)i realtid: Utnyttja [!DNL Identity Service] för att skapa detaljerade kundprofiler utifrån era datauppsättningar i realtid. [!DNL Real-time Customer Profile] hämtar data från Data Lake och behåller kundprofiler i sitt eget separata datalager.
* [Adobe Experience Platform Web SDK](../../../edge/home.md): Ett JavaScript-bibliotek på klientsidan som gör att du kan integrera olika [!DNL Platform] tjänster i kundens webbplats.
   * [SDK-medgivandekommandon](../../../edge/fundamentals/supporting-consent.md): En översikt över de medgivande-relaterade SDK-kommandona som visas i den här handboken.
* [Adobe Experience Platform segmenteringstjänst](../../../segmentation/home.md): Gör att ni kan dela in [!DNL Real-time Customer Profile] data i grupper av individer som delar liknande egenskaper och kommer att svara på liknande sätt som marknadsföringsstrategier.

Utöver de tjänster som anges ovan bör du även känna till [!DNL Platform] destinationer [och deras användning i](../../destinations/destinations-overview.md) [!DNL Real-time CDP].

## Sammanfattning av kundens godkännandeflöde {#summary}

I följande avsnitt beskrivs hur data om samtycke samlas in och används efter att systemet har konfigurerats korrekt.

### Samling av data för samtycke

[!DNL Real-time CDP] gör att ni kan samla in data om kundens samtycke genom följande process:

1. En kund ger sitt samtycke till datainsamling via en dialogruta på er webbplats.
1. Din CMP identifierar ändringen av medgivandeinställningen och genererar IAB-medgivandedata i enlighet med detta.
1. Med hjälp av [!DNL Experience Platform Web SDK]detta skickas data om det genererade medgivandet (returneras av CMP) till Adobe Experience Platform.
1. De insamlade data om samtycke importeras till en [!DNL Profile]aktiverad datauppsättning vars schema innehåller IAB-medgivandefält.

Förutom SDK-kommandon som aktiveras av CMP-kodekar för avtalsändringar kan data även flöda in [!DNL Experience Platform] via alla kundgenererade XDM-data som överförs direkt till en [!DNL Profile]aktiverad datauppsättning.

Alla segment som delas med [!DNL Platform] Adobe Audience Manager (via [!DNL Audience Manager] källkopplingen eller på annat sätt) kan också innehålla data om samtycke, förutsatt att lämpliga fält har tillämpats på dessa segment genom [!DNL Experience Cloud Identity Service]. Mer information om hur du samlar in medgivandedata i [!DNL Audience Manager]finns i dokumentet om plugin-programmet för [Adobe Audience Manager för IAB TCF](https://docs.adobe.com/help/sv-SE/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.translate.html).

### Efterföljande av samtycke

När IAB:s medgivandedata har importerats utan problem utförs följande processer i [!DNL Real-time CDP] tjänster i senare led:

1. [!DNL Real-time Customer Profile] uppdaterar lagrade medgivandedata för kundens profil.
1. [!DNL Real-time CDP] bearbetar endast kund-ID:n om leverantörsbehörighet för [!DNL Real-time CDP] (565) anges för varje ID i ett kluster.
1. När du exporterar segment till mål som tillhör medlemmar i leverantörslistan för TCF 2.0, inkluderas [!DNL Real-time CDP] bara profiler om leverantörsbehörigheterna för både [!DNL Real-time CDP] (565) *och* målet anges för varje ID i ett kluster.

Resten av avsnitten i det här dokumentet innehåller riktlinjer för hur du konfigurerar [!DNL Real-time CDP] och dina dataåtgärder så att de uppfyller de krav för insamling och verkställighet som beskrivs ovan.

## Bestäm hur ni genererar data om kundsamtycke i er CMP {#consent-data}

Eftersom varje CMP-system är unikt måste ni fastställa det bästa sättet för kunderna att ge sitt samtycke när de interagerar med tjänsten. Ett vanligt sätt att uppnå detta är genom att använda en dialogruta för godkännande av cookies, som liknar följande exempel:

![](../assets/iab/cmp-dialog.png)

Den här dialogrutan måste göra det möjligt för kunden att välja att inte göra något av följande:

| Medgivandealternativ | Beskrivning |
| --- | --- |
| **Syfte** | Ändamålen definierar vilka reklamsyften ett varumärke kan använda kundens data för. Följande syften måste väljas för att kunden ska kunna [!DNL Real-time CDP] bearbeta ID:n: <ul><li>**Syfte 1**: Lagra och/eller få åtkomst till information på en enhet</li><li>**Syfte 10**: Utveckla och förbättra produkter</li></ul> |
| **Leverantörsbehörigheter** | Utöver annonseringsteknologiska ändamål måste dialogen också göra det möjligt för kunden att välja att inte få sina data använda av specifika leverantörer, inklusive [!DNL  Real-time CDP] (565). |

### Samtyckessträngar {#consent-strings}

Oavsett vilken metod du använder för att samla in data är målet att generera ett strängvärde baserat på de alternativ för samtycke som kunden valt, vilket kallas en **medgivandesträng**.

I TCF-specifikationen används medgivandesträngar för att koda relevant information om en kunds medgivandeinställningar, i termer av specifika marknadsföringssyften som definieras av policyer och leverantörer. [!DNL Real-time CDP] använder dessa strängar för att lagra medgivandeinställningarna för varje kund, och därför måste en ny medgivandesträng skapas varje gång inställningarna ändras.

Samtyckessträngar kan bara skapas av en CMP som är registrerad med IAB TCF. Mer information om hur du skapar medgivandesträngar med din CMP finns i formateringsguiden [för](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) medgivandesträngar i IAB TCF GitHub-rapporten.

## Skapa datauppsättningar med IAB-medgivandefält {#datasets}

Kundens medgivandedata måste skickas till en datauppsättning vars schema innehåller IAB-medgivandefält. Se självstudiekursen om [hur du skapar datauppsättningar för att hämta TCF 2.0-samtycke](./dataset-preparation.md) för hur du skapar de två nödvändiga datauppsättningarna innan du fortsätter med den här guiden.

## Uppdatera [!DNL Profile] sammanfogningsprinciper så att de innehåller medgivandedata {#merge-policies}

När du har skapat en [!DNL Profile]aktiverad datauppsättning för insamling av medgivandedata måste du se till att dina kopplingsprofiler har konfigurerats så att de alltid innehåller IAB-medgivandefält i dina kundprofiler. Detta innebär att ange datauppsättningens prioritet så att din sambandsuppsättning prioriteras framför andra datauppsättningar som kan vara i konflikt.

Mer information om hur du arbetar med sammanfogningsprinciper finns i användarhandboken för [sammanfogningsprinciper](../../../profile/ui/merge-policies.md). När du konfigurerar dina sammanfogningsprinciper måste du se till att dina segment innehåller alla nödvändiga medgivandeattribut som tillhandahålls av [XDM:s integritetsblandning](./dataset-preparation.md#privacy-mixin), enligt riktlinjerna för datauppsättningsförberedelse.

## Integrera [!DNL Experience Platform] Web SDK för att samla in data om kundernas samtycke {#sdk}

>[!NOTE]
>
>Det krävs att [!DNL Experience Platform] Web SDK används för att behandla data som medgetts direkt i Adobe Experience Platform. [!DNL Experience Cloud Identity Service] stöds för närvarande inte.
>
>[!DNL Experience Cloud Identity Service] stöds dock fortfarande för godkännandebearbetning i Adobe Audience Manager, och efterlevnad av TCF 2.0 kräver bara att biblioteket uppdateras till [version 5.0](https://github.com/Adobe-Marketing-Cloud/id-service/releases).

När du har konfigurerat din CMP för att generera medgivandesträngar måste du integrera [!DNL Experience Platform] Web SDK för att samla in strängarna och skicka dem till [!DNL Platform]. SDK:n innehåller två kommandon som kan användas för att skicka IAB-medgivandedata till plattformen (som förklaras i underavsnitten nedan), och bör användas när en kund lämnar medgivandeinformation för första gången och när som helst där medgivandet ändras därefter. [!DNL Platform]

**SDK:n samverkar inte med några CMP:er som finns i kartongen**. Det är upp till dig att bestämma hur du ska integrera SDK i din webbplats, lyssna efter medgivandeändringar i CMP och anropa lämpligt kommando.

### Skapa en ny kantkonfiguration

För att SDK ska kunna skicka data till [!DNL Experience Platform]måste du först skapa en ny kantkonfiguration för [!DNL Platform] i [!DNL Adobe Experience Platform Launch]. Specifika steg för hur du skapar en ny konfiguration finns i [SDK-dokumentationen](../../../edge/fundamentals/edge-configuration.md).

När du har angett ett unikt namn för konfigurationen väljer du växlingsknappen bredvid *[!UICONTROL Adobe Experience Platform]*. Använd sedan följande värden för att fylla i resten av formuläret:

| Konfiguration av Edge-fält | Värde |
| --- | --- |
| [!UICONTROL Sandbox] | Namnet på den [!DNL Platform] sandlåda [](../../../sandboxes/home.md) som innehåller den strömningsanslutning och de datauppsättningar som krävs för att konfigurera edge-konfigurationen. |
| [!UICONTROL Streaming Inlet] | En giltig direktuppspelningsanslutning för [!DNL Experience Platform]. Se självstudiekursen om hur du [skapar en direktuppspelningsanslutning](../../../ingestion/tutorials/create-streaming-connection-ui.md) om du inte har ett befintligt direktuppspelningsinlopp. |
| [!UICONTROL Event Dataset] | Markera den [!DNL XDM ExperienceEvent] datauppsättning som skapades i [föregående steg](#datasets). |
| [!UICONTROL Profile Dataset] | Markera den [!DNL XDM Individual Profile] datauppsättning som skapades i [föregående steg](#datasets). |

![](../assets/iab/edge-config.png)

När du är klar klickar du **[!UICONTROL Save]** längst ned på skärmen och fortsätter att följa eventuella ytterligare anvisningar för att slutföra konfigurationen.

### Kommandon för att ändra samtycke

När du har skapat kantkonfigurationen som beskrivs i föregående avsnitt kan du börja använda SDK-kommandon för att skicka data för samtycke till [!DNL Platform]. Avsnitten nedan innehåller exempel på hur varje SDK-kommando kan användas i olika scenarier.

>[!NOTE]
>
>En introduktion till den vanliga syntaxen för alla [!DNL Platform] SDK-kommandon finns i dokumentet om hur du [kör kommandon](../../../edge/fundamentals/executing-commands.md).

#### Använda CMP-krokar för ändring av samtycke

Många CMP-modeller har färdiga kopplingar som lyssnar på händelser om samtycke. När dessa händelser inträffar kan du använda `setConsent` kommandot för att uppdatera kundens medgivandedata.

Kommandot förväntar `setConsent` sig två argument: (1) en sträng som anger kommandotypen (i det här fallet &quot;setConsent&quot;) och (2) en nyttolast som innehåller en `consent` array, som måste innehålla minst ett objekt som tillhandahåller de obligatoriska medgivandefälten, vilket visas nedan:

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
| `standard` | Den standard för samtycke som används. Värdet måste anges som IAB för TCF 2.0-godkännandebearbetning. |
| `version` | Versionsnumret för den medgivandestandard som anges under `standard`. Värdet måste vara 2.0 för TCF 2.0-godkännandebearbetning. |
| `value` | Den bas-64-kodade medgivandesträngen som genererats av CMP. |
| `gdprApplies` | Ett booleskt värde som anger om GDPR gäller för den inloggade kunden. För att TCF 2.0 ska kunna användas för den här kunden måste värdet anges till &quot;true&quot;. |

Kommandot ska användas som en del av en CMP-krok som upptäcker ändringar i medgivandeinställningarna. `setConsent` Följande JavaScript innehåller ett exempel på hur kommandot `setConsent` kan användas för OneTrust&#39;s `OnConsentChanged` krok:

```js
OneTrust.OnConsentChanged(function () {
  // Retrieve the TCF 2.0 consent data generated by the CMP, and pass it to Alloy. 
  __tcfapi("getTCData", 2, (data, success) => {
    if (success) {
      const { tcString, gdprApplies } = data;

      alloy("setConsent", {
        consent: [{
          standard: "IAB TCF",
          version: "2.0",
          value: tcString,
          gdprApplies
        }]
      });
    }
  });
});
```

#### Använda händelser

Du kan också samla in TCF 2.0-medgivandedata för varje händelse som utlöses i [!DNL Platform] med hjälp av `sendEvent` kommandot.

>[!NOTE]
>
>Om du vill använda den här metoden måste du ha lagt till [!DNL Experience Event Privacy mixin] i det [!DNL Profile]aktiverade [!DNL XDM ExperienceEvent] schemat. I avsnittet om att [uppdatera ExperienceEvent-schemat](./dataset-preparation.md#event-schema) i guiden för datauppsättningsförberedelser finns mer information om hur du konfigurerar det här.

Kommandot bör användas som återanrop i lämpliga händelseavlyssnare på webbplatsen. `sendEvent` Kommandot förväntar sig två argument: (1) en sträng som anger kommandotypen (i det här fallet &quot;sendEvent&quot;) och (2) en nyttolast som innehåller ett `xdm` objekt som tillhandahåller obligatoriska medgivandefält som JSON:

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
| `xdm.consentStrings` | En array som måste innehålla minst ett objekt som innehåller de obligatoriska medgivandefälten. |
| `consentStandard` | Den standard för samtycke som används. Värdet måste anges som IAB för TCF 2.0-godkännandebearbetning. |
| `consentStandardVersion` | Versionsnumret för den medgivandestandard som anges under `standard`. Värdet måste vara 2.0 för TCF 2.0-godkännandebearbetning. |
| `consentStringValue` | Den bas-64-kodade medgivandesträngen som genererats av CMP. |
| `gdprApplies` | Ett booleskt värde som anger om GDPR gäller för den inloggade kunden. För att TCF 2.0 ska kunna användas för den här kunden måste värdet anges till &quot;true&quot;. |

### Hantera SDK-svar

Alla [!DNL Platform SDK] kommandon returnerar löften som anger om anropet lyckades eller misslyckades. Du kan sedan använda dessa svar för ytterligare logik, till exempel för att visa bekräftelsemeddelanden för kunden. I avsnittet om att [hantera om det är fel eller om det är fel](../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) eller om det finns specifika exempel på hur SDK-kommandon körs.

## Exportera segment {#export}

>[!NOTE]
>
>Innan du börjar exportera segment måste du se till att dina segment innehåller alla obligatoriska fält för samtycke. Mer information finns i avsnittet [Konfigurera sammanfogningsprinciper](#merge-policies) .

När ni har samlat in kundens medgivandedata och skapat målgruppssegment som innehåller de obligatoriska medgivandeattributen, kan ni tillämpa TCF 2.0-kompatibilitet när ni exporterar dessa segment till efterföljande destinationer.

Förutsatt att inställningen för samtycke `gdprApplies` är inställd `true` för en uppsättning kundprofiler, filtreras alla data från de profiler som exporteras till efterföljande destinationer baserat på medgivandeinställningarna för varje profil. Alla profiler som inte uppfyller de obligatoriska medgivandeinställningarna hoppas över under exportprocessen.

Kunden måste godkänna följande syften (enligt riktlinjerna i [TCF 2.0-policyer](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions)) för att deras profiler ska kunna inkluderas i segment som exporteras till destinationer:

* **Syfte 1**: Lagra och/eller få åtkomst till information på en enhet
* **Syfte 10**: Utveckla och förbättra produkter

TCF 2.0 kräver också att datakällan måste kontrollera målets leverantörsbehörighet innan data skickas till det målet. Detta innebär att [!DNL Real-time CDP] kontrollerar om målets leverantörsbehörighet har valts in för alla ID:n i klustret innan data som är bundna till det målet inkluderas.

>[!NOTE]
>
>Alla segment som delas med Adobe Audience Manager innehåller samma TCF 2.0-medgivandevärden som deras [!DNL Platform] motsvarigheter. Eftersom [!DNL Audience Manager] delar samma leverantörs-ID som [!DNL Real-time CDP] (565) krävs samma syften och leverantörsbehörighet. Mer information finns i dokumentet om [Adobe Audience Manager plugin-programmet för IAB TCF](https://docs.adobe.com/help/sv-SE/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.translate.html) .

## Test your implementation {#test-implementation}

När du har konfigurerat implementeringen av TCF 2.0 och exporterat segment till destinationer, kommer data som inte uppfyller kraven för samtycke inte att exporteras. För att kunna se om rätt kundprofiler filtrerades under exporten måste du dock manuellt kontrollera datalagret på dina destinationer för att se om samtycke har använts på rätt sätt.

Observera att om flera ID:n utgör ett kluster och TCF 2.0 gäller, kommer hela klustret att uteslutas om inte ens ett ID innehåller rätt syften och leverantörsbehörighet.

## Nästa steg

I det här dokumentet beskrivs hur du konfigurerar dataåtgärder så [!DNL Real-time CDP] att de är kompatibla med TCF 2.0. Mer information om andra sekretessfunktioner i [!DNL Real-time CDP]finns i följande dokumentation:

* [Sekretess i CDP i realtid](../privacy-overview.md)
* [Datastyrning i realtid CDP](../data-governance-overview.md)