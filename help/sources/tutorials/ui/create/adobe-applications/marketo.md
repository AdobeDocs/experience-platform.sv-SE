---
keywords: Experience Platform;hem;populära ämnen;Marketo-källanslutning;Marketo-kontakt;Marketo-källa;Marketo
solution: Experience Platform
title: Skapa en Marketo Engage-källanslutning i användargränssnittet
topic-legacy: overview
type: Tutorial
description: I den här självstudiekursen beskrivs hur du skapar en koppling från Marketo Engage-källa i användargränssnittet för att hämta B2B-data till Adobe Experience Platform.
exl-id: a6aa596b-9cfa-491e-86cb-bd948fb561a8
source-git-commit: 9c8b63bf577a4258a7ef87c11bc8f87c1a01cc20
workflow-type: tm+mt
source-wordcount: '1272'
ht-degree: 0%

---

# Skapa en [!DNL Marketo Engage]-källkoppling i användargränssnittet

I den här självstudiekursen beskrivs hur du skapar en [!DNL Marketo Engage]-källkoppling (kallas nedan &quot;[!DNL Marketo]&quot;) i användargränssnittet för att hämta B2B-data till Adobe Experience Platform.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Experience Data Model (XDM)](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Skapa och redigera scheman i användargränssnittet](../../../../../xdm/ui/resources/schemas.md): Lär dig hur du skapar och redigerar scheman i användargränssnittet.
* [Identitetsnamnutrymmen](../../../../../identity-service/namespaces.md): Identitetsnamnutrymmen är en komponent i  [!DNL Identity Service] som fungerar som indikatorer för det sammanhang som en identitet relateras till. En fullständigt kvalificerad identitet innehåller ett ID-värde och ett namnutrymme.
* [[!DNL Real-time Customer Profile]](/help/profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till ditt [!DNL Marketo]-konto på Platform måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `munchkinId` | Munchkin-ID är den unika identifieraren för en specifik [!DNL Marketo]-instans. |
| `clientId` | Det unika klient-ID:t för din [!DNL Marketo]-instans. |
| `clientSecret` | Den unika klienthemligheten för din [!DNL Marketo]-instans. |

Mer information om hur du hämtar dessa värden finns i [[!DNL Marketo] autentiseringsguiden](../../../../connectors/adobe-applications/marketo/marketo-auth.md).

När du har samlat in dina inloggningsuppgifter kan du följa stegen i nästa avsnitt.

## Anslut ditt [!DNL Marketo]-konto

Välj **[!UICONTROL Sources]** i det vänstra navigeringsfältet i plattformsgränssnittet för att komma åt arbetsytan [!UICONTROL Sources]. Skärmen [!UICONTROL Catalog] visar en mängd olika källor som du kan skapa ett konto för.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också använda sökfältet till att hitta den källa du vill arbeta med.

Välj **[!UICONTROL Marketo Engage]** under kategorin [!UICONTROL Adobe applications]. Välj sedan **[!UICONTROL Add data]** för att skapa ett nytt [!DNL Marketo]-dataflöde.

![katalog](../../../../images/tutorials/create/marketo/catalog.png)

Sidan **[!UICONTROL Connect to Marketo Engage]** visas. På den här sidan kan du antingen använda ett nytt konto eller komma åt ett befintligt konto.

### Nytt konto

Om du skapar ett nytt konto väljer du **[!UICONTROL New account]**. Ange ett kontonamn, en valfri beskrivning och inloggningsuppgifterna för [!DNL Marketo] i det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![nytt konto](../../../../images/tutorials/create/marketo/new.png)

### Befintligt konto

Om du vill skapa ett dataflöde med ett befintligt konto väljer du **[!UICONTROL Existing account]** och sedan det [!DNL Marketo]-konto som du vill använda. Välj **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/marketo/existing.png)

## Välj en datauppsättning

När du har skapat ditt [!DNL Marketo]-konto får du i nästa steg ett gränssnitt där du kan utforska [!DNL Marketo]-datauppsättningar.

Den vänstra halvan av gränssnittet är en katalogwebbläsare som visar datauppsättningarna 10 [!DNL Marketo]. En fullt fungerande [!DNL Marketo]-källanslutning kräver att de nio olika datauppsättningarna matas in. Om du även använder kontobaserad marknadsföring [!DNL Marketo] (ABM) måste du också skapa ett 10:e dataflöde för att kunna importera [!UICONTROL Named Accounts]-datauppsättningen.

