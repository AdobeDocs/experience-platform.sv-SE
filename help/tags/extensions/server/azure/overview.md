---
title: Microsoft Azure-tilläggsöversikt
description: Läs mer om Microsoft Azure-tillägget för vidarebefordran av händelser i Adobe Experience Platform.
exl-id: 2337d99d-861e-44e7-94ed-ba21ef28d815
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 1c417744518a7ac7cfb9c65d6af8219dcbc70d46
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 0%

---

# [!DNL Microsoft Azure] tilläggsöversikt

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

I [!DNL Microsoft Azure], [[!DNL Event Hubs]](https://azure.microsoft.com/en-us/products/event-hubs/#overview) är en mycket skalbar dataindatatjänst i realtid som gör att du kan bearbeta och analysera den enorma mängd data som produceras av dina anslutna enheter och program. När data har samlats in i ett händelsehubb kan de omformas och lagras med hjälp av en realtidsanalysleverantör eller batch-/lagringsadaptrar.

The [!DNL Microsoft Azure] [händelsevidarebefordran](../../../ui/event-forwarding/overview.md) utbyggnadsutfall [!DNL Event Hubs] för att skicka händelser från Adobe Experience Platform Edge Network till [!DNL Azure] för vidare bearbetning. Den här guiden beskriver hur du installerar tillägget och använder dess funktioner i en regel för vidarebefordran av händelser.

## Förutsättningar

För att kunna använda det här tillägget måste du ha ett giltigt [!DNL Azure] konto med tillgång till [!DNL Event Hubs]. Du måste också [skapa en händelsehubb med [!DNL Azure] portal](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create) innan du följer stegen nedan.

## Installera tillägget

Installera Microsoft [!DNL Azure] navigerar du till användargränssnittet för datainsamling eller användargränssnittet för Experience Platform och väljer **[!UICONTROL Event Forwarding]** från vänster navigering. Här väljer du en egenskap som tillägget ska läggas till i eller skapar en ny egenskap i stället.

När du har markerat eller skapat den önskade egenskapen väljer du **[!UICONTROL Extensions]** i den vänstra navigeringen väljer du **[!UICONTROL Catalog]** -fliken. Sök efter [!UICONTROL Microsoft Azure] kort, välj **[!UICONTROL Install]**.

![The [!UICONTROL Install] knappen som markeras för [!UICONTROL Microsoft Azure] i användargränssnittet för datainsamling.](../../../images/extensions/server/azure/install.png)

Eftersom tillägget inte har några konfigurationsegenskaper läggs det omedelbart till i listan över installerade tillägg. Nu kan du börja använda [!DNL Event Hub] åtgärdstyper när regler för vidarebefordran av händelser konfigureras.

## Konfigurera en regel för vidarebefordran av händelser {#rule}

Börja skapa en ny regel för vidarebefordring av händelser och konfigurera villkoren efter behov. När du väljer åtgärder för regeln väljer du **[!UICONTROL Microsoft Azure]** för tillägget väljer du **[!UICONTROL Send Data to Event Hubs]** för åtgärdstyp.

![The [!UICONTROL Send Data to Event Hubs] åtgärdstypen som väljs för en regel i användargränssnittet för datainsamling.](../../../images/extensions/server/azure/select-action-type.png)

Den högra panelen uppdateras och visar konfigurationsalternativ för hur data ska skickas. Du måste tilldela [dataelement](../../../ui/managing-resources/data-elements.md) till de olika egenskaper som representerar [!DNL Event Hub] konfiguration.

![Konfigurationsalternativen för [!UICONTROL Send Data to Event Hubs] åtgärdstyp som visas i användargränssnittet.](../../../images/extensions/server/azure/event-hub-details.png)

**[!UICONTROL Event Hub Details]**

| Indata | Beskrivning |
| --- | --- |
| [!UICONTROL Namespace] | Namnet på [!DNL Event Hubs] namnutrymme som du skapade [konfigurera händelsehubben](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace). |
| [!UICONTROL Name] | Namnet på händelsehubben. |
| [!UICONTROL SAS Authorization Rule Name] | Namnet på auktoriseringsregeln för delad åtkomst för hela din [!DNL Event Hubs] namnutrymme eller den specifika händelsehubbsinstans som du vill skicka data till. Se avsnittet om bilagan [hämta SAS-auktoriseringsvärden](#sas) för mer information. |
| [!UICONTROL SAS Access Key] | Primärnyckeln för auktoriseringsregeln för delad åtkomst för hela din [!DNL Event Hubs] namnutrymme eller den specifika händelsehubbsinstans som du vill skicka data till. Se avsnittet om bilagan [hämta SAS-auktoriseringsvärden](#sas) för mer information. |
| [!UICONTROL Partition ID] | [!DNL Event Hubs] låter dig [skicka händelser direkt till specifika partitioner](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/event-hubs/partitioning-in-event-hubs-and-kafka). Om du vill använda den här funktionen anger du ID:t för den partition som du vill ta emot händelserna. |

{style="table-layout:auto"}

**Data**

| Indata | Beskrivning |
| --- | --- |
| [!UICONTROL Payload] | Det här fältet innehåller de data som ska vidarebefordras till [!DNL Event Hubs]. Data kan vara ett JSON-objekt, en sträng eller ett dataelement. |

{style="table-layout:auto"}

När du är klar väljer du **[!UICONTROL Keep Changes]** för att lägga till åtgärden i regelkonfigurationen. När du är nöjd med regeln väljer du **[!UICONTROL Save to Library]**.

Publicera slutligen en ny händelsevidarebefordring [bygga](../../../ui/publishing/builds.md) för att aktivera ändringar i biblioteket.

## Nästa steg

Den här guiden beskriver hur du skickar data till [!DNL Event Hubs] med [!DNL Microsoft Azure] tillägg för händelsevidarebefordran. Mer information om funktioner för att vidarebefordra händelser i Experience Platform finns i [händelsevidarebefordring - översikt](../../../ui/event-forwarding/overview.md).

## Bilaga: Hämta SAS-auktoriseringsvärden {#sas}

Externa program beviljas åtkomst till [!DNL Event Hubs] via [signaturer för delad åtkomst (SAS)](https://learn.microsoft.com/en-us/azure/event-hubs/authorize-access-shared-access-signature). Varje [!DNL Event Hubs] I navet för namnutrymme och händelser tilldelas en standard-SAS-auktoriseringsregel automatiskt när den skapas, men du kan också skapa ytterligare principer för varje resurs om du vill.

När [konfigurera en regel för vidarebefordran av händelser](#rule) med [!DNL Azure] måste du ange namnet och primärnyckeln för auktoriseringsregeln som styr det namnutrymme eller den specifika händelsehubb som du vill skicka data till. Mer information om hur du hämtar dessa värden finns i [!DNL Azure] se följande avsnitt i [!DNL Azure] dokumentation:

* [Hämta SAS-värden för en [!DNL Event Hubs] namespace](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-namespace)
* [Hämta SAS-värden för en specifik händelsehubb i ett namnutrymme](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-specific-event-hub-in-a-namespace)

När du har de obligatoriska värdena kan auktoriseringsregelnamnet anges direkt som en sträng i config-indata eller så kan du skapa ett dataelement av strängtyp för att referera till det i stället. Primärnyckeln måste dock först finnas inuti en händelsevidarebefordringshemlighet innan den kan anges i regelkonfigurationen för att skydda din datasäkerhet.

I gränssnittet för vidarebefordring av händelser [skapa en ny hemlighet](../../../ui/event-forwarding/secrets.md) och markera **[!UICONTROL Token]** som hemlig typ. Ange primärnyckeln som du kopierade tidigare för själva tokenvärdet. Skapa ett dataelement med typen när du har skapat hemligheten **[!UICONTROL Secret]** och väljer [!DNL Event Hubs] hemlighet från listan. När det hemliga dataelementet har ställts in kan du referera till det dataelementet i **[!UICONTROL SAS Access Key]** fält.
