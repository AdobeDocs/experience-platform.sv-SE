---
title: Hantera förfallodatum för datauppsättning
description: Lär dig hur du schemalägger en förfallotid för en datauppsättning i Adobe Experience Platform-gränssnittet.
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: a1628df7d0eefc795d1eaeefce842a65c7133322
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 0%

---

# Hantera förfallodatum för datauppsättning {#dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_description"
>title="Ta bort oönskade eller utgångna kundposter och datauppsättningar"
>abstract="<h2>Beskrivning</h2><p>Om du vill hantera livscykeln för dina Experience Platform-data som inte har att göra med efterlevnad av gällande bestämmelser, kan du ta bort konsumentposter och schemalägga förfallodatum för datauppsättningar. Om du vill skapa eller hantera förfrågningar från registrerade personer kan du läsa fallblocket&quot;Hedra in data subject privacy requests&quot;.</p>"

>[!IMPORTANT]
>
>Datahygien i Adobe Experience Platform är för närvarande endast tillgänglig för organisationer som har köpt **Adobe Healthcare Shield** eller **Adobe Privacy &amp; Security Shield**. De här funktionerna kommer att lanseras inom en snar framtid. Om du vill ha mer information om hur de kommer att bli tillgängliga kontaktar du Adobes servicerepresentant. Du kan dock göra det omedelbart [ta bort datauppsättningar via [!UICONTROL Datasets] UI](../../catalog/datasets/user-guide.md#delete).

The [[!UICONTROL Data Hygiene] arbetsyta](./overview.md) i Adobe Experience Platform UI kan du schemalägga förfallotider för datauppsättningar. När en datauppsättning når sitt förfallodatum startar datasjön, identitetstjänsten och kundprofilen i realtid separata processer för att ta bort datauppsättningens innehåll från sina respektive tjänster. När data har tagits bort från alla tre tjänsterna markeras förfallotiden som slutförd.

>[!WARNING]
>
>Om en datauppsättning är inställd på att förfalla måste du manuellt ändra alla dataflöden som kan inhämta data till datauppsättningen så att dina efterföljande arbetsflöden inte påverkas negativt.

Det här dokumentet beskriver hur du schemalägger och hanterar förfallodatum för datauppsättningar i plattformsgränssnittet.

## Schemalägg ett förfallodatum för datauppsättning {#schedule-dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_instructions"
>title="Instruktioner"
>abstract="<ul><li>Välj <a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/overview.html">Datahygien</a> i den vänstra navigeringen väljer du <b>Skapa förfrågan</b>.</li><li>Om du vill ta bort poster:</li>   <li>Välj <b>Post</b>.</li>   <li>Välj en specifik datauppsättning att ta bort poster från eller välj alternativet att ta bort dem från alla datauppsättningar.</li>   <li>Ange identiteten på de konsumenter vars register ska raderas. Välj <b>Lägg till identitet</b> för att tillhandahålla identiteterna en i taget eller välja <b>Välj filer</b> för att i stället överföra en JSON-fil med identiteter.</li>   <li>Välj <b>Mall</b> för att visa det förväntade formatet för JSON-filen.</li><li>Instruktioner finns i dokumentationen om du vill <a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/dataset-expiration.html#schedule-dataset-expiration">schemats förfallodatum för datauppsättningar</a>.</li></ul>"

Om du vill skapa en ny begäran väljer du **[!UICONTROL Create request]** från huvudsidan på arbetsytan.

![Bilden visar [!UICONTROL Create request] knappen markeras](../images/ui/ttl/create-request-button.png)

Dialogrutan där begäran skapas visas. Under **[!UICONTROL Requested Action]** avsnitt, markera **[!UICONTROL Delete Dataset]** om du vill uppdatera de tillgängliga kontrollerna för schemaläggning av datauppsättningens förfallodatum.

![Bilden visar [!UICONTROL Create request] knappen markeras](../images/ui/ttl/dataset-selected.png)

### Välj ett datum och en datauppsättning

Dialogrutan där begäran skapas visas. Under **[!UICONTROL Requested Action]** väljer du ett datum som du vill att datauppsättningen ska tas bort av. Du kan ange datumet manuellt (i formatet `mm/dd/yyyy`) eller välj kalenderikonen (![Bild på kalenderikonen](../images/ui/ttl/calendar-icon.png)) för att välja datumet i en dialogruta.

![Bild som visar ett förfallodatum som anges för datauppsättningen](../images/ui/ttl/select-date.png)

Nästa, under **[!UICONTROL Dataset Details]**, markerar du databasikonen (![Bild på databasikonen](../images/ui/ttl/database-icon.png)) för att öppna en dialogruta för val av datauppsättning. Välj en datauppsättning i listan som du vill tillämpa förfallodatumet på och välj sedan **[!UICONTROL Done]**.

![Bild som visar vilken datauppsättning som väljs](../images/ui/ttl/select-dataset.png)

>[!NOTE]
Endast datauppsättningar som tillhör den aktuella sandlådan visas.

### Skicka begäran

The [!UICONTROL Dataset Details] fyller i så att den primära identiteten och schemat för den valda datauppsättningen inkluderas. Under **[!UICONTROL Request settings]**, ange ett namn och en valfri beskrivning för begäran, följt av **[!UICONTROL Submit]**.

![Bilden visar [!UICONTROL Submit] knappen markeras](../images/ui/ttl/submit.png)

Du ombeds bekräfta datumet då datauppsättningen ska tas bort senast. Välj **[!UICONTROL Submit]** för att fortsätta.

När begäran har skickats skapas en arbetsorder och visas på huvudfliken i [!UICONTROL Data Hygiene] arbetsyta. Härifrån kan du övervaka arbetsorderns status medan den bearbetar begäran.

>[!NOTE]
Se översiktsavsnittet i [tidslinjer och genomskinlighet](../home.md#dataset-expiration-transparency) om du vill ha information om hur datauppsättningens förfallodatum behandlas när de har körts.

## Redigera eller avbryta en förfallotid för en datauppsättning

Om du vill redigera eller avbryta en förfallotid för en datauppsättning väljer du **[!UICONTROL Dataset]** på arbetsytans huvudsida och välj datauppsättningens förfallodatum i listan.

På informationssidan om datauppsättningens förfallodatum, visar den högra listen kontroller för att redigera eller avbryta den schemalagda borttagningen.

## Nästa steg

I det här dokumentet beskrivs hur du schemalägger förfallodatum för datauppsättningar i användargränssnittet i Experience Platform. Mer information om hur du utför andra datahygienuppgifter i användargränssnittet finns i [översikt över användargränssnittet för datahygien](./overview.md).

Om du vill lära dig hur du schemalägger förfallodatum för datauppsättningar med hjälp av API:t för datahygien kan du läsa [Slutpunktshandbok för datauppsättningens förfallodatum](../api/dataset-expiration.md).
