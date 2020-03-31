---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Mappa en CSV-fil till ett XDM-schema
topic: tutorial
translation-type: tm+mt
source-git-commit: 33282b1c8ab1129344bd4d7054e86fed75e7b899

---


# Mappa en CSV-fil till ett XDM-schema

För att kunna importera CSV-data till Adobe Experience Platform måste data mappas till ett XDM-schema (Experience Data Model). I den här självstudien beskrivs hur du mappar en CSV-fil till ett XDM-schema med användargränssnittet i Experience Platform.

I bilagan till den här självstudiekursen finns dessutom mer information om hur du använder [mappningsfunktioner](#mapping-functions).

## Komma igång

Den här självstudien kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Experience Data Model (XDM-system)](../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att organisera kundupplevelsedata.
- [Batchförtäring](../batch-ingestion/overview.md): Den metod som används för att importera data från användartillhandahållna datafiler.

Den här självstudien kräver också att du redan har skapat en datauppsättning att importera dina CSV-data till. Anvisningar om hur du skapar en datauppsättning i användargränssnittet finns i [självstudiekursen](./ingest-batch-data.md)om dataimport.

## Lägg till data

I Experience Platform-gränssnittet klickar du på **Arbetsflöden** i den vänstra navigeringen och sedan på **Mappa CSV till XDM-schema**. Klicka på **Starta** i den högra listen som visas.

![](../images/tutorials/map-a-csv-file/workflow-tab.png)

Arbetsflödet _Mappa CSV till XDM-schema_ visas med början i steget _Lägg till data_ .

![](../images/tutorials/map-a-csv-file/add-data.png)

Dra och släpp CSV-filen i det utrymme som anges eller klicka på **Bläddra** om du vill välja en fil direkt. Ett _exempeldataavsnitt_ visas när filen har överförts och visar de tio första dataraderna. När du har bekräftat att data har överförts som förväntat klickar du på **Nästa**.

![](../images/tutorials/map-a-csv-file/csv-added.png)

## Välj ett mål

Steget _Mål_ visas. I listan markerar du datauppsättningen som CSV-data ska hämtas till och klickar sedan på **Nästa**.

![](../images/tutorials/map-a-csv-file/select-destination.png)

## Mappa CSV-fält till XDM-schemafält

Steget _Mappning_ visas. Kolumnerna i CSV-filen listas under _Källfält_, med motsvarande XDM-schemafält listade under _Målfält_. Omarkerade målfält markeras med röda konturer.

Om du vill mappa en CSV-kolumn till ett XDM-fält klickar du på schemaikonen bredvid kolumnens motsvarande målfält.

![](../images/tutorials/map-a-csv-file/target-field-mapping.png)

Fönstret _Välj_ schema visas. Här kan du navigera i XDM-schemats struktur och leta upp det fält som du vill mappa CSV-kolumnen till. Klicka på ett XDM-fält för att markera det och klicka sedan på **Välj**.

![](../images/tutorials/map-a-csv-file/xdm-field-selection.png)

Skärmen _Mappning_ visas igen och det markerade XDM-fältet visas nu under _Målfält_.

![](../images/tutorials/map-a-csv-file/xdm-field-mapped.png)

Om du inte vill mappa en viss CSV-kolumn kan du ta bort mappningen genom att klicka på **borttagningsikonen** bredvid målfältet. Om du vill lägga till en ny mappning klickar du på **Lägg till ny mappning** längst ned i listan.

![](../images/tutorials/map-a-csv-file/remove-or-add-mapping.png)

När du mappar fält kan du även inkludera funktioner för att beräkna värden baserat på indatakällfält. Mer information finns i avsnittet om [mappningsfunktioner](#mapping-functions) i bilagan.

Upprepa stegen ovan om du vill fortsätta mappningen av CSV-kolumner till XDM-fält. När du är klar klickar du på **Nästa**.

![](../images/tutorials/map-a-csv-file/mapping-finish.png)

## Ingrediera data

Steget _Ingest_ visas så att du kan granska informationen om källfilen och måldatauppsättningen. Klicka på **Ingest** för att börja hämta CSV-data. Beroende på CSV-filens storlek kan den här processen ta flera minuter. Skärmen uppdateras när importen är klar, vilket anger att åtgärden lyckades eller misslyckades. Klicka på **Slutför** för att slutföra arbetsflödet.

![](../images/tutorials/map-a-csv-file/ingest-data.png)

## Nästa steg

I den här självstudiekursen har du mappat en platt CSV-fil till ett XDM-schema och infogat den i Platform. Dessa data kan nu användas av plattformstjänster längre fram i kedjan, t.ex. kundprofil i realtid. Mer information finns i [Kundprofilöversikt](../../profile/home.md) i realtid.

## Bilaga

I följande avsnitt finns ytterligare information om hur du mappar CSV-kolumner till XDM-fält.

### Mappningsfunktioner

Vissa mappningsfunktioner kan användas för att beräkna och beräkna värden baserat på vad som anges i källfält. Om du vill använda en funktion anger du den under _Källfält_ med lämplig syntax och indata.

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
| nu | Hämtar aktuell tid. | now() | `2019-10-23T10:10:24.556-07:00[America/Los_Angeles]` |
| tidsstämpel | Hämtar aktuell Unix-tid. | timestamp() | 1571850624571 |
| format | Formaterar indatadatum enligt ett angivet format. | format({DATE}, &quot;yyy-MM-dd HH:mm:ss&quot;) | &quot;2019-10-23 11:24:35&quot; |
| dformat | Konverterar en tidsstämpel till en datumsträng enligt ett angivet format. | format(1571829875, &quot;dd-MMM-yyyy hh:mm&quot;) | &quot;23-Oct-2019 11:24&quot; |
| datum | Konverterar en datumsträng till ett ZonedDateTime-objekt (ISO 8601-format). | date(&quot;23-Oct-2019 11:24&quot;) | &quot;2019-10-23T11:24:00+00:00&quot; |
| date_part | Hämtar datumets delar. Följande komponentvärden stöds: <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;kvartal&quot;<br>&quot;qq&quot;<br>&quot;q&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;dagÅÅ&quot;stapel&quot;y&quot;år&quot;dag&quot;Under&quot;dd&quot;dd&quot;Under&quot;vecka&quot;Under&quot;&quot;veckodag&quot;&quot;dagarna&quot;Dw&quot;Alltid&quot;w&quot;&quot;en&quot;timme&quot;Ni&quot;har&quot;Ni&quot;oberoende&quot;Ni&quot;Ni&quot;har&quot;rätt&quot; rätt&quot; Ni&quot;Ni&quot;Ni&quot;Ni&quot;Ni&quot;Ni&quot;Ni&quot;Ni&quot;har rättUnderUnderUnderUnderUnderUnderUnderUnderUnderUnderUnderUnderUnderUnderUnderUnderUnderNi&quot;Ni&quot;Ni&quot;Ni&quot;Ni&quot;Ni&quot;Ni&quot;har&quot;Ni&quot;Ni&quot;Ni&quot;Ni&quot;Ni&quot;Ni&quot;Ni&quot;Ni&quot;Ni&quot;har&quot;Ni&quot;Ni&quot;Ni&quot;Ni&quot;<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>&quot;Ni&quot;Ni&quot;Ni&quot;Ni&quot;Ni&quot;Ni&quot;Ni&quot;Ni&quot;Ni&quot;har&quot;har&quot;Ni&quot;har&quot;Ni&quot;Ni&quot;Ni&quot;Ni&quot;Ni&quot;Ni hh&quot;&quot;hh24&quot;&quot;hh12&quot;&quot;minut&quot;mi&quot;Under&quot;år&quot;andra&quot;&quot;&quot;s&quot;Under&quot;&quot;millisekunddelen&quot;ms&quot; | date_part(date(&quot;2019-10-17 11:55:12&quot;), &quot;MM&quot;) | 10 |
| set_date_part | Ersätter en komponent vid ett visst datum. Följande komponenter godkänns: <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br><br><br><br><br><br><br><br><br><br>&quot;hour&quot;hh&quot;&quot;minute&quot;mi&quot;¥&quot;n&quot;Under&quot;Under&quot;Sekunder&quot;&quot;ss&quot;&quot;s&quot;&quot; | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44.797&quot;) | &quot;2016-04-09T11:44:44.797&quot; |
| make_date_time /<br>make_timestamp | Skapar ett datum från delar. | make_date_time(2019, 10, 17, 11, 55, 12, 999, &quot;America/Los_Angeles&quot;) | `2019-10-17T11:55:12.0&#x200B;00000999-07:00[America/Los_Angeles]` |
| current_timestamp | Returnerar den aktuella tidsstämpeln. | current_timestamp() | 1571850624571 |
| aktuellt_datum | Returnerar det aktuella datumet utan någon tidskomponent. | current_date() | &quot;18-Nov-2019&quot; |