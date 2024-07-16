---
keywords: Experience Platform;hemmabruk;populära ämnen; analys;klassificeringar
description: Lär dig hur du skapar en Adobe Analytics-källanslutning i användargränssnittet för att överföra klassificeringsdata till Adobe Experience Platform.
solution: Experience Platform
title: Skapa en Adobe Analytics Source-anslutning för klassificeringsdata i användargränssnittet
type: Tutorial
exl-id: d606720d-f1ca-47cc-919b-643a8fc61e07
source-git-commit: fcebef97ba9cc667f80afd55980c5460912a56fb
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 0%

---

# Skapa en Adobe Analytics-källanslutning för klassificeringsdata i användargränssnittet

I den här självstudiekursen beskrivs hur du skapar en datakällanslutning för Adobe Analytics Classifications i användargränssnittet för att hämta klassificeringsdata till Adobe Experience Platform.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans till separata virtuella miljöer för att hjälpa till att utveckla och utveckla program för digitala upplevelser.

Data Connector för Analytics-klassificeringar kräver att dina data har migrerats till den nya [!DNL Classifications]-infrastrukturen i Adobe Analytics innan de används. Kontakta Adobe-kontoteamet om du vill bekräfta migreringsstatusen för dina data.

## Välj klassificeringar

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt källarbetsytan. På skärmen **[!UICONTROL Catalog]** visas tillgängliga källor för att skapa inkommande anslutningar. Varje källkort visar ett alternativ för att antingen konfigurera ett nytt konto eller lägga till data till ett befintligt konto.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också söka efter den specifika källa som du vill arbeta med med sökalternativet.

Välj **[!UICONTROL Adobe Analytics]**-kortet under kategorin **[!UICONTROL Adobe applications]** och välj sedan **[!UICONTROL Add data]** för att börja arbeta med Analytics-klassificeringsdata.

![](../../../../images/tutorials/create/classifications/catalog.png)

**[!UICONTROL Analytics source add data]**-steget visas. Välj **[!UICONTROL Classifications]** i den övre rubriken om du vill visa en lista över [!DNL Classifications] datauppsättningar, inklusive information om deras mått-ID, rapportsvitens namn och rapportsvitens-ID.

Varje sida visar upp till tio olika [!DNL Classifications] datauppsättningar som du kan välja mellan. Välj **[!UICONTROL Next]** längst ned på sidan om du vill bläddra efter fler alternativ. Panelen till höger visar det totala antalet [!DNL Classifications] datauppsättningar som du har valt samt deras namn. På den här panelen kan du även ta bort alla [!DNL Classifications]-datauppsättningar som du har valt av misstag eller rensa alla markeringar med en åtgärd.

Du kan välja upp till 30 olika [!DNL Classifications]-datauppsättningar att hämta till [!DNL Platform].

När du har valt dina [!DNL Classifications]-datauppsättningar väljer du **[!UICONTROL Next]** längst upp till höger på sidan.

![](../../../../images/tutorials/create/classifications/add-data.png)

## Granska dina klassificeringar

Steg **[!UICONTROL Review]** visas, så att du kan granska dina valda [!DNL Classifications]-datauppsättningar innan de skapas. Informationen är grupperad i följande kategorier:

* **[!UICONTROL Connection]**: Visar källplattformen och anslutningsstatus.
* **[!UICONTROL Data type]**: Visar antalet markerade [!DNL Classifications].
* **[!UICONTROL Scheduling]**: Visar synkroniseringsfrekvensen för [!DNL Classifications]-data.

När du har granskat dataflödet klickar du på **[!UICONTROL Finish]** och tillåt en tid innan dataflödet skapas.

![](../../../../images/tutorials/create/classifications/review.png)

## Övervaka klassificeringens dataflöde

När dataflödet har skapats kan du övervaka de data som hämtas genom det. På skärmen **[!UICONTROL Catalog]** väljer du **[!UICONTROL Dataflows]** för att visa en lista över etablerade flöden som är kopplade till ditt [!DNL Classifications]-konto.

![](../../../../images/tutorials/create/classifications/dataflows.png)

Skärmen **[!UICONTROL Dataflows]** visas. På den här sidan finns en lista med dataflöden, inklusive information om namn, källdata och körningsstatus för dataflöde. Till höger finns panelen **[!UICONTROL Properties]** som innehåller metadata om [!DNL Classifications]-dataflödet.

Markera de **[!UICONTROL Target dataset]** som du vill komma åt.

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

Sidan **[!UICONTROL Dataset activity]** visar information om den valda måldatauppsättningen, inklusive information om dess batchstatus, datauppsättnings-ID och schema.

![](../../../../images/tutorials/create/classifications/dataset.png)

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en dataanslutning för analysklassificeringar som samlar in [!DNL Classifications] data i [!DNL Platform]. Mer information om [!DNL Analytics]- och [!DNL Classifications]-data finns i följande dokument:

* [Översikt över Analytics Data Connector](../../../../connectors/adobe-applications/analytics.md)
* [Skapa en Analytics-dataanslutning i användargränssnittet](./analytics.md)
* [Om klassificeringar](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html)
