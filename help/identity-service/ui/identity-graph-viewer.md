---
keywords: Experience Platform;hem;populära ämnen;identitetsdiagramvisningsprogram;Identitetsdiagramvisningsprogram;diagramvisningsprogram;Graph viewer;identity namespace;Identity namespace;identity;Identity;Identity service;identity service
solution: Experience Platform
title: Översikt över Identity Graph Viewer
topic: tutorial
description: Ett identitetsdiagram är en karta över relationer mellan olika identiteter för en viss kund, vilket ger dig en visuell representation av hur kunden interagerar med varumärket i olika kanaler.
translation-type: tm+mt
source-git-commit: 8ec904d584225113a6791533ff544560fc2efdf3
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 0%

---


# (Beta) Översikt över visningsprogrammet för identitetsdiagram

>[!NOTE]
>
>Identitetsdiagramvisningsprogrammet är för närvarande i betaversion. Funktionerna kan komma att ändras.

Ett identitetsdiagram är en karta över relationer mellan olika identiteter för en viss kund, vilket ger dig en visuell representation av hur kunden interagerar med varumärket i olika kanaler. Alla kundidentitetsdiagram hanteras och uppdateras gemensamt av Adobe Experience Platform Identity Service i nära realtid som svar på kundaktivitet.

Med identitetsdiagramvisningsprogrammet i användargränssnittet för plattformen kan du visualisera och bättre förstå vilka kundidentiteter som sammanfogas och på vilka sätt. Med visningsprogrammet kan du dra och interagera med olika delar av diagrammet, vilket gör att du kan undersöka komplexa identitetsförhållanden, felsöka mer effektivt och dra nytta av ökad genomskinlighet när det gäller hur informationen används.

## Komma igång

Att arbeta med identitetsdiagramvisningsprogrammet kräver förståelse för de olika Adobe Experience Platform-tjänsterna. Innan du börjar arbeta med identitetsdiagramvisningsprogrammet bör du läsa dokumentationen för följande tjänster:

- [[!DNL Identity Service]](../home.md): Få en bättre bild av enskilda kunder och deras beteende genom att skapa en bro mellan identiteter på olika enheter och system.

### Terminologi

- **Identitet (nod):** En identitet eller en nod är data som är unika för en enhet, vanligtvis en person. En identitet består av ett namnutrymme och ett identitetsvärde.
- **Länk (kant):** En länk eller kant representerar kopplingen mellan identiteter.
- **Diagram (kluster):** Ett diagram eller ett kluster är en grupp identiteter och länkar som representerar en person.

## Åtkomst till identitetsdiagramvisningsprogrammet

Om du vill använda identitetsdiagramvisningsprogrammet i användargränssnittet väljer du **[!UICONTROL Identities]** i den vänstra navigeringen och sedan fliken **[!UICONTROL Identity graph]**. På skärmen **[!UICONTROL Identity Namespace]** klickar du på ikonen **[!UICONTROL Select identity namespace]** för att söka efter det namnutrymme som du tänker använda.

![namespace-screen](../images/identity-graph-viewer/identity-namespace.png)

Panelen **[!UICONTROL Select identity namespace]** visas. Den här skärmen innehåller en lista med namnutrymmen som är tillgängliga för din organisation, inklusive information om ett namnområdes **[!UICONTROL Display name]**, **[!UICONTROL Identity symbol]**, **[!UICONTROL Owner]**, **[!UICONTROL Last updated]** datum och **[!UICONTROL Description]**. Du kan använda vilket som helst av de angivna namnutrymmena om du har ett giltigt identitetsvärde kopplat till dem.

Markera det namnutrymme som du vill använda och klicka på **[!UICONTROL Select]** för att fortsätta.

![select-identity-namespace](../images/identity-graph-viewer/select-identity-namespace.png)

När du har valt ett namnutrymme anger du dess motsvarande värde för en viss kund i textrutan **[!UICONTROL Identity value]** och väljer **[!UICONTROL View]**.

![add-identity-value](../images/identity-graph-viewer/identity-value-filled.png)

