---
keywords: Experience Platform;hemmabruk;populära ämnen; varningar
description: Du kan prenumerera på aviseringar när du skapar ett dataflöde för att få varningsmeddelanden om status, lyckade eller misslyckade flödeskörningar.
title: Prenumerera på varningar i sitt sammanhang i användargränssnittet
exl-id: 5d51edaa-ecba-4ac0-8d3c-49010466b9a5
source-git-commit: 3f7f66c0d58d127299ad12027869ca0e9837f5cd
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 0%

---

# Prenumerera på aviseringar om källdataflöden i användargränssnittet

>[!NOTE]
>
>Varningar stöds inte i icke-produktionssandlådor. För att kunna prenumerera på varningar måste du se till att du använder en produktionssandlåda.

Med Adobe Experience Platform kan du prenumerera på händelsebaserade aviseringar om Adobe Experience Platform-aktiviteter. Varningar minskar eller eliminerar behovet av att ringa [[!DNL Observability Insights] API](../../../observability/api/overview.md) för att kontrollera om ett jobb har slutförts, om en viss milstolpe i ett arbetsflöde har nåtts eller om några fel har uppstått.

Du kan prenumerera på varningar när du skapar ett dataflöde för att få varningsmeddelanden om status, om det lyckades eller om det inte gick att köra ditt flöde.

Det här dokumentet innehåller anvisningar om hur du prenumererar på varningsmeddelanden för källans dataflöden.

## Komma igång

Dokumentet kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../home.md): [!DNL Experience Platform] tillåter att data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform] tjänster.
* [Observationer](../../../observability/home.md): [!DNL Observability Insights] gör att ni kan övervaka plattformsaktiviteter med hjälp av statistiska värden och händelsemeddelanden.
   * [Varningar](../../../observability/alerts/overview.md): När en viss uppsättning villkor för plattformsåtgärder har nåtts (t.ex. ett potentiellt problem när systemet överskrider ett tröskelvärde) kan Platform leverera varningsmeddelanden till alla användare i organisationen som har prenumererat på dem.

## Prenumerera på aviseringar i användargränssnittet {#subscribe-sources-alerts}

>[!CONTEXTUALHELP]
>id="platform_sources_alerts_subscribe"
>title="Prenumerera på källvarningar"
>abstract="Med varningar kan du ta emot meddelanden baserat på statusen för källans dataflöden. Du kan ange varningsmeddelanden för att få uppdateringar om dataflödet har startats, har misslyckats, eller om inga data har importerats."
>text="Learn more in documentation"

>[!IMPORTANT]
>
>Du måste aktivera snabbmeddelanden om e-post för ditt plattformskonto för att kunna ta emot e-postbaserade varningsmeddelanden för dina dataflöden.

Du kan aktivera varningar för dina dataflöden under [!UICONTROL Dataflow detail] steg i källarbetsflödet på källarbetsytan.

![dataflöde-detail](../../images/tutorials/alerts/dataflow-detail.png)

De tillgängliga aviseringarna för källdataflöden är:

| Larm | Beskrivning |
| --- | --- |
| Start för källdataflöde | Den här varningen skickar ett meddelande när källdataflödet har startats. |
| Slutförd körning av källdataflöde | Den här varningen skickar ett meddelande när data från källan har importerats till plattformen. |
| Körningsfel för källdataflöde | Den här varningen skickar ett meddelande till dig om ett fel inträffar i dataflödet. |
| ~~Källdataflöde Brist på intag~~ | ~~Den här varningen skickar ett meddelande om importen fördröjs med mer än sju timmar och inga data hämtas till Platform.~~ <br>**Obs!** Du får inte längre några varningar eftersom den här varningen har tagits bort. |

Välj de aviseringar du vill prenumerera på och välj sedan **[!UICONTROL Next]** för att granska och slutföra dataflödet.

![markera-varningar](../../images/tutorials/alerts/select-alerts.png)

Mer information om hur du skapar ett källdataflöde i användargränssnittet finns i följande handböcker:

