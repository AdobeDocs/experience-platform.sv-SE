---
keywords: aktivera profildestinationer;aktivera destinationer;aktivera data; aktivera e-postmarknadsföringsmål, aktivera molnlagringsmål
title: Aktivera målgrupper för att direktuppspela exportmål för profiler
type: Tutorial
description: Lär dig hur du aktiverar målgruppsdata som du har i Adobe Experience Platform genom att skicka målgrupper till direktuppspelade profilbaserade mål.
exl-id: bc0f781e-60de-44a5-93cb-06b4a3148591
source-git-commit: 37819b5a6480923686d327e30b1111ea29ae71da
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 0%

---


# Aktivera målgrupper för att direktuppspela exportmål för profiler

>[!IMPORTANT]
> 
> * Aktivera data och aktivera [mappningssteg](#mapping) i arbetsflödet behöver du **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions).
> * Aktivera data utan att gå igenom [mappningssteg](#mapping) i arbetsflödet behöver du **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Segment without Mapping]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions).
> 
> Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

## Översikt {#overview}

I den här artikeln beskrivs det arbetsflöde som krävs för att aktivera målgruppsdata i Adobe Experience Platform direktuppspelningsprofilbaserade mål, som Amazon Kinesis.

## Förutsättningar {#prerequisites}

Du måste ha aktiverat data till destinationer [ansluten till ett mål](./connect-destination.md). Om du inte redan har gjort det går du till [målkatalog](../catalog/overview.md), bläddra bland de mål som stöds och konfigurera det mål som du vill använda.

## Välj mål {#select-destination}

1. Gå till **[!UICONTROL Connections > Destinations]** och väljer **[!UICONTROL Catalog]** -fliken.

   ![Bild som visar fliken för målkatalogen.](../assets/ui/activate-streaming-profile-destinations/catalog-tab.png)

1. Välj **[!UICONTROL Activate audiences]** på kortet som motsvarar destinationen där du vill aktivera målgrupperna, vilket visas i bilden nedan.

   ![Bild som markerar kontrollen för att aktivera målgrupper på fliken för målkatalogen.](../assets/ui/activate-streaming-profile-destinations/activate-audiences-button.png)

1. Välj den målanslutning som du vill använda för att aktivera dina målgrupper och välj sedan **[!UICONTROL Next]**.

   ![Bild som visar ett urval av två mål som du kan ansluta till.](../assets/ui/activate-streaming-profile-destinations/select-destination.png)

1. Gå till nästa avsnitt till [välj era målgrupper](#select-audiences).

## Välj målgrupper {#select-audiences}

Om du vill välja vilka målgrupper du vill aktivera för målet använder du kryssrutorna till vänster om målgruppsnamnen och väljer sedan **[!UICONTROL Next]**.

Du kan välja mellan flera typer av målgrupper, beroende på deras ursprung:

* **[!UICONTROL Segmentation Service]**: Målgrupper som genererats i Experience Platform av segmenteringstjänsten. Se [segmenteringsdokumentation](../../segmentation/ui/overview.md) för mer information.
* **[!UICONTROL Custom upload]**: Publiker som genererats utanför Experience Platform och överförts till Platform som CSV-filer. Mer information om externa målgrupper finns i dokumentationen om [importera en publik](../../segmentation/ui/overview.md#import-audience).
* Andra typer av målgrupper som härrör från andra Adobe-lösningar, t.ex. [!DNL Audience Manager].

![Markera kryssrutorna i steget Välj målgrupper i aktiveringsarbetsflödet.](../assets/ui/activate-streaming-profile-destinations/select-audiences.png)

## Välj profilattribut {#select-attributes}

I **[!UICONTROL Mapping]** markerar du de profilattribut som du vill skicka till målmålet.

1. I **[!UICONTROL Select attributes]** sida, markera **[!UICONTROL Add new field]**.

   ![Bild som markerar kontrollen Lägg till nytt fält i mappningssteget.](../assets/ui/activate-streaming-profile-destinations/add-new-field.png)

1. Markera pilen till höger om **[!UICONTROL Schema field]** post.

   ![Bilden visar hur du väljer ett källfält i mappningssteget.](../assets/ui/activate-streaming-profile-destinations/select-schema-field.png)

1. I **[!UICONTROL Select field]** väljer du de XDM-attribut som du vill skicka till målet och väljer **[!UICONTROL Select]**.

   ![Bild som visar ett urval av XDM-fält som du kan välja som källfält.](../assets/ui/activate-streaming-profile-destinations/target-field-page.png)

1. Om du vill lägga till fler fält upprepar du steg 1 till 3 och väljer sedan **[!UICONTROL Next]**.

## Granska {#review}

På **[!UICONTROL Review]** kan du se en sammanfattning av markeringen. Välj **[!UICONTROL Cancel]** för att bryta upp flödet, **[!UICONTROL Back]** för att ändra dina inställningar, eller **[!UICONTROL Finish]** för att bekräfta ditt val och börja skicka data till målet.

![Markeringssammanfattning i granskningssteget.](../assets/ui/activate-streaming-profile-destinations/review.png)

### Principutvärdering av samtycke {#consent-policy-evaluation}

Om din organisation har köpt **Adobe Healthcare Shield** eller **Adobe Privacy &amp; Security Shield**, markera **[!UICONTROL View applicable consent policies]** för att se vilka regler för samtycke som tillämpas och hur många profiler som inkluderas i aktiveringen till följd av dessa. Läs om [utvärdering av godkännandepolicy](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) för mer information.

### Kontroller av policyer för dataanvändning {#data-usage-policy-checks}

I **[!UICONTROL Review]** Experience Platform kontrollerar också om dataanvändningspolicyn har överträtts. Nedan visas ett exempel där en princip överträds. Du kan inte slutföra arbetsflödet för målgruppsaktivering förrän du har löst överträdelsen. Mer information om hur du löser policyöverträdelser finns i [brott mot dataanvändningsprinciper](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) i dokumentationsavsnittet för datastyrning.

![dataprincipöverträdelse](../assets/common/data-policy-violation.png)

### Filtrera målgrupper {#filter-audiences}

I det här steget kan du även använda de tillgängliga filtren på sidan för att visa endast de målgrupper vars schema eller mappning har uppdaterats som en del av det här arbetsflödet.

![Skärminspelning som visar tillgängliga målgruppsfilter i granskningssteget.](../assets/ui/activate-streaming-profile-destinations/filter-audiences-review-step.gif)

Om du är nöjd med ditt val och inga policyöverträdelser har identifierats väljer du **[!UICONTROL Finish]** för att bekräfta ditt val och börja skicka data till målet.

## Verifiera målgruppsaktivering {#verify}

Dina exporterade [!DNL Experience Platform] i måldestinationen i JSON-format. Händelsen nedan innehåller till exempel e-postadressattributet för en profil som har kvalificerats för en viss målgrupp och avslutat en annan målgrupp. Identiteterna för den här potentiella kunden är `ECID` och `email_lc_sha256`.

```json
{
  "person": {
    "email": "yourstruly@adobe.com"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "realized"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```
