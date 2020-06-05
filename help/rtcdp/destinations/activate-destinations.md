---
title: Aktivera profiler och segment till ett mål
seo-title: Aktivera profiler och segment till ett mål
description: Aktivera data i Adobes kunddataplattform i realtid genom att mappa segment till mål. Följ stegen nedan för att uppnå detta.
seo-description: Aktivera data i Adobes kunddataplattform i realtid genom att mappa segment till mål. Följ stegen nedan för att uppnå detta.
translation-type: tm+mt
source-git-commit: 24e4746b28620210c138a1e803b6afadff79ab30
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 0%

---


# Aktivera profiler och segment till ett mål

Aktivera data i Adobes kunddataplattform i realtid genom att mappa segment till mål. Följ stegen nedan för att uppnå detta.

## Förutsättningar {#prerequisites}

Om du vill aktivera data till mål måste du ha [anslutit ett mål](/help/rtcdp/destinations/assets/connect-destination-1.png). Om du inte redan har gjort det går du till [målkatalogen](/help/rtcdp/destinations/destinations-catalog.md), bläddrar bland de mål som stöds och ställer in ett eller flera mål.

## Aktivera data {#activate-data}

1. I **[!UICONTROL Destinations > Browse]** väljer du det mål där du vill aktivera segmenten.
2. Klicka på målets namn. Då kommer du till aktiveringsflödet.
   ![activate-flow](/help/rtcdp/destinations/assets/activate-flow.png)Observera att om det redan finns ett aktiveringsflöde för ett mål kan du se de segment som för närvarande skickas till målet. Välj **[!UICONTROL Edit activation]** i den högra listen och följ stegen nedan för att ändra aktiveringsinformationen.
3. Välj **[!UICONTROL Activate]**;
4. Välj vilka segment som ska skickas till målet på **[!UICONTROL Activate destination]** **[!UICONTROL Select Segments]** sidan i arbetsflödet.
   ![segment-till-mål](/help/rtcdp/destinations/assets/select-segments.png)
5. *Villkorligt*. Det här steget skiljer sig åt beroende på vilken typ av mål du aktiverar dina segment på. <br> För *e-postmarknadsföringsmål* och *molnlagringsmål* väljer du de attribut du vill skicka till målet på **[!UICONTROL Select Attributes]** **[!UICONTROL Add new field]** sidan.
Vi rekommenderar att ett av attributen är en [unik identifierare](/help/rtcdp/destinations/email-marketing-destinations.md#identity) från ditt unionsschema. Mer information om obligatoriska attribut finns i Identitet i artikeln [E-postmarknadsföringsmål](/help/rtcdp/destinations/email-marketing-destinations.md#identity) .
   ![mål-attribut](/help/rtcdp/destinations/assets/select-attributes-step.png)

   <br> 

   För *sociala mål* kan du i **[!UICONTROL Identity mapping]** steget välja källattribut att mappa som målidentiteter i målet. Det här steget är antingen valfritt eller obligatoriskt, beroende på vilken primär identitet du använder i schemat. <br> 

   *E-postadress som primär identitet*: Om du använder e-postadress som primär identitet i ditt schema kan du hoppa över steget Identitetsmappning, vilket visas nedan:

   ![E-postadress som identitet](/help/rtcdp/destinations/assets/email-as-identity.gif)

   <br> 

   *Ett annat ID som primär identitet*: Om du använder ett annat ID, till exempel *Rewards ID* eller *Loyalty ID*, som primär identitet i ditt schema, måste du manuellt mappa e-postadressen från ditt identitetsschema som en målidentitet i det sociala målet, vilket visas nedan:

   ![Förmåns-ID som identitet](/help/rtcdp/destinations/assets/rewardsid-as-identity.gif)


   Välj `Email_LC_SHA256` som målidentitet om du har hashas i kundens e-postadresser vid dataöverföring till Adobe Experience Platform, enligt Facebooks [e-posthashkrav](/help/rtcdp/destinations/facebook-destination.md#email-hashing-requirements). <br> Välj `Email` som målidentitet om e-postadresserna du använder inte är hashas. Adobe CDP i realtid hash-kodar e-postadresserna så att de uppfyller Facebooks krav.

   ![identitetsmappning efter att fält fyllts i](/help/rtcdp/destinations/assets/identity-mapping.png)

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

>[!TIP]
>
>Integrationen mellan Adobe Real-time CDP och Facebook har stöd för historiska efterfyllningar av målgrupper. Alla historiska segmentkvalifikationer skickas till Facebook när du aktiverar segmenten till målet.

## Inaktivera aktivering {#disable-activation}

Följ stegen nedan för att inaktivera ett befintligt aktiveringsflöde:

1. Markera **[!UICONTROL Destinations]** i det vänstra navigeringsfältet, klicka på **[!UICONTROL Browse]** fliken och klicka på målnamnet.
2. Klicka på **[!UICONTROL Enabled]** kontrollen till höger för att ändra aktiveringsflödets status.
3. I fönstret **Uppdatera dataflöde** väljer du **Bekräfta** för att inaktivera aktiveringsflödet.

I AWS Kinesis skapar du en åtkomstnyckel - ett hemligt åtkomstnyckelpar som ger Adobe CDP-åtkomst i realtid till ditt AWS Kinesis-konto. Läs mer i dokumentationen [till](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)AWS Kinesis.