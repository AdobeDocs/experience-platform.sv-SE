---
keywords: Experience Platform;hemmabruk;populära ämnen; analys;klassificeringar
description: I den här självstudiekursen beskrivs hur du skapar en Adobe Analytics Classifications Data-koppling i användargränssnittet för att överföra klassificeringsdata till Adobe Experience Platform.
solution: Experience Platform
title: Skapa en Adobe Analytics Classifications-dataanslutning i användargränssnittet
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 2dbd92efbd992b70f4f750b09e9d2e0626e71315
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---


# Skapa en Adobe Analytics Classifications-dataanslutning i användargränssnittet

I den här självstudiekursen beskrivs hur du skapar en Adobe Analytics Classifications Data-koppling i användargränssnittet för att överföra klassificeringsdata till Adobe Experience Platform.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

Data Connector för Analytics-klassificeringar kräver att dina data har migrerats till den nya [!DNL Classifications]-infrastrukturen i Adobe Analytics innan de används. Kontakta Adobe Customer Success Manager för att bekräfta migreringsstatusen för dina data.

## Välj klassificeringar

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt källarbetsytan. Skärmen **[!UICONTROL Catalog]** visar tillgängliga källor för att skapa inkommande anslutningar med. Varje källkort visar ett alternativ för att antingen konfigurera ett nytt konto eller lägga till data till ett befintligt konto.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj **[!UICONTROL Adobe Analytics]**-kortet under kategorin **[!UICONTROL Adobe applications]** och välj sedan **[!UICONTROL Add data]** för att börja arbeta med Analytics Classifications Data.

![](../../../../images/tutorials/create/classifications/catalog.png)

**[!UICONTROL Analytics source add data]**-steget visas. Välj **[!UICONTROL Classifications]** i den översta rubriken om du vill visa en lista över [!DNL Classifications]-datauppsättningar, inklusive information om deras dimension-ID, rapportsvitnamn och rapportsvitens-ID.

Varje sida visar upp till tio olika [!DNL Classifications]-datauppsättningar som du kan välja mellan. Välj **[!UICONTROL Next]** längst ned på sidan om du vill bläddra efter fler alternativ. Panelen till höger visar det totala antalet [!DNL Classifications] datamängder som du har valt samt deras namn. På den här panelen kan du även ta bort alla [!DNL Classifications]-datauppsättningar som du har valt av misstag eller rensa alla markeringar med en åtgärd.

Du kan välja upp till 30 olika [!DNL Classifications]-datauppsättningar att hämta till [!DNL Platform].

När du har valt dina [!DNL Classifications]-datauppsättningar väljer du **[!UICONTROL Next]** längst upp till höger på sidan.

![](../../../../images/tutorials/create/classifications/add-data.png)

## Granska dina klassificeringar

Steget **[!UICONTROL Review]** visas så att du kan granska dina valda [!DNL Classifications]-datauppsättningar innan de skapas. Informationen är grupperad i följande kategorier:

* **[!UICONTROL Connection]**: Visar källplattformen och anslutningsstatus.
* **[!UICONTROL Data type]**: Visar antalet markerade  [!DNL Classifications].
* **[!UICONTROL Scheduling]**: Visar synkroniseringsfrekvensen för  [!DNL Classifications] data.

När du har granskat dataflödet klickar du på **[!UICONTROL Finish]** och ger dig tid att skapa dataflödet.

![](../../../../images/tutorials/create/classifications/review.png)

## Övervaka klassificeringens dataflöde

När dataflödet har skapats kan du övervaka de data som hämtas genom det. På skärmen **[!UICONTROL Catalog]** väljer du **[!UICONTROL Dataflows]** för att visa en lista över etablerade flöden som är kopplade till ditt [!DNL Classifications]-konto.

![](../../../../images/tutorials/create/classifications/dataflows.png)

Skärmen **[!UICONTROL Dataflows]** visas. På den här sidan finns en lista med dataflöden, inklusive information om namn, källdata och körningsstatus för dataflöde. Till höger finns panelen **[!UICONTROL Properties]** som innehåller metadata om [!DNL Classifications]-dataflödet.

Markera **[!UICONTROL Target dataset]** som du vill komma åt.

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

På sidan **[!UICONTROL Dataset activity]** visas information om den valda måldatauppsättningen, inklusive information om dess batchstatus, datauppsättnings-ID och schema.

>[!IMPORTANT]
>
>Även om det går att ta bort datauppsättningar för andra källanslutningar stöds det för närvarande inte för datakopplingen för analysklassificeringar. Om du tar bort en datauppsättning av misstag, kontakta Adobe kundtjänst.

![](../../../../images/tutorials/create/classifications/dataset.png)


## Nästa steg

Genom att följa den här självstudiekursen har du skapat en dataanslutning för Analytics-klassificeringar som hämtar [!DNL Classifications]-data till [!DNL Platform]. Mer information om [!DNL Analytics]- och [!DNL Classifications]-data finns i följande dokument:

* [Översikt över Analytics Data Connector](../../../../connectors/adobe-applications/analytics.md)
* [Skapa en Analytics Data Connector i användargränssnittet](./analytics.md)
* [Om klassificeringar](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html)