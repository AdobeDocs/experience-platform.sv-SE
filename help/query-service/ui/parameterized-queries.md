---
title: Parametriserade frågor
description: Lär dig hur du använder parametriserade frågor i Adobe Experience Platform-gränssnittet.
exl-id: 5c5ac691-5e29-4262-ba53-84dcc56e744f
source-git-commit: 9cf8dabfdf3f20f4032a79ba191bd2dc8123a369
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 0%

---

# Parametriserade frågor {#parameterized-queries}

>[!CONTEXTUALHELP]
>id="platform_queryService_queryEditor_parameterizedQueries"
>title="Parametriserade frågor"
>abstract="Använd parametriserade frågor för att lägga till parametervärden vid körningen. På så sätt kan du arbeta med dynamiska data och återanvända frågor för olika användningsområden. Använd `'$'` för att ange en frågeparameter i frågan i textredigeraren. Lägg sedan till ett värde för nyckeln i avsnittet Frågeparametrar nedanför redigeraren."

Frågetjänsten stöder användning av parametriserade frågor i Frågeredigeraren. Med parametriserade frågor kan du nu använda platshållare för parametrar och lägga till parametervärden vid körning. Med platshållare kan du arbeta med dynamiska data där du inte vet vilka värden som kommer att vara förrän programsatsen har körts. Du kan också förbereda dina frågor i förväg och återanvända dem för liknande syften. Att återanvända frågor sparar mycket arbete eftersom du slipper skapa distinkta SQL-frågor för varje användningsfall.

## Förutsättningar

Innan du fortsätter med den här guiden ska du läsa [Användargränssnittshandbok för frågeredigeraren](./user-guide.md). Frågeredigeringsguiden ger detaljerad information om hur man skriver, validerar och kör frågor om kundupplevelsedata i användargränssnittet i Experience Platform.

>[!NOTE]
>
>I Adobe Experience Platform-gränssnittet stöds parametriserade frågor bara på den överordnade nivån för textbundna mallar. Detta innebär att parametriserade frågor bara fungerar när de används i den ursprungliga mallen. Underordnade mallar måste vara en statisk mall och får inte ha dynamiska parametrar. Se [dokumentation för infogade mallar](../key-concepts/inline-templates.md) om du vill veta mer.

## Parametriserad frågesyntax {#syntax}

Parametriserade frågor använder formatet `'$YOUR_PARAMETER_NAME'` och kan sammanfogas med punktnotation. Ett exempel på en SQL-sats som använder parametriserade frågor visas nedan.

```sql
INSERT INTO
   $Database_Name.Schema_Name.adwh_lkup_process_delta_log
   (process_name, merge_policy_id, process_status, process_date, create_ts, change_ts)
SELECT
   '$Table_Process_Name' process_name,
   hash('$Merge_PolicyID') merge_policy_id,
   '$process_status' process_status,
   to_date('$date_key') process_date,
   CURRENT_TIMESTAMP create_ts,
   CURRENT_TIMESTAMP change_ts;
```

## Skapa en parametriserad fråga {#create}

Om du vill skapa en parametriserad fråga i användargränssnittet går du till Frågeredigeraren. Se avsnittet om [få åtkomst till Frågeredigeraren](./user-guide.md#accessing-query-editor) för fler instruktioner.

Använd `'$'` för att ange en frågeparameter i frågan i textredigeraren. Nästa steg är att välja **[!UICONTROL Query parameters]** -fliken bredvid [!UICONTROL Console] lägger till det saknade värdet för nyckeln. Frågan kan inte utföras om du inte lägger till ett värde till någon av nycklarna. En varningsikon (![En varningsikon.](../images/ui/parameterized-queries/alert-icon.png)) visas i avsnittet Frågeparametrar bredvid eventuella tomma [!UICONTROL Value] indatafält.

>[!NOTE]
>
>Om frågan inte innehåller några parametrar kan du ändå ange onödiga parametrar i Frågeredigeraren. Frågeredigeraren ignorerar alla onödiga nyckelvärdepar och påverkar inte körningen eller resultatet av frågan.

![Frågeredigeraren med en parametriserad fråga och avsnittet Frågeparametrar markerat.](../images/ui/parameterized-queries/parameterized-query.png)

>[!TIP]
>
>Ändra tabbar från [!UICONTROL Query parameters] till [!UICONTROL Console] för att visa konsolutdata för frågan.

## Använd frågeloggsdetaljer för att kontrollera parametervärden {#check-parameter-values}

Du kan inte spara parametrar i mallar eftersom de värden som används inte är beständiga. Du kan dock kontrollera [!UICONTROL Query log details] för att hitta parametervärdena som används i en frågekörning. I det här fallet anger loggarna inte att frågan var en parametriserad fråga. Se [dokumentation för frågeloggar](./query-logs.md) för instruktioner om hur du hittar de värden som används.

![Vyn med frågeloggar med SQL för en parametriserad fråga markerad i informationsavsnittet.](../images/ui/parameterized-queries/parameterized-query-logs.png)

<!-- improve screenshot above ^ I am waiting for a scheduled run to complete -->

## Schemalägg en parametriserad fråga {#schedule}

Parametervärden sparas när du schemalägger en parametriserad fråga. Om du vill schemalägga en parametriserad fråga följer du den vanliga processen och skapar en schemalagd fråga enligt anvisningarna i guiden för att [skapa ett frågeschema](./query-schedules.md#create-schedule)anger du sedan parametervärdena som ska användas i frågekörningen. Det här användargränssnittsavsnittet visas bara för parametriserade frågor. Se avsnittet om [ställa in parametrar för en schemalagd parametriserad fråga](./query-schedules.md#set-parameters) för specifika instruktioner.

>[!TIP]
>
>Frågetjänsten stöder förberedda satser med hjälp av parametriserade frågor. Se [guide för förberedda programsatser](../sql/prepared-statements.md) om du vill ha mer information om SQL-syntaxen.

## Nästa steg

Genom att läsa det här dokumentet har du lärt dig att parametrisera frågor i Adobe Experience Platform-gränssnittet och använda dem i schemalagda frågekörningar. Dokumentet visade också hur loggarna skulle kontrolleras för parametervärden som används i frågekörningar.

Därefter rekommenderar vi att du läser guiden [övervaka schemalagda frågor](./monitor-queries.md) för att få en bättre förståelse för statusen för alla frågejobb via plattformens användargränssnitt.
