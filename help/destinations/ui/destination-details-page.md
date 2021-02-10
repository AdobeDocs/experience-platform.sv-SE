---
keywords: mål;mål;destinationsdetaljsida;målinformationssida
title: Visa målinformation
description: 'På informationssidan för ett enskilt mål finns en översikt över målinformationen, t.ex. målnamn, ID, segment som är mappade till målet samt kontroller för att redigera aktiveringen samt för att aktivera och inaktivera dataflödet. '
seo-description: 'På informationssidan för ett enskilt mål finns en översikt över målinformationen, t.ex. målnamn, ID, segment som är mappade till målet samt kontroller för att redigera aktiveringen samt för att aktivera och inaktivera dataflödet. '
translation-type: tm+mt
source-git-commit: e13a19640208697665b0a7e0106def33fd1e456d
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---


# Visa målinformation

I Adobe Experience Platform användargränssnitt kan du visa och övervaka attributen och aktiviteterna för dina mål. Dessa uppgifter omfattar målets namn och ID, kontroller för att aktivera eller inaktivera destinationer och mycket annat. Detaljer för batchdestinationer omfattar även mått för aktiverade profilposter och en historik över dataflöden.

>[!NOTE]
>
>Målinformationssidan är en del av arbetsytan [!UICONTROL Destinations] i plattformsgränssnittet. Mer information finns i översikten [[!UICONTROL Destinations] för arbetsytan](./destinations-workspace.md).

Gå till fliken **[!UICONTROL Browse]** i arbetsytan **[!UICONTROL Destinations]** i plattformsgränssnittet och välj namnet på ett mål som du vill visa.

![](../assets/ui/details-page/select-destination.png)

Målets informationssida visas med de tillgängliga kontrollerna. Om du visar information om ett batchmål visas även en kontrollpanel.

![](../assets/ui/details-page/details.png)

På fliken Bläddra kan du dessutom välja att ta bort det markerade dataflödet genom att markera ikonen ![papperskorgen](../assets/ui/details-page/trash-icon.png). Alla segment som aktiveras för ett mål mappas om innan dataflödet tas bort.

![](../assets/ui/details-page/delete-flow.png)

## Höger räl

Den högra listen visar grundläggande information om målet.

![](../assets/ui/details-page/right-rail.png)

Följande tabell omfattar de kontroller och den information som tillhandahålls av den högra spåret:

| Högerrälsartikel | Beskrivning |
| --- | --- |
| [!UICONTROL Activate] | Välj den här kontrollen om du vill redigera vilka segment som mappas till målet. Mer information finns i guiden [aktivera segment till ett mål](./activate-destinations.md). |
| [!UICONTROL Delete] | Gör att du kan ta bort det här dataflödet och ta bort mappningar för segment som tidigare har aktiverats, om det finns några. |
| [!UICONTROL Destination name] | Det här fältet kan redigeras för att uppdatera målets namn. |
| [!UICONTROL Description] | Det här fältet kan redigeras för att uppdatera eller lägga till en valfri beskrivning till målet. |
| [!UICONTROL Destination] | Representerar målplattformen som målgrupperna skickas till. Mer information finns i [målkatalogen](../catalog/overview.md). |
| [!UICONTROL Status] | Anger om målet är aktiverat eller inaktiverat. |
| [!UICONTROL Marketing actions] | Anger de marknadsföringsåtgärder (användningsfall) som gäller för den här destinationen i datastyrningssyfte. |
| [!UICONTROL Category] | Anger måltypen. Mer information finns i [målkatalogen](../catalog/overview.md). |
| [!UICONTROL Connection type] | Anger det formulär som era målgrupper skickas till. Möjliga värden är [!UICONTROL Cookie] och [!UICONTROL Profile-based]. |
| [!UICONTROL Frequency] | Anger hur ofta målgrupperna skickas till målet. Möjliga värden är [!UICONTROL Streaming] och [!UICONTROL Batch]. |
| [!UICONTROL Identity] | Representerar det identitetsnamnutrymme som accepteras av målet, till exempel `GAID`, `IDFA` eller `email`. Mer information om godkända ID-namnutrymmen finns i [översikten över identitetsnamnrymden](../../identity-service/namespaces.md). |
| [!UICONTROL Created by] | Anger den användare som skapade det här målet. |
| [!UICONTROL Created] | Anger UTC-datum/tid när det här målet skapades. |

## [!UICONTROL Enabled]/[!UICONTROL Disabled] toggle

Du kan använda alternativet **[!UICONTROL Enabled]/[!UICONTROL Disabled]** för att starta och pausa all dataexport till målet.

![](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL Dataflow runs]

Fliken [!UICONTROL Dataflow runs] innehåller mätdata för dataflödet som körs till batchdestinationer. En lista över enskilda körningar och deras specifika mått visas tillsammans med följande summor för profilposter:

* **[!UICONTROL Profile records activated]**: Det totala antalet profilposter som har skapats eller uppdaterats för aktivering.
* **[!UICONTROL Profile records skipped]**: Det totala antalet profilposter som hoppas över för aktivering baserat på utträde eller saknade attribut.

![](../assets/ui/details-page/dataflow-runs.png)

>[!NOTE]
>
>Dataflödeskörningar genereras baserat på måldataflödets schemafrekvens. En separat dataflödeskörning görs för varje sammanfogningsprincip som tillämpas på ett segment.

Om du vill visa information om ett visst dataflöde väljer du körningens starttid i listan. Informationssidan för ett dataflöde innehåller ytterligare information, t.ex. storleken på de data som bearbetas och en lista över eventuella fel som inträffat med information om feldiagnostik.

![](../assets/ui/details-page/dataflow.png)

## [!UICONTROL Activation data]

På fliken [!UICONTROL Activation data] visas en lista med segment som har mappats till målet, inklusive startdatum och slutdatum (om tillämpligt). Om du vill visa information om ett visst segment väljer du dess namn i listan.

![](../assets/ui/details-page/activation-data.png)

>[!NOTE]
>
>Mer information om hur du utforskar informationssidan för ett segment finns i [Översikt över segmenteringsgränssnittet](../../segmentation/ui/overview.md#segment-details).

## Nästa steg

Det här dokumentet innehåller funktioner för sidan med målinformation. Mer information om hur du hanterar mål i användargränssnittet finns i översikten på arbetsytan [[!UICONTROL Destinations]](./destinations-workspace.md).