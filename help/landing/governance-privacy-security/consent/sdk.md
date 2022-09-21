---
title: Bearbeta data för kundgodkännande med Adobe Experience Platform Web SDK
topic-legacy: getting started
description: Lär dig hur du integrerar Adobe Experience Platform Web SDK för att bearbeta data om kundgodkännande i Adobe Experience Platform.
exl-id: 3a53d908-fc61-452b-bec3-af519dfefa41
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '1344'
ht-degree: 0%

---

# Integrera Platform Web SDK för att bearbeta data om kundernas samtycke

Med Adobe Experience Platform Web SDK kan du hämta kundens medgivandesignaler som genererats av CMP (Consent Management Platforms) och skicka dem till Adobe Experience Platform när en händelse om ändring av samtycke inträffar.

**SDK:n samverkar inte med några CMP:er**. Det är upp till dig att bestämma hur du ska integrera SDK i din webbplats, lyssna efter medgivandeändringar i CMP och anropa lämpligt kommando. Det här dokumentet innehåller allmän vägledning om hur du integrerar din CMP med Platform Web SDK.

## Förutsättningar {#prerequisites}

I den här självstudien förutsätts det att du redan har fastställt hur data för samtycke ska genereras i din CMP och att du har skapat en datauppsättning som innehåller medgivandefält som överensstämmer med Adobe-standarden eller standarden IAB Transparency and Consent Framework (TCF) 2.0. Om du inte har skapat den här datauppsättningen än, se följande självstudiekurser innan du återgår till den här guiden:

* [Skapa en datauppsättning med Adobe-standarden](./adobe/dataset.md)
* [Skapa en datauppsättning med TCF 2.0-standarden](./iab/dataset.md)

Den här guiden följer arbetsflödet för att konfigurera SDK med hjälp av taggtillägget i användargränssnittet. Om du inte vill använda tillägget och vill bädda in den fristående versionen av SDK direkt på din webbplats kan du läsa följande dokument i stället för den här handboken:

* [Konfigurera ett datastream](../../../edge/datastreams/overview.md)
* [Installera SDK](../../../edge/fundamentals/installing-the-sdk.md)
* [Konfigurera SDK för medgivandekommandon](../../../edge/consent/supporting-consent.md)

Installationsstegen i den här handboken kräver en fungerande förståelse för taggtillägg och hur de installeras i webbprogram. Mer information finns i följande dokumentation:

* [Översikt över taggar](../../../tags/home.md)
* [Snabbstartguide](../../../tags/quick-start/quick-start.md)
* [Översikt över publicering](../../../tags/ui/publishing/overview.md)

## Konfigurera en datastream

För att SDK ska kunna skicka data till Experience Platform måste du först konfigurera ett datastream. I användargränssnittet för datainsamling eller användargränssnittet för Experience Platform väljer du **[!UICONTROL Datastreams]** i den vänstra navigeringen.

När du har skapat ett nytt dataflöde eller valt ett befintligt som du vill redigera, markerar du växlingsknappen bredvid **[!UICONTROL Adobe Experience Platform]**. Använd sedan värdena nedan för att fylla i formuläret.

![](../../images/governance-privacy-security/consent/adobe/sdk/edge-config.png)

