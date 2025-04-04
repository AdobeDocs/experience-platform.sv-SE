---
title: Parametriserade frågor
description: Lär dig hur du använder parametriserade frågor i Adobe Experience Platform-gränssnittet.
exl-id: 5c5ac691-5e29-4262-ba53-84dcc56e744f
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 0%

---

# Parametriserade frågor {#parameterized-queries}

>[!CONTEXTUALHELP]
>id="platform_queryService_queryEditor_parameterizedQueries"
>title="Parametriserade frågor"
>abstract="Använd parametriserade frågor för att lägga till parametervärden vid körningen. På så sätt kan du arbeta med dynamiska data och återanvända frågor för olika användningsområden. Använd preface `'$'` för att ange en frågeparameter i frågan i textredigeraren. Lägg sedan till ett värde för nyckeln i avsnittet Frågeparametrar nedanför redigeraren."

Frågetjänsten stöder användning av parametriserade frågor i Frågeredigeraren. Med parametriserade frågor kan du nu använda platshållare för parametrar och lägga till parametervärden vid körning. Med platshållare kan du arbeta med dynamiska data där du inte vet vilka värden som kommer att vara förrän programsatsen har körts. Du kan också förbereda dina frågor i förväg och återanvända dem för liknande syften. Att återanvända frågor sparar mycket arbete eftersom du slipper skapa distinkta SQL-frågor för varje användningsfall.

## Förhandskrav

Läs [Användargränssnittsguiden för frågeredigering](./user-guide.md) innan du fortsätter med den här guiden. Frågeredigeringsguiden ger detaljerad information om hur man skriver, validerar och kör frågor om kundupplevelsedata i Experience Platform användargränssnitt.

>[!NOTE]
>
>I Adobe Experience Platform-gränssnittet stöds parametriserade frågor bara på den överordnade nivån för textbundna mallar. Detta innebär att parametriserade frågor bara fungerar när de används i den ursprungliga mallen. Underordnade mallar måste vara en statisk mall och får inte ha dynamiska parametrar. Mer information finns i [dokumentationen för textbundna mallar](../key-concepts/inline-templates.md).

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

Om du vill skapa en parametriserad fråga i användargränssnittet går du till Frågeredigeraren. Mer information finns i avsnittet [Åtkomst till frågeredigeraren](./user-guide.md#accessing-query-editor).

Använd preface `'$'` för att ange en frågeparameter i frågan i textredigeraren. Välj sedan fliken **[!UICONTROL Query parameters]** bredvid [!UICONTROL Console] och lägg till det värde som saknas för nyckeln. Frågan kan inte utföras om du inte lägger till ett värde till någon av nycklarna. En varningsikon (![En varningsikon.](/help/images/icons/alert.png)) visas i avsnittet Frågeparametrar bredvid tomma [!UICONTROL Value] indatafält.

>[!NOTE]
>
>Om frågan inte innehåller några parametrar kan du ändå ange onödiga parametrar i Frågeredigeraren. Frågeredigeraren ignorerar alla onödiga nyckelvärdepar och påverkar inte körningen eller resultatet av frågan.

![Frågeredigeraren med en parametriserad fråga och avsnittet Frågeparametrar är markerat.](../images/ui/parameterized-queries/parameterized-query.png)

>[!TIP]
>
>Ändra flikar från [!UICONTROL Query parameters] till [!UICONTROL Console] för att visa konsolutdata för frågan.

## Använd frågeloggsdetaljer för att kontrollera parametervärden {#check-parameter-values}

Du kan inte spara parametrar i mallar eftersom de värden som används inte är beständiga. Du kan dock kontrollera sidan [!UICONTROL Query log details] för att hitta parametervärdena som används i en frågekörning. I det här fallet anger loggarna inte att frågan var en parametriserad fråga. I [frågeloggsdokumentationen](./query-logs.md) finns instruktioner om hur du hittar de värden som används.

![Vyn med frågeloggar med SQL för en parametriserad fråga markerad i informationsavsnittet.](../images/ui/parameterized-queries/parameterized-query-logs.png)

<!-- improve screenshot above ^ I am waiting for a scheduled run to complete -->

## Schemalägg en parametriserad fråga {#schedule}

Parametervärden sparas när du schemalägger en parametriserad fråga. Om du vill schemalägga en parametriserad fråga skapar du en schemalagd fråga enligt anvisningarna i guiden för att [skapa ett frågeschema](./query-schedules.md#create-schedule) och anger sedan parametervärdena som ska användas i frågekörningen. Det här användargränssnittsavsnittet visas bara för parametriserade frågor. Mer information finns i avsnittet [Ange parametrar för en schemalagd parametriserad fråga](./query-schedules.md#set-parameters).

>[!TIP]
>
>Frågetjänsten stöder förberedda satser med hjälp av parametriserade frågor. Mer information om SQL-syntaxen som ingår finns i [förberedda programsatser ](../sql/prepared-statements.md).

## Nästa steg

Genom att läsa det här dokumentet har du lärt dig att parametrisera frågor i Adobe Experience Platform-gränssnittet och använda dem i schemalagda frågekörningar. Dokumentet visade också hur loggarna skulle kontrolleras för parametervärden som används i frågekörningar.

Därefter rekommenderar vi att du läser guiden om [övervakning av schemalagda frågor](./monitor-queries.md) för att få en bättre förståelse för statusen för alla frågejobb via Experience Platform-gränssnittet.
