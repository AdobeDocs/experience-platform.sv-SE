---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Aktivera inkommande källdata för att fylla i kundprofiler
topic: overview
translation-type: tm+mt
source-git-commit: d6d2faf3d5eabcd8e948d3717fd8f8df4b9cb85a

---


# Aktivera inkommande källdata för att fylla i kundprofiler

Inkommande data från källkopplingen kan användas för att berika och fylla i kundprofildata i realtid.

## Komma igång

Den här självstudien kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Experience Data Model (XDM) System](../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att organisera kundupplevelsedata.
   - [Grundläggande om schemakomposition](../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [Kundprofil](../../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Den här självstudien kräver dessutom att du redan har skapat och konfigurerat en källkoppling.  En lista med självstudiekurser för att skapa olika kopplingar i användargränssnittet finns i [källanslutningsöversikten](../../home.md).

## Fylla i kundprofildata i realtid

För att berika kundprofilerna måste måldatauppsättningens källschema vara kompatibelt för användning i kundprofilen i realtid. Ett kompatibelt schema uppfyller följande krav:

- Schemat har minst ett attribut angivet som en identitetsegenskap.
- Schemat har en identitetsegenskap definierad som primär identitet.
- Det finns en mappning i dataflödet där den primära identiteten är ett målattribut.

Klicka på fliken **Bläddra** på arbetsytan Källor för att visa dina basanslutningar. I listan som visas söker du efter anslutningen som innehåller det dataflöde som du vill fylla i profiler med. Klicka på anslutningens namn för att komma åt information om anslutningen.

![](../../images/tutorials/dataflow/cloud-storage/browse.png)

Anslutningens aktivitetsskärm för *Källa* visas med de datauppsättningar som anslutningen hämtar källdata till. Klicka på namnet på datauppsättningen som du vill aktivera för profil.

![](../../images/tutorials/dataflow/cloud-storage/dataset-dataflow.png)

Aktivitetsskärmen *för* datauppsättning visas. Kolumnen *Egenskaper* till höger på skärmen visar information om datauppsättningen och innehåller en **profilväxel** och en länk till det schema som datauppsättningen följer. Klicka på schemats namn för att visa dess komposition.

![](../../images/tutorials/dataflow/cloud-storage/select-dataset-schema.png)

Schemaredigeraren ** visas och visar schemats struktur på arbetsytan i mitten. Markera det fält som ska anges som primär identitet på arbetsytan. Under fliken *Fältegenskaper* som visas markerar du kryssrutan **Identitet** och sedan **Primär identitet**. Välj sedan ett lämpligt **identitetsnamnutrymme** och klicka på **Använd**.

![](../../images/tutorials/dataflow/cloud-storage/set-schema-identity.png)

Klicka på det översta nivåobjektet för schemats struktur och kolumnen *Schemaegenskaper* visas. Aktivera schemat för profilen genom att växla **profilväxeln** . Klicka på **Spara** för att slutföra ändringarna.

![](../../images/tutorials/dataflow/cloud-storage/enable-profile.png)

Nu när schemat är aktiverat för profilen går du tillbaka till aktivitetsskärmen för *datauppsättningen* och aktiverar datauppsättningen för profilen genom att klicka på **profilväxlingen** i kolumnen *Egenskaper* .

![](../../images/tutorials/dataflow/cloud-storage/enable-dataset-profile.png)

När både schemat och datauppsättningen är aktiverade för profilen fylls data som hämtas in i den datauppsättningen nu även i kundprofiler.

>[!NOTE] Befintliga data i en nyligen aktiverad datauppsättning används inte av profilen

## Nästa steg

Genom att följa den här självstudiekursen har du aktiverat inkommande data för profilpopulationen. Mer information finns i [Kundprofilöversikt](../../../profile/home.md)i realtid.