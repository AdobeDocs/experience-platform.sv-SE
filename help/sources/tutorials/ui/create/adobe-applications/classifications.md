---
description: Lär dig hur du skapar en Adobe Analytics-källanslutning i användargränssnittet för att överföra klassificeringsdata till Adobe Experience Platform.
title: Skapa en Adobe Analytics Source-anslutning för klassificeringsdata i användargränssnittet
exl-id: d606720d-f1ca-47cc-919b-643a8fc61e07
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---

# Skapa en Adobe Analytics-källanslutning för klassificeringsdata i användargränssnittet

>[!TIP]
>
>Som standard uppdateras klassificeringsdata för Adobe Analytics varje vecka. Intag av data för dina klassificeringsuppgifter behandlas sju dagar efter den första konfigurationen av dataflödet. Den första inläsningen importerar hela data och det efterföljande veckointaget kör inkrementella data.

I den här självstudiekursen får du lära dig hur du importerar klassificeringsuppgifter från Adobe Analytics till Adobe Experience Platform via användargränssnittet.

## Kom igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Experience Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

Källkopplingen för Analytics-klassificeringar kräver att dina data har migrerats till den nya klassificeringsinfrastrukturen i Adobe Analytics innan de används. Kontakta Adobe-kontoteamet om du vill bekräfta migreringsstatusen för dina data.

## Välj klassificeringar

I Experience Platform-gränssnittet väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i [!UICONTROL Sources]. Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under kategorin *Adobe-program* väljer du **[!UICONTROL Adobe Analytics]** och sedan **[!UICONTROL Set up]**.

>[!TIP]
>
>Källor i källkatalogen visar alternativet **[!UICONTROL Set up]** om det inte finns något autentiserat konto. När ett konto autentiseras ändras alternativet till **[!UICONTROL Add data]**.

![Källkatalogen i Experience Platform-gränssnittet med Adobe Analytics-källan markerad.](../../../../images/tutorials/create/classifications/catalog.png)

Välj sedan [!UICONTROL Classifications] och sedan de klassificeringsdatauppsättningar som du vill importera till Experience Platform.

Du kan välja upp till 30 olika klassificeringsdatauppsättningar att hämta till Experience Platform. Alla datauppsättningar som du väljer visas i den högra listen. När du är klar väljer du [!UICONTROL Next] för att fortsätta.

![Klassificeringssidan med flera markerade klassificeringsdatamängder.](../../../../images/tutorials/create/classifications/select.png)

## Granska dina klassificeringar

Steget **[!UICONTROL Review]** visas så att du kan granska de valda klassificeringsdatauppsättningarna innan de skapas. Informationen är grupperad i följande kategorier:

* **[!UICONTROL Connection]**: Visar källplattformen och anslutningsstatus.
* **[!UICONTROL Data type]**: Visar antalet valda klassificeringar.
* **[!UICONTROL Scheduling]**: Visar synkroniseringsfrekvensen för klassificeringsdata. **Obs!** Klassificeringsdata uppdateras varje vecka.

När du har granskat dataflödet klickar du på **[!UICONTROL Finish]** och tillåt en tid innan dataflödet skapas.

![Granskningssidan för Adobe Analytics-klassificeringsdata.](../../../../images/tutorials/create/classifications/review.png)

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en Statakoppling för Analytics-klassificeringar som samlar in klassificeringsdata i Experience Platform. Mer information om [!DNL Analytics] och klassificeringsdata finns i följande dokument:

* [Adobe Analytics Source Connector - översikt](../../../../connectors/adobe-applications/analytics.md)
* [Skapa en Analytics-källanslutning för rapportsvitdata i användargränssnittet](./analytics.md)
* [Om klassificeringar](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html)