* [Advertising](./dataflow/advertising.md)
* [molnlagring](./dataflow/batch/cloud-storage.md)
* [CRM](./dataflow/crm.md)
* [Databas](./dataflow/databases.md)
* [E-handel](./dataflow/ecommerce.md)
* [Lokala filer](./create/local-system/local-file-upload.md)
* [Automatisering av marknadsföring](./dataflow/marketing-automation.md)
* [Betalningar](./dataflow/payments.md)
* [Protokoll](./dataflow/protocols.md)

## Ta emot aviseringar

När dataflödet har körts kan du få aviseringar via användargränssnittet eller via e-post.

### I användargränssnittet

Varningar representeras i användargränssnittet av en meddelandeikon i det övre huvudet i användargränssnittet för plattformen. Välj meddelandeikonen om du vill visa specifika varningsmeddelanden om dina dataflöden.

![meddelande](../../images/tutorials/alerts/notification.png)

Meddelandepanelen visas med en lista över statusuppdateringar för det dataflöde som du skapade.

![varningsfönster](../../images/tutorials/alerts/alert-window.png)

Du kan hovra över ett varningsmeddelande och markera det som läst eller välja klockikonen för att ange framtida påminnelser om dataflödets status.

![påminnelse-me](../../images/tutorials/alerts/remind-me.png)

Markera varningsmeddelandet om du vill visa specifik information om dataflödet.

![select-alert-message](../../images/tutorials/alerts/select-alert-message.png)

The [!UICONTROL Dataflow run overview] visas. I den övre halvan av skärmen visas en översikt över dataflödet, inklusive information om dess attribut, motsvarande körnings-ID för dataflöde och en sammanfattning av högnivåfel.

![dataflow-overview](../../images/tutorials/alerts/dataflow-overview.png)

Den nedre halvan av sidan visar alla [!UICONTROL Dataflow run errors] som uppstod under körningsfasen för dataflödet. Härifrån kan du förhandsgranska feldiagnostik eller använda [[!DNL Data Access] API](https://www.adobe.io/experience-platform-apis/references/data-access/) för att hämta feldiagnostik eller det filmanifest som motsvarar ditt dataflöde.

![dataflow-run-errors](../../images/tutorials/alerts/dataflow-run-error.png)

Mer information om hur du hanterar dataflödesfel finns i handboken om [övervaka källornas dataflöden i användargränssnittet](../../../dataflows/ui/monitor-sources.md).

### Per e-post

Varningar för dataflödena levereras också till dig via e-post. Välj dataflödets namn i e-postbrödtexten om du vill ha mer information om dataflödet.

![e-post](../../images/tutorials/alerts/email.png)

Liknar gränssnittsvarningen visas [!UICONTROL Dataflow run overview] visas så att du får ett gränssnitt där du kan undersöka eventuella fel som är kopplade till dataflödet.

![dataflow-overview](../../images/tutorials/alerts/dataflow-overview.png)

## Prenumerera och avbeställa aviseringar

Du kan prenumerera på fler aviseringar eller avbryta prenumerationen på etablerade aviseringar för ett befintligt dataflöde i [!UICONTROL Dataflows] sida. Leta reda på det dataflöde du skapar i listan och välj sedan ellipserna (`...`) för att se en listruta med alternativ. Nästa, välj **[!UICONTROL Subscribe alerts]** om du vill ändra aviseringsinställningarna för dataflödet.

![alternativ](../../images/tutorials/alerts/options.png)

Ett popup-fönster visas med en lista över källvarningar. Markera de aviseringar som du vill prenumerera på eller avmarkera aviseringar som du vill avsluta prenumerationen på. När du är klar väljer du **[!UICONTROL Save]**.

![spara](../../images/tutorials/alerts/save.png)

## Nästa steg

Det här dokumentet innehåller en stegvis guide om hur du prenumererar på sammanhangsberoende aviseringar för källans dataflöden. Mer information finns i [guide för varningsgränssnitt](../../../observability/alerts/ui.md).