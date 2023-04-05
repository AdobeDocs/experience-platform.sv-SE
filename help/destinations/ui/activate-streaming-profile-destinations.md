---
keywords: aktivera profildestinationer;aktivera destinationer;aktivera data; aktivera e-postmarknadsföringsmål, aktivera molnlagringsmål
title: Aktivera målgruppsdata till exportmål för direktuppspelningsprofiler
type: Tutorial
description: Lär dig hur du aktiverar målgruppsdata som du har i Adobe Experience Platform genom att skicka segment till direktuppspelade profilbaserade mål.
exl-id: bc0f781e-60de-44a5-93cb-06b4a3148591
source-git-commit: 5bb2981b8187fcd3de46f80ca6c892421b3590f6
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 0%

---

# Aktivera målgruppsdata till exportmål för direktuppspelningsprofiler

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

1. Välj **[!UICONTROL Activate segments]** på kortet som motsvarar destinationen där du vill aktivera dina segment, vilket visas i bilden nedan.

   ![Bild som markerar kontrollen för aktivering av segment på fliken för målkatalogen.](../assets/ui/activate-streaming-profile-destinations/activate-segments-button.png)

1. Markera målanslutningen som du vill använda för att aktivera dina segment och välj sedan **[!UICONTROL Next]**.

   ![Bild som visar ett urval av två mål som du kan ansluta till.](../assets/ui/activate-streaming-profile-destinations/select-destination.png)

1. Gå till nästa avsnitt till [markera segment](#select-segments).

## Välj segment {#select-segments}

Använd kryssrutorna till vänster om segmentnamnen för att markera de segment som du vill aktivera för målet och markera sedan **[!UICONTROL Next]**.

![Markera kryssrutorna i steget Markera segment i aktiveringsarbetsflödet.](../assets/ui/activate-streaming-profile-destinations/select-segments.png)

## Välj profilattribut {#select-attributes}

I **[!UICONTROL Mapping]** markerar du de profilattribut som du vill skicka till målmålet.

>[!NOTE]
>
> Adobe Experience Platform fyller markeringen i förväg med fyra rekommenderade attribut från ditt schema: `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

Filexporter varierar på följande sätt, beroende på om `segmentMembership.status` är markerat:
* Om `segmentMembership.status` fältet är markerat, exporterade filer innehåller **[!UICONTROL Active]** medlemmar i den första fullständiga ögonblicksbilden och **[!UICONTROL Active]** och **[!UICONTROL Expired]** medlemmar i efterföljande stegvisa exporter.
* Om `segmentMembership.status` fältet är inte markerat, exporterade filer innehåller endast **[!UICONTROL Active]** medlemmar i den första fullständiga ögonblicksbilden och i efterföljande stegvisa exporter.

![Bild som visar de förfyllda, rekommenderade attributen i mappningssteget.](../assets/ui/activate-streaming-profile-destinations/attributes-default.png)

1. I **[!UICONTROL Select attributes]** sida, markera **[!UICONTROL Add new field]**.

   ![Bild som markerar kontrollen Lägg till nytt fält i mappningssteget.](../assets/ui/activate-streaming-profile-destinations/add-new-field.png)

1. Markera pilen till höger om **[!UICONTROL Schema field]** post.

   ![Bilden visar hur du väljer ett källfält i mappningssteget.](../assets/ui/activate-streaming-profile-destinations/select-schema-field.png)

1. I **[!UICONTROL Select field]** väljer du de XDM-attribut som du vill skicka till målet och väljer **[!UICONTROL Select]**.

   ![Bild som visar ett urval av XDM-fält som du kan välja som källfält.](../assets/ui/activate-streaming-profile-destinations/target-field-page.png)


1. Om du vill lägga till fler mappningar upprepar du steg 1 till 3 och väljer sedan **[!UICONTROL Next]**.

## Granska {#review}

På **[!UICONTROL Review]** kan du se en sammanfattning av markeringen. Välj **[!UICONTROL Cancel]** för att bryta upp flödet, **[!UICONTROL Back]** för att ändra dina inställningar, eller **[!UICONTROL Finish]** för att bekräfta ditt val och börja skicka data till målet.

![Markeringssammanfattning i granskningssteget.](/help/destinations/assets/ui/activate-streaming-profile-destinations/review.png)

### Principutvärdering av samtycke {#consent-policy-evaluation}

Om din organisation har köpt **Adobe Healthcare Shield** eller **Adobe Privacy &amp; Security Shield**, markera **[!UICONTROL View applicable consent policies]** för att se vilka regler för samtycke som tillämpas och hur många profiler som inkluderas i aktiveringen till följd av dessa. Läs om [utvärdering av godkännandepolicy](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) för mer information.

### Kontroller av policyer för dataanvändning {#data-usage-policy-checks}

I **[!UICONTROL Review]** Experience Platform kontrollerar också om dataanvändningspolicyn har överträtts. Nedan visas ett exempel där en princip överträds. Du kan inte slutföra arbetsflödet för segmentaktivering förrän du har löst konflikten. Mer information om hur du löser policyöverträdelser finns i [brott mot dataanvändningsprinciper](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) i dokumentationsavsnittet för datastyrning.

![dataprincipöverträdelse](../assets/common/data-policy-violation.png)

### Filtrera segment {#filter-segments}

I det här steget kan du även använda de tillgängliga filtren på sidan för att endast visa segment vars schema eller mappning har uppdaterats som en del av det här arbetsflödet.

![Skärminspelning som visar tillgängliga segmentfilter i granskningssteget.](/help/destinations/assets/ui/activate-streaming-profile-destinations/filter-segments-review-step.gif)

Om du är nöjd med ditt val och inga policyöverträdelser har identifierats väljer du **[!UICONTROL Finish]** för att bekräfta ditt val och börja skicka data till målet.

## Verifiera segmentaktivering {#verify}

Dina exporterade [!DNL Experience Platform] i måldestinationen i JSON-format. Händelsen nedan innehåller till exempel e-postadressprofilattributet för en målgrupp som har kvalificerat sig för ett visst segment och avslutat ett annat segment. Identiteterna för den här potentiella kunden är ECID och e-post.

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