Identitetsdiagramvisningsprogrammet visas. Till vänster på skärmen finns identitetsdiagrammet som visar alla identiteter som är länkade till det namnutrymme som du har markerat och det identitetsvärde som du har angett. Varje identitetsnod består av ett namnutrymme och dess motsvarande ID-värde. Du kan markera och hålla kvar en identitet om du vill dra och interagera med diagrammet. Du kan också hovra över en identitet för att se information om dess ID-värde. Diagramresultatet visas också som en inskickad lista mitt på skärmen.

>[!IMPORTANT]
>
>Ett identitetsdiagram kräver minst två länkade identiteter att generera, samt ett giltigt namnutrymme och ID-par. Det maximala antalet identiteter som diagramvisningsprogrammet kan visa är 150. Mer information finns i avsnittet [appendix](#appendix) nedan.

![identitetsdiagram](../images/identity-graph-viewer/graph-viewer.png)

Välj en identitet för att uppdatera den markerade raden i tabellen **[!UICONTROL Identities]** och för att uppdatera informationen som finns på den högra listen, som innehåller identitetsdata **[!UICONTROL Value]**, **[!UICONTROL Batch ID]** och **[!UICONTROL Last updated]**-datumet.

![select-identity](../images/identity-graph-viewer/select-identity.png)

Du kan filtrera genom ett diagram och isolera ett specifikt namnutrymme med sorteringsalternativet ovanför tabellen **[!UICONTROL Identities]**. Välj det namnutrymme som du vill markera i listrutan.

![filter-för-namnutrymme](../images/identity-graph-viewer/filter-namespace.png)

Diagramvisningsprogrammet returnerar och namnutrymmet som du markerade markeras. Filteralternativet uppdaterar även tabellen **[!UICONTROL Identities]** så att endast information returneras för det namnutrymme som du har valt.

![filtrerad](../images/identity-graph-viewer/filtered.png)

Den övre högra delen av diagramvisningsrutan innehåller alternativ för förstoring. Välj ikonen **(+)** om du vill zooma in i diagrammet eller ikonen **(-)** om du vill zooma ut.

![zooma](../images/identity-graph-viewer/zoom.png)

Du kan visa mer information om grupper genom att välja **[!UICONTROL Data source]** i rubriken. Tabellen **[!UICONTROL Data source]** visar en lista över **[!UICONTROL Batch IDs]** som är associerad med diagrammet samt dess **[!UICONTROL Linked IDs]**, källschema och datum för inmatningen.

![datakälla](../images/identity-graph-viewer/data-source-table.png)

Du kan välja någon av länkarna i ett identitetsdiagram om du vill se alla källgrupper som har bidragit till länken.

![select-links](../images/identity-graph-viewer/select-edge.png)

Du kan också markera en grupp om du vill se alla länkar som den här gruppen har bidragit till.

![select-links](../images/identity-graph-viewer/select-batch.png)

Identitetsdiagram med större kluster av identiteter kan även nås via visningsprogrammet för identitetsdiagram.

![stora kluster](../images/identity-graph-viewer/large-cluster.png)

## Bilaga

Följande avsnitt innehåller ytterligare information om hur du arbetar med identitetsdiagramvisningsprogrammet.

### Om felmeddelanden

Fel kan inträffa vid åtkomst till identitetsdiagramvisningsprogrammet. Nedan följer en lista över krav och begränsningar som ska beaktas när du arbetar med identitetsdiagramvisningsprogrammet.

- Ett identitetsvärde måste finnas i det valda namnutrymmet.
- Identitetsdiagramvisningsprogrammet kräver minst två länkade identiteter för att kunna generera. Det är möjligt att det bara finns ett identitetsvärde och inga länkade identiteter, och i det här fallet finns värdet bara i [!DNL Profile]-visningsprogrammet.
- Identitetsdiagramvisningsprogrammet får inte överskrida det maximala antalet 150 identiteter.

![error-screen](../images/identity-graph-viewer/error-screen.png)

## Nästa steg

Genom att läsa det här dokumentet har du lärt dig att utforska kundernas identitetsdiagram i användargränssnittet för plattformen. Mer information om identiteter i Platform finns i [Översikt över identitetstjänsten](../home.md)

## Ytterligare resurser

Följande video är avsedd att ge stöd för din förståelse av identitetsdiagramvisningsprogrammet.

>[!VIDEO](https://video.tv.adobe.com/v/331030/?quality=12&learn=on)
