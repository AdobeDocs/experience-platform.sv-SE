---
keywords: Experience Platform;home;populära topics;Customer Attributes connector
solution: Experience Platform
title: Kundattribut Source Connector - översikt
description: Lär dig koppla kundattribut till Adobe Experience Platform med API:er eller användargränssnittet
exl-id: 63765ecd-ddb5-4992-a3de-d53f054bfb28
source-git-commit: 5b37b51308dc2097c05b0e763293467eb12a2f21
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# Koppling för kundattribut

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Med [[!DNL Customer Attributes]](https://experienceleague.adobe.com/docs/core-services/interface/services/customer-attributes/attributes.html) i Experience Cloud kan du överföra dina hämtade företagsdata från en CRM-databas (Customer relationship management). Du kan överföra data till en kundattributdatakälla i Experience Cloud och sedan använda data i Adobe Analytics och Adobe Target.

Experience Platform har stöd för att importera [!DNL Customer Attributes]-profildata till Adobe Experience Platform.

## Datauppsättningar och scheman

[!DNL Customer Attributes]-källan skapar automatiskt datauppsättningen för data som ska landas i. Den automatiskt skapade datauppsättningen är fast och kan inte väljas manuellt. Källan skapar också automatiskt schemat för datauppsättningen baserat på indatadatakällan. Den här processen innebär också att nödvändiga mappningar mellan schemat och källdata skapas automatiskt.

## Identiteter

Den primära identiteten för en datauppsättning finns i den första kolumnen i CSV-filen för källdata. Källan [!DNL Customer Attributes] förutsätter att identiteten alltid är mappad till [`CORE` namespace ](../../../identity-service/features/namespaces.md), ett systemgenererat namnutrymme som stöds av [[!DNL Identity Service]](../../../identity-service/home.md).

Du kan inte välja ett befintligt namnområde för identiteten när du använder källan [!DNL Customer Attributes] eftersom [!DNL Customer Attributes] förutsätter att schemats primära identitet alltid finns i identitetskartan. [!DNL Customer Attributes] skapar sedan mappningen av käll-ID:t till identitetsmappningens UUID automatiskt.

För att [!DNL Customer Attributes]-data ska kunna kopplas till andra [!DNL Profile]-datauppsättningar måste dess data och identiteter kunna matchas mot ett Experience Cloud-ID.

Du kan upprätta namnutrymmet `CORE` genom att ange Experience Cloud-ID för besökaren med [Web SDK](/help/web-sdk/identity/overview.md), [Mobile SDK](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/) eller [Experience Cloud ID Service API](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html).

Filen [!DNL Customer Attributes] fyller inte i några andra identitetsrelationer. Om en [!DNL Customer Attributes]-källdatauppsättning till exempel innehåller ett **E-post** och ett **Förmåns-ID** måste dessa fält ha en etikett som identitetsfält i schemat för att kunna bearbetas till [!DNL Identity Service].

Mer information finns i självstudiekursen [Skapa en [!DNL Customer Attributes] källanslutning i användargränssnittet](../../tutorials/ui/create/adobe-applications/customer-attributes.md).
