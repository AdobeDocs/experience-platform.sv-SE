---
keywords: RTCDP;CDP;B2B Edition;Real-time Customer Data Platform;kunddataplattform i realtid;cdp i realtid;b2b;cdp
solution: Experience Platform
title: Komma igång med Real-time Customer Data Platform B2B Edition
description: Använd det här exempelscenariot som exempel när du konfigurerar din implementering av Adobe Real-time Customer Data Platform B2B Edition.
exl-id: ad9ace46-9915-4b8f-913a-42e735859edf
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '1196'
ht-degree: 0%

---

# Komma igång med Real-time Customer Data Platform B2B Edition

Det här dokumentet innehåller ett avancerat arbetsflöde från början till slut för att komma igång med Real-time Customer Data Platform (CDP) B2B Edition, där man kan använda exempel för att illustrera viktiga koncept.

Teknikföretaget Bodea vill kombinera person- och kontodata från olika externa datakällor för att effektivt kunna rikta in sig på kunderna med ett e-postmeddelande och en reklamkampanj från LinkedIn för sin nya produkt. Bodea använder Marketo Engage som sin automatiseringsplattform för marknadsföring och behöver segmentera en B2B-specifik målgrupp från flera CRM-system som innehåller kunddata.

## Komma igång

Det här självstudiearbetsflödet bygger på flera Adobe Experience Platform-tjänster som en del av demonstrationen. Om du vill följa med i utvecklingen rekommenderar vi att du har god förståelse för följande tjänster:

- [Experience Data Modal (XDM)](../xdm/home.md)
- [Källor](../sources/home.md)
- [Segmentering](../segmentation/home.md)
- [Mål ](../destinations/home.md)

## Skapa scheman för dina data

Som en del av den första konfigurationen måste Bodeas IT-avdelning skapa ett XDM-schema för att säkerställa att deras data följer ett standardformat när de hämtas till Platform och kan användas i olika plattformstjänster och Adobe Experience Cloud-produkter (som Adobe Analytics och Adobe Target).

>[!WARNING]
>
>Du måste följa de intag-mönster som beskrivs i den relevanta källdokumentationen som är länkad till genom den här självstudiekursen. Andra fältmappningsmetoder fungerar inte med säkerhet.

Med Adobe Experience Platform kan du automatiskt generera scheman och namnutrymmen som krävs för B2B-datakällor. Detta verktyg ser till att de scheman som skapas beskriver data på ett strukturerat återanvändbart sätt. Följ [Dokumentation för verktyg för automatisk generering av B2B-namnutrymmen och scheman](../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) för en fullständig referens till konfigurationsprocessen.

I Adobe Experience Platform-gränssnittet väljer Bodea-marknadsföraren **[!UICONTROL Schemas]** i den vänstra listen, följt av **[!UICONTROL Browse]** -fliken. Eftersom de använde autogenereringsverktyget för Marketo Engage visas de nya tomma scheman i listan med prefixet&quot;B2B&quot;.

![Fliken Bläddra i arbetsytan Schema](./assets/b2b-tutorial/empty-b2b-schemas.png)

