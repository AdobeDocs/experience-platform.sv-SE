---
title: Ansluta Oracle Eloqua (V2) till Experience Platform i användargränssnittet
description: Lär dig hur du ansluter ditt Oracle Eloqua-konto till Experience Platform i användargränssnittet.
source-git-commit: 180754969d4ae8dbd1308dfc85dae73baf64f759
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 0%

---

# Anslut [!DNL Oracle Eloqua] (V2) till Experience Platform i användargränssnittet

Med källkopplingen [!DNL Oracle Eloqua (V2)] kan du koppla ditt Oracle Eloqua-konto till Adobe Experience Platform, vilket möjliggör automatiserat och skalbart inmatning av viktiga B2B-marknadsföringsdata, inklusive kontakter, konton, kampanjer och engagemangsaktiviteter.

Använd den här källkopplingen för att konfigurera säker autentisering, välj exakt de Eloqua-datatabeller du behöver och mappa dem till standardiserade XDM-scheman (Experience Data Model). Flexibla schemaläggningsalternativ gör att ni kan ställa in både initiala dataladdningar och återkommande stegvisa synkroniseringar, vilket säkerställer att era marknadsföringsdata är aktuella och användbara.

Källkopplingen [!DNL Oracle Eloqua (V2)] bygger på Adobe ramverk för företagsintag och är en tillförlitlig och utbyggbar grund för kampanjoptimering, prestandamätning och kanalövergripande personalisering.

Läs den här vägledningen när du vill lära dig hur du ansluter ditt [!DNL Oracle Eloqua]-konto till Adobe Experience Platform med hjälp av källarbetsytan i Experience Platform användargränssnitt.

## Kom igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

### Samla in nödvändiga inloggningsuppgifter {#credentials}

Läs [[!DNL Eloqua] översikten](../../../../connectors/marketing-automation/eloqua.md) om du vill ha information om autentisering.

## Navigera i källkatalogen {#catalog}

I Experience Platform-gränssnittet väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i *[!UICONTROL Sources]*. Välj en kategori eller använd sökfältet för att hitta källan.

Om du vill ansluta till [!DNL Eloqua] går du till kategorin *[!UICONTROL Marketing Automation]*, markerar **[!UICONTROL (V2) Oracle Eloqua]**-källkortet och väljer **[!UICONTROL Set up]**.

>[!TIP]
>
>Källor i källkatalogen visar alternativet **[!UICONTROL Set up]** när en angiven källa ännu inte har något autentiserat konto. När ett autentiserat konto har skapats ändras alternativet till **[!UICONTROL Add data]**.

![Källkortet Eloqua i källkatalogen med knappen Konfigurera markerad.](../../../../images/tutorials/create/eloqua/catalog.png)

## Använd ett befintligt konto {#existing}

Om du vill använda ett befintligt konto väljer du **[!UICONTROL Existing account]** och sedan det [!DNL Eloqua]-konto som du vill använda.

![Alternativet Befintligt konto har valts i gränssnittet för att skapa kontot.](../../../../images/tutorials/create/eloqua/existing.png)

## Skapa ett nytt konto {#new}

Om du vill skapa ett nytt konto väljer du **[!UICONTROL New account]** och anger ett namn och en beskrivning under [!UICONTROL Source connection details]. Under [!UICONTROL Account authentication] anger du sedan värden för ditt **klient-ID**, **klienthemlighet**, **användarnamn**, **lösenord** och **basslutpunkt**. Du kan läsa [autentiseringsguiden](../../../../connectors/marketing-automation/eloqua.md) om du vill ha mer information om dessa autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt några sekunder för att upprätta anslutningen.

![Det nya kontogränssnittet med fält för källanslutningsinformation och autentiseringsuppgifter.](../../../../images/tutorials/create/eloqua/new.png)

## Markera data

Använd datagränssnittet för att välja den [!DNL Eloqua]-entitet som du vill importera till Experience Platform.

>[!TIP]
>
>När du väljer data kommer du att lägga märke till att de andra enheterna, förutom för kampanjer, visar representativa exempeldata. Med den här metoden kan du förhandsgranska tillgängliga fält och strukturer eftersom [!DNL Eloqua] publika API:er för närvarande bara hämtar verkliga data för kampanjer. För de återstående enheterna anges exempeldata som stöd för ditt konfigurationsarbetsflöde.

![Gränssnittet för dataurval visar tillgängliga Eloqua-datatabeller.](../../../../images/tutorials/create/eloqua/select-data.png)

## Information om datauppsättning och dataflöde {#details}

Därefter måste du ange information om datauppsättningen och dataflödet. Under det här steget kan du antingen använda en befintlig datauppsättning eller skapa en ny datauppsättning. Dessutom kan du välja att aktivera datauppsättningen för inmatning till kundprofilen i realtid under det här steget.

![Gränssnittet för datauppsättningar och dataflöden med alternativ för att konfigurera datauppsättningsegenskaper.](../../../../images/tutorials/create/eloqua/details.png)

## Mappning {#mapping}

Mappningar för [!DNL Eloqua] är ordnade i fyra huvudentitetstyper:

* **Konton** - Företags-/organisationsposter från [!DNL Eloqua].
* **Aktiviteter** - Marknadsföringsaktivitet och engagemangshändelser från [!DNL Eloqua].
* **Kampanjer** - marknadsföringskampanjposter från [!DNL Eloqua].
* **Kontakter** - Individuella personposter från [!DNL Eloqua].

