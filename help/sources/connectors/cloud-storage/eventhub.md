---
keywords: Experience Platform;hem;populära ämnen;Azure Event Hubs;azure event hubs;Event Hubs;event hubs
solution: Experience Platform
title: Översikt över Azure Event Hubs Source Connector
description: Lär dig hur du ansluter Azure Event Hubs till Adobe Experience Platform med API:er eller användargränssnittet.
exl-id: b4d4bc7f-2241-482d-a5c2-4422c31705bf
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---


# [!DNL Azure Event Hubs] koppling

Adobe Experience Platform erbjuder anslutningsmöjligheter för molnleverantörer som AWS, [!DNL Google Cloud Platform]och [!DNL Azure]. Ni kan överföra data från dessa system till plattformen.

Lagringskällor i molnet kan hämta dina egna data till plattformen utan att du behöver hämta, formatera eller överföra dem. Inkapslade data kan formateras som XDM JSON, XDM Parquet eller avgränsade. Varje steg i processen är integrerat i arbetsflödet för källor. Plattformen gör att du kan hämta in data från [!DNL Event Hubs] i realtid.

## Skala med [!DNL Event Hubs]

Skalfaktorn för [!DNL Event Hubs] -instansen måste ökas om du behöver lägga in stora datavolymer, öka parallellismen eller öka hastigheten på intag-plattformen.

### Högre volymdata

För närvarande, den maximala datavolym du kan hämta från din [!DNL Event Hubs] kontot till Platform är 2 000 poster per sekund. Om du vill skala upp och importera data i större volymer kontaktar du Adobe.

### Öka parallellismen på [!DNL Event Hubs] och plattform

Parallellitet avser samtidig körning av samma uppgifter på flera bearbetningsenheter för att öka hastighet och prestanda. Du kan öka parallellismen på [!DNL Event Hubs] genom att öka partitionen eller genom att köpa fler bearbetningsenheter för [!DNL Event Hubs] konto. Se det här [[!DNL Event Hubs] dokument vid skalförändring](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-scalability) för mer information.

För att öka hastigheten för intag på plattformssidan måste Platform öka antalet uppgifter i källkopplingen som ska läsas från din [!DNL Event Hubs] partitioner. När du har ökat parallellismen på [!DNL Event Hubs] Kontakta din Adobe-representant för att skala plattformsuppgifter baserat på din nya partition. Den här processen är för närvarande inte automatiserad.

## Använd ett virtuellt nätverk att ansluta till [!DNL Event Hubs] till plattform

Du kan konfigurera ett virtuellt nätverk att ansluta till [!DNL Event Hubs] till Platform samtidigt som brandväggsåtgärderna är aktiverade. Om du vill konfigurera ett virtuellt nätverk går du till [[!DNL Event Hubs] uppsättningsdokument för nätverksregel](https://docs.microsoft.com/en-us/rest/api/eventhub/preview/namespaces-network-rule-set/create-or-update-network-rule-set#code-try-0) och följ stegen nedan:

* Välj **Prova** från REST API-panelen,
* Autentisera [!DNL Azure] kontot med hjälp av dina inloggningsuppgifter i samma webbläsare,
* Välj [!DNL Event Hubs] namnutrymme, resursgrupp och prenumeration som du vill hämta till plattformen och sedan välja **KÖR**;
* I JSON-brödtexten som visas lägger du till följande Platform-undernät under `virtualNetworkRules` inuti `properties`:


>[!IMPORTANT]
>
>Du måste skapa en säkerhetskopia av det JSON-innehåll som du får innan du uppdaterar `virtualNetworkRules` med Platform-undernätet eftersom det innehåller dina befintliga IP-filtreringsregler. Annars tas reglerna bort efter anropet.


```json
{
    "subnet": {
        "id": "/subscriptions/93f21779-b1fd-49ee-8547-2cdbc979a44f/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_va7_network_10_19_144_0_22/subnets/ethos_12_prod_va7_network_10_19_144_0_22"
    },
    "ignoreMissingVnetServiceEndpoint": true
}
```

Se listan nedan för olika regioner av plattformsundernät:

### VA7: Nordamerika

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
          "id": "/subscriptions/93f21779-b1fd-49ee-8547-2cdbc979a44f/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_va7_network_10_19_144_0_22/subnets/ethos_12_prod_va7_network_10_19_144_0_22"
        },
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

### NLD2: Europa

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
            "id": "/subscriptions/40bde086-46ad-44c3-afba-c306f54b64ec/resourceGroups/ethos_12_prod_nld2_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_nld2_network_10_20_40_0_23/subnets/ethos_12_prod_nld2_network_10_20_40_0_23"
        }, 
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

### AUS5: Australien

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
          "id": "/subscriptions/1618ef18-9edc-48bf-88dd-61cc979629b5/resourceGroups/ethos_12_prod_aus5_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_aus5_network_10_21_116_0_22/subnets/ethos_12_prod_aus5_network_10_21_116_0_22"
        },
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

Se följande [[!DNL Event Hubs] dokument](https://docs.microsoft.com/en-us/rest/api/eventhub/preview/namespaces-network-rule-set/create-or-update-network-rule-set) om du vill ha mer information om uppsättningar av nätverksregler.

## Anslut [!DNL Event Hubs] till plattform

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Event Hubs] till Plattform med API:er eller användargränssnittet:

### Använda API:er

* [Skapa en Event Hubs-källanslutning med API:t för Flow Service](../../tutorials/api/create/cloud-storage/eventhub.md)
* [Samla in strömmande data med API:t för Flow Service](../../tutorials/api/collect/streaming.md)

### Använda gränssnittet

* [Skapa en källanslutning för händelsehubbar i användargränssnittet](../../tutorials/ui/create/cloud-storage/eventhub.md)
* [Konfigurera ett dataflöde för en molnlagringsanslutning i användargränssnittet](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
