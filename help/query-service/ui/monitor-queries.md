---
title: Övervaka schemalagda frågor
description: Lär dig hur du övervakar frågor med hjälp av gränssnittet för frågetjänsten.
exl-id: 4640afdd-b012-4768-8586-32f1b8232879
source-git-commit: 41c069ef1c0a19f34631e77afd7a80b8967c5060
workflow-type: tm+mt
source-wordcount: '2333'
ht-degree: 0%

---

# Övervaka schemalagda frågor

Adobe Experience Platform ger bättre synlighet för status för alla frågefunktioner via användargränssnittet. Från [!UICONTROL Scheduled Queries] kan du nu hitta viktig information om frågekörningar som innehåller status, schemainformation och felmeddelanden/koder om de skulle misslyckas. Du kan även prenumerera på aviseringar för frågor baserat på deras status via användargränssnittet för någon av dessa frågor via [!UICONTROL Scheduled Queries] -fliken.

## [!UICONTROL Scheduled Queries]

The [!UICONTROL Scheduled Queries] ger en översikt över alla dina schemalagda CTAS- och ITAS-frågor. Det går att hitta körningsinformation för alla schemalagda frågor samt felkoder och meddelanden för eventuella misslyckade frågor.

Navigera till [!UICONTROL Scheduled Queries] flik, välja **[!UICONTROL Queries]** från vänster navigeringsfält följt av **[!UICONTROL Scheduled Queries]**

![Fliken Schemalagda frågor på arbetsytan Frågor med schemalagda frågor och frågor markerade.](../images/ui/monitor-queries/scheduled-queries.png)

Tabellen nedan beskriver varje tillgänglig kolumn.

