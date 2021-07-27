---
title: Bearbeta data för kundgodkännande med Adobe Experience Platform Web SDK
topic-legacy: getting started
description: Lär dig hur du integrerar Adobe Experience Platform Web SDK för att bearbeta data om kundgodkännande i Adobe Experience Platform med hjälp av standarden Adobe 2.0.
exl-id: 3a53d908-fc61-452b-bec3-af519dfefa41
source-git-commit: 8b58bb60ae40f224433f3513060f4ae7ddc7d5b3
workflow-type: tm+mt
source-wordcount: '1253'
ht-degree: 0%

---

# Integrera Platform Web SDK för att bearbeta kunddata med hjälp av Adobe 2.0-standarden

Med Adobe Experience Platform Web SDK kan du hämta kundens medgivandesignaler som genererats av CMP (Consent Management Platforms) och skicka dem till Adobe Experience Platform när en händelse om ändring av samtycke inträffar.

**SDK:n samverkar inte med några CMP:er som finns i kartongen**. Det är upp till dig att bestämma hur du ska integrera SDK i din webbplats, lyssna efter medgivandeändringar i CMP och anropa lämpligt kommando. Det här dokumentet innehåller allmän vägledning om hur du integrerar din CMP med Platform Web SDK.

>[!NOTE]
>
>Den här guiden går igenom stegen för att integrera SDK via ett taggtillägg i användargränssnittet för datainsamling. Om du vill använda den fristående versionen av SDK i stället, se följande dokument:
>
>* [Konfigurera ett datastream](../../../../edge/fundamentals/datastreams.md)
* [Installera SDK](../../../../edge/fundamentals/installing-the-sdk.md)
* [Konfigurera SDK för medgivandekommandon](../../../../edge/consent/supporting-consent.md)


## Förutsättningar

I den här självstudien förutsätts att du redan har bestämt hur du ska generera medgivandedata i din CMP och har skapat en datauppsättning som innehåller medgivandefält som har aktiverats för kundprofil i realtid. Mer information om de här stegen finns i översikten om [godkännandebearbetning i Experience Platform](./overview.md) innan du återgår till den här handboken.

Handboken kräver dessutom en fungerande förståelse för Adobe Experience Platform Launch-tillägg och hur de installeras i webbprogram. Mer information finns i följande dokumentation:

* [Översikt över platforma launchen](https://experienceleague.adobe.com/docs/launch/using/home.html)
* [Snabbstartguide](https://experienceleague.adobe.com/docs/launch/using/get-started/quick-start.html)
* [Översikt över publicering](https://experienceleague.adobe.com/docs/launch/using/publish/overview.html)

## Konfigurera en datastream

För att SDK ska kunna skicka data till Experience Platform måste du ha en befintlig datastream för Platform konfigurerad i Adobe Experience Platform Launch. Dessutom måste de [!UICONTROL Profile Dataset] som du väljer för konfigurationen innehålla standardiserade medgivandefält.

När du har skapat en ny konfiguration eller valt en befintlig som du vill redigera, väljer du växlingsknappen bredvid **[!UICONTROL Adobe Experience Platform]**. Använd sedan värdena nedan för att fylla i formuläret.

![](../../../images/governance-privacy-security/consent/adobe/sdk/edge-config.png)

| Datastream-fält | Värde |
| --- | --- |
| [!UICONTROL Sandbox] | Namnet på plattformen [sandlådan](../../../../sandboxes/home.md) som innehåller den strömningsanslutning och de datauppsättningar som krävs för att konfigurera dataströmmen. |
| [!UICONTROL Streaming Inlet] | En giltig direktuppspelningsanslutning för Experience Platform. Se självstudiekursen om att [skapa en direktuppspelningsanslutning](../../../../ingestion/tutorials/create-streaming-connection-ui.md) om du inte har ett befintligt direktuppspelningsinlopp. |
| [!UICONTROL Event Dataset] | En [!DNL XDM ExperienceEvent]-datauppsättning som du planerar att skicka händelsedata till med SDK. Du måste tillhandahålla en händelsedatamängd för att kunna skapa en plattformsdatastam, men tänk på att det för närvarande inte finns stöd för att skicka data direkt via händelser. |
| [!UICONTROL Profile Dataset] | Den [!DNL Profile]-aktiverade datauppsättningen med medgivandefält som du skapade tidigare. |

När du är klar väljer du **[!UICONTROL Save]** längst ned på skärmen och fortsätter att följa eventuella ytterligare uppmaningar för att slutföra konfigurationen.


## Installera och konfigurera Platform Web SDK

När du har skapat ett datastream enligt beskrivningen i föregående avsnitt måste du konfigurera det Platform Web SDK-tillägg som du slutligen distribuerar på din plats. Om du inte har SDK-tillägget installerat på din Platform launch-egenskap väljer du **[!UICONTROL Extensions]** i den vänstra navigeringen, följt av fliken **[!UICONTROL Catalog]**. Välj sedan **[!UICONTROL Install]** under plattforms-SDK-tillägget i listan över tillgängliga tillägg.

![](../../../images/governance-privacy-security/consent/adobe/sdk/install.png)

När du konfigurerar SDK, under **[!UICONTROL Edge Configurations]**, väljer du datastream som du skapade i föregående steg.

![](../../../images/governance-privacy-security/consent/adobe/sdk/config-sdk.png)

Välj **[!UICONTROL Save]** om du vill installera tillägget.

### Skapa ett dataelement för att ange standardsamtycke

Med SDK-tillägget installerat kan du skapa ett dataelement som representerar standardvärdet för datainsamlingsmedgivande (`collect.val`) för dina användare. Detta kan vara användbart om du vill ha olika standardvärden beroende på användaren, till exempel `pending` för användare i Europeiska unionen och `in` för användare i Nordamerika.

I det här fallet kan du implementera följande för att ange standardsamtycke baserat på användarens region:

1. Ange användarens region på webbservern.
1. Före Platforma launchens skripttagg (inbäddningskod) på webbsidan återger du en separat skripttagg som anger variabeln `adobeDefaultConsent` baserat på användarens region.
1. Konfigurera ett dataelement som använder JavaScript-variabeln `adobeDefaultConsent` och använd det här dataelementet som standardvärde för samtycke för användaren.

Om användarens region bestäms av en CMP kan du använda följande steg i stället:

1. Hantera händelsen &quot;CMP loaded&quot; på sidan.
1. I händelsehanteraren anger du en `adobeDefaultConsent`-variabel baserat på användarens region och läser sedan in Platforma launchens biblioteksskript med JavaScript.
1. Konfigurera ett dataelement som använder JavaScript-variabeln `adobeDefaultConsent` och använd det här dataelementet som standardvärde för samtycke för användaren.

Om du vill skapa ett dataelement i användargränssnittet för Platforma launcher väljer du **[!UICONTROL Data Elements]** i den vänstra navigeringen och sedan **[!UICONTROL Add Data Element]** för att navigera till dialogrutan för att skapa dataelement.

härifrån måste du skapa ett [!UICONTROL JavaScript Variable]-dataelement baserat på `adobeDefaultConsent`. Välj **[!UICONTROL Save]** när du är klar.

![](../../../images/governance-privacy-security/consent/adobe/sdk/data-element.png)

När dataelementet har skapats går du tillbaka till konfigurationssidan för Web SDK-tillägget. Under avsnittet [!UICONTROL Privacy] väljer du **[!UICONTROL Provided by data element]** och använder den angivna dialogrutan för att välja det standardelement med medgivandedata som du skapade tidigare.

![](../../../images/governance-privacy-security/consent/adobe/sdk/default-consent.png)

### Distribuera tillägget på webbplatsen

När du har konfigurerat tillägget kan det integreras med webbplatsen. Se [publiceringsguiden](https://experienceleague.adobe.com/docs/launch/using/publish/overview.html) i Platforma launchens dokumentation för mer information om hur du distribuerar din uppdaterade biblioteksversion.

## Kommandon för att ändra samtycke {#commands}

När du har integrerat SDK-tillägget på webbplatsen kan du börja använda kommandot Platform Web SDK `setConsent` för att skicka data om samtycke till plattformen.

Det finns två scenarier där `setConsent` ska anropas på din plats:

1. När samtycke har lästs in på sidan (med andra ord vid varje sidinläsning)
1. Som en del av en CMP-krok eller händelseavlyssnare som upptäcker ändringar i medgivandeinställningarna

>[!NOTE]
En introduktion till den vanliga syntaxen för Platform SDK-kommandon finns i dokumentet om [utförande av kommandon](../../../../edge/fundamentals/executing-commands.md).

Kommandot `setConsent` förväntar sig två argument:

1. En sträng som anger kommandotypen (i det här fallet `"setConsent"`)
1. Ett nyttolastobjekt som innehåller en enda arraytypsegenskap: `consent`. Matrisen `consent` måste innehålla minst ett objekt som innehåller de obligatoriska medgivandefälten för Adobe-standarden.

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
        time: "2020-10-12T15:52:25+00:00"
      }
    }
  }]
});
```

| Nyttolastegenskap | Beskrivning |
| --- | --- |
| `standard` | Den standard för samtycke som används. För Adobe-standarden måste det här värdet anges till `Adobe`. |
| `version` | Versionsnumret för den medgivandestandard som anges under `standard`. Det här värdet måste anges till `2.0` för Adobe-standardbearbetning av samtycke. |
| `value` | Kundens uppdaterade medgivandeinformation, som tillhandahålls som ett XDM-objekt som följer strukturen i den profilaktiverade datauppsättningens medgivandefält. |

>[!NOTE]
Om du använder andra medgivandestandarder i kombination med `Adobe` (till exempel `IAB TCF`) kan du lägga till ytterligare objekt i `consent`-arrayen för varje standard. Varje objekt måste innehålla lämpliga värden för `standard`, `version` och `value` för den standard de representerar.

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

Alla [!DNL Platform SDK]-kommandon returnerar löften som anger om anropet lyckades eller misslyckades. Du kan sedan använda dessa svar för ytterligare logik, till exempel för att visa bekräftelsemeddelanden för kunden. Se avsnittet [Hantera om ](../../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) lyckades eller misslyckades i guiden om hur SDK-kommandon körs för specifika exempel.

## Nästa steg

Genom att följa den här guiden har du konfigurerat plattformstillägget för Web SDK för att skicka data om samtycke till Experience Platform. Nu kan du gå tillbaka till översikten över godkännandebearbetning för att få information om hur du [testar implementeringen](./overview.md#test-implementation).