| Datastream-fält | Värde |
| --- | --- |
| [!UICONTROL Sandbox] | Namnet på plattformen [sandlåda](../../../sandboxes/home.md) som innehåller den strömningsanslutning och de datauppsättningar som krävs för att konfigurera dataströmmen. |
| [!UICONTROL Streaming Inlet] | En giltig direktuppspelningsanslutning för Experience Platform. Se självstudiekursen om [skapa en direktuppspelningsanslutning](../../../ingestion/tutorials/create-streaming-connection-ui.md) om du inte har ett befintligt inlopp för direktuppspelning. |
| [!UICONTROL Event Dataset] | An [!DNL XDM ExperienceEvent] datauppsättning som du planerar att skicka händelsedata till med SDK. Du måste tillhandahålla en händelsedatamängd för att kunna skapa ett plattformsdatastam, men observera att data som skickas via händelser inte hanteras i arbetsflöden för efterföljande tillämpning. |
| [!UICONTROL Profile Dataset] | The [!DNL Profile]-aktiverad datauppsättning med kundmedgivandefält som du har skapat [tidigare](#prerequisites). |

När du är klar väljer du **[!UICONTROL Save]** längst ned på skärmen och fortsätta att följa eventuella ytterligare anvisningar för att slutföra konfigurationen.

## Installera och konfigurera Platform Web SDK

När du har skapat ett datastream enligt beskrivningen i föregående avsnitt måste du konfigurera det Platform Web SDK-tillägg som du slutligen distribuerar på din plats. Om du inte har SDK-tillägget installerat på taggegenskapen väljer du **[!UICONTROL Extensions]** i den vänstra navigeringen, följt av **[!UICONTROL Catalog]** -fliken. Välj sedan **[!UICONTROL Install]** under plattformens SDK-tillägg i listan över tillgängliga tillägg.

![](../../images/governance-privacy-security/consent/adobe/sdk/install.png)

När SDK konfigureras, under **[!UICONTROL Edge Configurations]** väljer du den datastam du skapade i föregående steg.

![](../../images/governance-privacy-security/consent/adobe/sdk/config-sdk.png)

Välj **[!UICONTROL Save]** för att installera tillägget.

### Skapa ett dataelement för att ange standardsamtycke

Med SDK-tillägget installerat kan du skapa ett dataelement som representerar standardvärdet för datainsamlingsmedgivande (`collect.val`) för användarna. Detta kan vara användbart om du vill ha olika standardvärden beroende på användaren, till exempel `pending` för användare i Europeiska unionen och `in` för användare i Nordamerika.

I det här fallet kan du implementera följande för att ange standardsamtycke baserat på användarens region:

1. Ange användarens region på webbservern.
1. Före `script` -tagg (inbäddningskod) på webbsidan, återge en separat `script` tagg som anger `adobeDefaultConsent` variabel som baseras på användarens region.
1. Konfigurera ett dataelement som använder `adobeDefaultConsent` JavaScript-variabel och använd det här dataelementet som standardvärde för samtycke för användaren.

Om användarens region bestäms av en CMP kan du använda följande steg i stället:

1. Hantera händelsen &quot;CMP loaded&quot; på sidan.
1. I händelsehanteraren anger du en `adobeDefaultConsent` variabel som baseras på användarens region och sedan läsa in taggbiblioteksskriptet med JavaScript.
1. Konfigurera ett dataelement som använder `adobeDefaultConsent` JavaScript-variabel och använd det här dataelementet som standardvärde för samtycke för användaren.

Om du vill skapa ett dataelement i användargränssnittet väljer du **[!UICONTROL Data Elements]** i den vänstra navigeringen väljer du **[!UICONTROL Add Data Element]** för att navigera till dialogrutan för att skapa dataelement.

Härifrån måste du skapa en [!UICONTROL JavaScript Variable] dataelement baserat på `adobeDefaultConsent`. Välj **[!UICONTROL Save]** när du är klar.

![](../../images/governance-privacy-security/consent/adobe/sdk/data-element.png)

När dataelementet har skapats går du tillbaka till konfigurationssidan för Web SDK-tillägget. Under [!UICONTROL Privacy] avsnitt, markera **[!UICONTROL Provided by data element]** och använd den angivna dialogrutan för att välja det standardelement för medgivandedata som du skapade tidigare.

![](../../images/governance-privacy-security/consent/adobe/sdk/default-consent.png)

### Distribuera tillägget på webbplatsen

När du har konfigurerat tillägget kan det integreras med webbplatsen. Se [publiceringshandbok](../../../tags/ui/publishing/overview.md) i taggdokumentationen för att få detaljerad information om hur du distribuerar din uppdaterade biblioteksversion.

## Kommandon för att ändra samtycke {#commands}

När du har integrerat SDK-tillägget på webbplatsen kan du börja använda Platform Web SDK `setConsent` för att skicka data om samtycke till plattformen.

The `setConsent` kommandot utför två åtgärder:

1. Uppdaterar användarens profilattribut direkt i profilarkivet. Detta skickar inga data till datasjön.
1. Skapar en [Experience Event](../../../xdm/classes/experienceevent.md) som registrerar ett tidsstämplat konto för händelsen för tillståndsändring. Dessa data skickas direkt till datasjön och kan användas för att hålla reda på ändringar av medgivandepreferenser över tiden.

### När ska du ringa `setConsent`

Det finns två scenarier där `setConsent` ska anropas på din webbplats:

1. När samtycke har lästs in på sidan (med andra ord vid varje sidinläsning)
1. Som en del av en CMP-krok eller händelseavlyssnare som upptäcker ändringar i medgivandeinställningarna

### `setConsent` syntax

>[!NOTE]
>
>En introduktion till den vanliga syntaxen för SDK-kommandon för plattformar finns i dokumentet om [köra kommandon](../../../edge/fundamentals/executing-commands.md).

The `setConsent` -kommandot förväntar sig två argument:

1. En sträng som anger kommandotypen (i det här fallet `"setConsent"`)
1. Ett nyttolastobjekt som innehåller en enda arraytypsegenskap: `consent`. The `consent` arrayen måste innehålla minst ett objekt som innehåller de obligatoriska medgivandefälten för Adobe-standarden.

De obligatoriska medgivandefälten för Adobe-standarden visas i följande exempel `setConsent` ring:

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
        time: "2020-10-12T15:52:25+00:00"
      }
    }
  }]
});
```

| Nyttolastegenskap | Beskrivning |
| --- | --- |
| `standard` | Den standard för samtycke som används. För Adobe-standarden måste det här värdet anges till `Adobe`. |
| `version` | Versionsnumret för den medgivandestandard som anges under `standard`. Värdet måste anges till `2.0` för Adobe-standardiserad behandling av samtycke. |
| `value` | Kundens uppdaterade medgivandeinformation, som tillhandahålls som ett XDM-objekt som följer strukturen i den profilaktiverade datauppsättningens medgivandefält. |

>[!NOTE]
>
>Om du använder andra medgivandestandarder i kombination med `Adobe` (till exempel `IAB TCF`) kan du lägga till fler objekt i `consent` för varje standard. Varje objekt måste innehålla lämpliga värden för `standard`, `version`och `value` för den standard för samtycke de representerar.

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

Alla [!DNL Platform SDK] kommandon returnerar löften som anger om anropet lyckades eller misslyckades. Du kan sedan använda dessa svar för ytterligare logik, till exempel för att visa bekräftelsemeddelanden för kunden. Se avsnittet om [hantering av lyckade eller misslyckade](../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) i guiden om hur du kör SDK-kommandon för specifika exempel.

När du är klar `setConsent` anrop med SDK kan du använda profilvisningsprogrammet i plattformsgränssnittet för att kontrollera om data landas i profilarkivet. Se avsnittet om [söka efter profiler utifrån identitet](../../../profile/ui/user-guide.md#browse-identity) för mer information.

## Nästa steg

Genom att följa den här guiden har du konfigurerat plattformstillägget för Web SDK för att skicka data om samtycke till Experience Platform. Anvisningar om hur du testar implementeringen finns i dokumentationen för den standard för samtycke som du implementerar:

* [Adobe standard](./adobe/overview.md#test)
* [TCF 2.0-standard](./iab/overview.md#test)
