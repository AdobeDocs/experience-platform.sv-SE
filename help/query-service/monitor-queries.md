---
title: Övervaka frågor
description: Lär dig hur du övervakar frågor med hjälp av gränssnittet för frågetjänsten.
source-git-commit: 62863fc5b59a8185ea01f19dd3c50bf22fdd1e55
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 0%

---

# Övervaka frågor (begränsad version)

>[!IMPORTANT]
>
>Den här funktionen är för närvarande en begränsad version och endast tillgänglig för ett litet antal kunder.

Adobe Experience Platform ger bättre synlighet för status för alla frågefunktioner via användargränssnittet. Från [!UICONTROL Scheduled Queries] kan du nu hitta viktig information om frågekörningar som innehåller status, schemainformation och felmeddelanden/koder om de skulle misslyckas. Du kan även prenumerera på aviseringar för frågor baserat på deras status via användargränssnittet för någon av dessa frågor via [!UICONTROL Scheduled Queries] -fliken.

## [!UICONTROL Scheduled Queries]

The [!UICONTROL Scheduled Queries] ger en översikt över körda och schemalagda frågor. Arbetsytan innehåller alla dina CTAS- och ITAS-frågor som antingen är schemalagda att köras eller har körts minst en gång. Det går att hitta körningsinformation för alla schemalagda frågor samt felkoder och meddelanden för misslyckade frågor.

Navigera till [!UICONTROL Scheduled Queries] flik, välja **[!UICONTROL Queries]** från vänster navigeringsfält följt av **[!UICONTROL Scheduled Queries]**

![Fliken Schemalagda frågor på arbetsytan Frågor.](./images/monitor-queries/scheduled-queries.png)

Tabellen nedan beskriver varje tillgänglig kolumn.

