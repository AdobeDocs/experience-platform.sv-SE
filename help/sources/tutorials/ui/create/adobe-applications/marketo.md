---
title: Skapa en Marketo Engage-källanslutning och ett dataflöde i användargränssnittet
description: I den här självstudiekursen beskrivs hur du skapar en källanslutning och ett dataflöde i Marketo Engage i användargränssnittet för att hämta B2B-data till Adobe Experience Platform.
exl-id: a6aa596b-9cfa-491e-86cb-bd948fb561a8
source-git-commit: 744098777141c61ac27fe6f150c05469d5705dee
workflow-type: tm+mt
source-wordcount: '1766'
ht-degree: 0%

---

# Skapa en [!DNL Marketo Engage] källanslutning och dataflöde i användargränssnittet

>[!IMPORTANT]
>
>Innan du skapar [!DNL Marketo Engage] källanslutning och ett dataflöde måste du först se till att du har [mappade ditt organisations-ID i Adobe](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html) in [!DNL Marketo]. Dessutom måste du se till att du har slutfört [automatiskt fylla i [!DNL Marketo] B2B-namnutrymmen och scheman](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md) innan du skapar en källanslutning och ett dataflöde.

Den här självstudiekursen innehåller steg för att skapa en [!DNL Marketo Engage] (nedan kallad[!DNL Marketo]&quot;) i användargränssnittet för att hämta B2B-data till Adobe Experience Platform.

