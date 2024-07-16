---
title: Microsoft Azure-tilläggsöversikt
description: Läs mer om Microsoft Azure-tillägget för vidarebefordran av händelser i Adobe Experience Platform.
exl-id: 2337d99d-861e-44e7-94ed-ba21ef28d815
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 1c417744518a7ac7cfb9c65d6af8219dcbc70d46
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---

# Översikt över tillägget [!DNL Microsoft Azure]

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. I följande [dokument](../../../term-updates.md) finns en konsoliderad referens till de ändrade terminologin.

I [!DNL Microsoft Azure] är [[!DNL Event Hubs]](https://azure.microsoft.com/en-us/products/event-hubs/#overview) en mycket skalbar datainpressningstjänst i realtid som gör att du kan bearbeta och analysera den enorma mängd data som produceras av dina anslutna enheter och program. När data har samlats in i ett händelsehubb kan de omformas och lagras med hjälp av en realtidsanalysleverantör eller batch-/lagringsadaptrar.

Tillägget [!DNL Microsoft Azure] [Vidarebefordra ](../../../ui/event-forwarding/overview.md) använder [!DNL Event Hubs] för att skicka händelser från Adobe Experience Platform Edge Network till [!DNL Azure] för vidare bearbetning. Den här guiden beskriver hur du installerar tillägget och använder dess funktioner i en regel för vidarebefordran av händelser.

## Förhandskrav

För att kunna använda det här tillägget måste du ha ett giltigt [!DNL Azure]-konto med åtkomst till [!DNL Event Hubs]. Du måste också [skapa ett händelsehubb med hjälp av  [!DNL Azure] portalen](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create) innan du följer stegen nedan.

## Installera tillägget

Om du vill installera Microsoft-tillägget [!DNL Azure] går du till användargränssnittet för datainsamlingen eller användargränssnittet för Experience Platform och väljer **[!UICONTROL Event Forwarding]** i den vänstra navigeringen. Här väljer du en egenskap som tillägget ska läggas till i eller skapar en ny egenskap i stället.

När du har markerat eller skapat den önskade egenskapen väljer du **[!UICONTROL Extensions]** i den vänstra navigeringen och väljer sedan fliken **[!UICONTROL Catalog]**. Sök efter kortet [!UICONTROL Microsoft Azure] och välj sedan **[!UICONTROL Install]**.

![Knappen [!UICONTROL Install] som väljs för tillägget [!UICONTROL Microsoft Azure] i användargränssnittet för datainsamling.](../../../images/extensions/server/azure/install.png)

Eftersom tillägget inte har några konfigurationsegenskaper läggs det omedelbart till i listan över installerade tillägg. Du kan nu börja använda åtgärdstyperna [!DNL Event Hub] när du konfigurerar regler för vidarebefordran av händelser.

## Konfigurera en regel för vidarebefordran av händelser {#rule}

Börja skapa en ny regel för vidarebefordring av händelser och konfigurera villkoren efter behov. När du väljer åtgärder för regeln väljer du **[!UICONTROL Microsoft Azure]** som tillägg och sedan **[!UICONTROL Send Data to Event Hubs]** som åtgärdstyp.

![Åtgärdstypen [!UICONTROL Send Data to Event Hubs] som väljs för en regel i användargränssnittet för datainsamling.](../../../images/extensions/server/azure/select-action-type.png)

Den högra panelen uppdateras och visar konfigurationsalternativ för hur data ska skickas. Du måste tilldela [dataelement](../../../ui/managing-resources/data-elements.md) till de olika egenskaper som representerar din [!DNL Event Hub]-konfiguration.

![Konfigurationsalternativen för åtgärdstypen [!UICONTROL Send Data to Event Hubs] som visas i gränssnittet.](../../../images/extensions/server/azure/event-hub-details.png)

**[!UICONTROL Event Hub Details]**

| Indata | Beskrivning |
| --- | --- |
| [!UICONTROL Namespace] | Namnet på det [!DNL Event Hubs]-namnområde som du skapade när [händelsehubben ](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace) konfigurerades. |
| [!UICONTROL Name] | Namnet på händelsehubben. |
| [!UICONTROL SAS Authorization Rule Name] | Namnet på auktoriseringsregeln för delad åtkomst för hela [!DNL Event Hubs]-namnområdet eller den specifika händelsehubbsinstansinstansen som du vill skicka data till. Mer information finns i bilagan om [att erhålla SAS-auktoriseringsvärden](#sas). |
| [!UICONTROL SAS Access Key] | Den primära nyckeln för auktoriseringsregeln för delad åtkomst för hela [!DNL Event Hubs]-namnområdet eller den specifika händelsehubbsinstansinstansen som du vill skicka data till. Mer information finns i bilagan om [att erhålla SAS-auktoriseringsvärden](#sas). |
| [!UICONTROL Partition ID] | Med [!DNL Event Hubs] kan du [skicka händelser direkt till specifika partitioner](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/event-hubs/partitioning-in-event-hubs-and-kafka). Om du vill använda den här funktionen anger du ID:t för den partition som du vill ta emot händelserna. |

{style="table-layout:auto"}

**Data**

| Indata | Beskrivning |
| --- | --- |
| [!UICONTROL Payload] | Det här fältet innehåller de data som kommer att vidarebefordras till [!DNL Event Hubs]. Data kan vara ett JSON-objekt, en sträng eller ett dataelement. |

{style="table-layout:auto"}

När du är klar väljer du **[!UICONTROL Keep Changes]** för att lägga till åtgärden i regelkonfigurationen. När du är nöjd med regeln väljer du **[!UICONTROL Save to Library]**.

Publicera slutligen en ny händelse som vidarebefordrar [build](../../../ui/publishing/builds.md) för att aktivera ändringarna i biblioteket.

## Nästa steg

I den här guiden beskrivs hur du skickar data till [!DNL Event Hubs] med hjälp av tillägget [!DNL Microsoft Azure] för vidarebefordran av händelser. Mer information om funktioner för att vidarebefordra händelser i Experience Platform finns i [översikten över vidarebefordran av händelser](../../../ui/event-forwarding/overview.md).

## Bilaga: Hämta SAS-auktoriseringsvärden {#sas}

Externa program beviljas åtkomst till [!DNL Event Hubs] via [delade åtkomstsignaturer (SAS)](https://learn.microsoft.com/en-us/azure/event-hubs/authorize-access-shared-access-signature). Varje [!DNL Event Hubs]-namnrymd och händelsehubbsinstans tilldelas automatiskt en standard-SAS-auktoriseringsregel när den skapas, men du kan också skapa ytterligare principer för varje resurs om du vill.

När [konfigurerar en regel för vidarebefordran av händelser](#rule) med tillägget [!DNL Azure] måste du ange namnet och primärnyckeln för auktoriseringsregeln som styr det namnområde eller den specifika händelsehubb som du vill skicka data till. Mer information om hur du hämtar dessa värden från portalen [!DNL Azure] finns i följande avsnitt i dokumentationen för [!DNL Azure]:

* [Hämta SAS-värden för ett  [!DNL Event Hubs] namnutrymme](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-namespace)
* [Hämta SAS-värden för en specifik händelsehubb i ett namnutrymme](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-specific-event-hub-in-a-namespace)

När du har de obligatoriska värdena kan auktoriseringsregelnamnet anges direkt som en sträng i config-indata eller så kan du skapa ett dataelement av strängtyp för att referera till det i stället. Primärnyckeln måste dock först finnas inuti en händelsevidarebefordringshemlighet innan den kan anges i regelkonfigurationen för att skydda din datasäkerhet.

I gränssnittet för vidarebefordran av händelser skapar [en ny hemlighet](../../../ui/event-forwarding/secrets.md) och väljer **[!UICONTROL Token]** som hemlig typ. Ange primärnyckeln som du kopierade tidigare för själva tokenvärdet. När du har skapat hemligheten skapar du ett dataelement med typen **[!UICONTROL Secret]** och väljer [!DNL Event Hubs]-hemligheten i listan. När det hemliga dataelementet har konfigurerats kan du referera till det dataelementet i fältet **[!UICONTROL SAS Access Key]**.