>[!NOTE]
>
>I följande självstudiekurs används [!UICONTROL Named Accounts] som exempel, men stegen som beskrivs nedan gäller för alla datauppsättningar om 10 [!DNL Marketo].

Markera den datauppsättning som du vill importera först och välj sedan **[!UICONTROL Next]**.

![select-data](../../../../images/tutorials/create/marketo/select-data.png)

## Mappa [!DNL Marketo]-scheman till plattformen

[!UICONTROL Mapping]-steget visas och innehåller ett gränssnitt för att mappa [!DNL Marketo]-scheman till plattformen.

Välj en datauppsättning för inkommande data som ska importeras till. Du kan antingen använda en befintlig datauppsättning eller skapa en ny datauppsättning.

### Använd en befintlig datauppsättning

Om du vill importera data till en befintlig datauppsättning väljer du **[!UICONTROL Existing dataset]** och sedan datamängdikonen.

![befintlig datamängd](../../../../images/tutorials/create/marketo/existing-dataset.png)

Dialogrutan **[!UICONTROL Select dataset]** visas. Hitta datauppsättningen med rätt schema som du vill använda, markera den och välj sedan **[!UICONTROL Confirm]**.

![select-existing-dataset](../../../../images/tutorials/create/marketo/select-dataset.png)

### Använd en ny datauppsättning

Om du vill importera data till en ny datauppsättning väljer du **[!UICONTROL New dataset]** och anger ett namn och en beskrivning för datauppsättningen i de angivna fälten.

Du kan söka efter ett schema genom att ange dess namn i sökfältet **[!UICONTROL Select schema]**. Du kan också välja listruteikonen för att visa en lista över befintliga scheman. Du kan också välja **[!UICONTROL Advanced search]** om du vill komma åt sidan med befintliga scheman, inklusive deras respektive information.

Aktivera måldatauppsättningen för **[!UICONTROL Profile dataset]** för [!DNL Profile] genom att växla på knappen , så att du kan skapa en helhetsbild av en enhets attribut och beteenden. Data från alla [!DNL Profile]-aktiverade datauppsättningar inkluderas i [!DNL Profile] och ändringarna tillämpas när du sparar dataflödet.

![create-new-dataset](../../../../images/tutorials/create/marketo/new-dataset-schema.png)

När du har valt ett schema bläddrar du nedåt för att visa mappningsdialogrutan för att börja mappa dina [!DNL Marketo]-datamängdsfält till rätt mål-XDM-fält.

### Mappa dina [!DNL Marketo]-datakällfält till mål-XDM-fält

Varje [!DNL Marketo]-datauppsättning har sina egna specifika mappningsregler att följa. Mer information om hur du mappar [!DNL Marketo]-datauppsättningar till XDM finns i följande:

