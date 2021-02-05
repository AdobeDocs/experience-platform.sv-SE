---
keywords: Experience Platform;hem;populära ämnen;aktivera inkommande data;fyll i profil;fyll i rtcp;ifylld enhetlig profil
solution: Experience Platform
title: Aktivera inkommande källdata för att fylla i kundprofiler i användargränssnittet
topic: overview
type: Tutorial
description: Inkommande data från källkopplingen kan användas för att berika och fylla i kundprofildata i realtid.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---


# Aktivera inkommande källdata för att fylla i kundprofiler

Inkommande data från din källanslutning kan användas för att berika och fylla i dina [!DNL Real-time Customer Profile]-data.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] System](../../../xdm/home.md): Det standardiserade ramverket som  [!DNL Experience Platform] organiserar kundupplevelsedata.
   - [Grundläggande om schemakomposition](../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Den här självstudien kräver dessutom att du redan har skapat och konfigurerat en källkoppling.  En lista med självstudiekurser för att skapa olika kopplingar i användargränssnittet finns i [översikten över källanslutningar](../../home.md).

## Fyll i dina [!DNL Real-time Customer Profile]-data

Om du vill utöka kundprofiler måste måldatauppsättningens källschema vara kompatibelt för användning i [!DNL Real-time Customer Profile]. Ett kompatibelt schema uppfyller följande krav:

- Schemat har minst ett attribut angivet som en identitetsegenskap.
- Schemat har en identitetsegenskap definierad som primär identitet.
- Det finns en mappning i dataflödet där den primära identiteten är ett målattribut.

Klicka på fliken **[!UICONTROL Browse]** på arbetsytan Källor för att visa dina basanslutningar. I listan som visas söker du efter anslutningen som innehåller det dataflöde som du vill fylla i profiler med. Klicka på anslutningens namn för att komma åt information om anslutningen.

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

Anslutningens **[!UICONTROL Source activity]**-skärm visas och visar de datauppsättningar som anslutningen hämtar källdata till. Klicka på namnet på datauppsättningen som du vill aktivera för [!DNL Profile].

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

Skärmen **[!UICONTROL Dataset activity]** visas. Kolumnen **[!UICONTROL Properties]** till höger på skärmen visar informationen om datauppsättningen och innehåller en **[!UICONTROL Profile]**-växel och en länk till det schema som datauppsättningen följer. Klicka på schemats namn för att visa dess komposition.

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

**[!UICONTROL Schema Editor]** visas och visar strukturen för schemat på arbetsytan i mitten. Markera det fält som ska anges som primär identitet på arbetsytan. Under fliken **[!UICONTROL Field properties]** som visas markerar du kryssrutan **[!UICONTROL Identity]** och sedan **[!UICONTROL Primary identity]**. Välj sedan en lämplig **[!UICONTROL Identity namespace]** och klicka sedan på **[!UICONTROL Apply]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

Klicka på det översta nivåobjektet i schemats struktur så visas kolumnen **[!UICONTROL Schema properties]**. Aktivera schemat för [!DNL Profile] genom att växla **[!UICONTROL Profile]**-växeln. Klicka på **[!UICONTROL Save]** för att slutföra ändringarna.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

Nu när schemat är aktiverat för [!DNL Profile] går du tillbaka till skärmen **[!UICONTROL Dataset activity]** och aktiverar datauppsättningen för [!DNL Profile] genom att klicka på växlingsknappen **[!UICONTROL Profile]** i kolumnen **[!UICONTROL Properties]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

När både schemat och datauppsättningen är aktiverad för [!DNL Profile] fylls även kundprofiler i data som hämtas in i den datauppsättningen.

>[!NOTE]
>
>Befintliga data i en nyligen aktiverad datauppsättning används inte av [!DNL Profile].

## Nästa steg

Genom att följa den här självstudiekursen har du aktiverat inkommande data för [!DNL Profile]-populationen. Mer information finns i [[!DNL Real-time Customer Profile] översikten](../../../profile/home.md).