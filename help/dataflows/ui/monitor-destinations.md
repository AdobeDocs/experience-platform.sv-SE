---
keywords: Experience Platform;hem;populära ämnen;övervakningskonton;övervaka dataflöden;dataflöden;mål
description: Med destinationer kan ni aktivera data från Adobe Experience Platform för ett oändligt antal externa partner. I den här självstudiekursen finns anvisningar om hur du kan övervaka dataflöden för dina mål med hjälp av användargränssnittet i Experience Platform.
solution: Experience Platform
title: Övervaka dataflöden för mål i användargränssnittet
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: f8186e467dc982003c6feb01886ed16d23572955
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---


# Övervaka dataflöden för mål i användargränssnittet

Med destinationer kan ni aktivera data från Adobe Experience Platform för ett oändligt antal externa partner. I den här självstudiekursen finns anvisningar om hur du kan övervaka dataflöden för dina mål med hjälp av användargränssnittet i Experience Platform.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Destinationer](../../destinations/home.md): Destinationer är färdiga integreringar med vanliga applikationer som möjliggör smidig aktivering av data från Platform för flerkanalskampanjer, e-postkampanjer, riktad annonsering och många andra användningsfall.
- [Sandlådor](../../sandboxes/home.md):  [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda  [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

## Övervaka dataflöden

Gå till fliken **[!UICONTROL Browse]** i arbetsytan **[!UICONTROL Destinations]** i plattformsgränssnittet och välj namnet på ett mål som du vill visa.

![](../assets/ui/monitor-destinations/select-destination.png)

En lista över befintliga dataflöden visas. På den här sidan finns en lista med visningsbara dataflöden, inklusive information om mål, användarnamn, antal dataflöden och status.

Se följande tabell för mer information om status:

| Status | Beskrivning |
| ------ | ----------- |
| Aktiverad | Statusen `Enabled` anger att ett dataflöde är aktivt och att data hämtas enligt det schema som det tillhandahölls. |
| Handikappade | Statusen `Disabled` indikerar att ett dataflöde är inaktivt och inte innehåller några data. |
| Bearbetar | Statusen `Processing` anger att ett dataflöde ännu inte är aktivt. Denna status inträffar ofta omedelbart efter att ett nytt dataflöde har skapats. |
| Fel | Statusen `Error` anger att aktiveringsprocessen för ett dataflöde har avbrutits. |

## [!UICONTROL Dataflow runs]

Fliken [!UICONTROL Dataflow runs] innehåller mätdata för dataflödet som körs till batchdestinationer. En lista över enskilda körningar och deras specifika mått visas tillsammans med följande summor för profilposter:

- **[!UICONTROL Profile records activated]**: Det totala antalet profilposter som har skapats eller uppdaterats för aktivering.
- **[!UICONTROL Profile records skipped]**: Det totala antalet profilposter som hoppas över för aktivering baserat på utträde eller saknade attribut.

![](../assets/ui/monitor-destinations/dataflow-runs.png)

>[!NOTE]
>
>Dataflödeskörningar genereras baserat på måldataflödets schemafrekvens. En separat dataflödeskörning görs för varje sammanfogningsprincip som tillämpas på ett segment.

Om du vill visa information om ett visst dataflöde väljer du körningens starttid i listan. Informationssidan för ett dataflöde innehåller ytterligare information, t.ex. storleken på de data som bearbetas och en lista över eventuella fel som inträffat med information om feldiagnostik.

![](../assets/ui/monitor-destinations/dataflow.png)