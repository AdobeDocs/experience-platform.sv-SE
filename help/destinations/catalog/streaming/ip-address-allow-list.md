---
keywords: IP-adress, IP-intervall, tillåtelselista-mål, tillåtelselista, direktuppspelningsmål för tillåtelselista
title: IP-adress tillåtelselista för direktuppspelningsmål
type: Documentation
description: Den här sidan innehåller IP-intervall som du kan lägga till i tillåtelselista för att på ett säkert sätt exportera data från Experience Platform till HTTP REST API-slutpunkten, Amazon Kinesis eller Azure Event Hubs-instansen.
exl-id: f41303bd-c886-4c67-9e39-21efc3f5b768
source-git-commit: d4833821105433518ee30415fe08f281effa5616
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# IP-adress tillåtelselista för direktuppspelningsmål {#ip-address-allowlist}

>[!IMPORTANT]
>
> * Adobe rekommenderar att du bokmärker den här sidan och går tillbaka till den var tredje månad för att kontrollera de senaste IP-adresserna. Adobe meddelar inte om nya IP-intervall.
> * Listan över IP-adresser som beskrivs här *inte* gäller för alla mål som du skapar med [[!DNL Destination SDK]](/help/destinations/destination-sdk/overview.md).

## Översikt {#overview}

De IP-intervall som beskrivs här gäller följande destinationer:

* [HTTP API-mål](./http-destination.md)
* [[!DNL Amazon Kinesis]](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)
* [[!DNL Azure Event Hubs]](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)

Utgående trafik från Experience Platform till dessa destinationer går alltid igenom de IP-adresser som anges på denna sida.

Den här sidan innehåller IP-intervall som du kan lägga till i tillåtelselista för att på ett säkert sätt exportera data från Experience Platform till HTTP-slutpunkten, [!DNL Amazon Kinesis], eller [!DNL Azure Event Hubs] -instans. Den här funktionen är särskilt användbar om HTTP-slutpunkten finns bakom en brandvägg för företag eller om företagets säkerhets- och efterlevnadsstandarder kräver att en lista över IP-intervall tillåtslista.

Du kan definiera nätverksåtkomstkontroller via nätverkets brandvägg. Genom att ange rätt IP-intervall kan du tillåta trafik för dataöverföringstjänsten.

Adobe rekommenderar att du lägger till följande IP-intervall till en tillåtelselista innan du börjar arbeta med de mål som nämns ovan på den här sidan. Om du inte lägger till ditt regionspecifika IP-intervall på tillåtelselista kan det leda till fel eller utebliven prestanda när du använder dessa direktuppspelningsmål.

## VA7: Kunder i USA och Amerika {#us-americas}

`20.186.185.239`
`40.70.154.136/29`
`52.254.106.160/28`
`52.254.106.176/28`
`52.254.105.192/28`
`20.186.185.181`
`52.254.107.64/28`
`52.254.107.80/28`
`52.254.106.144/28`
`52.254.106.0/28`
`52.254.107.16/28`
`52.254.107.32/28`
`52.254.106.224/28`
`20.186.185.227`
`52.254.106.192/28`
`52.254.107.128/28`
`52.254.106.208/28`
`52.254.106.240/28`
`52.254.107.0/28`
`52.254.107.144/28`
`20.22.83.112`

## NLD2: EMEA-kunder {#emea}

`40.74.4.160/28`
`40.74.6.128/28`
`40.74.7.128/28`
`40.74.4.176/28`
`51.144.184.248/29`
`40.74.7.208/28`
`52.142.236.87`
`20.50.23.153`
`20.101.246.9`
`40.74.4.144/28`
`40.74.7.160/28`
`40.74.3.176/28`
`40.74.6.144/28`
`40.74.6.80/28`
`40.74.5.128/28`
`40.74.7.144/28`
`40.74.7.176/28`
`40.74.6.96/28`
`40.74.6.112/28`
`51.105.144.1`
`40.74.7.192/28`
`51.105.144.81`
`51.124.70.4`
`20.101.233.128`

## AUS5: APAC-kunder {#apac}

`20.43.104.80/28`
`20.43.104.16/28`
`20.43.104.128/28`
`20.40.188.166`
`20.40.191.224/28`
`20.43.104.176/28`
`20.43.104.0/28`
`20.43.105.0/28`
`20.43.105.48/28`
`20.40.191.240/28`
`20.43.104.192/28`
`20.40.188.227`
`20.40.188.194`
`20.43.104.144/28`
`20.43.104.160/28`
`20.43.104.96/28`
`20.43.105.32/28`
`20.43.104.112/28`
`20.43.105.16/28`
`20.43.104.48/28`
`20.40.191.96/28`
`20.43.104.32/28`
`20.43.104.64/28`
`20.53.206.128`
`20.227.35.177`

## CAN2: Kanadas kunder {#can}

`20.104.46.128/28`
`20.104.46.160/28`
`20.104.46.64/28`
`20.104.46.80/28`
`20.116.145.94`
`20.116.147.168`
`20.200.70.192/28`
`20.200.70.208/28`
`20.200.70.224/28`
`20.200.70.240/28`
`20.200.71.0/28`
`20.200.71.112/28`
`20.200.71.128/28`
`20.200.71.144/28`
`20.200.71.16/28`
`20.200.71.160/28`
`20.200.71.176/28`
`20.200.71.32/28`
`20.200.71.48/28`
`20.200.71.64/28`
`20.200.71.80/28`
`20.200.71.96/28`
`20.200.93.180`
`20.200.94.116`
`20.200.94.83`
