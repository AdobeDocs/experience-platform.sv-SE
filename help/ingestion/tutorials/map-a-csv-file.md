---
keywords: Experience Platform;home;popular topics;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;
solution: Experience Platform
title: Mappa en CSV-fil till ett XDM-schema
topic: tutorial
type: Tutorial
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '1297'
ht-degree: 2%

---


# Mappa en CSV-fil till ett XDM-schema

För att kunna importera CSV-data till [!DNL Adobe Experience Platform]måste data mappas till ett [!DNL Experience Data Model] (XDM) schema. I den här självstudiekursen beskrivs hur du mappar en CSV-fil till ett XDM-schema med hjälp av [!DNL Platform] användargränssnittet.

I bilagan till den här självstudiekursen finns dessutom mer information om hur du använder [mappningsfunktioner](#mapping-functions).

## Komma igång

Den här självstudien kräver en fungerande förståelse av följande komponenter i [!DNL Platform]:

- [[!DNL Experience Data Model (XDM-system)]](../../xdm/home.md): Det standardiserade ramverket som [!DNL Platform] organiserar kundupplevelsedata.
- [[!DNL Batch-ingång]](../batch-ingestion/overview.md): Den metod som används för att [!DNL Platform] importera data från datafiler som användaren anger.

Den här självstudien kräver också att du redan har skapat en datauppsättning att importera dina CSV-data till. Anvisningar om hur du skapar en datauppsättning i användargränssnittet finns i [självstudiekursen](./ingest-batch-data.md)om dataimport.

## Välj ett mål

Logga in på [[!DNL Adobe Experience Platform]](https://platform.adobe.com) och välj sedan **[!UICONTROL Workflows]** i det vänstra navigeringsfältet för att komma åt **[!UICONTROL Workflows]** arbetsytan.

På **[!UICONTROL Workflows]** skärmen väljer du **[!UICONTROL Map CSV to XDM schema]** under **[!UICONTROL Data ingestion]** avsnittet och sedan **[!UICONTROL Launch]**.

![](../images/tutorials/map-a-csv-file/workflows.png)

Arbetsflödet **[!UICONTROL Map CSV to XDM schema]** visas med början på **[!UICONTROL Destination]** steget. Välj en datauppsättning för inkommande data som ska importeras till. Du kan antingen använda en befintlig datauppsättning eller skapa en ny.

**Använd en befintlig datauppsättning**

Om du vill importera dina CSV-data till en befintlig datauppsättning väljer du **[!UICONTROL Use existing dataset]**. Du kan antingen hämta en befintlig datauppsättning med sökfunktionen eller genom att bläddra igenom listan med befintliga datauppsättningar i panelen.

![](../images/tutorials/map-a-csv-file/use-existing-dataset.png)

Om du vill importera dina CSV-data till en ny datauppsättning markerar du **[!UICONTROL Create new dataset]** och anger ett namn och en beskrivning för datauppsättningen i fälten som anges. Välj ett schema med antingen sökfunktionen eller genom att bläddra igenom listan med scheman. Välj **[!UICONTROL Next]** att fortsätta.

![](../images/tutorials/map-a-csv-file/create-new-dataset.png)

## Lägg till data

Steget **[!UICONTROL Add data]** visas. Dra och släpp CSV-filen i det tillgängliga utrymmet, eller välj **[!UICONTROL Choose files]** om du vill ange CSV-filen manuellt.

![](../images/tutorials/map-a-csv-file/add-data.png)

Avsnittet visas när filen har överförts och visar de tio första dataraderna. **[!UICONTROL Sample data]** När du har bekräftat att data har överförts som förväntat väljer du **[!UICONTROL Next]**.

![](../images/tutorials/map-a-csv-file/sample-data.png)

## Mappa CSV-fält till XDM-schemafält

Steget **[!UICONTROL Mapping]** visas. Kolumnerna i CSV-filen listas under **[!UICONTROL Source Field]**, med motsvarande XDM-schemafält listade under **[!UICONTROL Target Field]**. Omarkerade målfält markeras med röda konturer. Du kan använda filterfältalternativet för att begränsa listan med tillgängliga källfält.

>[!TIP]
>
>[!DNL Platform] innehåller intelligenta rekommendationer för automatiskt mappade fält baserat på det målschema eller den datamängd som du har valt. Du kan justera mappningsreglerna manuellt så att de passar dina användningsfall.

Om du vill mappa en CSV-kolumn till ett XDM-fält väljer du schemaikonen bredvid kolumnens motsvarande målfält.

![](../images/tutorials/map-a-csv-file/mapping.png)

Fönstret **[!UICONTROL Select schema field]** visas. Här kan du navigera i XDM-schemats struktur och leta upp det fält som du vill mappa CSV-kolumnen till. Klicka på ett XDM-fält för att markera det och klicka sedan på **[!UICONTROL Select]**.

![](../images/tutorials/map-a-csv-file/select-schema-field.png)

När du har slutfört stegen för de återstående omappade källfälten visas skärmen igen och det markerade XDM-fältet visas nu under **[!UICONTROL Mapping]** **[!UICONTROL Target Field]**.

![](../images/tutorials/map-a-csv-file/field-mapped.png)

När du mappar fält kan du även inkludera funktioner för att beräkna värden baserat på indatakällfält. Mer information finns i avsnittet om [mappningsfunktioner](#mapping-functions) i bilagan.

### Lägg till beräknat fält

Beräknade fält tillåter att värden skapas baserat på attributen i indatabladet. Dessa värden kan sedan tilldelas attribut i målschemat och ges ett namn och en beskrivning som gör det enklare att referera till.

Klicka på **[!UICONTROL Add calculated field]** knappen för att fortsätta.

![](../images/tutorials/map-a-csv-file/add-calculate-field.png)

Panelen **[!UICONTROL Create calculated field]** visas. Den vänstra dialogrutan innehåller de fält, funktioner och operatorer som stöds i beräkningsfält. Välj en av flikarna för att börja lägga till funktioner, fält eller operatorer i uttrycksredigeraren.

![](../images/tutorials/map-a-csv-file/create-calculated-fields.png)

| Tabb | Beskrivning |
| --------- | ----------- |
| Fält | Fliken Fält visar de fält och attribut som är tillgängliga i källschemat. |
| Funktioner | På fliken Funktioner visas de funktioner som är tillgängliga för att omforma data. |
| Operatorer | På fliken Operatorer visas de operatorer som är tillgängliga för att omforma data. |

Du kan lägga till fält, funktioner och operatorer manuellt med uttrycksredigeraren i mitten. Välj redigeraren för att börja skapa ett uttryck.

![](../images/tutorials/map-a-csv-file/expression-editor.png)

Välj **[!UICONTROL Save]** att fortsätta.

Mappningsskärmen visas igen med det nya källfältet. Tillämpa motsvarande målfält och välj **[!UICONTROL Finish]** för att slutföra mappningen.

![](../images/tutorials/map-a-csv-file/new-field.png)

## Övervaka dataflödet

När CSV-filen har mappats och skapats kan du övervaka de data som hämtas genom den. Mer information om att övervaka dataflöden finns i självstudiekursen om [övervakning av dataflöden](../../ingestion/quality/monitor-data-flows.md)för direktuppspelning.

## Nästa steg

I den här självstudiekursen har du mappat en platt CSV-fil till ett XDM-schema och infogat den [!DNL Platform]. Dessa data kan nu användas av [!DNL Platform] tjänster längre fram i kedjan, till exempel [!DNL Real-time Customer Profile]. Mer information finns i översikten för [[!DNL Real-time Customer Profile]](../../profile/home.md) .

## Bilaga

I följande avsnitt finns ytterligare information om hur du mappar CSV-kolumner till XDM-fält.

### Mappningsfunktioner

Vissa mappningsfunktioner kan användas för att beräkna och beräkna värden baserat på vad som anges i källfält. Om du vill använda en funktion skriver du in den under **[!UICONTROL Source Field]** med lämplig syntax och indata.

Om du till exempel vill sammanfoga CSV-fält för **ort** och **land** och tilldela dem till XDM-fältet för **stad** anger du källfältet som `concat(city, ", ", county)`.

![](../images/tutorials/map-a-csv-file/mapping-function.png)

I följande tabell visas alla mappningsfunktioner som stöds, inklusive exempeluttryck och deras resulterande utdata.

|  -funktion | Beskrivning | Exempeluttryck | Exempelutdata |
| -------- | ----------- | ----------------- | ------------- |
| concat | Sammanfogar angivna strängar. | concat(&quot;Hi, &quot;, &quot;there&quot;, &quot;!&quot;) | `"Hi, there!"` |
| explodera | Delar strängen baserat på en regex och returnerar en array med delar. | explode(&quot;Hej, där!&quot;, &quot;&quot;) | `["Hi,", "there"]` |
| instr | Returnerar platsen/indexvärdet för en delsträng. | instr(&quot;adobe<span>.com&quot;, &quot;com&quot;) | 6 |
| replacester | Ersätter söksträngen om den finns i den ursprungliga strängen. | replacestr(&quot;This is a string re test&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;This is a string replace test&quot; |
| substr | Returnerar en delsträng med en viss längd. | substr(&quot;This is a substring test&quot;, 7, 8) | &quot; a subst&quot; |
| lower /<br>lcase | Konverterar en sträng till gemener. | lower(&quot;HanLo&quot;)<br>lcase(&quot;HanLo&quot;) | &quot;hello&quot; |
| upper /<br>ucase | Konverterar en sträng till versaler. | upper(&quot;HanLo&quot;)<br>ucase(&quot;HanLo&quot;) | &quot;HELLO&quot; |
| dela | Delar en indatasträng på en avgränsare. | split(&quot;Hello world&quot;, &quot; &quot;) | `["Hello", "world"]` |
| join | Sammanfogar en lista med objekt med hjälp av avgränsaren. | `join(" ", ["Hello", "world"]`) | &quot;Hello world&quot; |
| coalesce | Returnerar det första icke-null-objektet i en given lista. | coalesce(null, null, null, &quot;first&quot;, null, &quot;second&quot;) | &quot;first&quot; |
| decode | Om en nyckel och en lista med nyckelvärdepar förenklas som en array, returnerar funktionen värdet om nyckeln hittas eller returnerar ett standardvärde om det finns i arrayen. | decode(&quot;k2&quot;, &quot;k1&quot;, &quot;v1&quot;, &quot;k2&quot;, &quot;v2&quot;, &quot;default&quot;) | &quot;v2&quot; |
| iif | Utvärderar ett givet booleskt uttryck och returnerar det angivna värdet baserat på resultatet. | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;Sant&quot; |
| min | Returnerar det minsta av de angivna argumenten. Använder naturlig beställning. | min(3, 1, 4) | 1 |
| max | Returnerar det maximala antalet angivna argument. Använder naturlig beställning. | max(3, 1, 4) | 4 |
| först | Hämtar det första angivna argumentet. | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| sista | Hämtar det senast angivna argumentet. | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| uuid /<br>guid | Skapar ett pseudoslumpmässigt ID. | uuid()<br>guid() | {UNIQUE_ID} |
| nu | Hämtar aktuell tid. | nu() | `2019-10-23T10:10:24.556-07:00[America/Los_Angeles]` |
| tidsstämpel | Hämtar aktuell Unix-tid. | tidsstämpel() | 1571850624571 |
| format | Formaterar indatadatum enligt ett angivet format. | format({DATE}, &quot;yyy-MM-dd HH:mm:ss&quot;) | &quot;2019-10-23 11:24:35&quot; |
| dformat | Konverterar en tidsstämpel till en datumsträng enligt ett angivet format. | format(1571829875, &quot;dd-MMM-yyyy hh:mm&quot;) | &quot;23-Oct-2019 11:24&quot; |
| datum | Konverterar en datumsträng till ett ZonedDateTime-objekt (ISO 8601-format). | date(&quot;23-Oct-2019 11:24&quot;) | &quot;2019-10-23T11:24:00+00:00&quot; |
| date_part | Hämtar datumets delar. Följande komponentvärden stöds: <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;kvartal&quot;<br>&quot;qq&quot;<br>&quot;q&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;day&quot;<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>&quot;dy&quot;år&quot;y&quot;&quot;dag&quot;dd&quot;dd&quot;dd&quot;d&quot;&quot;vecka&quot;Under&quot;&quot;veckodag&quot;&quot;dw&quot;&quot;w&quot;stapel&quot;timme&quot;Du&quot;har&quot;Under&quot;Under&quot;UnderUnderUnderUnderUnderUnderUnderUnder&quot;UnderUnderUnderUnderUnderUnderUnderUnderUnderUnder&quot;UnderUnder&quot;UnderUnderUnderUnderUnderUnderUnder&quot;Under&quot;UnderUnderUnderUnderUnderUnderUnderUnderUnderUnderUnderUnderUnderUnderUnderUnderUnder&quot;UnderUnderUnderUnder&quot;Under&quot;Under&quot;Under&quot;UnderUnderUnderUnderUnderUnderUnderUnderUnderUnderUnderUnderUnderUnderUnder&quot;UnderUnderUnderUnderUnder&quot;Under&quot;Under&quot;h&quot;&quot;hh24&quot;&quot;hh12&quot;&quot;minut&quot;mi&quot;&quot;n&quot;&quot;sekund&quot;&quot;ss&quot;s&quot;&quot;millisekundnamn&quot;ms&quot; | date_part(date(&quot;2019-10-17 11:55:12&quot;), &quot;MM&quot;) | 10 |
| set_date_part | Ersätter en komponent ett visst datum. Följande komponenter godkänns: <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;hour&quot;<br><br><br><br><br><br><br><br><br>&quot;hh&quot;&quot;minut&quot;mi&quot;Under&quot;&quot;n&quot;&quot;sekund&quot;Under&quot;ss&quot;&quot;s&quot; | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44.797&quot;) | &quot;2016-04-09T11:44:44.797&quot; |
| make_date_time /<br>make_timestamp | Skapar ett datum från delar. | make_date_time(2019, 10, 17, 11, 55, 12, 999, &quot;America/Los_Angeles&quot;) | `2019-10-17T11:55:12.0&#x200B;00000999-07:00[America/Los_Angeles]` |
| current_timestamp | Returnerar den aktuella tidsstämpeln. | current_timestamp() | 1571850624571 |
| aktuellt_datum | Returnerar det aktuella datumet utan någon tidskomponent. | current_date() | &quot;18-Nov-2019&quot; |