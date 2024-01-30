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

## Förutsättningar

Du måste ha [!UICONTROL Manage queries] behörighet har aktiverats för att komma åt frågeredigeraren och visa frågeinstrumentpanelen i plattformsgränssnittet. Behörigheten aktiveras via Adobe [Admin Console](https://adminconsole.adobe.com/). Kontakta organisationens administratör om du inte har administratörsbehörighet för att aktivera den här behörigheten. Dokumentation om åtkomstkontroll finns i [fullständiga anvisningar om hur du lägger till behörigheter via Admin Console](../../access-control/home.md).

## Skapa en frågemall

Du kan skapa frågemallar på två sätt, antingen genom att göra en POST-förfrågan till API:t för frågetjänsten `query-templates` genom att skriva, namnge och spara en fråga via Frågeredigeraren.

### Använda Frågeredigeraren för att redigera och spara en fråga som en mall

I dokumentationen finns instruktioner om hur du använder Frågeredigeraren för att [skriva](./user-guide.md#query-authoring) och [spara frågor](./user-guide.md#saving-queries). När du har namngett och sparat frågan kan den återanvändas som en frågemall från [!UICONTROL Templates] -fliken.

>[!TIP]
>
>När du sparar en fråga i Frågeredigeraren visas ett bekräftelsemeddelande som informerar dig om den slutförda åtgärden. Det här popup-meddelandet innehåller en länk som gör det enkelt att navigera till arbetsytan för schemaläggning av frågor. Se [dokumentation för schemafrågor](./query-schedules.md) om du vill lära dig hur du kör frågor på en anpassad cadence.

## Bläddra bland frågemallar {#browse}

På arbetsytan Frågor i plattformsgränssnittet väljer du **[!UICONTROL Templates]** om du vill visa en lista med tillgängliga sparade frågor.

![Frågearbetsytan med fliken Mallar markerad.](../images/ui/query-templates/query-templates.png)

Om du vill hitta relevant mallinformation väljer du en frågemall i den tillgängliga listan för att öppna informationspanelen.

![Panelen Detaljer på arbetsytan Frågor med fråge-ID markerat.](../images/ui/query-templates/details-panel.png)

På informationspanelen kan du utföra följande åtgärder:

* Välj **[!UICONTROL Run as CTAS]** om du vill skapa en ny tabell genom att välja data från en befintlig tabell eller tabeller. Det här alternativet är bara tillgängligt om du har en SELECT-fråga.
* Välj **[!UICONTROL Add schedule]** för att börja redigera ditt schema för din frågemall.
* Välj **[!UICONTROL View schedule]** navigera till [!UICONTROL Schedules] i frågeredigeraren. Den här vyn innehåller schemainformation som är kopplad till frågan.
* Välj **[!UICONTROL Delete query]** för att ta bort mallen.
* Välj mallnamnet för att navigera till Frågeredigeraren där SQL är förifylld för redigering.

### Använd API:t för frågetjänsten för att skapa en mall

I dokumentationen finns instruktioner om [skapa en frågemall](../api/query-templates.md#create-a-query-template) med hjälp av API:t för frågetjänsten. Information om en ny frågemall finns i svarstexten.

>[!NOTE]
>
>Mallar som skapas med API:t visas också på fliken Mallar för plattformsgränssnittstjänst.

## Nästa steg

Genom att läsa det här dokumentet får du nu en bättre förståelse för hur du skapar frågemallar i Query Service. Se [Översikt över användargränssnittet](./overview.md)eller [API-guide för frågetjänst](../api/getting-started.md) om du vill veta mer om funktionerna i frågetjänsten.

Se [slutpunktsguide för schemalagda frågor](../api/scheduled-queries.md) om du vill veta hur du schemalägger frågor med API:t eller [Frågeredigeringsguide](./user-guide.md#scheduled-queries) för användargränssnittet.
