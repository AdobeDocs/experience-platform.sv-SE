---
keywords: Experience Platform;hem;populära ämnen;aktivera inkommande data;fyll i profil;fyll i rtcp;ifylld enhetlig profil
solution: Experience Platform
title: Aktivera inkommande källdata för att fylla i kundprofiler i användargränssnittet
type: Tutorial
description: Inkommande data från källkopplingen kan användas för att berika och fylla i kundprofildata i realtid.
exl-id: ddd3766a-3f55-4bbc-8358-c578eae2c629
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---

# Aktivera inkommande källdata för att fylla i kundprofiler

Inkommande data från din källanslutning kan användas för att berika och fylla i dina [!DNL Real-Time Customer Profile] data.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] System](../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
   - [Grunderna för schemakomposition](../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Den här självstudien kräver dessutom att du redan har skapat och konfigurerat en källkoppling.  En lista med självstudiekurser för att skapa olika kopplingar i användargränssnittet finns i [översikt över källanslutningar](../../home.md).

## Fyll i [!DNL Real-Time Customer Profile] data

För att utöka kundprofiler måste måldatasetens källschema vara kompatibelt för användning i [!DNL Real-Time Customer Profile]. Ett kompatibelt schema uppfyller följande krav:

- Schemat har minst ett attribut angivet som en identitetsegenskap.
- Schemat har en identitetsegenskap definierad som primär identitet.
- Det finns en mappning i dataflödet där den primära identiteten är ett målattribut.

Klicka på **[!UICONTROL Browse]** för att visa dina basanslutningar. I listan som visas söker du efter anslutningen som innehåller det dataflöde som du vill fylla i profiler med. Klicka på anslutningens namn för att komma åt information om anslutningen.

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

Anslutningens **[!UICONTROL Source activity]** visas och visar de datauppsättningar som anslutningen hämtar källdata till. Klicka på namnet på datauppsättningen som du vill aktivera för [!DNL Profile].

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

The **[!UICONTROL Dataset activity]** visas. The **[!UICONTROL Properties]** -kolumnen till höger på skärmen visar informationen om datauppsättningen och innehåller en **[!UICONTROL Profile]** växla och en länk till det schema som datauppsättningen följer. Klicka på schemats namn för att visa dess komposition.

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

The **[!UICONTROL Schema Editor]** visas med schemats struktur på arbetsytan i mitten. Markera det fält som ska anges som primär identitet på arbetsytan. Under **[!UICONTROL Field properties]** som visas väljer du **[!UICONTROL Identity]** kryssruta, sedan **[!UICONTROL Primary identity]**. Välj en lämplig **[!UICONTROL Identity namespace]** och sedan klicka **[!UICONTROL Apply]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

Klicka på det översta nivåobjektet för schemats struktur och **[!UICONTROL Schema properties]** visas. Aktivera schemat för [!DNL Profile] genom att växla **[!UICONTROL Profile]** byt. Klicka **[!UICONTROL Save]** för att slutföra ändringarna.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

Nu när schemat är aktiverat för [!DNL Profile], gå tillbaka till **[!UICONTROL Dataset activity]** skärm och aktivera datauppsättningen för [!DNL Profile] genom att klicka på **[!UICONTROL Profile]** växla i **[!UICONTROL Properties]** kolumn.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

Med både schema och datamängd aktiverat för [!DNL Profile]kommer data som hämtas in till den datauppsättningen nu också att fylla i kundprofiler.

>[!NOTE]
>
>Befintliga data i en nyligen aktiverad datauppsättning används inte av [!DNL Profile].

## Nästa steg

Genom att följa den här självstudiekursen har du aktiverat inkommande data för [!DNL Profile] populationen. Mer information finns i [[!DNL Real-Time Customer Profile] översikt](../../../profile/home.md).
