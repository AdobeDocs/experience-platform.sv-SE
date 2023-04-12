---
title: AWS Extension - översikt
description: Läs mer om AWS-tillägget för vidarebefordran av händelser i Adobe Experience Platform.
exl-id: 826a96aa-2d64-4a8b-88cf-34a0b6c26df5
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 1c417744518a7ac7cfb9c65d6af8219dcbc70d46
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 0%

---

# [!DNL AWS] tilläggsöversikt

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

[[!DNL Amazon Web Services] ([!DNL AWS])](https://aws.amazon.com/) är en plattform för cloud computing som erbjuder ett brett utbud av tjänster som distribuerad datorhantering, databaslagring, innehållsleverans och SaaS-integrationstjänster (Software-as-a-service) för kundrelationshantering (CRM) och resursplanering (ERP) för företag.

The [!DNL AWS] [händelsevidarebefordran](../../../ui/event-forwarding/overview.md) utbyggnadsutfall [[!DNL Amazon Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/introduction.html) för att skicka händelser från Adobe Experience Platform Edge Network till [!DNL AWS] för vidare bearbetning. Den här guiden beskriver hur du installerar tillägget och använder dess funktioner i en regel för vidarebefordran av händelser.

## Förutsättningar

Du måste ha en [!DNL AWS] konto med ett befintligt [!DNL Kinesis] dataström för att kunna använda det här tillägget. Om du inte har en befintlig dataström kan du läsa [!DNL AWS] dokumentation om [skapa en ny dataström med [!DNL AWS] Management Console](https://docs.aws.amazon.com/streams/latest/dev/how-do-i-create-a-stream.html).

## Installera tillägget {#install}

Så här installerar du [!DNL AWS] navigerar du till användargränssnittet för datainsamling eller användargränssnittet för Experience Platform och väljer **[!UICONTROL Event Forwarding]** från vänster navigering. Här väljer du en egenskap som tillägget ska läggas till i eller skapar en ny egenskap i stället.

När du har markerat eller skapat den önskade egenskapen väljer du **[!UICONTROL Extensions]** i den vänstra navigeringen väljer du **[!UICONTROL Catalog]** -fliken. Sök efter [!UICONTROL AWS] kort, välj **[!UICONTROL Install]**.

![The [!UICONTROL Install] knappen som markeras för [!UICONTROL AWS] i användargränssnittet för datainsamling.](../../../images/extensions/server/aws/install.png)

På nästa skärm måste du ange anslutningsinformationen för [!DNL AWS] konto. Du måste ange [!DNL AWS] ID för åtkomstnyckel och hemlig åtkomstnyckel. Om du inte känner till dessa värden kan du läsa [!DNL AWS] dokumentation om [hur du får ditt åtkomstnyckel-ID och din hemliga åtkomstnyckel](https://docs.aws.amazon.com/powershell/latest/userguide/pstools-appendix-sign-up.html).

![Åtkomstnyckel-ID och hemlig åtkomstnyckel som lagts till i tilläggskonfigurationsvyn.](../../../images/extensions/server/aws/credentials.png)

>[!IMPORTANT]
>
>En åtkomstprincip måste bifogas till [!DNL AWS] konto som används för att generera autentiseringsuppgifter för åtkomst. Den här principen måste konfigureras för att ge åtkomsträttigheter för att skicka data till [!DNL Kinesis] dataström. Se **Exempel 2** i [!DNL AWS] dokument på [exempelprinciper för [!DNL Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html#kinesis-using-iam-examples) för att se hur policyn ska definieras.

När du är klar väljer du **[!UICONTROL Save]** och tillägget installeras.

## Konfigurera en regel för vidarebefordran av händelser {#rule}

Skapa en ny händelsevidarebefordring när du har installerat tillägget [regel](../../../ui/managing-resources/rules.md) och konfigurera villkoren efter behov. När du konfigurerar åtgärderna för regeln väljer du **[!UICONTROL AWS]** tillägg, välj **[!UICONTROL Send Data to Kinesis Data Stream]** för åtgärdstypen.

![The [!UICONTROL Send Data to Kinesis Data Stream] åtgärdstypen som väljs för en regel i användargränssnittet för datainsamling.](../../../images/extensions/server/aws/select-action-type.png)

Den högra panelen uppdateras och visar konfigurationsalternativ för hur data ska skickas. Du måste tilldela [dataelement](../../../ui/managing-resources/data-elements.md) till de olika egenskaper som representerar [!DNL Event Hub] konfiguration.

![Konfigurationsalternativen för [!UICONTROL Send Data to Kinesis Data Stream] åtgärdstyp som visas i användargränssnittet.](../../../images/extensions/server/aws/data-stream-details.png)

**[!UICONTROL Kinesis Data Stream Details]**

| Indata | Beskrivning |
| --- | --- |
| [!UICONTROL Stream Name] | Namnet på dataströmmen som den här regeln för vidarebefordran av händelser skickar dataposter till. |
| [!UICONTROL AWS Region] | The [!DNL AWS] region där [!DNL Kinesis] dataström skapas. |
| [!UICONTROL Partition Key] | The [partitionsnyckel](https://docs.aws.amazon.com/streams/latest/dev/key-concepts.html#partition-key) som tillägget ska använda när data skickas till dataströmmen.<br><br>[!DNL Kinesis Data Streams] delar upp de dataposter som tillhör en ström i flera delningar. Den använder den partitionsnyckel som skickas med varje datapost för att avgöra vilken del en viss datapost tillhör.<br><br>En bra partitionsnyckel för att distribuera kunder kan vara kundnumret, eftersom det är olika för varje kund. En dålig partitionsnyckel kan ha sitt postnummer eftersom de alla kan finnas i samma område som närliggande. I allmänhet bör du välja en partitionsnyckel som har det högsta intervallet av olika möjliga värden. Se [!DNL AWS] artikel om [skala [!DNL Kinesis] dataströmmar](https://aws.amazon.com/blogs/big-data/under-the-hood-scaling-your-kinesis-data-streams/) om du vill ha tips om hur du hanterar partitionsnycklar. |

{style="table-layout:auto"}

**[!UICONTROL Data]**

| Indata | Beskrivning |
| --- | --- |
| [!UICONTROL Payload] | Det här fältet innehåller de data som ska vidarebefordras till [!DNL Kinesis] dataström, i JSON-format.<br><br>Under **[!UICONTROL Raw]** kan du klistra in JSON-objektet direkt i det angivna textfältet, eller så kan du välja dataelementsikonen (![Ikon för datauppsättning](../../../images/extensions/server/aws/data-element-icon.png)) för att välja från en lista med befintliga dataelement som ska representera nyttolasten.<br><br>Du kan också använda **[!UICONTROL JSON Key-Value Pairs Editor]** för att manuellt lägga till nyckelvärdepar via en UI-redigerare. Varje värde kan representeras av en rådatainmatning, eller ett dataelement kan markeras i stället. |

{style="table-layout:auto"}

När du är klar väljer du **[!UICONTROL Keep Changes]** för att lägga till åtgärden i regelkonfigurationen. När du är nöjd med regeln väljer du **[!UICONTROL Save to Library]**.

Publicera slutligen en ny händelsevidarebefordring [bygga](../../../ui/publishing/builds.md) för att aktivera ändringar i biblioteket.

## Nästa steg

Den här guiden beskriver hur du skickar data till [!DNL Kinesis Data Streams] med [!DNL AWS] tillägg för händelsevidarebefordran. Mer information om funktioner för att vidarebefordra händelser i Experience Platform finns i [händelsevidarebefordring - översikt](../../../ui/event-forwarding/overview.md).
