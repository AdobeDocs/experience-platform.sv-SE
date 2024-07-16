---
title: AWS Extension - översikt
description: Läs mer om AWS-tillägget för vidarebefordran av händelser i Adobe Experience Platform.
exl-id: 826a96aa-2d64-4a8b-88cf-34a0b6c26df5
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 1c417744518a7ac7cfb9c65d6af8219dcbc70d46
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---

# Översikt över tillägget [!DNL AWS]

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. I följande [dokument](../../../term-updates.md) finns en konsoliderad referens till de ändrade terminologin.

[[!DNL Amazon Web Services] ([!DNL AWS])](https://aws.amazon.com/) är en molnbaserad datorplattform som erbjuder en mängd olika tjänster, till exempel distribuerad databehandling, databaslagring, innehållsleverans och SaaS-integrationstjänster (Software-as-a-service) för kundrelationshantering (CRM) och resursplanering (ERP).

Tillägget [!DNL AWS] [Vidarebefordra ](../../../ui/event-forwarding/overview.md) använder [[!DNL Amazon Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/introduction.html) för att skicka händelser från Adobe Experience Platform Edge Network till [!DNL AWS] för vidare bearbetning. Den här guiden beskriver hur du installerar tillägget och använder dess funktioner i en regel för vidarebefordran av händelser.

## Förhandskrav

Du måste ha ett [!DNL AWS]-konto med en befintlig [!DNL Kinesis]-dataström för att kunna använda det här tillägget. Om du inte har någon befintlig dataström läser du [!DNL AWS]-dokumentationen om hur du [skapar en ny dataström med  [!DNL AWS] hanteringskonsolen](https://docs.aws.amazon.com/streams/latest/dev/how-do-i-create-a-stream.html).

## Installera tillägget {#install}

Om du vill installera tillägget [!DNL AWS] går du till användargränssnittet för datainsamling eller användargränssnittet för Experience Platform och väljer **[!UICONTROL Event Forwarding]** i den vänstra navigeringen. Här väljer du en egenskap som tillägget ska läggas till i eller skapar en ny egenskap i stället.

När du har markerat eller skapat den önskade egenskapen väljer du **[!UICONTROL Extensions]** i den vänstra navigeringen och väljer sedan fliken **[!UICONTROL Catalog]**. Sök efter kortet [!UICONTROL AWS] och välj sedan **[!UICONTROL Install]**.

![Knappen [!UICONTROL Install] som väljs för tillägget [!UICONTROL AWS] i användargränssnittet för datainsamling.](../../../images/extensions/server/aws/install.png)

På nästa skärm måste du ange anslutningsautentiseringsuppgifterna för ditt [!DNL AWS]-konto. Du måste ange ditt [!DNL AWS]-ID för åtkomstnyckel och en hemlig åtkomstnyckel. Om du inte känner till dessa värden läser du [!DNL AWS]-dokumentationen om [hur du får ditt åtkomstnyckel-ID och din hemliga åtkomstnyckel](https://docs.aws.amazon.com/powershell/latest/userguide/pstools-appendix-sign-up.html).

![Åtkomstnyckel-ID och hemlig åtkomstnyckel har lagts till i tilläggskonfigurationsvyn.](../../../images/extensions/server/aws/credentials.png)

>[!IMPORTANT]
>
>En åtkomstprincip måste bifogas till kontot [!DNL AWS] som används för att generera åtkomstautentiseringsuppgifterna. Den här principen måste konfigureras för att ge åtkomstbehörighet att skicka data till dataströmmen [!DNL Kinesis]. Se **Exempel 2** i dokumentet [!DNL AWS] om [exempelprofiler för  [!DNL Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html#kinesis-using-iam-examples) för att se hur principen ska definieras.

När du är klar väljer du **[!UICONTROL Save]** så installeras tillägget.

## Konfigurera en regel för vidarebefordran av händelser {#rule}

När du har installerat tillägget skapar du en ny händelsevidarebefordring av [regeln](../../../ui/managing-resources/rules.md) och konfigurerar villkoren efter behov. När du konfigurerar åtgärderna för regeln väljer du tillägget **[!UICONTROL AWS]** och väljer sedan **[!UICONTROL Send Data to Kinesis Data Stream]** som åtgärdstyp.

![Åtgärdstypen [!UICONTROL Send Data to Kinesis Data Stream] som väljs för en regel i användargränssnittet för datainsamling.](../../../images/extensions/server/aws/select-action-type.png)

Den högra panelen uppdateras och visar konfigurationsalternativ för hur data ska skickas. Du måste tilldela [dataelement](../../../ui/managing-resources/data-elements.md) till de olika egenskaper som representerar din [!DNL Event Hub]-konfiguration.

![Konfigurationsalternativen för åtgärdstypen [!UICONTROL Send Data to Kinesis Data Stream] som visas i gränssnittet.](../../../images/extensions/server/aws/data-stream-details.png)

**[!UICONTROL Kinesis Data Stream Details]**

| Indata | Beskrivning |
| --- | --- |
| [!UICONTROL Stream Name] | Namnet på dataströmmen som den här regeln för vidarebefordran av händelser skickar dataposter till. |
| [!UICONTROL AWS Region] | Regionen [!DNL AWS] där dataströmmen [!DNL Kinesis] skapas. |
| [!UICONTROL Partition Key] | [partitionsnyckeln](https://docs.aws.amazon.com/streams/latest/dev/key-concepts.html#partition-key) som tillägget använder när data skickas till dataströmmen.<br><br>[!DNL Kinesis Data Streams] delar upp de dataposter som tillhör en ström i flera delningar. Den använder den partitionsnyckel som skickas med varje datapost för att avgöra vilken del en viss datapost tillhör.<br><br>En bra partitionsnyckel för att distribuera kunder kan vara kundnumret eftersom det är olika för varje kund. En dålig partitionsnyckel kan ha sitt postnummer eftersom de alla kan finnas i samma område som närliggande. I allmänhet bör du välja en partitionsnyckel som har det högsta intervallet av olika möjliga värden. Mer information om hur du hanterar partitionsnycklar finns i artikeln [!DNL AWS] om [skalning av  [!DNL Kinesis] dataströmmar](https://aws.amazon.com/blogs/big-data/under-the-hood-scaling-your-kinesis-data-streams/). |

{style="table-layout:auto"}

**[!UICONTROL Data]**

| Indata | Beskrivning |
| --- | --- |
| [!UICONTROL Payload] | Det här fältet innehåller de data som kommer att vidarebefordras till dataströmmen [!DNL Kinesis] i JSON-format.<br><br>Under alternativet **[!UICONTROL Raw]** kan du klistra in JSON-objektet direkt i det angivna textfältet, eller så kan du välja dataelementsikonen (![Datauppsättningsikonen](../../../images/extensions/server/aws/data-element-icon.png)) och välja från en lista över befintliga dataelement som ska representera nyttolasten.<br><br>Du kan också använda alternativet **[!UICONTROL JSON Key-Value Pairs Editor]** för att manuellt lägga till nyckelvärdepar via en gränssnittsredigerare. Varje värde kan representeras av en rådatainmatning, eller ett dataelement kan markeras i stället. |

{style="table-layout:auto"}

När du är klar väljer du **[!UICONTROL Keep Changes]** för att lägga till åtgärden i regelkonfigurationen. När du är nöjd med regeln väljer du **[!UICONTROL Save to Library]**.

Publicera slutligen en ny händelse som vidarebefordrar [build](../../../ui/publishing/builds.md) för att aktivera ändringarna i biblioteket.

## Nästa steg

I den här guiden beskrivs hur du skickar data till [!DNL Kinesis Data Streams] med hjälp av tillägget [!DNL AWS] för vidarebefordran av händelser. Mer information om funktioner för att vidarebefordra händelser i Experience Platform finns i [översikten över vidarebefordran av händelser](../../../ui/event-forwarding/overview.md).
