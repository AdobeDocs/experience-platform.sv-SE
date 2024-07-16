---
title: Frågemallar
description: Frågemallar är återanvändbara sparade SQL-frågor som kan återanvändas av andra användare för att spara tid och arbete. De kan skapas med Frågeredigeraren eller API:t för frågetjänsten och är tillgängliga för användning på alla Experience Platform-datauppsättningar.
exl-id: e74d058f-bb89-45ed-83cc-2e3a33401270
source-git-commit: 1a44be939a4678078b414658199472e07dee153b
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---

# Frågemallar

Med Adobe Experience Platform Query Service kan du spara och återanvända SQL-kod i form av frågemallar. Mallar sparar arbete eftersom de ofta utförda uppgifterna inte behöver upprepas. Du kan dela mallar inom organisationen och enkelt ändra frågevärdena utan att behöva komma åt eller förstå underliggande SQL.

Det här dokumentet innehåller den information som behövs för att skapa frågemallar i Query Service.

## Förhandskrav

Du måste ha behörigheten [!UICONTROL Manage queries] aktiverad för att få åtkomst till Frågeredigeraren och visa frågeinstrumentpanelen i plattformsgränssnittet. Behörigheten aktiveras via Adobe [Admin Console](https://adminconsole.adobe.com/). Kontakta organisationens administratör om du inte har administratörsbehörighet för att aktivera den här behörigheten. I åtkomstkontrollsdokumentationen finns [fullständiga instruktioner om hur du lägger till behörigheter via Admin Console](../../access-control/home.md).

## Skapa en frågemall

Du kan skapa frågemallar på två sätt, antingen genom att göra en POST-förfrågan till frågetjänstens API `query-templates`-slutpunkt eller genom att skriva, namnge och spara en fråga med Frågeredigeraren.

### Använda Frågeredigeraren för att redigera och spara en fråga som en mall

I dokumentationen finns instruktioner om hur du använder Frågeredigeraren för att [skriva](./user-guide.md#query-authoring) och [spara frågor](./user-guide.md#saving-queries). När du har namngett och sparat frågan kan den återanvändas som en frågemall på fliken [!UICONTROL Templates].

>[!TIP]
>
>När du sparar en fråga i Frågeredigeraren visas ett bekräftelsemeddelande som informerar dig om den slutförda åtgärden. Det här popup-meddelandet innehåller en länk som gör det enkelt att navigera till arbetsytan för schemaläggning av frågor. Läs [dokumentationen för schemafrågor](./query-schedules.md) om du vill veta hur du kör frågor på en anpassad cache.

## Bläddra bland frågemallar {#browse}

Välj **[!UICONTROL Templates]** på arbetsytan Frågor i plattformsgränssnittet för att visa listan över tillgängliga sparade frågor.

![Arbetsytan för frågor med fliken Mallar markerad.](../images/ui/query-templates/query-templates.png)

Om du vill hitta relevant mallinformation väljer du en frågemall i den tillgängliga listan för att öppna informationspanelen.

![Informationspanelen på arbetsytan för frågor med fråge-ID markerat.](../images/ui/query-templates/details-panel.png)

På informationspanelen kan du utföra följande åtgärder:

* Välj **[!UICONTROL Run as CTAS]** om du vill skapa en ny tabell genom att välja data från en befintlig tabell eller tabeller. Det här alternativet är bara tillgängligt om du har en SELECT-fråga.
* Välj **[!UICONTROL Add schedule]** om du vill börja redigera ditt schema för din frågemall.
* Välj **[!UICONTROL View schedule]** om du vill gå till fliken [!UICONTROL Schedules] i Frågeredigeraren. Den här vyn innehåller schemainformation som är kopplad till frågan.
* Välj **[!UICONTROL Delete query]** om du vill ta bort mallen.
* Välj mallnamnet för att navigera till Frågeredigeraren där SQL är förifylld för redigering.

### Använd API:t för frågetjänsten för att skapa en mall

I dokumentationen finns instruktioner om [hur du skapar en frågemall](../api/query-templates.md#create-a-query-template) med hjälp av API:t för frågetjänsten. Information om en ny frågemall finns i svarstexten.

>[!NOTE]
>
>Mallar som skapas med API:t visas också på fliken Mallar för plattformsgränssnittstjänst.

## Nästa steg

Genom att läsa det här dokumentet får du nu en bättre förståelse för hur du skapar frågemallar i Query Service. Se [användargränssnittsöversikt](./overview.md) eller [API-handboken för frågetjänsten](../api/getting-started.md) om du vill veta mer om funktionerna i frågetjänsten.

Se [slutpunktshandboken för schemalagda frågor](../api/scheduled-queries.md) om du vill veta hur du schemalägger frågor med API:t eller [Frågeredigeringsguiden](./user-guide.md#scheduled-queries) för användargränssnittet.
