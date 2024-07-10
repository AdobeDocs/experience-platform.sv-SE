---
solution: Experience Platform
title: Användargränssnittshandbok för segmenteringstjänst
description: Lär dig hur du skapar och hanterar målgrupper och segmentdefinitioner i Adobe Experience Platform användargränssnitt.
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
source-git-commit: acfe91144175e136955ffd9f0cdae2c351217c16
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---

# Användargränssnittsguide för segmenteringstjänst

[!DNL Adobe Experience Platform Segmentation Service] innehåller ett användargränssnitt för att skapa och hantera målgrupper och segmentdefinitioner.

## Komma igång

Att arbeta med målgrupper och segmentdefinitioner kräver en förståelse för de olika [!DNL Experience Platform] tjänster som rör segmentering. Innan du läser den här användarhandboken bör du läsa dokumentationen för följande tjänster:

- [[!DNL Segmentation Service]](../home.md): [!DNL Segmentation Service] gör att du kan segmentera data som lagras i [!DNL Experience Platform] som rör individer (t.ex. kunder, prospects, användare eller organisationer) i mindre grupper.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Gör det möjligt att skapa kundprofiler genom att överbrygga identiteter från olika datakällor som hämtas in till [!DNL Platform].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverk som [!DNL Platform] organiserar kundupplevelsedata. För att utnyttja segmenteringen på bästa sätt bör du se till att dina data är inmatade som profiler och händelser enligt [bästa praxis för datamodellering](../../xdm/schema/best-practices.md).

Du bör också förstå följande nyckeltermer som används i det här dokumentet och förstå skillnaden mellan dem:

- **Målgrupp**: En samling personer som delar liknande beteenden och/eller egenskaper. Den här mängden personer kan antingen genereras av Adobe Experience Platform med hjälp av segmentdefinitioner (plattformsgenererad publik), målgruppssammansättning eller externa källor som anpassade uppladdningar (externt genererade målgrupper).
- **Segmentdefinition**: De regler som Adobe Experience Platform använder för att beskriva viktiga egenskaper eller beteenden hos en målgrupp.
- **Segment**: Att separera profiler i målgrupper.

## Översikt

I användargränssnittet för Experience Platform väljer du **[!UICONTROL Audiences]** i den vänstra navigeringen för att öppna **[!UICONTROL Overview]** flik som visar [!UICONTROL Audiences] kontrollpanel.

>[!NOTE]
>
>Om din organisation inte har använt Platform tidigare och ännu inte har några aktiva profildatauppsättningar eller sammanfogningsprinciper har skapats kan [!UICONTROL Audiences] Kontrollpanelen visas inte. I stället [!UICONTROL Overview] -fliken visar länkar och dokumentation som hjälper dig att komma igång med målgrupper.

### [!UICONTROL Audiences] kontrollpanel {#segments-dashboard}

The **[!UICONTROL Audiences]** Instrumentpanelen sammanfattar nyckeltal relaterade till organisationens målgruppsdata.

Mer information finns på [guide för målgrupper](../../dashboards/guides/audiences.md).

![Målgruppspanelen visas. Den visar olika widgetar, inklusive målgruppsstorlek, profiler efter identitet, identitetsöverlappning och trenden för storleksändring för målgrupper.](../../dashboards/images/segments/dashboard-overview.png)

## Bläddra {#browse}

Välj **[!UICONTROL Browse]** för att se Audience Portal. Audience Portal innehåller en lista med alla målgrupper som tillhör din organisation och sandlåda, och innehåller information som antal profiler, ursprung, skapad den, senaste ändringsdatum, taggar och uppdelning.

Dessutom kan ni med Audience Portal skapa nya målgrupper med hjälp av Segment Builder eller Audience Composition, samt importera externt genererade målgrupper till Platform.

Mer information om Audience Portal finns i [Översikt över målgruppsportalen](./audience-portal.md).

## Kompositioner {#compositions}

Välj **[!UICONTROL Compositions]** om du vill visa en lista över alla målgrupper som genererats via Audience Composition för din organisation.

![En lista över målgrupper som skapats i Audience Composition för din organisation.](../images/ui/overview/compositions.png)

Som standard visar den här vyn information om målgrupperna inklusive namn, status, skapad den, skapad av, senaste uppdateringsdatum och senast uppdaterad av.

