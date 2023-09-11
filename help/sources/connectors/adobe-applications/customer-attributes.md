---
keywords: Experience Platform;home;populära topics;Customer Attributes connector
solution: Experience Platform
title: Översikt över källkopplingen för kundattribut
description: Lär dig koppla kundattribut till Adobe Experience Platform med API:er eller användargränssnittet
exl-id: 63765ecd-ddb5-4992-a3de-d53f054bfb28
source-git-commit: 139d6a6632532b392fdf8d69c5c59d1fd779a6d1
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# Koppling för kundattribut

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

[[!DNL Customer Attributes]](https://experienceleague.adobe.com/docs/core-services/interface/services/customer-attributes/attributes.html?lang=en) i Experience Cloud kan du överföra dina hämtade företagsdata från en CRM-databas (customer relationship management). Du kan överföra data till en kundattributdatakälla i Experience Cloud och sedan använda data i Adobe Analytics och Adobe Target.

Experience Platform stöder inmatning [!DNL Customer Attributes] profildata till Adobe Experience Platform.

## Datauppsättningar och scheman

The [!DNL Customer Attributes] source skapar automatiskt datauppsättningen för data som ska landas i. Den automatiskt skapade datauppsättningen är fast och kan inte väljas manuellt. Källan skapar också automatiskt schemat för datauppsättningen baserat på indatadatakällan. Den här processen innebär också att nödvändiga mappningar mellan schemat och källdata skapas automatiskt.

## Identiteter

Den primära identiteten för en datauppsättning finns i den första kolumnen i CSV-filen för källdata. The [!DNL Customer Attributes] källan förutsätter att identiteten alltid är mappad till [`CORE` namespace](../../../identity-service/namespaces.md), ett systemgenererat namnutrymme som stöds av [[!DNL Identity Service]](../../../identity-service/home.md).

Du kan inte välja ett befintligt namnutrymme för identiteten när du använder [!DNL Customer Attributes] källa [!DNL Customer Attributes] antar att schemats primära identitet alltid finns i identitetskartan. [!DNL Customer Attributes] skapar sedan mappningen av käll-ID:t till identitetsmappningens UUID på ett automatiskt sätt.

För [!DNL Customer Attributes] data att knyta till andra [!DNL Profile] datauppsättningar, dess data och identiteter måste kunna matchas mot ett Experience Cloud-ID.

Du kan skapa `CORE` namnutrymme genom att ange Experience Cloud-ID för besökaren med [Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en), [Mobile SDK](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/)eller [Experience Cloud ID-tjänste-API](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=en).

The [!DNL Customer Attributes] filen fyller inte i några andra identitetsrelationer. Exempel: om en [!DNL Customer Attributes] källdatauppsättningen innehåller en **E-post** och **Förmåns-ID** måste fälten märkas som identitetsfält i schemat för att kunna bearbetas till [!DNL Identity Service].

Se självstudiekursen om [skapa [!DNL Customer Attributes] källanslutning i användargränssnittet](../../tutorials/ui/create/adobe-applications/customer-attributes.md) för mer information.
