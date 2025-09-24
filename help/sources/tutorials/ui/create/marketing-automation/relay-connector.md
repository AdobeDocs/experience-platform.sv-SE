---
title: Connect Relay till Experience Platform i användargränssnittet
description: Lär dig hur du skapar en anpassad Relay Connector-källanslutning med Adobe Experience Platform-gränssnittet.
hide: true
hidefromtoc: true
exl-id: f80855f5-0769-4253-b737-28c46e4dea6e
source-git-commit: b3b1542f7e297f4ca872a155ac3801266bc1e6a6
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 0%

---

# Connect Relay till Experience Platform i användargränssnittet

>[!NOTE]
>
>Källan [!DNL Relay Connector] är i betaversion. Läs [källöversikten](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade källor.

Med [!DNL Relay Connector] kan du leverera personaliserade upplevelser till dina kunder vid de mest meningsfulla ögonblicken på deras resa, vilket hjälper dig att bygga starkare relationer och få större lojalitet och värde genom att skapa en inkommande anslutning för att strömma händelser från din [!DNL Relay Network]-integrering till Adobe Experience Platform.

Läs den här vägledningen när du vill lära dig hur du använder [!DNL Relay Connector] på arbetsytan för källor i Experience Platform-gränssnittet.

>[!IMPORTANT]
>
>Den här dokumentationssidan hanteras av *[!DNL Relay Network]*-teamet. Om du har frågor eller uppdateringsfrågor kontaktar du dem direkt på *[[!DNL Relay Network]](https://www.relaynetwork.com/) eller via e-post [info@relaynetwork.com](mailto:info@relaynetwork.com)*.

## Anslut [!DNL Relay Connector]-källan

I Experience Platform-gränssnittet väljer du **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan i [!UICONTROL Sources]. På skärmen [!UICONTROL Catalog] visas en mängd olika källor som du kan använda för att skapa ett konto. Du kan välja lämplig kategori i katalogen till vänster på skärmen eller använda sökalternativet för att hitta en viss källa.

Välj *[!UICONTROL Marketing automation]*-källkortet under kategorin [!DNL Relay Connector] och välj **[!UICONTROL Add data]**.

>[!TIP]
>
>Källor i källkatalogen visar alternativet **[!UICONTROL Set up]** när det inte finns något autentiserat konto. När ett konto har autentiserats ändras alternativet till **[!UICONTROL Add data]**.

![Katalogsidan för källarbetsytan.](../../../../images/tutorials/create/relay-connector/relay-source.jpg)

### Markera data

Gränssnittet **[!UICONTROL Connect Relay Connector source]** visas. Använd gränssnittet *[!UICONTROL Select data]* för att bläddra eller ange källdataschemat. Du kan också överföra en JSON-exempelfil för att definiera källschemat.

>[!NOTE]
>
>Den tillåtna filstorleken är upp till 1 GB.

![Gränssnittet ](../../../../images/tutorials/create/relay-connector/upload-data.jpg) för val av data

När data har överförts kan du använda avsnittet [!UICONTROL Preview sample data] för att förhandsgranska data.

![Överförda data.](../../../../images/tutorials/create/relay-connector/uploaded-data.jpg)

### Information om dataflöde

Använd sedan gränssnittet *[!UICONTROL Dataflow details]* för att ange ett **name** och en **valfri beskrivning** för dataflödet. Markera dessutom **[!UICONTROL Target dataset]** som du vill använda. Du kan antingen skapa en ny datauppsättning eller använda en befintlig datauppsättning.

![Gränssnittet för dataflödesinformation. ](../../../../images/tutorials/create/relay-connector/dataflow.jpg)

### Mappning

Du kan mappa dina källfält till XDM-schemafält med hjälp av funktionen för automatisk mappning, som matchar fält baserat på deras namn, eller skapa anpassade mappningar för mer exakt kontroll. Om det behövs kan du även använda omformningar som sammanfogning, formatering eller namnändring för att säkerställa att dina data passar in perfekt i målschemat. Mer information om mappning finns i [Användargränssnittsguiden för dataförberedelser](../../../../../data-prep/ui/mapping.md).

![Mappningsgränssnittet i källarbetsflödet.](../../../../images/tutorials/create/relay-connector/mapping.jpg)

>[!TIP]
>
>Mer information om vilka typer av händelser och datavärden som Relay skickar till källan finns i dokumentationen för [[!DNL Relay Network] push-händelser](https://docs.relaynetwork.com/docs/push-events). Den här informationen hjälper dig att utforma ditt **Experience Events-schema** korrekt.

### Granska

Granska slutligen alla konfigurationer, inklusive din **källa, datamängd och mappningar**. När du är klar väljer du **Slutför** för att skapa dataflödet.

![Granskningssteget för källarbetsflödet.](../../../../images/tutorials/create/relay-connector/review.jpg)

### Hämta URL:en för direktuppspelningsslutpunkten

När du har skapat dataflödet hittar du *URL:en för direktuppspelningsslutpunkten* och annan relaterad information i avsnittet **Egenskaper** till höger på dataflödessidan.

![Dataflödesegenskaperna](../../../../images/tutorials/create/relay-connector/streaming-endpoint.jpg)

Använd dessa värden för att konfigurera webkroken i **Relay-konsolen**. Detaljerade instruktioner om hur du konfigurerar push-funktionen finns i Relay-dokumentationen: [Konfigurera push-API:t](https://docs.relaynetwork.com/docs/configuring-the-push-api).

## Ytterligare resurser

* [Skapa en ny anslutningsspecifikation med API:t för Flow Service ](https://experienceleague.adobe.com/sv/docs/experience-platform/sources/sdk/streaming-sdk/create)
* [Anslut till källan med användargränssnittet](https://experienceleague.adobe.com/sv/docs/experience-platform/sources/sdk/streaming-sdk/submit#test-your-source-using-the-ui)
