---
title: Anslut ditt Salesforce Marketing Cloud-konto (v2) till Experience Platform via gränssnittet
description: Lär dig hur du ansluter ditt Salesforce Marketing Cloud-konto (V2) till Experience Platform via användargränssnittet.
source-git-commit: 91bf8bf6e6f7030574d693484ce9797800c2d5dd
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# Anslut [!DNL Salesforce Marketing Cloud] till Experience Platform

Läs den här vägledningen när du vill lära dig hur du ansluter ditt [!DNL Salesforce Marketing Cloud]-konto till Adobe Experience Platform med hjälp av källarbetsytan i Experience Platform användargränssnitt.

## Kom igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata med.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

### Samla in nödvändiga inloggningsuppgifter

Läs [[!DNL Salesforce Marketing Cloud] översikten](../../../../connectors/marketing-automation/sfmc.md#prerequisites) om du vill ha information om autentisering.

## Navigera i källkatalogen

I Experience Platform-gränssnittet väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i *[!UICONTROL Sources]*. Välj en kategori eller använd sökfältet för att hitta källan.

Om du vill ansluta till [!DNL Salesforce Marketing Cloud] går du till kategorin *[!UICONTROL Marketing Automation]*, markerar **[!UICONTROL (V2) Salesforce Marketing Cloud]**-källkortet och väljer **[!UICONTROL Set up]**.

>[!TIP]
>
>Källor i källkatalogen visar alternativet **[!UICONTROL Set up]** när en angiven källa ännu inte har något autentiserat konto. När ett autentiserat konto har skapats ändras alternativet till **[!UICONTROL Add data]**.

![Källkatalogen med Salesforce Marketing Cloud-källan vald.](../../../../images/tutorials/create/sfmc/catalog.png)

## Använd ett befintligt konto {#existing}

Om du vill använda ett befintligt konto väljer du **[!UICONTROL Existing account]** och sedan det [!DNL Salesforce Marketing Cloud]-konto som du vill använda.

![Det befintliga kontogränssnittet för källarbetsflödet](../../../../images/tutorials/create/sfmc/existing.png)

## Skapa ett nytt konto {#new}

Om du vill skapa ett nytt konto väljer du **[!UICONTROL New account]** och anger ett namn och en beskrivning under [!UICONTROL Source connection details]. Under [!UICONTROL Account authentication] anger du sedan värden för ditt **klient-ID**, **klienthemlighet** och **basslutpunkt**. Du kan läsa [autentiseringsguiden](../../../../connectors/marketing-automation/sfmc.md#gather-required-credentials) om du vill ha mer information om dessa autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt några sekunder för att upprätta anslutningen.

![Källarbetsflödets nya kontogränssnitt.](../../../../images/tutorials/create/sfmc/new.png)

## Markera data

Källan [!DNL Salesforce Marketing Cloud] stöder endast datainmatning från datatillägg från [!DNL Salesforce Marketing Cloud].

Använd gränssnittet [!UICONTROL Select data] för att välja det datatillägg som du vill importera från din [!DNL Salesforce Marketing Cloud]-instans. När du har valt datatillägget kan du använda förhandsgranskningspanelen för att bekräfta att datauppsättningen innehåller de förväntade fälten innan du fortsätter.

![Steg för val av data i källarbetsflödet](../../../../images/tutorials/create/sfmc/select-data.png)

## Information om datauppsättning och dataflöde

Därefter måste du ange information om datauppsättningen och dataflödet. Under det här steget kan du antingen använda en befintlig datauppsättning eller skapa en ny datauppsättning. Dessutom kan du välja att aktivera datauppsättningen för inmatning till kundprofilen i realtid under det här steget.

![Datamängd- och dataflödesinformationssteget i källarbetsflödet.](../../../../images/tutorials/create/sfmc/dataset-details.png)

## Mappning

I [!DNL Salesforce Marketing Cloud] betraktas inte datatillägg som standardobjekt. Därför finns det inga fördefinierade eller fasta mappningsfält till ett Experience Platform-schema. Medan Data Prep i Experience Platform utför en optimalt anpassad justering mellan källfält från [!DNL Salesforce Marketing Cloud] och XDM-schemat (target Experience Data Model), kan det fortfarande finnas fall där en manuell granskning eller justering krävs för att matcha omappade eller felaktiga fält.

![Mappningssteget för källarbetsflödet.](../../../../images/tutorials/create/sfmc/mapping.png)

## Schemalägg ett dataflöde

När mappningen är klar kan du nu konfigurera ett intag-schema för ditt dataflöde. Ange [!UICONTROL Frequency] till `Once` för att konfigurera en engångsinmatning. För inkrementellt intag kan du ange [!UICONTROL Frequency] till `Hour`, `Day` eller `Week`. När du använder inkrementellt intag måste du även konfigurera [!UICONTROL Interval] för att definiera hur lång tid som ska gå mellan att ha intagit. En matningsfrekvens som till exempel är inställd på `Day` och ett intervall på `15` innebär att dataflödet är schemalagt att importera data var 15:e dag.

>[!TIP]
>
> Inmatningsfrekvensen per minut är inte tillgänglig för källan [!DNL Salesforce Marketing Cloud]. Det vanligaste schemat du kan välja är timvis. Välj ett schema som matchar dina behov av aktuell information. Tänk på att beräkningskostnaderna kommer att öka om du väljer ett mer frekvent schema.

Du måste markera ett deltafält (datum/tid) i datauppsättningen för att kunna aktivera inkrementell synkronisering. Om datauppsättningen inte innehåller något lämpligt deltafält kan du inte skapa dataflödet.

![Schemaläggningssteget för källarbetsflödet.](../../../../images/tutorials/create/sfmc/schedule.png)

## Granska

Använd [!UICONTROL Review]-gränssnittet för att bekräfta informationen om dataflödet när du har konfigurerat matningsschemat. Välj **[!UICONTROL Finish]** om du vill slutföra konfigurationen och vänta tills dataflödet har startat.

![Granskningssteget för källarbetsflödet.](../../../../images/tutorials/create/sfmc/review.png)

## Övervaka

När dataflödet är markerat görs en engångsåterfyllning av data och efterföljande stegvis synkronisering enligt det angivna schemat. Synkstatus kan övervakas genom att navigera till dataflödet. Mer information finns i guiden om [att övervaka källans dataflöden i användargränssnittet](../../../../../dataflows/ui/monitor-sources.md).

## Nästa steg

Den här självstudiekursen vägledde dig genom att ansluta ditt [!DNL Salesforce Marketing Cloud] (V2)-konto till Experience Platform via användargränssnittet. Du lärde dig att välja eller skapa ett källkonto, ange nödvändiga autentiseringsuppgifter, välja datatillägg att importera, ange data- och dataflödesdetaljer, mappa dina data, konfigurera ett schema för datainhämtning och övervaka dina dataflöden. Genom att följa de här stegen har du integrerat dina [!DNL Salesforce Marketing Cloud]-data med Experience Platform för aktivering och analys.

Mer information finns i följande dokumentation:

* [Översikt över källor](../../../../home.md)
* [Real-Time CDP B2B Edition](../../../../../rtcdp/b2b-overview.md)

