---
keywords: RTCDP;CDP;B2B edition;Real-Time Customer Data Platform;kunddataplattform i realtid;cdp i realtid;b2b;cdp
solution: Experience Platform
title: Komma igång med Real-Time Customer Data Platform B2B edition
description: Använd det här exempelscenariot som exempel när du konfigurerar din implementering av Adobe Real-Time Customer Data Platform B2B edition.
feature: Get Started, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/se/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: ad9ace46-9915-4b8f-913a-42e735859edf
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 0%

---

# Komma igång med Real-Time Customer Data Platform B2B edition

Det här dokumentet innehåller ett avancerat arbetsflöde från början till slut för att komma igång med Real-Time Customer Data Platform (CDP) B2B edition, där man kan använda ett exempel för att illustrera viktiga koncept.

Teknikföretaget Bodea vill kombinera person- och kontodata från olika externa datakällor för att effektivt kunna rikta in sig på kunderna med ett e-postmeddelande och en LinkedIn-reklamkampanj för den nya produkten. Bodea använder Marketo Engage som sin automatiseringsplattform för marknadsföring och behöver segmentera en B2B-specifik målgrupp från flera CRM:er som innehåller kunddata.

## Komma igång

Det här självstudiearbetsflödet bygger på flera Adobe Experience Platform-tjänster som en del av demonstrationen. Om du vill följa med i utvecklingen rekommenderar vi att du har god förståelse för följande tjänster:

- [Experience Data Model (XDM)](../xdm/home.md)
- [Källor](../sources/home.md)
- [Segmentering](../segmentation/home.md)
- [Mål](../destinations/home.md)

## Skapa scheman för dina data

Som en del av den första konfigurationen måste Bodeas IT-avdelning skapa ett XDM-schema för att säkerställa att deras data följer ett standardformat när de hämtas till Experience Platform, och kan användas i olika Experience Platform-tjänster och Adobe Experience Cloud-produkter (som Adobe Analytics och Adobe Target).

>[!WARNING]
>
>Du måste följa de intag-mönster som beskrivs i den relevanta källdokumentationen som är länkad till genom den här självstudiekursen. Andra fältmappningsmetoder fungerar inte med säkerhet.

Med Adobe Experience Platform kan du automatiskt generera scheman och namnutrymmen som krävs för B2B-datakällor. Detta verktyg ser till att de scheman som skapas beskriver data på ett strukturerat återanvändbart sätt. Följ [dokumentationen för B2B-namnutrymmen och automatisk generering av scheman](../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) för en fullständig referens till konfigurationsprocessen.

I Adobe Experience Platform-gränssnittet väljer Bodea-markören **[!UICONTROL Schemas]** i den vänstra listen, följt av fliken **[!UICONTROL Browse]**. Eftersom de använde Marketo Engage autogenereringsverktyg visas de nya tomma scheman i listan och alla har prefixet &quot;B2B&quot;.

![Fliken Bläddra i arbetsytan Schema](./assets/b2b-tutorial/empty-b2b-schemas.png)

