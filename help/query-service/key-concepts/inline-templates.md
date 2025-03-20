---
title: Textbundna mallar
description: Lär dig återanvända flera villkor i flera frågor med infogade mallar.
exl-id: 78959070-f9e5-4736-b72a-a8ef518bfa4f
source-git-commit: ef4c7f20710f56ca0de7c0dfdb99751ff2fe8ebe
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# Textbundna mallar

Med infogade mallar kan du återanvända flera villkor i flera frågor. Du kan spara villkor i en mall och sedan återanvända dem i flera frågor. Återanvändbara SQL-mallar minskar utvecklingsarbetet och risken för fel när långa satser kopieras mellan frågor. Med textbundna mallar kan du göra ändringar på en plats och låta dessa ändringar återspeglas i alla frågor som refererar till den här mallen.

Det här dokumentet innehåller information om användning och begränsningar för infogade mallar i Frågeredigeraren.

## Förhandskrav

Textbundna mallar stöds både av API:t för användargränssnittet och frågetjänsten. Läs dokumentationen om hur du [skapar en frågemall via API:t ](../api/query-templates.md#create-a-query-template) eller med [frågeredigeraren](../ui/user-guide.md#query-authoring) innan du fortsätter med den här guiden.

## Syntax för infogad mall {#syntax}

När en fråga har sparats kallas den en mall. När mallen refererar till en annan mall i programsatsen kallas den för en infogad mall. Textbundna mallar anges i SQL med hash-symbolen (#) följt av mallnamnet. Ett exempel på denna syntax är `#YOUR_TEMPLATE_NAME`.

## Användningsfall {#use-case}

I följande SQL-mallar visas hur användbart det är att använda textbundna mallar, med ett exempel som räknar antalet amerikanska kunder från en region som spenderat mer än &#39;maximal intäkt&#39; och som beställts före juni 2023. Fördelen med den infogade mallen är att du enkelt kan redigera den underordnade mallen (i det här fallet det maximala intäkt- och orderdatumet) och inte behöver ändra den överordnade mallen.

**Exempel**

```sql
#parent_template : SELECT count(*) FROM customer WHERE region=NA AND country=US AND revenue > #revenue_max
#revenue_max: SELECT max(revenue) FROM revenue_table WHERE order_date > '01-06-2023'
```

När frågan körs ersätter frågetjänsten mallnamnet med början från hash-symbolen med den namngivna mallens SQL-sats.

>[!NOTE]
>
>Frågemallar kan anropa valfritt antal andra infogade mallar. Det finns ingen begränsning för hur många infogade mallar du kan anropa från en enstaka fråga. Mallar kan också kapslas i andra infogade mallar.

Du kan använda mallar för att lagra ett eller flera villkor. De behöver inte vara en komplett fråga själva. Om mallen innehåller en giltig fråga kan du köra frågan genom att anropa mallnamnet som föregås av en hash-symbol. Om du till exempel lagrade `SELECT * FROM JUNE_2023_LOYALTY_MEMBERS;` som en mall med namnet `JUNE_2023_LOYALTY_MEMBERS` kör kommandot `#JUNE_2023_LOYALTY_MEMBERS;` den giltiga frågan som finns i mallen.

>[!NOTE]
>
>I Adobe Experience Platform-användargränssnittet stöds textbundna mallar i form av parametriserade frågor bara på överordnad nivå. Detta innebär att parametriserade frågor bara fungerar när de används i den ursprungliga mallen. Den underordnade mallen måste vara en statisk mall och kan inte ha dynamiska parametrar. Mer information finns i [dokumentationen för parametriserade frågor](../ui/parameterized-queries.md).

## Nästa steg

När du har läst det här dokumentet vet du nu hur du refererar till andra mallar i SQL, antingen i frågeredigeraren eller via API:t för frågetjänsten.

Dessutom bör du läsa [guiden för anonyma block](./anonymous-block.md), som förklarar hur du minimerar utvecklingsutgifter genom att länka en eller flera SQL-satser som körs i sekvens.