Om du behöver åtkomst till extrafält utöver de som anges som standard, kan du lägga till dessa fält med hjälp av datapersonmappningsprocessen i Experience Platform. Om standardschemat (standard) inte har stöd för vissa av dina obligatoriska fält kan du definiera ett anpassat schema i Experience Platform. Använd den här funktionen för att skapa och mappa de nödvändiga fälten så att du kan importera alla relevanta data från [!DNL Eloqua] till Experience Platform.

Sammanfattning av nästa steg:

* Granska standardmappade fält som är tillgängliga med integreringen.
* Inkludera eventuella ytterligare fält som behövs från [!DNL Eloqua] under mappningssteget.
* Om det inte finns några nya fält i standardschemat kan du utöka eller skapa ett anpassat schema i Experience Platform som innehåller dessa fält.
* Slutför mappningen för att säkerställa att alla önskade data är inkapslade.

Om du vill vara säker på att din externa CRM-information återspeglas korrekt använder du funktionen för beräknat fält i Dataprep för att uppdatera platshållaren `{CRM_INSTANCE_ID}` med ditt specifika CRM-instans-ID i källdatafältet. Detta ger er flexibilitet att skräddarsy integreringen efter organisationens unika inställningar.

Om du vill använda redigeraren för beräknat fält markerar du det källfält som du vill uppdatera.

![Eloqua-källfältet med beräknade fält.](../../../../images/tutorials/create/eloqua/select-calculated-field.png)

>[!BEGINTABS]

>[!TAB Salesforce]

För [!DNL Salesforce]-användare använder du redigeraren för beräknat fält och uppdaterar `{CRM_INSTANCE_ID}` med rätt instans-ID.

![Det beräknade fältet för Salesforce.](../../../../images/tutorials/create/eloqua/sf-field.png)

>[!TAB Microsoft Dynamics]

För [!DNL Microsoft]-användare använder du redigeraren för beräknat fält och uppdaterar `{CRM_INSTANCE_ID}` med rätt instans-ID.

![Det beräknade fältet för Dynamics.](../../../../images/tutorials/create/eloqua/dynamics-field.png)

>[!ENDTABS]

När du har uppdaterat dina beräknade fält väljer du **[!UICONTROL Next]** för att fortsätta.

![Mappningsgränssnittet som visar fältmappningar för Eloqua-datatentiteter.](../../../../images/tutorials/create/eloqua/mapping.png)

## Schemaläggning

>[!NOTE]
>
>Följande deltafält används internt för inkrementell datainläsning:
>
>* **Kontakter:** `C_DateModified`
>* **Konton:** `M_DateModified`
>* **Aktivitet:** `CreatedAt`
>* **Egna objekt:** `UpdatedAt`
>* **Kampanj:** `updatedAt`

När mappningen är klar kan du nu konfigurera ett intag-schema för ditt dataflöde. Ange [!UICONTROL Frequency] till `Once` för att konfigurera en engångsinmatning. För inkrementellt intag kan du ange [!UICONTROL Frequency] till `Hour`, `Day` eller `Week`. När du använder inkrementellt intag måste du även konfigurera [!UICONTROL Interval] för att definiera hur lång tid som ska gå mellan att ha intagit. En matningsfrekvens som till exempel är inställd på `Day` och ett intervall på `15` innebär att dataflödet är schemalagt att importera data var 15:e dag.

Inmatningsfrekvensen per minut är inte tillgänglig för källan [!DNL Eloqua]. Det vanligaste schemat du kan välja är timvis. Välj ett schema som matchar dina behov av aktuell information. Tänk på att beräkningskostnaderna kommer att öka om du väljer ett mer frekvent schema.

![Planeringsgränssnittet med alternativ för att konfigurera matningsfrekvens och -intervall.](../../../../images/tutorials/create/eloqua/scheduling.png)

## Granska

Använd [!UICONTROL Review]-gränssnittet för att bekräfta informationen om dataflödet när du har konfigurerat matningsschemat. Välj **[!UICONTROL Finish]** om du vill slutföra konfigurationen och vänta tills dataflödet har startat.

![Granskningsgränssnittet visar en sammanfattning av dataflödeskonfigurationen innan den slutförs.](../../../../images/tutorials/create/eloqua/review.png)

## Övervaka

När dataflödet är markerat görs en engångsåterfyllning av data och efterföljande stegvis synkronisering enligt det angivna schemat. Synkstatus kan övervakas genom att navigera till dataflödet. Mer information finns i guiden om [att övervaka källans dataflöden i användargränssnittet](../../../../../dataflows/ui/monitor-sources.md).

## Nästa steg

Du har nu slutfört konfigurationen och konfigurationen av din [!DNL Eloqua]-källa i Experience Platform. När ditt dataflöde är etablerat kommer dina [!DNL Eloqua]-data att importeras enligt ditt valda schema och mappas till XDM-scheman (Standard Experience Data Model). Fortsätt övervaka era dataflöden och utforska era inkapslade data inom Platform för att få insikter och aktivera era användningsfall inom marknadsföring. Om du vill ha mer avancerade konfigurationer och felsökning läser du i den relaterade dokumentationen eller kontaktar Adobe supportresurser.

Mer information finns i följande dokumentation:

* [Översikt över källor](../../../../home.md)
* [Real-Time CDP B2B Edition](../../../../../rtcdp/b2b-overview.md)
