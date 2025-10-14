---
title: Azure Event Hubs Source Connector - översikt
description: Lär dig hur du ansluter Azure Event Hubs till Adobe Experience Platform med hjälp av API:er eller användargränssnittet.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: b4d4bc7f-2241-482d-a5c2-4422c31705bf
source-git-commit: 02c777b5db9734cf45b35f131d83c35c5ce670fb
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 0%

---

# [!DNL Azure Event Hubs]-källa

>[!IMPORTANT]
>
>* Källan [!DNL Azure Event Hubs] är tillgänglig i källkatalogen för användare som har köpt Real-Time CDP Ultimate.
>
>* Du kan nu använda källan [!DNL Azure Event Hubs] när du kör Adobe Experience Platform på Amazon Web Services (AWS). Experience Platform som körs på AWS är för närvarande tillgängligt för ett begränsat antal kunder. Mer information om den Experience Platform-infrastruktur som stöds finns i [Experience Platform översikt över flera moln](../../../landing/multi-cloud.md).

Adobe Experience Platform erbjuder inbyggd anslutning för molnleverantörer som AWS, [!DNL Google Cloud Platform] och [!DNL Azure]. Ni kan överföra data från dessa system till Experience Platform.

Lagringskällor i molnet kan överföra dina egna data till Experience Platform utan att du behöver hämta, formatera eller överföra dem. Inkapslade data kan formateras som XDM JSON, XDM Parquet eller avgränsade. Varje steg i processen är integrerat i arbetsflödet för källor. Med Experience Platform kan du hämta in data från [!DNL Event Hubs] i realtid.

## Skalar med [!DNL Event Hubs]

Skalningsfaktorn för [!DNL Event Hubs]-instansen måste ökas om du behöver få in stora datavolymer, öka parallellismen eller öka hastigheten för intaget på Experience Platform.

### Högre volymdata

För närvarande är den maximala datavolymen som du kan hämta från ditt [!DNL Event Hubs]-konto till Experience Platform 2 000 poster per sekund. Om du vill skala upp och importera data i större volymer kontaktar du Adobe.

### Öka parallellismen på [!DNL Event Hubs] och Experience Platform

Parallellitet avser samtidig körning av samma uppgifter på flera bearbetningsenheter för att öka hastighet och prestanda. Du kan öka parallelliteten på [!DNL Event Hubs]-sidan genom att öka partitionen eller genom att köpa fler bearbetningsenheter för ditt [!DNL Event Hubs]-konto. Mer information finns i det här [[!DNL Event Hubs] dokumentet om skalning](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-scalability).

Om du vill öka hastigheten för intag på Experience Platform-sidan måste Experience Platform öka antalet aktiviteter i källkopplingen som ska läsas från dina [!DNL Event Hubs]-partitioner. När du har ökat parallelliteten på [!DNL Event Hubs]-sidan kontaktar du Adobe-representanten för att skala Experience Platform-aktiviteter baserat på den nya partitionen. Den här processen är för närvarande inte automatiserad.

## Använd ett virtuellt nätverk för att ansluta till [!DNL Event Hubs] till Experience Platform

Experience Platform stöder anslutning till [!DNL Event Hubs] via ett virtuellt nätverk. På så sätt kan du överföra data via en säker, privat anslutning i stället för via det offentliga Internet. Du kan tillåtslista Experience Platform VNet för att på ett säkert sätt dirigera [!DNL Event Hubs]-trafik via det privata [!DNL Azure]-stamnätet samtidigt som du behåller dina befintliga brandväggsskydd.

Om du vill konfigurera ett virtuellt nätverk går du till det här [[!DNL Event Hubs] uppsättningsdokumentet för nätverksregler](https://learn.microsoft.com/en-us/azure/event-hubs/network-security) och följer stegen nedan:

* Välj **Prova** på REST API-panelen;
* Autentisera ditt [!DNL Azure]-konto med dina autentiseringsuppgifter i samma webbläsare;
* Markera namnområdet [!DNL Event Hubs], resursgruppen och prenumerationen som du vill hämta till Experience Platform och välj sedan **KÖR**;
* I JSON-brödtexten som visas lägger du till följande Experience Platform-undernät under `virtualNetworkRules` i `properties`:


>[!IMPORTANT]
>
>Du måste skapa en säkerhetskopia av det JSON-innehåll som du får innan du uppdaterar `virtualNetworkRules` med Experience Platform-undernätet eftersom det innehåller dina befintliga IP-filtreringsregler. Annars tas reglerna bort efter anropet.


```json
{
    "subnet": {
        "id": "/subscriptions/93f21779-b1fd-49ee-8547-2cdbc979a44f/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_va7_network_10_19_144_0_22/subnets/ethos_12_prod_va7_network_10_19_144_0_22"
    },
    "ignoreMissingVnetServiceEndpoint": true
}
```

Se listan nedan för olika områden i Experience Platform undernät:

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
            "id": "/subscriptions/40bde086-46ad-44c3-afba-c306f54b64ec/resourceGroups/ethos_12_prod_nld2_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_nld2-vnet/subnets/ethos_12_prod_nld2_network_10_20_40_0_23"
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
          "id": "/subscriptions/1618ef18-9edc-48bf-88dd-61cc979629b5/resourceGroups/ethos_12_prod_aus5_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_aus5-vnet/subnets/ethos_12_prod_aus5_network_10_21_116_0_22"
        },
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

Mer information om uppsättningar nätverksregler finns i följande [[!DNL Event Hubs] dokument](https://learn.microsoft.com/en-us/azure/event-hubs/network-security).

## Anslut [!DNL Event Hubs] till Experience Platform

>[!NOTE]
>
>När du har skapat eller uppdaterat ett dataflöde för direktuppspelning krävs en kort 5-minuters paus i datainmatningen för att förhindra eventuella fall av dataförlust eller dataförlust.

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Event Hubs] till Experience Platform med API:er eller användargränssnittet:

### Använda API:er

* [Skapa en Event Hubs-källanslutning med API:t för Flow Service](../../tutorials/api/create/cloud-storage/eventhub.md)
* [Samla in strömmande data med API:t för Flow Service](../../tutorials/api/collect/streaming.md)

### Använda gränssnittet

* [Skapa en källanslutning för händelsehubbar i användargränssnittet](../../tutorials/ui/create/cloud-storage/eventhub.md)
* [Konfigurera ett dataflöde för en molnlagringsanslutning i användargränssnittet](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