>[!NOTE]
>
>Varningskopian (![En prenumerationsikon för aviseringar.](../images/ui/monitor-queries/alert-subscription-icon.png)) finns i varje rad i en namnlös kolumn. Se [aviseringsprenumerationer](#alert-subscription) för mer information.

| Kolumn | Beskrivning |
|---|---|
| **[!UICONTROL Name]** | Namnfältet är antingen mallnamnet eller de första tecknen i SQL-frågan. Alla frågor som skapas via gränssnittet med Frågeredigeraren får i början ett namn. Om frågan skapades med API:t blir dess namn ett fragment av den ursprungliga SQL-kod som användes för att skapa frågan. Om du vill visa en lista över alla körningar som är associerade med frågan väljer du ett objekt i [!UICONTROL Name] kolumn. Mer information finns i [fråga kör schemadetaljer](#query-runs) -avsnitt. |
| **[!UICONTROL Template]** | Frågans mallnamn. Välj ett mallnamn för att gå till Frågeredigeraren. Frågemallen visas i Frågeredigeraren. Om det inte finns något mallnamn markeras raden med ett bindestreck och det går inte att omdirigera till Frågeredigeraren för att visa frågan. |
| **[!UICONTROL SQL]** | Ett fragment av SQL-frågan. |
| **[!UICONTROL Run frequency]** | Den gräns som frågan är inställd på att köras vid. De tillgängliga värdena är `Run once` och `Scheduled`. |
| **[!UICONTROL Created by]** | Namnet på den användare som skapade frågan. |
| **[!UICONTROL Created]** | Tidsstämpeln när frågan skapades, i UTC-format. |
| **[!UICONTROL Last run timestamp]** | Den senaste tidsstämpeln när frågan kördes. Den här kolumnen visar om en fråga har körts enligt det aktuella schemat. |
| **[!UICONTROL Last run status]** | Status för den senaste frågekörningen. Statusvärdena är: `Success`, `Failed`, `In progress`och `No runs`. |
| **[!UICONTROL Schedule Status]** | Den schemalagda frågans aktuella status. Det finns sex möjliga värden, [!UICONTROL Registering], [!UICONTROL Active], [!UICONTROL Inactive], [!UICONTROL Deleted], ett bindestreck och [!UICONTROL Quarantined].<ul><li>The **[!UICONTROL Registering]** status anger att systemet fortfarande bearbetar skapandet av det nya schemat för frågan. Observera att du inte kan inaktivera eller ta bort en schemalagd fråga medan den registreras.</li><li>The **[!UICONTROL Active]** status anger att den schemalagda frågan har **ännu inte godkänt** datum och tid för slutförande.</li><li>The **[!UICONTROL Inactive]** status anger att den schemalagda frågan har **passerad** datum och tid för slutförande eller har markerats av en användare som inaktiv.</li><li>The **[!UICONTROL Deleted]** status anger att frågeschemat har tagits bort.</li><li>Avstavningen anger att den schemalagda frågan är en enstaka, icke återkommande fråga.</li><li>The **[!UICONTROL Quarantined]** status anger att frågan har misslyckats tio gånger i följd och kräver att du gör något innan fler körningar kan utföras.</li></ul> |

>[!TIP]
>
>Om du går till Frågeredigeraren kan du välja **[!UICONTROL Queries]** för att gå tillbaka till [!UICONTROL Templates] -fliken.

## Anpassa tabellinställningar för schemalagda frågor {#customize-table}

Du kan justera kolumnerna på [!UICONTROL Scheduled Queries] efter behov. Öppna [!UICONTROL Customize table] inställningsdialogrutan och redigera tillgängliga kolumner väljer du inställningsikonen (![En inställningsikon.](../images/ui/monitor-queries/settings-icon.png)) längst upp till höger på skärmen.

>[!NOTE]
>
>The [!UICONTROL Created] kolumn som refererar till det datum då schemat skapades döljs som standard.

![Fliken Schemalagda frågor med ikonen Anpassa tabellinställningar markerad.](../images/ui/monitor-queries/customze-table-settings-icon.png)

Växla mellan de relevanta kryssrutorna för att ta bort eller lägga till en tabellkolumn. Nästa, välj **[!UICONTROL Apply]** för att bekräfta dina val.

>[!NOTE]
>
>Alla frågor som har skapats via användargränssnittet blir en namngiven mall som en del av skapandeprocessen. Mallnamnet visas i mallkolumnen. Om frågan skapades via API är mallkolumnen tom.

![Dialogrutan Anpassa tabellinställningar.](../images/ui/monitor-queries/customize-table-dialog.png)

## Hantera schemalagda frågor med infogade åtgärder {#inline-actions}

The [!UICONTROL Scheduled Queries] I vyn finns olika textbundna åtgärder för att hantera alla schemalagda frågor från en och samma plats. Textbundna åtgärder anges på varje rad med ellips. Markera ellipsen för en schemalagd fråga som du vill hantera för att se de tillgängliga alternativen på en snabbmeny. De tillgängliga alternativen omfattar [[!UICONTROL Disable schedule]](#disable) eller [!UICONTROL Enable schedule], [[!UICONTROL Delete schedule]](#delete), [[!UICONTROL Subscribe]](#alert-subscription) för att fråga efter varningar, och [Aktivera eller [!UICONTROL Disable quarantine]](#quarantined-queries).

![Fliken Schemalagda frågor med de infogade åtgärdsellipserna och popup-menyn markerade.](../images/ui/monitor-queries/inline-actions.png)

### Inaktivera eller aktivera en schemalagd fråga {#disable}

Om du vill inaktivera en schemalagd fråga markerar du ellipsen för den schemalagda fråga som du vill hantera och väljer sedan **[!UICONTROL Disable schedule]** från alternativen på snabbmenyn. En dialogruta visas där du kan bekräfta åtgärden. Välj **[!UICONTROL Disable]** för att bekräfta inställningen.

När en schemalagd fråga har inaktiverats kan du aktivera schemat via samma process. Markera ellipsen och välj **[!UICONTROL Enable schedule]** bland de tillgängliga alternativen.

>[!NOTE]
>
>Om en fråga har placerats i karantän bör du granska mallens SQL innan du aktiverar dess schema. Detta förhindrar slöseri med beräkningstimmar om mallfrågan fortfarande har problem.

### Ta bort en schemalagd fråga {#delete}

Om du vill ta bort en schemalagd fråga markerar du ellipsen för den schemalagda fråga som du vill hantera och väljer sedan **[!UICONTROL Delete schedule]** från alternativen på snabbmenyn. En dialogruta visas där du kan bekräfta åtgärden. Välj **[!UICONTROL Delete]** för att bekräfta inställningen.

När en schemalagd fråga har tagits bort är den **not** som tagits bort från listan med schemalagda frågor. De infogade åtgärder som tillhandahålls av ellipserna tas bort och ersätts av den nedtonade prenumerationsikonen för att lägga till aviseringar. Du kan inte prenumerera på aviseringar för det borttagna schemat. Raden finns kvar i användargränssnittet för att ge information om körningar som utförts som en del av den schemalagda frågan.

![Fliken Schemalagda frågor med en borttagen schemalagd fråga och en nedtonad aviseringsprenumerationsikon markerad.](../images/ui/monitor-queries/post-delete.png)

Om du vill schemalägga körningar för den frågemallen väljer du mallnamnet på lämplig rad för att navigera till Frågeredigeraren och följer sedan [instruktioner för att lägga till ett schema i en fråga](./query-schedules.md#create-schedule) enligt beskrivningen i dokumentationen.

### Prenumerera på aviseringar {#alert-subscription}

Om du vill prenumerera på aviseringar för schemalagda frågekörningar väljer du antingen `...` (ellips) eller aviseringsprenumerationsikon (![En aviseringsprenumerationsikon.](../images/ui/monitor-queries/alert-subscription-icon.png)) för den schemalagda fråga som du vill hantera. Listrutan för textbundna åtgärder visas. Nästa, välj **[!UICONTROL Subscribe]** bland de tillgängliga alternativen.

![Arbetsytan för schemalagda frågor med en ellips, en aviseringsprenumerationsikon och listrutan för textbundna åtgärder markerad.](../images/ui/monitor-queries/subscribe.png)

The [!UICONTROL Alerts] öppnas. The [!UICONTROL Alerts] prenumererar på både UI-meddelanden och e-postaviseringar. Det finns flera olika prenumerationsalternativ: `start`, `success`, `failure`, `quarantine`och `delay`. Markera lämplig ruta eller rutor och välj **[!UICONTROL Save]** prenumerera.

![Dialogrutan med aviseringsprenumerationer.](../images/ui/monitor-queries/alert-subscription-dialog.png)

Tabellen nedan förklarar vilka frågeartikeltyper som stöds:

| Aviseringstyp | Beskrivning |
|---|---|
| `start` | Den här varningen meddelar dig när en schemalagd frågekörning initieras eller börjar bearbetas. |
| `success` | Den här varningen informerar dig när en schemalagd frågekörning har slutförts, vilket anger att frågan har körts utan fel. |
| `failed` | Den här varningen utlöses när en schemalagd frågekörning påträffar ett fel eller misslyckas med att köras. Det hjälper er att snabbt identifiera och åtgärda problem. |
| `quarantine` | Den här varningen aktiveras när en schemalagd frågekörning sätts i karantän. När frågor registreras i [karantänfunktion](#quarantined-queries), kommer alla schemalagda frågor som misslyckas tio på varandra följande körningar automatiskt att placeras i [!UICONTROL Quarantined] tillstånd. De måste sedan ingripa innan fler avrättningar kan utföras. |
| `delay` | Den här varningen meddelar dig om det finns en [fördröjning av resultatet av en frågekörning](#query-run-delay) över ett angivet tröskelvärde. Du kan ange en anpassad tid som utlöser varningen när frågan körs för den tidslängden utan att slutföra eller misslyckas. |

>[!NOTE]
>
>Om du vill få meddelanden om att en fråga hamnar i karantän måste du först registrera körningarna av den schemalagda frågan i [karantänfunktion](#quarantined-queries).

Se [API-dokumentation för aviseringsprenumerationer](../api/alert-subscriptions.md) för mer information.

### Visa frågedetaljer {#query-details}

Välj informationsikonen (![En informationsikon.](../images/ui/monitor-queries/information-icon.png)) om du vill visa informationspanelen för frågan. Panelen Detaljer innehåller all relevant information om frågan utöver de fakta som finns i tabellen med schemalagda frågor. Ytterligare information omfattar fråge-ID, senaste ändringsdatum, frågans SQL, schema-ID och aktuellt uppsättningsschema.

![Fliken Schemalagda frågor med informationsikonen och informationspanelen markerad.](../images/ui/monitor-queries/details-panel.png)

## Frågor i karantän {#quarantined-queries}

>[!NOTE]
>
>Karantänsvarningen är inte tillgänglig för ad hoc-frågor som körs en gång. Karantänsvarningen gäller endast för schemalagda batchfrågor (CTAS och ITAS).

När en schemalagd fråga som misslyckas tio på varandra följande körningar registreras i en [!UICONTROL Quarantined] status. En fråga med den här statusen blir inaktiv och körs inte vid den schemalagda tidpunkten. Sedan måste du ingripa innan fler exekveringar kan utföras. Detta skyddar systemresurser eftersom du måste granska och korrigera problemen med din SQL innan fler körningar utförs.

Om du vill aktivera en schemalagd fråga för karantänfunktionen markerar du ellipserna (`...`) följt av [!UICONTROL Enable quarantine] i listrutan som visas.

![Fliken för schemalagda frågor med ellipserna och Aktivera karantän markerat i listrutan för infogade åtgärder.](../images/ui/monitor-queries/inline-enable.png)

Frågor kan också registreras i karantänfunktionen när schemat skapas. Se [dokumentation för frågescheman](./query-schedules.md#quarantine) för mer information.

## Fördröjning för frågekörning {#query-run-delay}

Ha full kontroll över beräkningstiden genom att ange varningar för fördröjning av frågor. Du kan övervaka frågeprestanda och få meddelanden om en frågas status inte ändras efter en viss period. Använd[!UICONTROL Query Run Delay]&#39; ska meddelas om en fråga fortsätter att bearbetas efter en viss tidsperiod utan att slutföras.

När du [prenumerera på aviseringar](#alert-subscription) för schemalagda frågekörningar är en av de tillgängliga varningarna [!UICONTROL Query Run Delay]. Den här varningen kräver att du anger en tröskel för hur lång tid som har ägnats åt att köra. Då får du ett meddelande om fördröjningen i bearbetningen.

Om du vill välja en tröskelvaraktighet som utlöser meddelandet anger du antingen ett tal i textinmatningsfältet eller använder upp- och nedpilarna för att öka i steg om en minut. Eftersom tröskelvärdet anges i minuter är den längsta tiden för att observera en fördröjning av frågekörning 1 440 minuter (24 timmar). Standardtidsperioden för en körningsfördröjning är 150 minuter.

>[!NOTE]
>
>En frågekörning kan bara ha en körfördröjningstid. Om du ändrar fördröjningströskeln ändras den för användaren som prenumererar på aviseringen och för hela organisationen.

![Dialogrutan Varningar på fliken för schemalagda frågor med inmatningsfältet för fördröjning av frågekörning markerat.](../images/ui/monitor-queries/query-run-delay-input.png)

Se avsnittet om prenumerationer på aviseringar om du vill veta mer om [prenumerera på [!UICONTROL Query Run Delay] varningar](#alert-subscription).

## Filtrera frågor {#filter}

Du kan filtrera frågor baserat på körningsfrekvens. Från [!UICONTROL Scheduled Queries] väljer du filterikonen (![En filterikon](../images/ui/monitor-queries/filter-icon.png)) för att öppna filtersidofältet.

![Fliken för schemalagda frågor med filterikonen markerad.](../images/ui/monitor-queries/filter-queries.png)

Om du vill filtrera listan med frågor baserat på deras körningsfrekvens väljer du antingen **[!UICONTROL Scheduled]** eller **[!UICONTROL Run once]** filterkryssrutor.

>[!NOTE]
>
>Alla frågor som har körts men inte schemalagts kvalificeras som [!UICONTROL Run once].

![Fliken för schemalagda frågor med filtersidofältet markerat.](../images/ui/monitor-queries/filter-sidebar.png)

När du har aktiverat filtervillkoren väljer du **[!UICONTROL Hide Filters]** för att stänga filterpanelen.

## Information om schemaläggning av frågekörningar {#query-runs}

Om du vill öppna sidan med schemainformation väljer du ett frågenamn på menyn [!UICONTROL Scheduled Queries] -fliken. Den här vyn innehåller en lista över alla körningar som har utförts som en del av den schemalagda frågan. Informationen omfattar start- och sluttid, status och datauppsättning som används.

![Sidan med schemainformation.](../images/ui/monitor-queries/schedule-details.png)

Den här informationen finns i en tabell med fem kolumner. Varje rad betecknar en frågekörning.

| Kolumnnamn | Beskrivning |
|---|---|
| **[!UICONTROL Query run ID]** | Frågekörnings-ID för daglig körning. Välj **[!UICONTROL Query run ID]** navigera till [!UICONTROL Query run overview]. |
| **[!UICONTROL Query run start]** | Tidsstämpeln när frågan kördes. Tidsstämpeln är i UTC-format. |
| **[!UICONTROL Query run complete]** | Tidsstämpeln när frågan slutfördes. Tidsstämpeln är i UTC-format. |
| **[!UICONTROL Status]** | Status för den senaste frågekörningen. Statusvärdena är: `Success`, `Failed`, `In progress`, eller `Quarantined`. |
| **[!UICONTROL Dataset]** | Den datauppsättning som ingår i körningen. |

Information om frågan som schemaläggs finns i [!UICONTROL Properties] -panelen. Panelen innehåller det inledande fråge-ID:t, klienttyp, mallnamn, frågans SQL-kod och schemats avslutning.

![Sidan med information om schemat med egenskapspanelen markerad.](../images/ui/monitor-queries/properties-panel.png)

Välj ett ID för frågekörning för att navigera till sidan med körningsinformation och visa frågeinformation.

![Skärmen med schemainformation och ett körnings-ID markerat.](../images/ui/monitor-queries/navigate-to-run-details.png)

## Översikt över frågekörning {#query-run-overview}

The [!UICONTROL Query run overview] ger information om enskilda körningar för den här schemalagda frågan och en mer detaljerad beskrivning av körningsstatusen. Den här sidan innehåller även klientinformation och information om eventuella fel som kan ha gjort att frågan misslyckades.

![Skärmen med körningsinformation med översiktsavsnittet markerat.](../images/ui/monitor-queries/query-run-details.png)

I avsnittet med frågestatus finns felkoden och felmeddelandet om frågan skulle ha misslyckats.

![Skärmen med körningsinformation med felavsnittet markerat.](../images/ui/monitor-queries/failed-query.png)

Du kan kopiera frågans SQL till Urklipp från den här vyn. Om du vill kopiera frågan väljer du kopieringsikonen i det övre högra hörnet av SQL-fragmentet. Ett popup-meddelande bekräftar att koden har kopierats.

![Skärmen med körningsinformation där SQL-kopieringsikonen är markerad.](../images/ui/monitor-queries/copy-sql.png)

### Kör information för frågor med anonymt block {#anonymous-block-queries}

Frågor som använder anonyma block för att bilda SQL-satser separeras till sina individuella underfrågor. Genom att dela upp i underfrågor kan du inspektera körningsinformationen för varje frågeblock individuellt.

>[!NOTE]
>
>Körningsinformationen för ett anonymt block som använder DROP-kommandot kommer att **not** rapporteras som en separat underfråga. Separata körningsdetaljer finns tillgängliga för CTAS-frågor, ITAS-frågor och COPY-satser som används som anonyma blockunderfrågor. Körningsinformation för DROP-kommandot stöds för närvarande inte.

Anonyma block markeras med en `$$` prefix före frågan. Mer information om anonyma block i frågetjänsten finns i [anonymt blockdokument](../key-concepts/anonymous-block.md).

Anonyma blockunderfrågor har tabbar till vänster om körningsstatusen. Välj en flik för att visa körningsinformation.

![Översikt över frågekörningen som visar en anonym blockfråga. Flerfrågeflikarna markeras.](../images/ui/monitor-queries/anonymous-block-overview.png)

Om en anonym blockfråga misslyckas, kan du hitta felkoden för just det blocket via det här användargränssnittet.

![Översikt över frågekörningen som visar en anonym blockfråga med felkoden för ett enskilt block markerat.](../images/ui/monitor-queries/anonymous-block-failed-query.png)

Välj **[!UICONTROL Query]** för att återgå till skärmen med schemainformation, eller **[!UICONTROL Scheduled Queries]** för att gå tillbaka till [!UICONTROL Scheduled Queries] -fliken.

![Skärmen med körningsinformation och frågan markerad.](../images/ui/monitor-queries/return-navigation.png)
