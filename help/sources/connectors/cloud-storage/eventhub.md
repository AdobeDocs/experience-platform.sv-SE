---
keywords: Experience Platform;hem;populära ämnen;Azure Event Hubs;azure event hubs;Event Hubs;event hubs
solution: Experience Platform
title: Översikt över Azure Event Hubs Source Connector
topic-legacy: overview
description: Lär dig hur du ansluter Azure Event Hubs till Adobe Experience Platform med API:er eller användargränssnittet.
exl-id: b4d4bc7f-2241-482d-a5c2-4422c31705bf
source-git-commit: cda9ca9c560b1af2147c00ea4e89dff09b7428ba
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# [!DNL Azure Event Hubs] koppling

Adobe Experience Platform erbjuder anslutningsmöjligheter för molnleverantörer som AWS, [!DNL Google Cloud Platform]och [!DNL Azure]. Ni kan överföra data från dessa system till plattformen.

Lagringskällor i molnet kan hämta dina egna data till plattformen utan att du behöver hämta, formatera eller överföra dem. Inkapslade data kan formateras som XDM JSON, XDM Parquet eller avgränsade. Varje steg i processen är integrerat i arbetsflödet för källor. Plattformen gör att du kan hämta in data från [!DNL Event Hubs] i realtid.

## Använd ett virtuellt nätverk att ansluta till [!DNL Event Hubs] till plattform

Du kan konfigurera ett virtuellt nätverk att ansluta till [!DNL Event Hubs] till Platform samtidigt som brandväggsåtgärderna är aktiverade. Om du vill konfigurera ett virtuellt nätverk går du till [[!DNL Event Hubs] uppsättningsdokument för nätverksregel](https://docs.microsoft.com/en-us/rest/api/eventhub/preview/namespaces-network-rule-set/create-or-update-network-rule-set#code-try-0) och sedan markera **Prova** från REST API-panelen. Autentisera sedan [!DNL Azure] ditt konto med dina inloggningsuppgifter och välj sedan [!DNL Event Hubs] namnutrymme, resursgrupp och prenumeration som du vill ta med på plattformen.

Uppdatera **begärandetext** med den JSON som motsvarar din nätregion, från listan nedan:

>[!TIP]
>
>Du måste säkerhetskopiera IP-filtreringsreglerna för brandväggen eftersom de tas bort efter det här anropet.

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
          "id": "/subscriptions/40bde086-46ad-44c3-afba-c306f54b64ec/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_nld2_network_10_20_40_0_23/subnets/ethos_12_prod_nld2_network_10_20_40_0_23"
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

- [Skapa en Event Hubs-källanslutning med API:t för Flow Service](../../tutorials/api/create/cloud-storage/eventhub.md)
- [Samla in strömmande data med API:t för Flow Service](../../tutorials/api/collect/streaming.md)

### Använda gränssnittet

- [Skapa en källanslutning för händelsehubbar i användargränssnittet](../../tutorials/ui/create/cloud-storage/eventhub.md)
- [Konfigurera ett dataflöde för en molnlagringsanslutning i användargränssnittet](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