Bredvid varje publik finns en ellips-ikon. Om du väljer det här alternativet visas en lista med tillgängliga snabbåtgärder för målgruppen.

| Åtgärd | Beskrivning |
| ------ | ----------- |
| Duplicera | Kopierar den valda målgruppen. |
| Hantera åtkomst | Hanterar de åtkomstetiketter som tillhör målgruppen. Mer information om åtkomstetiketter finns i dokumentationen om [hantera etiketter](../../access-control/abac/ui/labels.md). |
| Ta bort | Tar bort den valda målgruppen. Målgrupper som används i senare led eller som är beroende i andra målgrupper **inte** tas bort. Mer information om borttagning av målgrupper finns i [segmentering - frågor och svar](../faq.md#lifecycle-states). |

Du kan välja ![Anpassa tabell](../images/ui/overview/customize-table.png) om du vill ändra vilka fält som visas.

![Knappen Anpassa tabell är markerad. Om du väljer den här knappen kan du anpassa fälten som visas på sidan för publikkompositioner.](../images/ui/overview/compositions-select-customize-table.png)

En pover visas med en lista över alla fält som kan visas i tabellen.

![De attribut som kan visas för dispositionssektionen.](../images/ui/overview/compositions-customize-table.png)

| Fält | Beskrivning |
| ----- | ----------- | 
| [!UICONTROL Name] | Namnet på publiken. |
| [!UICONTROL Status] | Publiken. Möjliga värden för det här fältet är `Draft`, `Inactive`och `Published`. |
| [!UICONTROL Created] | Tid och datum då målgruppen skapades. |
| [!UICONTROL Created by] | Namnet på den person som skapade målgruppen. |
| [!UICONTROL Updated] | Tid och datum då målgruppen senast uppdaterades. |
| [!UICONTROL Updated by] | Namnet på den person som senast uppdaterade målgruppen. |

Om du vill se hur målgruppen är uppbyggd väljer du en målgrupps namn i [!UICONTROL Audiences] -fliken.

Sidan Audience Composition visas med de byggstenar som utgör målgruppen. Mer information om hur du använder Audience Composition finns i [Användargränssnittsguide för målgruppskomposition](./audience-composition.md).

## Direktuppspelningssegmentering {#streaming-segmentation}

Direktuppspelningssegmentering är möjligheten att segmentera på [!DNL Platform] i nära realtid, samtidigt som datamöjligheter fokuseras. Med direktuppspelningssegmentering blir det numera möjligt att kvalificera sig för segmentering allt eftersom data når [!DNL Platform], vilket minskar behovet av att schemalägga och köra segmenteringsjobb.

Mer information om direktuppspelningssegmentering finns i [användarhandbok för direktuppspelningssegmentering](./streaming-segmentation.md).

>[!NOTE]
>
>För att direktuppspelningssegmenteringen ska fungera måste du aktivera schemalagd segmentering för organisationen. Mer information om att aktivera schemalagd segmentering finns i [avsnittet om direktuppspelningssegmentering i den här användarhandboken](#scheduled-segmentation).

## Edge segmentering {#edge-segmentation}

Edge segmentering är möjligheten att omedelbart utvärdera målgrupper i Platform, vilket möjliggör användning av samma sida och nästa sida vid personalisering.

Mer information om kantsegmentering finns i [gränssnittsguide för kantsegmentering](./edge-segmentation.md)

## Policyöverträdelser

>[!NOTE]
>
>Policyöverträdelser gäller bara om du skapar en målgrupp som har tilldelats ett mål.

När ni är klara med att skapa er målgrupp kommer målgruppen att analyseras av Adobe Experience Platform Data Governance för att säkerställa att det inte förekommer några brott mot policyn inom målgruppen. Se [Datastyrning - översikt](../../data-governance/home.md) för mer information.

![Policyöverträdelser för publiken visas.](../images/ui/overview/audience-dule-policy-violations.png)

## Nästa steg och ytterligare resurser {#next-steps}

The [!DNL Segmentation Service] Gränssnittet innehåller ett omfattande arbetsflöde som gör att du kan skapa marknadsföringsbara målgrupper från [!DNL Real-Time Customer Profile] data.

Mer information om [!DNL Segmentation Service], fortsätt att läsa dokumentationen. Så här använder du [!DNL Segmentation Service] API, läs [[!DNL Segmentation Service] utvecklarhandbok](../api/overview.md).
