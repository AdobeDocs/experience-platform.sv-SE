---
keywords: Experience Platform;hemmabruk;populära ämnen; analys;klassificeringar
description: Lär dig hur du skapar en Adobe Analytics-källanslutning i användargränssnittet för att överföra klassificeringsdata till Adobe Experience Platform.
solution: Experience Platform
title: Skapa en Adobe Analytics-källanslutning för klassificeringsdata i användargränssnittet
type: Tutorial
exl-id: d606720d-f1ca-47cc-919b-643a8fc61e07
source-git-commit: f619bbf2c8d313eabc6444b4bd8c09615a00cc42
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---

# Skapa en Adobe Analytics-källanslutning för klassificeringsdata i användargränssnittet

I den här självstudiekursen beskrivs hur du skapar en datakällanslutning för Adobe Analytics Classifications i användargränssnittet för att hämta klassificeringsdata till Adobe Experience Platform.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

Data Connector för Analytics-klassificeringar kräver att dina data har migrerats till den nya [!DNL Classifications] Adobe Analytics infrastruktur före användning. Kontakta Adobe-kontoteamet om du vill bekräfta migreringsstatusen för dina data.

## Välj klassificeringar

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och sedan markera **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt källarbetsytan. The **[!UICONTROL Catalog]** visas tillgängliga källor för att skapa inkommande anslutningar. Varje källkort visar ett alternativ för att antingen konfigurera ett nytt konto eller lägga till data till ett befintligt konto.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under **[!UICONTROL Adobe applications]** väljer du **[!UICONTROL Adobe Analytics]** och välj **[!UICONTROL Add data]** för att börja arbeta med data från analysklassificeringar.

![](../../../../images/tutorials/create/classifications/catalog.png)

The **[!UICONTROL Analytics source add data]** visas. Välj **[!UICONTROL Classifications]** från den övre rubriken för att se en lista över [!DNL Classifications] datauppsättningar, inklusive information om deras dimensions-ID, rapportsvitnamn och rapportsvitens-ID.

Varje sida visar upp till tio olika [!DNL Classifications] datauppsättningar du kan välja bland. Välj **[!UICONTROL Next]** längst ned på sidan om du vill bläddra efter fler alternativ. Panelen till höger visar det totala antalet [!DNL Classifications] de datamängder du har valt samt deras namn. Med den här panelen kan du även ta bort [!DNL Classifications] datauppsättningar som du kan ha valt av misstag eller rensa alla markeringar med en åtgärd.

Du kan välja upp till 30 olika [!DNL Classifications] datauppsättningar som [!DNL Platform].

När du har valt [!DNL Classifications] datauppsättningar, välja **[!UICONTROL Next]** längst upp till höger på sidan.

![](../../../../images/tutorials/create/classifications/add-data.png)

## Granska dina klassificeringar

The **[!UICONTROL Review]** visas så att du kan granska det du valt [!DNL Classifications] datauppsättningar innan de skapas. Informationen är grupperad i följande kategorier:

* **[!UICONTROL Connection]**: Visar källplattformen och anslutningsstatus.
* **[!UICONTROL Data type]**: Visar antalet markerade [!DNL Classifications].
* **[!UICONTROL Scheduling]**: Visar synkroniseringsfrekvensen för [!DNL Classifications] data.

När du har granskat dataflödet klickar du på **[!UICONTROL Finish]** så att dataflödet kan skapas.

![](../../../../images/tutorials/create/classifications/review.png)

## Övervaka klassificeringens dataflöde

När dataflödet har skapats kan du övervaka de data som hämtas genom det. Från **[!UICONTROL Catalog]** skärm, välja **[!UICONTROL Dataflows]** för att visa en lista över etablerade flöden som är kopplade till din [!DNL Classifications] konto.

![](../../../../images/tutorials/create/classifications/dataflows.png)

The **[!UICONTROL Dataflows]** visas. På den här sidan finns en lista med dataflöden, inklusive information om namn, källdata och körningsstatus för dataflöde. Till höger finns **[!UICONTROL Properties]** panel som innehåller metadata om [!DNL Classifications] dataflöde.

Välj **[!UICONTROL Target dataset]** du vill komma åt.

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

The **[!UICONTROL Dataset activity]** sidan visar information om den valda måldatauppsättningen, inklusive information om dess batchstatus, datauppsättnings-ID och schema.

>[!IMPORTANT]
>
>Även om det går att ta bort datauppsättningar för andra källanslutningar stöds det för närvarande inte för datakopplingen för analysklassificeringar. Om du tar bort en datauppsättning av misstag, kontakta Adobe kundtjänst.

![](../../../../images/tutorials/create/classifications/dataset.png)


## Nästa steg

Genom att följa den här självstudiekursen har du skapat en dataanslutning för Analytics-klassificeringar som ger [!DNL Classifications] data till [!DNL Platform]. Se följande dokument för mer information om [!DNL Analytics] och [!DNL Classifications] data:

* [Översikt över Analytics Data Connector](../../../../connectors/adobe-applications/analytics.md)
* [Skapa en Analytics-dataanslutning i användargränssnittet](./analytics.md)
* [Om klassificeringar](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html)
