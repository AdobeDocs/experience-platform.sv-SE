---
keywords: Experience Platform;home;popular topics; analytics;classifications
description: I den här självstudiekursen beskrivs hur du skapar en Adobe Analytics Classifications Data-koppling i användargränssnittet för att överföra klassificeringsdata till Adobe Experience Platform.
solution: Experience Platform
title: Skapa en Adobe Analytics Classifications-dataanslutning i användargränssnittet
topic: overview
translation-type: tm+mt
source-git-commit: 0da686743e8bc57d310f7eff6f1bf812a8f31238
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 1%

---


# Skapa en Adobe Analytics Classifications-dataanslutning i användargränssnittet

I den här självstudiekursen beskrivs hur du skapar en Adobe Analytics Classifications Data-koppling i användargränssnittet för att överföra klassificeringsdata till Adobe Experience Platform.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model] (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [[!DNL-sandlådor]](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

## Välj klassificeringar

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj sedan **[!UICONTROL Sources]** från det vänstra navigeringsfältet för att komma åt källarbetsytan. På **[!UICONTROL Catalog]** skärmen visas tillgängliga källor för att skapa inkommande anslutningar. Varje källkort visar ett alternativ för att antingen konfigurera ett nytt konto eller lägga till data till ett befintligt konto.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under **[!UICONTROL Adobe applications]** kategorin markerar du **[!UICONTROL Adobe Analytics]** kortet och väljer sedan **[!UICONTROL Add data]** att börja arbeta med Analytics-klassificeringsdata.

![](../../../../images/tutorials/create/classifications/catalog.png)

Steget **[!UICONTROL Analytics source add data]** visas. Välj **[!UICONTROL Classifications]** i det övre huvudet om du vill se en lista över [!DNL Classifications] datauppsättningar, inklusive information om deras **[!UICONTROL Dimension ID]**, **[!UICONTROL Report Suite name]** och **[!UICONTROL Report Suite ID]**.

Varje sida visar upp till tio olika [!DNL Classifications] datauppsättningar som du kan välja mellan. Välj **[!UICONTROL Next]** längst ned på sidan om du vill bläddra efter fler alternativ. Panelen till höger visar det totala antalet datauppsättningar som du har valt samt deras namn. [!DNL Classifications] På den här panelen kan du även ta bort alla datauppsättningar som du har valt av misstag eller rensa alla markeringar med en åtgärd. [!DNL Classifications]

Du kan välja upp till 30 olika [!DNL Classifications] datauppsättningar att hämta till [!DNL Platform].

När du har valt dina [!DNL Classifications] datauppsättningar väljer du **[!UICONTROL Next]** längst upp till höger på sidan.

![](../../../../images/tutorials/create/classifications/add-data.png)

## Granska dina klassificeringar

Steget visas så att du kan granska de markerade datauppsättningarna innan du skapar dem **[!UICONTROL Review]** [!DNL Classifications] . Informationen är grupperad i följande kategorier:

* **[!UICONTROL Connection]**: Visar källplattformen och anslutningsstatus.
* **[!UICONTROL Data type]**: Visar antalet markerade [!DNL Classifications].
* **[!UICONTROL Scheduling]**: Visar synkroniseringsfrekvensen för [!DNL Classifications] data.

När du har granskat dataflödet kan du klicka **[!UICONTROL Finish]** och vänta tills dataflödet har skapats.

![](../../../../images/tutorials/create/classifications/review.png)

## Övervaka klassificeringens dataflöde

När dataflödet har skapats kan du övervaka de data som hämtas genom det. På **[!UICONTROL Catalog]** skärmen väljer du **[!UICONTROL Dataflows]** för att visa en lista över etablerade flöden som är kopplade till ditt [!DNL Classifications] konto.

![](../../../../images/tutorials/create/classifications/dataflows.png)

Skärmen visas **[!UICONTROL Dataflows]** . På den här sidan finns en lista med dataflöden, inklusive information om namn, källdata och körningsstatus för dataflöde. Till höger finns den panel **[!UICONTROL Properties]** som innehåller metadata om [!DNL Classifications] dataflödet.

Välj den **[!UICONTROL Target dataset]** du vill komma åt.

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

På **[!UICONTROL Dataset activity]** sidan visas information om den valda måldatauppsättningen, inklusive information om dess batchstatus, datauppsättnings-ID och schema.

>[!IMPORTANT]
>
>Även om det går att ta bort datauppsättningar för andra källanslutningar stöds det för närvarande inte för datakopplingen för analysklassificeringar. Om du tar bort en datauppsättning av misstag, kontakta Adobe kundtjänst.

![](../../../../images/tutorials/create/classifications/dataset.png)


## Nästa steg

Genom att följa den här självstudiekursen har du skapat en dataanslutning för Analytics-klassificeringar som samlar in [!DNL Classifications] data [!DNL Platform]. Mer information om [!DNL Analytics] och [!DNL Classifications] data finns i följande dokument:

* [Översikt över Analytics Data Connector](../../../../connectors/adobe-applications/analytics.md)
* [Skapa en Analytics Data Connector i användargränssnittet](./analytics.md)
* [Om klassificeringar](https://docs.adobe.com/content/help/en/analytics/components/classifications/c-classifications.html#)