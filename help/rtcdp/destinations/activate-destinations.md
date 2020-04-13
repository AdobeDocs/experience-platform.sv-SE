---
title: Aktivera profiler och segment till ett mål
seo-title: Aktivera profiler och segment till ett mål
description: Aktivera data i Adobes kunddataplattform i realtid genom att mappa segment till mål. Följ stegen nedan för att uppnå detta.
seo-description: Aktivera data i Adobes kunddataplattform i realtid genom att mappa segment till mål. Följ stegen nedan för att uppnå detta.
translation-type: tm+mt
source-git-commit: 2eddd5bb7b62dcc414ad906647b05ce10c766ac6

---


# Aktivera profiler och segment till ett mål

Aktivera data i Adobes kunddataplattform i realtid genom att mappa segment till mål. Följ stegen nedan för att uppnå detta.

## Förutsättningar {#prerequisites}

Om du vill aktivera data till mål måste du ha [anslutit ett mål](/help/rtcdp/destinations/assets/connect-destination.png). Om du inte redan har gjort det går du till [målkatalogen](/help/rtcdp/destinations/destinations-catalog.md), bläddrar bland de mål som stöds och ställer in ett eller flera mål.

## Aktivera data {#activate-data}

1. I **[!UICONTROL Destinations > Browse]** väljer du det mål där du vill aktivera segmenten.
2. Klicka på målets namn. Då kommer du till aktiveringsflödet.
   ![activate-flow](/help/rtcdp/destinations/assets/activate-flow.png)Observera att om det redan finns ett aktiveringsflöde för ett mål kan du se de segment som för närvarande skickas till målet. Välj **[!UICONTROL Edit activation]** i den högra listen och följ stegen nedan för att ändra aktiveringsinformationen.
3. Välj **[!UICONTROL Activate]**;
4. Välj vilka segment som ska skickas till målet på **[!UICONTROL Activate destination]** **[!UICONTROL Select Segments]** sidan i arbetsflödet.
   ![segment-till-mål](/help/rtcdp/destinations/assets/select-segments.png)
5. *Villkorligt*. Det här steget gäller endast för segment som är mappade till e-postmarknadsföringsmål. <br> På **[!UICONTROL Destination Attributes]** sidan markerar du **[!UICONTROL Add new field]** och väljer de attribut som du vill skicka till målet.
Vi rekommenderar att ett av attributen är en [unik identifierare](/help/rtcdp/destinations/email-marketing-destinations.md#identity) från ditt unionsschema. Mer information om obligatoriska attribut finns i Identitet i artikeln [E-postmarknadsföringsmål](/help/rtcdp/destinations/email-marketing-destinations.md#identity) .
   ![mål-attribut](/help/rtcdp/destinations/assets/destination-attributes.png)
6. På **[!UICONTROL Segment schedule]** sidan kan du se startdatumet för att skicka data till målet samt hur ofta data skickas till målet.

   >[!IMPORTANT]
   >
   >För sociala mål måste du välja målgruppens ursprung i det här steget. Du kan bara fortsätta till nästa steg efter att du har valt något av alternativen i bilden nedan.

   ![välj datakälla](/help/rtcdp/destinations/assets/choose-data-origin.png)

7. På **[!UICONTROL Review]** sidan visas en sammanfattning av markeringen. Välj **[!UICONTROL Cancel]** om du vill dela upp flödet, **[!UICONTROL Back]** om du vill ändra inställningarna eller **[!UICONTROL Finish]** om du vill bekräfta urvalet och börja skicka data till målet.

![bekräfta-val](/help/rtcdp/destinations/assets/confirm-selection.png)

## Redigera aktivering {#edit-activation}

Följ stegen nedan för att redigera befintliga aktiveringsflöden i realtid med CDP:

1. Markera **[!UICONTROL Destinations]** i det vänstra navigeringsfältet, klicka på **[!UICONTROL Browse]** fliken och klicka på målnamnet.
2. Välj **[!UICONTROL Edit activation]** i den högra listen för att ändra vilka segment som ska skickas till målet.

## Verifiera att segmentaktiveringen lyckades {#verify-activation}

### Destinationer för e-postmarknadsföring och molnlagring

För e-postmarknadsföringsmål och molnlagringsmål skapar Adobe Real-time CDP en tabbavgränsad `.txt` eller `.csv` fil på den lagringsplats som du angav. Förvänta dig att en ny fil ska skapas på din lagringsplats varje dag. Filformatet är:
`<destination name>id<destination id><timestamp-yyyymmddhhmmss>`

De filer du får tre dagar i följd kan se ut så här:

```
Salesforce_id3544_20191120110000.csv
Salesforce_id3544_20191121123000.csv
Salesforce_id3544_20191122124530.csv
```

De här filerna finns på lagringsplatsen och du har fått en bekräftelse på att aktiveringen har slutförts.

### Annonsmål

Kontrollera respektive annonsmål som du aktiverar dina data till. Om aktiveringen lyckades, fylls målgrupperna i er annonsplattform.

### Målgrupper i sociala nätverk

För Facebook innebär en lyckad aktivering att en anpassad Facebook-målgrupp skapas programmatiskt i [Facebook Ads Manager](https://www.facebook.com/adsmanager/manage/). Segmentmedlemskap i målgruppen skulle läggas till och tas bort eftersom användarna är kvalificerade eller diskvalificerade för de aktiverade segmenten.

## Inaktivera aktivering {#disable-activation}

Följ stegen nedan för att inaktivera ett befintligt aktiveringsflöde:

1. Markera **[!UICONTROL Destinations]** i det vänstra navigeringsfältet, klicka på **[!UICONTROL Browse]** fliken och klicka på målnamnet.
2. Klicka på **[!UICONTROL Enabled]** kontrollen till höger för att ändra aktiveringsflödets status.
3. I fönstret **Uppdatera dataflöde** väljer du **Bekräfta** för att inaktivera aktiveringsflödet.