Verktyget för automatisk generering definierade datamodellstrukturen för scheman med hjälp av standardklasserna XDM B2B (till exempel [XDM Business Account](../xdm/classes/b2b/business-account.md) och [XDM - affärsmöjlighet](../xdm/classes/b2b/business-opportunity.md)) som samlar in grundläggande B2B-datatabeller. Dessutom har de automatiskt genererade B2B-scheman som bygger på dessa klasser redan etablerade relationer som möjliggör avancerad segmenteringsanvändning. Alla ytterligare fältgrupper som krävs för datastrukturen kan enkelt göras här via användargränssnittet. Se [Användargränssnittshandbok för XDM, lägga till fältgrupper i ett schemaavsnitt](../xdm/ui/resources/schemas.md#add-field-groups) för mer information.

>[!NOTE]
> 
>Om du inte använder verktyget för autogenerering eller om du behöver skapa en ny relation läser du självstudiekursen om [skapa relationer mellan B2B-scheman](../xdm/tutorials/relationship-b2b.md).

Kundprofilen i realtid sammanfogar data från olika källor för att skapa konsoliderade profiler för viktiga B2B-företag. Eftersom profiler genereras baserat på en enda klass skapar verktyget för automatisk generering relationer mellan scheman baserat på vanliga användningsfall. Därför är Bodea-teamet nu redo att importera data baserat på deras B2B-scheman.

>[!NOTE]
> 
>Standardnamnutrymmen för identiteter, primärnycklar och relationer som skapas för scheman av verktyget för automatisk generering kan enkelt upptäckas i arbetsytan Schema.
>
>![standardschema-identitet och relationsgränssnitt](./assets/b2b-tutorial/schema-identity-relationship.png)

## Infoga data i Experience Platform

Sedan använder Bodea-marknadsföraren [Marketo Engage-kontakt](../sources/connectors/adobe-applications/marketo/marketo.md) att importera data till plattformen för användning i tjänster längre fram i kedjan. Du kan även importera data genom att använda någon av de godkända källorna för Real-Time CDP B2B Edition.

>[!NOTE]
> 
>Om du vill veta vilka källanslutningar som är tillgängliga för din organisation kan du visa källkatalogen i användargränssnittet för plattformen. Om du vill komma åt katalogen väljer du **Källor** i den vänstra navigeringen väljer du **Katalog**.

Om du vill skapa en anslutning mellan ett Marketo-konto och en plattform måste du hämta autentiseringsuppgifter. Se [guide om hur du får inloggningsuppgifter för Marketo-källanslutning](../sources/connectors/adobe-applications/marketo/marketo-auth.md) för detaljerade anvisningar.

När autentiseringsuppgifterna har inhämtats skapar Bodea-marknadsföraren en anslutning mellan Marketo-kontot och deras plattforms-IMS-organisation. I dokumentationen finns instruktioner om [hur du ansluter ett Marketo-konto med hjälp av plattformsgränssnittet](../sources/tutorials/ui/create/adobe-applications/marketo.md).

Marketo Engage-källkopplingen har en automatisk mappningsfunktion som gör det enklare att mappa alla dina datafält till de nya scheman.

>[!NOTE]
> 
>Om du har skapat anpassade fältgrupper i XDM-scheman kan det finnas okopplade fält i det här skedet av processen. Kontrollera alla värden som fyller i dina anpassade fältgrupper.

Bodea-markören kontrollerar att alla fältgrupper är korrekt mappade och fortsätter källkonfigurationen genom att initiera ett dataflöde. Genom att skapa ett dataflöde för att hämta in Marketo-data kan inkommande data användas av plattformstjänster längre fram i kedjan. Under den inledande intagsprocessen förs data in i Experience Platform som en sats. Därefter direktuppspelas inkapslade data till profilen med nästan realtidsuppdateringar.

## Skapa ett segment för att utvärdera dina data

Nästa uppgift är att skapa en målgrupp för Bodeas nya e-postmarknadsföringskampanj baserat på specifika attribut från relaterade enheter i källdata. I plattformsgränssnittet väljer Bodea-marknadsföraren först **[!UICONTROL Segments]** i den vänstra navigeringen och sedan **[!UICONTROL Create segment]**.

I det här exemplet hittar segmentet alla personer som arbetar på försäljningsavdelningen och som är kopplade till ett konto som har minst en öppen affärsmöjlighet. Det här segmentet kräver en länk mellan klassen XDM Individual Profile, klassen XDM Business Account och klassen XDM Business Opportunity.

![Använd skiftlägessegment](./assets/b2b-tutorial/use-case-segment.png)

>[!NOTE]
> 
>Instruktioner om hur du skapar segment för att utvärdera data finns i [Användargränssnittsguide för segmentbyggare](../segmentation/ui/segment-builder.md). Mer specifika användningsfall för B2B-segmentering finns i [segmenteringsöversikt för Real-Time CDP B2B Edition](./segmentation/b2b.md).

Med Segment Builder kan ni skapa en marknadsföringsbar publik utifrån kundprofildata i realtid och visa uppskattningar av er presumtiva målgrupp baserat på den kombination av attribut, händelser och befintliga målgrupper som ni har definierat.

## Aktivera utvärderade data till ett mål

När segmentet har skapats visas en sammanfattning i [!UICONTROL Details] i arbetsytan. Eftersom inga destinationer är aktiverade för segmentet måste Bodea-marknadsföraren exportera målgruppen till en datauppsättning där den kan nås och hanteras.

I [!UICONTROL Segments] arbetsytan i plattformsgränssnittet, markeras av Bodea-marknadsföraren **[!UICONTROL Activate to destination]**.

![Aktivera segmentet till ett mål](./assets/b2b-tutorial/activate-to-destination.png)

>[!NOTE]
> 
>Se självstudiekursen om [aktivera ett segment till ett mål](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html) om du vill ha mer information om hur du uppnår detta.

Bodea-marknadsföraren aktiverar segmentet till Marketo-destinationen, vilket gör att de kan skicka segmentdata från Platform till Marketo Engage i form av en statisk lista. Se guiden på [Marketo](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/adobe/marketo-engage.html) för mer information.

## Nästa steg

Genom att följa den här självstudiekursen har du lyckats utnyttja de olika Adobe Experience Platform-tjänster som används av Real-Time CDP B2B Edition. Därför har ni lärt er att importera, segmentera, utvärdera och exportera era B2B-data som användbara målgrupper som kan engageras i olika kanaler.
