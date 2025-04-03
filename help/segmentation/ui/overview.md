---
solution: Experience Platform
title: Användargränssnittshandbok för segmenteringstjänst
description: Lär dig hur du skapar och hanterar målgrupper och segmentdefinitioner i Adobe Experience Platform användargränssnitt.
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
source-git-commit: f6d700087241fb3a467934ae8e64d04f5c1d98fa
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 0%

---

# Användargränssnittsguide för segmenteringstjänst

[!DNL Adobe Experience Platform Segmentation Service] innehåller ett användargränssnitt för att skapa och hantera målgrupper och segmentdefinitioner.

## Komma igång

Att arbeta med målgrupper och segmentdefinitioner kräver en förståelse för de olika [!DNL Experience Platform]-tjänster som är involverade i segmenteringen. Innan du läser den här användarhandboken bör du läsa dokumentationen för följande tjänster:

- [[!DNL Segmentation Service]](../home.md): [!DNL Segmentation Service] gör att du kan segmentera data som lagras i [!DNL Experience Platform] och som relaterar till enskilda personer (till exempel kunder, potentiella kunder, användare eller organisationer) i mindre grupper.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Gör det möjligt att skapa kundprofiler genom att brygga identiteter från olika datakällor som importeras till [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata med. För att du ska kunna använda segmentering bör du se till att dina data är inmatade som profiler och händelser enligt [bästa praxis för datamodellering](../../xdm/schema/best-practices.md).

Du bör också förstå följande nyckeltermer som används i det här dokumentet och förstå skillnaden mellan dem:

- **Målgrupp**: En samling personer som delar liknande beteenden och/eller egenskaper. Den här mängden personer kan antingen genereras av Adobe Experience Platform med segmentdefinitioner (en upplevelseplattformsgenererad publik), målgruppskomposition eller från externa källor som anpassade uppladdningar (externt genererad publik).
- **Segmentdefinition**: De regler som Adobe Experience Platform använder för att beskriva nyckelegenskaper eller beteenden hos en målpublik.
- **Segment**: Åtgärden att dela upp profiler i målgrupper.

## Översikt

I Experience Platform-gränssnittet väljer du **[!UICONTROL Audiences]** i den vänstra navigeringen för att öppna fliken **[!UICONTROL Overview]** med kontrollpanelen [!UICONTROL Audiences].

>[!NOTE]
>
>Om din organisation inte har använt Experience Platform tidigare och ännu inte har några aktiva profildatauppsättningar eller sammanslagningsprinciper skapade, visas inte instrumentpanelen [!UICONTROL Audiences]. Istället visar fliken [!UICONTROL Overview] länkar och dokumentation som hjälper dig att komma igång med målgrupper.

### Kontrollpanel för [!UICONTROL Audiences] {#segments-dashboard}

Instrumentpanelen **[!UICONTROL Audiences]** visar viktiga mått som rör organisationens målgruppsdata.

Mer information finns i handboken [Publikpaneler](../../dashboards/guides/audiences.md).

![Publiken visas. Den visar olika widgetar, inklusive målgruppsstorlek, profiler efter identitet, identitetsöverlappning och trenden för storleksändring för målgrupper.](../../dashboards/images/segments/dashboard-overview.png)

## Bläddra {#browse}

Välj fliken **[!UICONTROL Browse]** för att visa målportalen. Audience Portal innehåller en lista med alla målgrupper som tillhör din organisation och sandlåda, och innehåller information som antal profiler, ursprung, skapad den, senaste ändringsdatum, taggar och uppdelning.

Dessutom kan ni med Audience Portal skapa nya målgrupper med hjälp av Segment Builder eller Audience Composition, samt importera externt genererade målgrupper till Experience Platform.

Mer information om Audience Portal finns i [Översikt över Audience Portal](./audience-portal.md).

## Kompositioner {#compositions}

Välj fliken **[!UICONTROL Compositions]** om du vill visa en lista över alla målgrupper som genererats via Audience Composition för din organisation.

![En lista över målgrupper som har skapats i Audience Composition för din organisation.](../images/ui/overview/compositions.png)

Som standard visar den här vyn information om målgrupperna inklusive namn, status, skapad den, skapad av, senaste uppdateringsdatum och senast uppdaterad av.

Bredvid varje publik finns en ellips-ikon. Om du väljer det här alternativet visas en lista med tillgängliga snabbåtgärder för målgruppen.

| Åtgärd | Beskrivning |
| ------ | ----------- |
| Duplicera | Kopierar den valda målgruppen. |
| Hantera åtkomst | Hanterar de åtkomstetiketter som tillhör målgruppen. Mer information om åtkomstetiketter finns i dokumentationen om [hantering av etiketter](../../access-control/abac/ui/labels.md). |
| Ta bort | Tar bort den valda målgruppen. Publiker som används i underordnade mål eller är beroende av andra målgrupper **kan inte** tas bort. Mer information om borttagning av målgrupper finns i [Frågor och svar om segmentering](../faq.md#lifecycle-states). |

Du kan välja ikonen ![Anpassa tabell](/help/images/icons/column-settings.png) om du vill ändra vilka fält som visas.

![Knappen för att anpassa tabell är markerad. Om du väljer den här knappen kan du anpassa fälten som visas på sidan för publikkompositioner.](../images/ui/overview/compositions-select-customize-table.png)

En pover visas med en lista över alla fält som kan visas i tabellen.

![De attribut som kan visas för dispositionssektionen.](../images/ui/overview/compositions-customize-table.png)

| Fält | Beskrivning |
| ----- | ----------- | 
| [!UICONTROL Name] | Namnet på publiken. |
| [!UICONTROL Status] | Publiken. Möjliga värden för fältet är `Draft`, `Inactive` och `Published`. |
| [!UICONTROL Created] | Tid och datum då målgruppen skapades. |
| [!UICONTROL Created by] | Namnet på den person som skapade målgruppen. |
| [!UICONTROL Updated] | Tid och datum då målgruppen senast uppdaterades. |
| [!UICONTROL Updated by] | Namnet på den person som senast uppdaterade målgruppen. |

Om du vill se hur målgruppen är sammansatt väljer du en målgrupps namn på fliken [!UICONTROL Audiences].

Sidan Audience Composition visas med de byggstenar som utgör målgruppen. Mer information om hur du använder Audience Composition finns i handboken [Audience Composition UI](./audience-composition.md).

## Federerad målgruppssammansättning {#fac}

Förutom målgruppskompositioner och segmentdefinitioner kan du använda Adobe Federated Audience Composition för att skapa nya målgrupper från företagsdatauppsättningar utan att kopiera underliggande data och lagra dessa målgrupper i Adobe Experience Platform Audience Portal. Ni kan också berika befintliga målgrupper i Adobe Experience Platform genom att använda sammansatta målgruppsdata som har federerats från företagets datalager. Läs guiden om [Federated Audience Composition](https://experienceleague.adobe.com/sv/docs/federated-audience-composition/using/home).

![En lista över målgrupper som skapats i Federated Audience Composition för din organisation.](../images/ui/overview/federated-audience-composition.png)

## Direktuppspelningssegmentering {#streaming-segmentation}

Direktuppspelningssegmentering är möjligheten att segmentera på [!DNL Experience Platform] i nära realtid, samtidigt som dataverifikation fokuseras. Med direktuppspelningssegmentering blir kvalificering för segmentering nu allt eftersom data landar i [!DNL Experience Platform], vilket minskar behovet av att schemalägga och köra segmenteringsjobb.

Mer information om direktuppspelningssegmentering finns i användarhandboken för [direktuppspelningssegmentering](../methods/streaming-segmentation.md).

>[!NOTE]
>
>För att direktuppspelningssegmenteringen ska fungera måste du aktivera schemalagd segmentering för organisationen. Mer information om att aktivera schemalagd segmentering finns i [avsnittet om direktuppspelningssegmentering i den här användarhandboken](#scheduled-segmentation).

## Edge segmentering {#edge-segmentation}

Edge segmentering är möjligheten att omedelbart utvärdera målgrupper i Experience Platform, vilket möjliggör användning av samma sida och nästa sida vid personalisering.

Mer information om kantsegmentering finns i [gränssnittsguiden för kantsegmentering](../methods/edge-segmentation.md)

## Policyöverträdelser

>[!NOTE]
>
>Policyöverträdelser gäller bara om du skapar en målgrupp som har tilldelats ett mål.

När ni är klara med att skapa er målgrupp kommer målgruppen att analyseras av Adobe Experience Platform Data Governance för att säkerställa att det inte förekommer några brott mot policyn inom målgruppen. Mer information finns i [Översikt över datastyrning](../../data-governance/home.md).

![Policyöverträdelser för målgruppen visas.](../images/ui/overview/audience-dule-policy-violations.png)

## Nästa steg och ytterligare resurser {#next-steps}

Användargränssnittet [!DNL Segmentation Service] innehåller ett omfattande arbetsflöde som gör att du kan skapa marknadsföringsbara målgrupper utifrån [!DNL Real-Time Customer Profile]-data.

Om du vill veta mer om [!DNL Segmentation Service] kan du fortsätta läsa dokumentationen. Läs [[!DNL Segmentation Service] utvecklarhandboken](../api/overview.md) om du vill lära dig hur du använder [!DNL Segmentation Service]-API:t.
