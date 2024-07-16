---
title: Bearbeta data för kundgodkännande med Adobe Experience Platform Web SDK
description: Lär dig hur du integrerar Adobe Experience Platform Web SDK för att bearbeta data om kundgodkännande i Adobe Experience Platform.
exl-id: 3a53d908-fc61-452b-bec3-af519dfefa41
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '1282'
ht-degree: 0%

---

# Integrera Platform Web SDK för att bearbeta data om kundernas samtycke

Med Adobe Experience Platform Web SDK kan du hämta kundens medgivandesignaler som genererats av CMP (Consent Management Platforms) och skicka dem till Adobe Experience Platform när en händelse om ändring av samtycke inträffar.

**SDK:n samverkar inte med några CMP:er i rutan**. Det är upp till dig att bestämma hur du ska integrera SDK i din webbplats, lyssna efter medgivandeändringar i CMP och anropa lämpligt kommando. Det här dokumentet innehåller allmän vägledning om hur du integrerar din CMP med Platform Web SDK.

## Förhandskrav {#prerequisites}

I den här självstudien förutsätts det att du redan har fastställt hur data för samtycke ska genereras i din CMP och att du har skapat en datauppsättning som innehåller medgivandefält som överensstämmer med Adobe-standarden eller standarden IAB Transparency and Consent Framework (TCF) 2.0. Om du inte har skapat den här datauppsättningen än, se följande självstudiekurser innan du återgår till den här guiden:

* [Skapa en datauppsättning med Adobe-standarden](./adobe/dataset.md)
* [Skapa en datauppsättning med TCF 2.0-standarden](./iab/dataset.md)

Den här guiden följer arbetsflödet för att konfigurera SDK med hjälp av taggtillägget i användargränssnittet. Om du inte vill använda tillägget och vill bädda in den fristående versionen av SDK direkt på din webbplats kan du läsa följande dokument i stället för den här handboken:

* [Konfigurera ett datastream](/help/datastreams/overview.md)
* [Installera SDK](/help/web-sdk/install/overview.md)
* [Konfigurera SDK för medgivandekommandon](/help/web-sdk/commands/configure/defaultconsent.md)

Installationsstegen i den här handboken kräver en fungerande förståelse för taggtillägg och hur de installeras i webbprogram. Mer information finns i följande dokumentation:

* [Översikt över taggar](/help/tags/home.md)
* [Snabbstartguide](/help/tags/quick-start/quick-start.md)
* [Översikt över publicering](/help/tags/ui/publishing/overview.md)

## Konfigurera en datastream

För att SDK ska kunna skicka data till Experience Platform måste du först konfigurera ett datastream. I användargränssnittet för datainsamlingen eller användargränssnittet för Experience Platform väljer du **[!UICONTROL Datastreams]** i den vänstra navigeringen.

När du har skapat ett nytt datastam eller valt ett befintligt som ska redigeras, markerar du växlingsknappen bredvid **[!UICONTROL Adobe Experience Platform]**. Använd sedan värdena nedan för att fylla i formuläret.

![](../../images/governance-privacy-security/consent/adobe/sdk/edge-config.png)