* [Aktiviteter](../../../../connectors/adobe-applications/mapping/marketo.md#activities)
* [Program](../../../../connectors/adobe-applications/mapping/marketo.md#programs)
* [Programmedlemskap](../../../../connectors/adobe-applications/mapping/marketo.md#program-memberships)
* [Företag](../../../../connectors/adobe-applications/mapping/marketo.md#companies)
* [Statiska listor](../../../../connectors/adobe-applications/mapping/marketo.md#static-lists)
* [Statiska listmedlemskap](../../../../connectors/adobe-applications/mapping/marketo.md#static-list-memberships)
* [Namngivna konton](../../../../connectors/adobe-applications/mapping/marketo.md#named-accounts)
* [Möjligheter](../../../../connectors/adobe-applications/mapping/marketo.md#opportunities)
* [Kontaktroller för affärsmöjlighet](../../../../connectors/adobe-applications/mapping/marketo.md#opportunity-contact-roles)
* [Personer](../../../../connectors/adobe-applications/mapping/marketo.md#persons)

Välj **[!UICONTROL Preview data]** om du vill visa mappningsresultat baserat på den valda datauppsättningen.

![mappning](../../../../images/tutorials/create/marketo/mapping.png)

Med [!UICONTROL Preview]-porten kan du utforska mappningsresultat på upp till 100 rader med exempeldata från den valda datauppsättningen.

![förhandsgranska](../../../../images/tutorials/create/marketo/mapping-preview.png)

När källfälten har mappats till rätt målfält väljer du **[!UICONTROL Close]**.

## Ange information om dataflöde

Steget [!UICONTROL Dataflow detail] visas så att du kan ange ett namn och en kort beskrivning av det nya dataflödet.

![dataflöde-detail](../../../../images/tutorials/create/marketo/dataflow-detail.png)

Aktivera växeln **[!UICONTROL Error diagnostics]** för att tillåta detaljerad generering av felmeddelanden för nyligen importerade batchar, som du kan hämta med API:t. Mer information finns i självstudiekursen om att [hämta feldiagnos för datainmatningsfel](../../../../../ingestion/quality/error-diagnostics.md).

![fel](../../../../images/tutorials/create/marketo/errors.png)

[!DNL Marketo]-anslutningen använder batchinmatning för att importera alla historikposter och använder direktuppspelningsinmatning för realtidsuppdateringar. Detta gör att anslutaren kan fortsätta direktuppspelningen samtidigt som felaktiga poster hämtas. Aktivera växlingsknappen **[!UICONTROL Partial ingestion]** och ställ sedan in [!UICONTROL Error threshold %] på maximum för att förhindra att dataflödet misslyckas.

**[!UICONTROL Partial ingestion]** ger möjlighet att importera data som innehåller fel upp till ett visst tröskelvärde. Mer information finns i [översikten över partiell gruppöverföring](../../../../../ingestion/batch-ingestion/partial.md).

När du har angett dataflödesinformationen och angett feltröskelvärdet som max väljer du **[!UICONTROL Next]**.

![partiellt intag](../../../../images/tutorials/create/marketo/partial-ingestion.png)

## Granska ditt dataflöde

**[!UICONTROL Review]**-steget visas, så att du kan granska det nya dataflödet innan det skapas. Informationen är grupperad i följande kategorier:

* **[!UICONTROL Connection]**: Visar källtypen, den relevanta sökvägen för den valda källentiteten och mängden kolumner i källentiteten.
* **[!UICONTROL Assign dataset & map fields]**: Visar vilken datauppsättning källdata hämtas till, inklusive det schema som datauppsättningen följer.

När du har granskat dataflödet väljer du **[!UICONTROL Finish]** och anger en tid innan dataflödet skapas.

![recension](../../../../images/tutorials/create/marketo/review.png)

## Övervaka dataflödet

När dataflödet har skapats kan du övervaka de data som importeras genom det för att se information om hur mycket data som har intagits, hur bra de är och vilka fel som har uppstått. Mer information om hur du övervakar dataflöden finns i självstudiekursen om [övervakning av dataflöden i användargränssnittet](../../../../../dataflows/ui/monitor-sources.md).

## Ta bort dina attribut

Anpassade attribut i datauppsättningar kan inte döljas eller tas bort retroaktivt. Om du vill dölja eller ta bort ett anpassat attribut från en befintlig datauppsättning måste du skapa en ny datauppsättning utan det här anpassade attributet, ett nytt XDM-schema och konfigurera ett nytt dataflöde för den nya datauppsättningen som du skapar. Du måste också inaktivera eller ta bort det ursprungliga dataflöde som består av datauppsättningen med det anpassade attribut som du vill dölja eller ta bort.

## Ta bort ditt dataflöde

Du kan ta bort dataflöden som inte längre är nödvändiga eller som har skapats felaktigt med funktionen **[!UICONTROL Delete]** som finns på arbetsytan [!UICONTROL Dataflows]. Mer information om hur du tar bort dataflöden finns i självstudiekursen om att [ta bort dataflöden i användargränssnittet](../../delete.md).

## Nästa steg

Genom att följa den här självstudiekursen har du skapat ett dataflöde som hämtar in [!DNL Marketo]-data. Inkommande data kan nu användas av plattformstjänster längre fram i kedjan, t.ex. [!DNL Real-time Customer Profile] och [!DNL Data Science Workspace]. Mer information finns i följande dokument:

* [[!DNL Real-time Customer Profile] översikt](/help/profile/home.md)
* [[!DNL Data Science Workspace] översikt](/help/data-science-workspace/home.md)