## Kom igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [B2B-namnutrymmen och automatisk schemagenerering](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md): Med B2B-namnutrymmen och automatisk schemagenerering kan du använda [!DNL Postman] för att automatiskt generera värden för B2B-namnutrymmen och scheman. Du måste fylla i B2B-namnutrymmen och scheman innan du skapar en [!DNL Marketo] källanslutning och dataflöde.
* [Källor](../../../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Experience Data Model (XDM)](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Skapa och redigera scheman i användargränssnittet](../../../../../xdm/ui/resources/schemas.md): Lär dig hur du skapar och redigerar scheman i gränssnittet.
* [Identitetsnamnutrymmen](../../../../../identity-service/features/namespaces.md): Identitetsnamnutrymmen är en komponent i [!DNL Identity Service] som fungerar som indikatorer för det sammanhang som en identitet hör till. En fullständigt kvalificerad identitet innehåller ett ID-värde och ett namnutrymme.
* [[!DNL Real-Time Customer Profile]](/help/profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till [!DNL Marketo] på Experience Platform måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---- | ---- |
| `munchkinId` | Munchkin-ID är den unika identifieraren för en specifik [!DNL Marketo] -instans. |
| `clientId` | Ditt unika klient-ID [!DNL Marketo] -instans. |
| `clientSecret` | Den unika klienthemligheten hos [!DNL Marketo] -instans. |

Mer information om hur du hämtar dessa värden finns i [[!DNL Marketo] autentiseringsguide](../../../../connectors/adobe-applications/marketo/marketo-auth.md).

När du har samlat in dina inloggningsuppgifter kan du följa stegen i nästa avsnitt.

## Koppla samman [!DNL Marketo] konto

Välj **[!UICONTROL Sources]** från vänster navigering för att komma åt [!UICONTROL Sources] arbetsyta. Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under *Adobe-program* kategori, välj **[!UICONTROL Marketo Engage]** och sedan markera **[!UICONTROL Add data]**.

>[!TIP]
>
>Källor i källkatalogen visas **[!UICONTROL Set up]** när en viss källa ännu inte har något autentiserat konto. När det finns ett autentiserat konto ändras det här alternativet till **[!UICONTROL Add data]**.

![Källkatalogen med Marketo Engage-källan markerad.](../../../../images/tutorials/create/marketo/catalog.png)

The **[!UICONTROL Connect Marketo Engage account]** visas. På den här sidan kan du antingen använda ett nytt konto eller komma åt ett befintligt konto.

>[!BEGINTABS]

>[!TAB Skapa ett nytt konto]

Om du vill skapa ett nytt konto väljer du **[!UICONTROL New account]** och ange ett namn, en valfri beskrivning och dina autentiseringsuppgifter.

När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![Det nya kontogränssnittet för autentisering av ett nytt Marketo-konto.](../../../../images/tutorials/create/marketo/new.png)

>[!TAB Använd ett befintligt konto]

Om du vill använda ett befintligt konto väljer du **[!UICONTROL Existing account]** och välj sedan det konto som du vill använda i den befintliga kontokatalogen.

Välj **[!UICONTROL Next]** för att fortsätta.

![Det befintliga kontogränssnittet där du kan välja ett befintligt Marketo-konto.](../../../../images/tutorials/create/marketo/existing.png)

>[!ENDTABS]

## Välj en datauppsättning

När du har skapat [!DNL Marketo] kommer nästa steg att ge dig ett gränssnitt att utforska [!DNL Marketo] datauppsättningar.

Den vänstra halvan av gränssnittet är en katalogwebbläsare som visar de 10 [!DNL Marketo] datauppsättningar. En fullt fungerande [!DNL Marketo] källanslutningen kräver att de nio olika datauppsättningarna matas in. Om du även använder [!DNL Marketo] kontobaserad marknadsföring (ABM) måste du också skapa ett 10:e dataflöde för att kunna importera [!UICONTROL Named Accounts] datauppsättning.

>[!NOTE]
>
>Följande självstudiekurser används för att arbeta snabbt [!UICONTROL Opportunities] som ett exempel, men stegen som beskrivs nedan gäller för någon av de 10 [!DNL Marketo] datauppsättningar.

Markera den datauppsättning som du vill importera. Detta uppdaterar gränssnittet så att en förhandsgranskning av datauppsättningen visas. När du är klar väljer du **[!UICONTROL Next]**.

![Gränssnittet för förhandsgranskning](../../../../images/tutorials/create/marketo/preview.png)

## Ange information om datauppsättning och dataflöde {#provide-dataset-and-dataflow-details}

Därefter måste du ange information om datauppsättningen och dataflödet.

### Information om datauppsättning {#dataset-details}

En datauppsättning är en lagrings- och hanteringskonstruktion för en datamängd, vanligtvis en tabell, som innehåller ett schema (kolumner) och fält (rader). Data som har inhämtats till Experience Platform lagras i datasjön som datauppsättningar. Under det här steget kan du skapa en ny datauppsättning eller använda en befintlig datauppsättning.

>[!BEGINTABS]

>[!TAB Använd en ny datauppsättning]

Om du vill använda en ny datauppsättning väljer du **[!UICONTROL New dataset]** och ange sedan ett namn och en valfri beskrivning av datauppsättningen. Du måste också välja ett XDM-schema (Experience Data Model) som datauppsättningen följer.

![Det nya gränssnittet för val av datauppsättning.](../../../../images/tutorials/create/marketo/new-dataset.png)

>[!TAB Använd en befintlig datamängd]

Om du redan har en befintlig datauppsättning väljer du **[!UICONTROL Existing dataset]** och sedan använda **[!UICONTROL Advanced search]** om du vill visa ett fönster med alla datauppsättningar i organisationen, inklusive deras respektive information, t.ex. om de är aktiverade för förtäring i kundprofilen i realtid eller inte.

![Det befintliga gränssnittet för val av datauppsättning.](../../../../images/tutorials/create/marketo/existing-dataset.png)

>[!ENDTABS]

### Dataflödeskonfigurationer {#dataflow-configurations}

>[!IMPORTANT]
>
>The [!DNL Marketo] I källan används batchinmatning för att importera alla historikposter och direktuppspelning används för realtidsuppdateringar. Detta gör att källan kan fortsätta direktuppspelningen samtidigt som felaktiga poster hämtas. Aktivera **[!UICONTROL Partial ingestion]** växla och ange sedan [!UICONTROL Error threshold %] till maximum för att förhindra att dataflödet misslyckas.

Om din datauppsättning är aktiverad för kundprofil i realtid kan du under det här steget växla **[!UICONTROL Profile dataset]** för att aktivera data för profilinmatning. Du kan även använda det här steget för att aktivera **[!UICONTROL Error diagnostics]** och **[!UICONTROL Partial ingestion]**.

* **[!UICONTROL Error diagnostics]**: Välj **[!UICONTROL Error diagnostics]** för att instruera källan att skapa feldiagnostik som du senare kan referera till när du övervakar datauppsättningsaktiviteten och dataflödesstatusen.
* **[!UICONTROL Partial ingestion]**: [Partiellt batchintag](../../../../../ingestion/batch-ingestion/partial.md) är möjligheten att importera data som innehåller fel, upp till ett visst konfigurerbart tröskelvärde. Med den här funktionen kan du importera alla korrekta data till Experience Platform, medan alla felaktiga data batchas separat med information om varför de är ogiltiga.

Under det här steget kan du aktivera **[!UICONTROL Sample dataflow]** för att begränsa inmatningen av data och undvika extrakostnader som uppstår vid inmatning av alla historiska data, inklusive personidentiteter.

>[!BEGINSHADEBOX]

**Snabbguide om hur du använder exempeldataflöde**

Exempeldataflöde är en konfiguration som du kan ställa in för din [!DNL Marketo] dataflöde för att begränsa ditt intag och sedan prova Experience Platform-funktioner utan att behöva importera stora mängder data.

* Aktivera exempeldataflöde för att begränsa historiska data genom att importera upp till 100 kB (från det största post-ID:t) eller upp till de sista 10 dagarna i aktivitet under backfill-jobbet.
* När du använder exempeldataflödeskonfigurationen för alla B2B-entiteter måste du tänka på att det är möjligt att vissa relaterade poster saknas eftersom hela källdatahistoriken inte hämtas.

>[!ENDSHADEBOX]

![Avsnittet med dataflödeskonfigurationer på informationssidan för dataflöde.](../../../../images/tutorials/create/marketo/dataflow-configurations.png)

Om du dessutom hämtar data från företagsdatauppsättningen kan du aktivera **[!UICONTROL Exclude unclaimed accounts]** för att exkludera ej ianspråktagna konton från förtäring.

När enskilda fyller i ett formulär, [!DNL Marketo] skapar en post för ett skenkonto baserat på företagsnamnet som inte innehåller några andra data. För nya dataflöden är alternativet för att exkludera ej ianspråktagna konton aktiverat som standard. För befintliga dataflöden kan du aktivera eller inaktivera funktionen, med ändringar som gäller för nyinmatade data och inte befintliga data.

![Exkludera ej begärda konton](../../../../images/tutorials/create/marketo/unclaimed-accounts.png)

## Kartlägg [!DNL Marketo] datakällfält för mål-XDM-fält

The [!UICONTROL Mapping] visas med ett gränssnitt för att mappa källfälten från källschemat till rätt mål-XDM-fält i målschemat.

Varje [!DNL Marketo] datauppsättningen har sina egna specifika mappningsregler att följa. Se följande för mer information om hur du mappar [!DNL Marketo] datauppsättningar till XDM:

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

Beroende på dina behov kan du välja att mappa fält direkt eller använda förinställningsfunktioner för data för att omvandla källdata för att härleda beräknade eller beräknade värden. Mer information om hur du använder mappningsgränssnittet finns i [Användargränssnittsguide för dataprep](../../../../../data-prep/ui/mapping.md).

![Mappningsgränssnittet för Marketo-data.](../../../../images/tutorials/create/marketo/mapping.png)

När mappningsuppsättningarna är klara väljer du **[!UICONTROL Next]** och kan ta en stund innan det nya dataflödet skapas.

## Granska ditt dataflöde

The **[!UICONTROL Review]** visas så att du kan granska det nya dataflödet innan det skapas. Informationen är grupperad i följande kategorier:

* **[!UICONTROL Connection]**: Visar källtypen, den relevanta sökvägen för den valda källentiteten och mängden kolumner i källentiteten.
* **[!UICONTROL Assign dataset & map fields]**: Visar vilken datauppsättning källdata hämtas till, inklusive det schema som datauppsättningen följer.

När du har granskat dataflödet väljer du **[!UICONTROL Save & ingest]** så att dataflödet kan skapas.

![Granskningssidan där du kan bekräfta information om dataflödet före intag.](../../../../images/tutorials/create/marketo/review.png)

## Övervaka dataflödet

När dataflödet har skapats kan du övervaka de data som importeras genom det för att se information om hur mycket data som har intagits, hur bra de är och vilka fel som har uppstått. Mer information om hur du övervakar dataflöden finns i självstudiekursen om [övervaka dataflöden i användargränssnittet](../../../../../dataflows/ui/monitor-sources.md).

## Ta bort dina attribut

Anpassade attribut i datauppsättningar kan inte döljas eller tas bort retroaktivt. Om du vill dölja eller ta bort ett anpassat attribut från en befintlig datauppsättning måste du skapa en ny datauppsättning utan det här anpassade attributet, ett nytt XDM-schema och konfigurera ett nytt dataflöde för den nya datauppsättningen som du skapar. Du måste också inaktivera eller ta bort det ursprungliga dataflöde som består av datauppsättningen med det anpassade attribut som du vill dölja eller ta bort.

## Ta bort ditt dataflöde

Du kan ta bort dataflöden som inte längre är nödvändiga eller som har skapats felaktigt med **[!UICONTROL Delete]** finns i [!UICONTROL Dataflows] arbetsyta. Mer information om hur du tar bort dataflöden finns i självstudiekursen om [ta bort dataflöden i användargränssnittet](../../delete.md).

## Nästa steg

Genom att följa den här självstudiekursen har du skapat ett dataflöde där du kan importera B2B-data från [!DNL Marketo Engage] källa till Experience Platform.

## Bilaga {#appendix}

Följande avsnitt innehåller ytterligare riktlinjer som du kan följa när du använder [!DNL Marketo] källa.

### Felmeddelanden i användargränssnittet {#error-messages}

Följande felmeddelanden visas i användargränssnittet när Platform upptäcker problem med konfigurationen:

#### [!DNL Munchkin ID] är inte mappad till rätt organisation

Autentisering nekas om din [!DNL Munchkin ID] är inte mappad till den plattformsorganisation som du använder. Konfigurera mappningen mellan [!DNL Munchkin ID] och din organisation med [[!DNL Marketo] gränssnitt](https://app-sjint.marketo.com/#MM0A1).

![Ett felmeddelande som visar att Marketo-instansen inte är korrekt mappad till organisationen Adobe.](../../../../images/tutorials/create/marketo/munchkin-not-mapped.png)

#### Primär identitet saknas

Ett dataflöde kan inte sparas och importeras om en primär identitet saknas. Se till att [en primär identitet finns i XDM-schemat](../../../../../xdm/tutorials/create-schema-ui.md)innan du försöker konfigurera ett dataflöde.

![Ett felmeddelande som visar att den primära identiteten saknas i XDM-schemat.](../../../../images/tutorials/create/marketo/no-primary-identity.png)