>[!NOTE]
>
>Varningssymbolen för prenumerationer finns på varje rad i en namnlös kolumn. Se [aviseringsprenumerationer](#alert-subscription) för mer information.

| Kolumn | Beskrivning |
|---|---|
| Namn | Namnfältet är antingen mallnamnet eller de första tecknen i SQL-frågan. Alla frågor som skapas via gränssnittet med Frågeredigeraren får i början ett namn. Om frågan skapades via API är namnet på frågan ett fragment av det SQL-uttryck som användes för att skapa frågan. |
| Mall | Frågans mallnamn. Välj ett mallnamn för att gå till Frågeredigeraren. Frågemallen visas i Frågeredigeraren. Om det inte finns något mallnamn markeras raden med ett bindestreck och det går inte att omdirigera till Frågeredigeraren för att visa frågan. |
| SQL | Ett fragment av SQL-frågan. |
| Körningsfrekvens | Det här är den avslutning som frågan är inställd på att köras. De tillgängliga värdena är `Run once` och `Scheduled`. Frågor kan filtreras utifrån deras körningsfrekvens. |
| Skapad av | Namnet på den användare som skapade frågan. |
| Skapad | Tidsstämpeln när frågan skapades, i UTC-format. |
| Tidsstämpel för senaste körning | Den senaste tidsstämpeln när frågan kördes. Den här kolumnen visar om en fråga har körts enligt det aktuella schemat. |
| Senaste körningsstatus | Status för den senaste frågekörningen. De tre statusvärdena är: `successful` `failed` eller `in progress`. |

>[!TIP]
>
>Om du går till Frågeredigeraren kan du välja **[!UICONTROL Queries]** för att gå tillbaka till [!UICONTROL Templates] -fliken.

### Anpassa tabellinställningar för schemalagda frågor

Du kan justera kolumnerna på [!UICONTROL Scheduled Queries] efter behov. Välj inställningsikonen (![En inställningsikon.](./images/monitor-queries/settings-icon.png)) för att öppna [!UICONTROL Customize table] och redigera tillgängliga kolumner.

![Ikonen Anpassa tabellinställningar.](./images/monitor-queries/customze-table-settings-icon.png)

Växla mellan de relevanta kryssrutorna för att ta bort eller lägga till en tabellkolumn. Nästa, välj **[!UICONTROL Apply]** för att bekräfta dina val.

>[!NOTE]
>
>Alla frågor som har skapats via användargränssnittet blir en namngiven mall som en del av skapandeprocessen. Mallnamnet visas i mallkolumnen. Om frågan skapades via API är mallkolumnen tom.

![Dialogrutan Anpassa tabellinställningar.](./images/monitor-queries/customize-table-dialog.png)

### Prenumerera på aviseringar {#alert-subscription}

Du kan prenumerera på aviseringar från [!UICONTROL Scheduled Queries] -fliken. Markera varningsmeddelandeikonen (![En varningsikon.](./images/monitor-queries/alerts-icon.png)) bredvid ett frågenamn för att öppna [!UICONTROL Alerts] -dialogrutan. The [!UICONTROL Alerts] prenumererar på både UI-meddelanden och e-postaviseringar. Varningar baseras på frågans status. Det finns tre alternativ: `start`, `success`och `failure`. Markera lämplig ruta eller rutor och välj **[!UICONTROL Save]** prenumerera.

<!-- This dialog will be updated before release. THe image below will need to be updated inline with these changes. -->

![Dialogrutan med aviseringsprenumerationer.](./images/monitor-queries/alert-subscription-dialog.png)

<!-- Link to alert subscriptions doc when available -->

### Filtrera frågor

Du kan filtrera frågor baserat på körningsfrekvens. Från [!UICONTROL Scheduled Queries] väljer du filterikonen (![En filterikon](./images/monitor-queries/filter-icon.png)) för att öppna filtersidofältet.

![Fliken för schemalagda frågor med filterikonen markerad.](./images/monitor-queries/filter-queries.png)

Välj antingen **[!UICONTROL Scheduled]** eller **[!UICONTROL Run once]** kör kryssrutor för frekvensfilter för att filtrera listan med frågor.

>[!NOTE]
>
>Alla frågor som har körts men inte schemalagts kvalificeras som [!UICONTROL Run once].

![Fliken för schemalagda frågor med filtersidofältet markerat.](./images/monitor-queries/filter-sidebar.png)

När du har aktiverat filtervillkoren väljer du **[!UICONTROL Hide Filters]** för att stänga filterpanelen.

## Schemaläggningsdetaljer för frågekörningar

Välj ett frågenamn för att navigera till sidan med schemainformation. Den här vyn innehåller en lista över alla körningar som har utförts som en del av den schemalagda frågan. Informationen omfattar start- och sluttid, status och datauppsättning som används.

![Sidan med schemainformation.](./images/monitor-queries/schedule-details.png)

Den här informationen finns i en tabell med fem kolumner. Varje rad betecknar en frågekörning.

| Kolumnnamn | Beskrivning |
|---|---|
| Frågekörnings-ID | Frågekörnings-ID för daglig körning. |
| Körningsstart av fråga | Tidsstämpeln när frågan kördes. Detta är i UTC-format. |
| Frågekörningen har slutförts | Tidsstämpeln när frågan slutfördes. Detta är i UTC-format. |
| Status | Status för den senaste frågekörningen. De tre statusvärdena är: `successful` `failed` eller `in progress`. |
| Datauppsättning | Den datauppsättning som ingår i körningen. |

Information om frågan som schemaläggs finns i [!UICONTROL Properties] -panelen. Panelen innehåller det inledande fråge-ID:t, klienttyp, mallnamn, frågans SQL-kod och schemats avslutning.

![Sidan med information om schemat med egenskapspanelen markerad.](./images/monitor-queries/properties-panel.png)

### Körningsinformation

Välj ett ID för frågekörning för att navigera till sidan med körningsinformation och visa frågeinformation.

![Skärmen med schemainformation och ett körnings-ID markerat.](./images/monitor-queries/navigate-to-run-details.png)

Den här vyn innehåller information om enskilda körningar för den schemalagda frågan och en mer detaljerad beskrivning av körningsstatusen. Den här sidan innehåller även klientinformation och information om eventuella fel som orsakade att frågan misslyckades.

![Skärmen med körningsinformation med översiktsavsnittet markerat.](./images/monitor-queries/query-run-details.png)

Avsnittet med frågans status innehåller felkoden och felmeddelandet om frågan skulle ha misslyckats.

![Skärmen med körningsinformation med felavsnittet markerat.](./images/monitor-queries/failed-query.png)

Du kan kopiera frågans SQL till Urklipp från den här vyn. Kopiera frågan genom att markera kopieringsikonen i det övre högra hörnet av SQL-fragmentet. Ett popup-meddelande bekräftar att koden har kopierats.

![Skärmen med körningsinformation där SQL-kopieringsikonen är markerad.](./images/monitor-queries/copy-sql.png)

Välj **[!UICONTROL Query]** för att återgå till skärmen med schemainformation, eller **[!UICONTROL Scheduled Queries]** för att gå tillbaka till [!UICONTROL Scheduled Queries] -fliken.

![Skärmen med körningsinformation och frågan markerad.](./images/monitor-queries/return-navigation.png)

