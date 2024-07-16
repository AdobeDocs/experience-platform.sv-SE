---
keywords: Experience Platform;hem;populära ämnen;aktivera inkommande data;fyll i profil;fyll i rtcp;ifylld enhetlig profil
solution: Experience Platform
title: Aktivera inkommande Source-data för att fylla i kundprofiler i användargränssnittet
type: Tutorial
description: Inkommande data från källkopplingen kan användas för att berika och fylla i kundprofildata i realtid.
exl-id: ddd3766a-3f55-4bbc-8358-c578eae2c629
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---

# Aktivera inkommande källdata för att fylla i kundprofiler

Inkommande data från din källanslutning kan användas för att berika och fylla i dina [!DNL Real-Time Customer Profile]-data.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] System](../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata med.
   - [Grundläggande om schemakomposition](../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   - [Schemaredigeraren, självstudiekurs](../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Den här självstudien kräver dessutom att du redan har skapat och konfigurerat en källkoppling.  En lista med självstudiekurser för att skapa olika anslutningar i användargränssnittet finns i [översikten över källanslutningar](../../home.md).

## Fyll i dina [!DNL Real-Time Customer Profile]-data

Om du vill utöka kundprofiler måste måldatamängdens källschema vara kompatibelt för användning i [!DNL Real-Time Customer Profile]. Ett kompatibelt schema uppfyller följande krav:

- Schemat har minst ett attribut angivet som en identitetsegenskap.
- Schemat har en identitetsegenskap definierad som primär identitet.
- Det finns en mappning i dataflödet där den primära identiteten är ett målattribut.

Klicka på fliken **[!UICONTROL Browse]** på arbetsytan Källor för att visa dina basanslutningar. I listan som visas söker du efter anslutningen som innehåller det dataflöde som du vill fylla i profiler med. Klicka på anslutningens namn för att komma åt information om anslutningen.

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

Anslutningens **[!UICONTROL Source activity]**-skärm visas och visar datauppsättningarna som anslutningen hämtar källdata till. Klicka på namnet på datauppsättningen som du vill aktivera för [!DNL Profile].

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

Skärmen **[!UICONTROL Dataset activity]** visas. Kolumnen **[!UICONTROL Properties]** till höger på skärmen visar information om datauppsättningen och innehåller en **[!UICONTROL Profile]**-växel och en länk till det schema som datauppsättningen följer. Klicka på schemats namn för att visa dess komposition.

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

**[!UICONTROL Schema Editor]** visas och visar schemats struktur på arbetsytan i mitten. Markera det fält som ska anges som primär identitet på arbetsytan. Under fliken **[!UICONTROL Field properties]** som visas markerar du kryssrutan **[!UICONTROL Identity]** och sedan **[!UICONTROL Primary identity]**. Välj sedan en lämplig **[!UICONTROL Identity namespace]** och klicka sedan på **[!UICONTROL Apply]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

Klicka på det översta nivåobjektet i schemats struktur så visas kolumnen **[!UICONTROL Schema properties]**. Aktivera schemat för [!DNL Profile] genom att växla **[!UICONTROL Profile]**. Klicka på **[!UICONTROL Save]** för att slutföra ändringarna.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

Nu när schemat är aktiverat för [!DNL Profile] går du tillbaka till skärmen **[!UICONTROL Dataset activity]** och aktiverar datauppsättningen för [!DNL Profile] genom att klicka på växlingsknappen **[!UICONTROL Profile]** i kolumnen **[!UICONTROL Properties]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

När både schemat och datauppsättningen är aktiverad för [!DNL Profile] fylls även kundprofiler i när data som hämtas in i den datauppsättningen.

>[!NOTE]
>
>Befintliga data i en nyligen aktiverad datauppsättning används inte av [!DNL Profile].

## Nästa steg

Genom att följa den här självstudiekursen har du aktiverat inkommande data för [!DNL Profile]-populationen. Mer information finns i [[!DNL Real-Time Customer Profile] översikten](../../../profile/home.md).
