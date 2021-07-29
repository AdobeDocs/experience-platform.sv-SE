---
keywords: Experience Platform;home;populära topics;Customer Attributes connector
solution: Experience Platform
title: Översikt över källkopplingen för kundattribut
topic-legacy: overview
description: Lär dig koppla kundattribut till Adobe Experience Platform med API:er eller användargränssnittet
exl-id: 63765ecd-ddb5-4992-a3de-d53f054bfb28
source-git-commit: 541cc87f218a6ef3dcca37573f6d0f9cf560edfb
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# Koppling för kundattribut

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

[[!DNL Customer Attributes]](https://experienceleague.adobe.com/docs/core-services/interface/services/customer-attributes/attributes.html?lang=en) i Experience Cloud kan du överföra dina hämtade företagsdata från en CRM-databas (customer relationship management). Du kan överföra data till en Customer Attribute-datakälla i Experience Cloud och sedan använda data i Adobe Analytics och Adobe Target.

Experience Platform har stöd för att importera [!DNL Customer Attributes] profildata till Adobe Experience Platform.

## Datauppsättningar och scheman

Källan [!DNL Customer Attributes] skapar automatiskt datauppsättningen för data som ska landas i. Den automatiskt skapade datauppsättningen är fast och kan inte väljas manuellt. Källan skapar också automatiskt schemat för datauppsättningen baserat på indatadatakällan. Den här processen innebär också att nödvändiga mappningar mellan schemat och källdata skapas automatiskt.

## Identiteter

Den primära identiteten för en datauppsättning finns i den första kolumnen i CSV-filen för källdata. Källan [!DNL Customer Attributes] förutsätter att identiteten alltid är mappad till namnutrymmet [`CORE`](../../../identity-service/namespaces.md), ett systemgenererat namnutrymme som stöds av [[!DNL Identity Service]](../../../identity-service/home.md).

Du kan inte välja ett befintligt namnutrymme för identiteten när du använder källan [!DNL Customer Attributes] eftersom [!DNL Customer Attributes] förutsätter att schemats primära identitet alltid finns i identitetskartan. [!DNL Customer Attributes] skapar sedan mappningen av käll-ID:t till identitetsmappningens UUID på ett automatiserat sätt.

För att [!DNL Customer Attributes]-data ska kunna kopplas till andra [!DNL Profile]-datauppsättningar måste data och identiteter kunna matchas mot ett Experience Cloud-ID.

Du kan upprätta namnutrymmet `CORE` genom att ange Experience Cloud-ID för besökaren med [Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en), [Mobile SDK](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/identity) eller [Experience Cloud ID Service API](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=en).

Filen [!DNL Customer Attributes] fyller inte i några andra identitetsrelationer ytterligare. Om en [!DNL Customer Attributes]-källdatauppsättning till exempel innehåller ett **e-postfält** och ett **lojalitets-ID**-fält, måste dessa fält ha en etikett som identitetsfält i schemat för att kunna bearbetas till [!DNL Identity Service].

Mer information finns i självstudiekursen om att [skapa en [!DNL Customer Attributes] källanslutning i användargränssnittet](../../tutorials/ui/create/adobe-applications/customer-attributes.md).