Verktyget för automatisk generering definierade datamodellstrukturen för scheman med hjälp av standardklasserna XDM B2B (till exempel [XDM Business Account](../xdm/classes/b2b/business-account.md) och [XDM Business Opportunity](../xdm/classes/b2b/business-opportunity.md)) som samlar in grundläggande B2B-datatabeller. Dessutom har de automatiskt genererade B2B-scheman som bygger på dessa klasser redan etablerade relationer som möjliggör avancerad segmenteringsanvändning. Alla ytterligare fältgrupper som krävs för datastrukturen kan enkelt göras här via användargränssnittet. Mer information finns i [XDM-gränssnittsguiden, som lägger till fältgrupper i ett schemaavsnitt](../xdm/ui/resources/schemas.md#add-field-groups).

>[!NOTE]
> 
>Om du inte använder verktyget för autogenerering eller om en ny relation behöver skapas, se självstudiekursen [Skapa relationer mellan B2B-scheman](../xdm/tutorials/relationship-b2b.md).

Kundprofilen i realtid sammanfogar data från olika källor för att skapa konsoliderade profiler för viktiga B2B-företag. Eftersom profiler genereras baserat på en enda klass skapar verktyget för automatisk generering relationer mellan scheman baserat på vanliga användningsfall. Därför är Bodea-teamet nu redo att importera data baserat på deras B2B-scheman.

>[!NOTE]
> 
>Standardnamnutrymmen för identiteter, primärnycklar och relationer som skapas för scheman av verktyget för automatisk generering kan enkelt upptäckas i arbetsytan Schema.
>
>![standardschemaidentitet och relationsgränssnitt](./assets/b2b-tutorial/schema-identity-relationship.png)

## Importera data till Experience Platform

Därefter använder Bodea-marknadsföraren [Marketo Engage-kopplingen](../sources/connectors/adobe-applications/marketo/marketo.md) för att importera data till Experience Platform för användning i underordnade tjänster. Du kan även importera data med någon av de godkända källorna för Real-Time CDP B2B edition.

>[!NOTE]
> 
>Om du vill veta vilka källanslutningar som är tillgängliga för din organisation kan du visa källkatalogen i Experience Platform användargränssnitt. Om du vill komma åt katalogen väljer du **Källor** i den vänstra navigeringen och sedan **Katalog**.

Om du vill skapa en anslutning mellan ett Marketo-konto och Experience Platform måste du skaffa inloggningsuppgifter. Detaljerade instruktioner finns i [handboken om hur du får Marketo-autentiseringsuppgifter för källanslutning](../sources/connectors/adobe-applications/marketo/marketo-auth.md).

När du har fått inloggningsuppgifter skapar Bodea-marknadsföraren en anslutning mellan Marketo-kontot och deras Experience Platform-organisation. I dokumentationen finns instruktioner om hur du ansluter ett Marketo-konto med Experience Platform-gränssnittet [&#128279;](../sources/tutorials/ui/create/adobe-applications/marketo.md).

Marketo Engage-källkopplingen har en automatisk mappningsfunktion som gör det enklare att mappa alla dina datafält till de nya scheman.

>[!NOTE]
> 
>Om du har skapat anpassade fältgrupper i XDM-scheman kan det finnas okopplade fält i det här skedet av processen. Kontrollera alla värden som fyller i dina anpassade fältgrupper.

Bodea-markören kontrollerar att alla fältgrupper är korrekt mappade och fortsätter källkonfigurationen genom att initiera ett dataflöde. Genom att skapa ett dataflöde för att hämta in Marketo-data kan inkommande data användas av Experience Platform-tjänster längre fram i kedjan. Under den inledande matningsprocessen överförs data till Experience Platform som en batch. Därefter direktuppspelas inkapslade data till profilen med nästan realtidsuppdateringar.

## Skapa en målgrupp för att utvärdera era data

Nästa uppgift är att skapa en målgrupp för Bodeas nya e-postmarknadsföringskampanj baserat på specifika attribut från relaterade enheter i källdata. I Experience Platform-användargränssnittet väljer Bodea-markören först **[!UICONTROL Segments]** i den vänstra navigeringen och sedan **[!UICONTROL Create segment]**.

I det här exemplet hittar målgruppen alla personer som arbetar på försäljningsavdelningen och som är kopplade till ett konto som har minst en öppen affärsmöjlighet. Dessa målgrupper kräver en länk mellan klassen XDM Individual Profile, klassen XDM Business Account och klassen XDM Business Opportunity.

![Använd skiftlägessegment](./assets/b2b-tutorial/use-case-segment.png)

>[!NOTE]
> 
>Instruktioner om hur du skapar målgrupper för att utvärdera dina data finns i [gränssnittshandboken för segmentbyggaren](../segmentation/ui/segment-builder.md). Mer specifika användningsexempel för B2B-segmentering finns i [segmenteringsöversikten för Real-Time CDP B2B edition](./segmentation/b2b.md).

Med Segment Builder kan ni skapa en marknadsföringsbar publik utifrån kundprofildata i realtid och visa uppskattningar av er presumtiva målgrupp baserat på den kombination av attribut, händelser och befintliga målgrupper som ni har definierat.

## Aktivera utvärderade data till ett mål

När målgruppen har skapats visas en sammanfattning i avsnittet [!UICONTROL Details] på arbetsytan. Eftersom inga destinationer för närvarande är aktiverade för segmentdefinitionen måste Bodea-marknadsföraren exportera målgruppen till en datauppsättning där den kan nås och hanteras.

I arbetsytan [!UICONTROL Segments] i Experience Platform-gränssnittet väljer Bodea-markören **[!UICONTROL Activate to destination]**.

![Aktivera målgruppen till ett mål](./assets/b2b-tutorial/activate-to-destination.png)

>[!NOTE]
> 
>I självstudiekursen [Aktivera en målgrupp till ett mål](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=sv-SE) finns mer information om hur du slutför det här.

Bodea-marknadsföraren aktiverar målgruppen till Marketo-destinationen, vilket gör att de kan skicka målgruppsdata från Experience Platform till Marketo Engage i form av en statisk lista. Mer information finns i guiden för [Marketo-målet](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/adobe/marketo-engage.html?lang=sv-SE).

## Nästa steg

Genom att följa den här självstudiekursen har du lyckats utnyttja de olika Adobe Experience Platform-tjänster som används av Real-Time CDP B2B edition. Därför har ni lärt er att importera, segmentera, utvärdera och exportera era B2B-data som användbara målgrupper som kan engageras i olika kanaler.