| Datastream-fält | Värde |
| --- | --- |
| [!UICONTROL Sandbox] | Namnet på plattformen [sandlådan](../../../sandboxes/home.md) som innehåller den nödvändiga direktuppspelningsanslutningen och de datauppsättningar som krävs för att konfigurera dataströmmen. |
| [!UICONTROL Event Dataset] | En [!DNL XDM ExperienceEvent]-datauppsättning som du planerar att skicka händelsedata till med SDK. Du måste tillhandahålla en händelsedatamängd för att kunna skapa ett plattformsdatastam, men observera att data som skickas via händelser inte hanteras i arbetsflöden för efterföljande tillämpning. |
| [!UICONTROL Profile Dataset] | Den [!DNL Profile]-aktiverade datauppsättningen med kundmedgivandefält som du skapade [tidigare](#prerequisites). |

När du är klar väljer du **[!UICONTROL Save]** längst ned på skärmen och fortsätter att följa eventuella ytterligare uppmaningar för att slutföra konfigurationen.

## Installera och konfigurera Platform Web SDK

När du har skapat ett datastream enligt beskrivningen i föregående avsnitt måste du konfigurera det Platform Web SDK-tillägg som du slutligen distribuerar på din plats. Om du inte har SDK-tillägget installerat på taggegenskapen väljer du **[!UICONTROL Extensions]** i den vänstra navigeringen, följt av fliken **[!UICONTROL Catalog]**. Välj sedan **[!UICONTROL Install]** under plattforms-SDK-tillägget i listan över tillgängliga tillägg.

![](../../images/governance-privacy-security/consent/adobe/sdk/install.png)

När du konfigurerar SDK, under **[!UICONTROL Edge Configurations]**, markerar du datastream som du skapade i föregående steg.

![](../../images/governance-privacy-security/consent/adobe/sdk/config-sdk.png)

Välj **[!UICONTROL Save]** om du vill installera tillägget.

### Skapa ett dataelement för att ange standardsamtycke

Med SDK-tillägget installerat kan du skapa ett dataelement som representerar standardvärdet för datainsamlingsmedgivande (`collect.val`) för dina användare. Detta kan vara användbart om du vill ha olika standardvärden beroende på användaren, till exempel `pending` för användare i Europeiska unionen och `in` för användare i Nordamerika.

I det här fallet kan du implementera följande för att ange standardsamtycke baserat på användarens region:

1. Identifiera användarens region på webbservern.
1. Före taggen `script` (inbäddningskod) på webbsidan återger du en separat `script` -tagg som anger en `adobeDefaultConsent`-variabel baserat på användarens region.
1. Konfigurera ett dataelement som använder JavaScript-variabeln `adobeDefaultConsent` och använd det här dataelementet som standardvärde för samtycke för användaren.

Om användarens region bestäms av en CMP kan du använda följande steg i stället:

1. Hantera händelsen &quot;CMP loaded&quot; på sidan.
1. I händelsehanteraren anger du en `adobeDefaultConsent`-variabel baserat på användarens region och läser sedan in taggbiblioteksskriptet med JavaScript.
1. Konfigurera ett dataelement som använder JavaScript-variabeln `adobeDefaultConsent` och använd det här dataelementet som standardvärde för samtycke för användaren.

Om du vill skapa ett dataelement i användargränssnittet väljer du **[!UICONTROL Data Elements]** i den vänstra navigeringen och sedan **[!UICONTROL Add Data Element]** för att navigera till dialogrutan för att skapa dataelement.

härifrån måste du skapa ett [!UICONTROL JavaScript Variable]-dataelement baserat på `adobeDefaultConsent`. Välj **[!UICONTROL Save]** när du är klar.

![](../../images/governance-privacy-security/consent/adobe/sdk/data-element.png)

När dataelementet har skapats går du tillbaka till konfigurationssidan för Web SDK-tillägget. Under avsnittet [!UICONTROL Privacy] väljer du **[!UICONTROL Provided by data element]** och använder den angivna dialogrutan för att välja det standardelement med medgivandedata som du skapade tidigare.

![](../../images/governance-privacy-security/consent/adobe/sdk/default-consent.png)

### Distribuera tillägget på webbplatsen

När du har konfigurerat tillägget kan det integreras med webbplatsen. Mer information om hur du distribuerar det uppdaterade biblioteksbygget finns i [publiceringshandboken](../../../tags/ui/publishing/overview.md) i taggdokumentationen.

## Kommandon för att ändra samtycke {#commands}

När du har integrerat SDK-tillägget på webbplatsen kan du börja använda kommandot Platform Web SDK `setConsent` för att skicka medgivandedata till plattformen.

Kommandot `setConsent` utför två åtgärder:

1. Uppdaterar användarens profilattribut direkt i profilarkivet. Detta skickar inga data till datasjön.
1. Skapar en [upplevelsehändelse](../../../xdm/classes/experienceevent.md) som registrerar ett tidsstämplat konto för medgivandeändringshändelsen. Dessa data skickas direkt till datasjön och kan användas för att hålla reda på ändringar av medgivandepreferenser över tiden.

### När `setConsent` ska anropas

Det finns två scenarier där `setConsent` ska anropas på din plats:

1. När samtycke har lästs in på sidan (med andra ord vid varje sidinläsning)
1. Som en del av en CMP-krok eller händelseavlyssnare som upptäcker ändringar i medgivandeinställningarna

### Syntax för `setConsent`

Kommandot [`setConsent`](/help/web-sdk/commands/setconsent.md) förväntar sig ett nyttolastobjekt som innehåller en enda arraytypsegenskap: `consent`. Arrayen `consent` måste innehålla minst ett objekt som innehåller de obligatoriska medgivandefälten för Adobe-standarden.

De obligatoriska medgivandefälten för Adobe-standarden visas i följande exempel på `setConsent`-anrop:

```js
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "2.0",
    value: {
      collect: {
        val: "y"
      },
      share: {
        val: "y"
      },
      personalize: {
        content: {
          val: "y"
        }
      },
      metadata: {
        time: "YYYY-10-12T15:52:25+00:00"
      }
    }
  }]
});
```

| Nyttolastegenskap | Beskrivning |
| --- | --- |
| `standard` | Den standard för samtycke som används. Värdet måste anges till `Adobe` för Adobe-standarden. |
| `version` | Versionsnumret för den medgivandestandard som anges under `standard`. Det här värdet måste anges till `2.0` för Adobe-standardbearbetning av samtycke. |
| `value` | Kundens uppdaterade medgivandeinformation, som tillhandahålls som ett XDM-objekt som följer strukturen i den profilaktiverade datauppsättningens medgivandefält. |

>[!NOTE]
>
>Om du använder andra medgivandestandarder i samband med `Adobe` (till exempel `IAB TCF`) kan du lägga till ytterligare objekt i arrayen `consent` för varje standard. Varje objekt måste innehålla lämpliga värden för `standard`, `version` och `value` för den medgivandestandard som de representerar.

Följande JavaScript innehåller ett exempel på en funktion som hanterar ändringar av medgivandeinställningar på en webbplats, som kan användas som återanrop i en händelseavlyssnare eller en CMP-krok:

```js
var setConsent = function () {

  // Retrieve the current consent data.
  var categories = getConsentData();

  // If the script is running on a consent change, generate a new timestamp.
  // If the script is running on page load, set the timestamp to when the consent values last changed.
  var now = new Date();
  var collectedAt = consentChanged ? now.toISOString() : categories.collectedAt;

  //  Map the consent values and timestamp to XDM
  var consentXDM = {
    collect: {
      val: categories.collect !== -1 ? "y" : "n"
    },
    personalize: {
      content: {
        val: categories.personalizeContent !== -1 ? "y" : "n"
      }
    },
    share: {
      val: categories.share !== -1 ? "y" : "n"
    },
    metadata: {
      time: collectedAt
    }
  };

  // Pass the XDM object to the Platform Web SDK
  alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: consentXDM
    }]
  });
});
```

## Hantera SDK-svar

Alla [!DNL Platform SDK]-kommandon returnerar löften som anger om anropet lyckades eller misslyckades. Du kan sedan använda dessa svar för ytterligare logik, till exempel för att visa bekräftelsemeddelanden för kunden. Mer information finns i [Kommandosvar](/help/web-sdk/commands/command-responses.md).

När du har gjort `setConsent` anrop med SDK kan du använda profilvisningsprogrammet i plattformsgränssnittet för att kontrollera om data landar i profilarkivet. Mer information finns i avsnittet [Bläddra bland profiler efter identitet](../../../profile/ui/user-guide.md#browse-identity).

## Nästa steg

Genom att följa den här guiden har du konfigurerat plattformstillägget för Web SDK för att skicka data om samtycke till Experience Platform. Anvisningar om hur du testar implementeringen finns i dokumentationen för den standard för samtycke som du implementerar:

* [Adobe standard](./adobe/overview.md#test)
* [TCF 2.0-standard](./iab/overview.md#test)
