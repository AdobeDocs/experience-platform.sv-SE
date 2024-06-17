---
title: Användargränssnittshandbok för diagramsimulering
description: Lär dig hur du använder Graph Simulation i gränssnittet för identitetstjänsten.
badge: Beta
exl-id: 89f0cf6e-c43f-40ec-859a-f3b73a6da8c8
source-git-commit: 4c49bec7974dafe18d18deded6ddc936ece47dc3
workflow-type: tm+mt
source-wordcount: '1401'
ht-degree: 0%

---

# [!DNL Graph Simulation] Användargränssnittsguide

>[!AVAILABILITY]
>
>Den här funktionen är inte tillgänglig ännu. Betaprogrammet för länkningsregler för identitetsdiagram förväntas starta i juli för utvecklingssandlådor. Kontakta ditt Adobe-kontoteam för att få information om deltagandekriterierna.

[!DNL Graph Simulation] är ett verktyg i identitetstjänstens gränssnitt som du kan använda för att simulera hur ett identitetsdiagram beter sig när en viss kombination av identiteter anges och hur du konfigurerar [algoritm för identitetsoptimering](./identity-optimization-algorithm.md).

Läs det här dokumentet om du vill veta hur du kan använda [!DNL Graph Simulation] för att bättre förstå identitetsgrafens beteende och hur diagramalgoritmen fungerar.

## Lär känna [!DNL Graph Simulation] gränssnitt {#interface}

Du kan komma åt [!DNL Graph Simulation] i Adobe Experience Platform användargränssnitt. Välj **[!UICONTROL Identities]** i den vänstra navigeringen och sedan väljer **[!UICONTROL Graph Simulation]** i det övre sidhuvudet.

![Gränssnittet Graph Simulation i Adobe Experience Platform-gränssnittet.](../images/graph-simulation/graph-simulation.png)

The [!DNL Graph Simulation] gränssnittet kan delas in i tre delar:

>[!BEGINTABS]

>[!TAB Händelser]

Händelser: Använd **[!UICONTROL Events]** för att lägga till identiteter för att simulera ett diagram. En fullständigt kvalificerad identitet måste ha ett ID-namnutrymme och dess motsvarande identitetsvärde. Du måste lägga till minst två identiteter för att simulera ett diagram. Du kan också välja **[!UICONTROL Load Example]** för att ange en förkonfigurerad händelse- och algoritminställning.

![Händelsepanelen i verktyget Diagramsimulering.](../images/graph-simulation/events.png)

>[!TAB Algoritmkonfiguration]

Algoritmkonfiguration: Använd **[!UICONTROL Algorithm configuration]** för att lägga till och konfigurera optimeringsalgoritmen för dina namnutrymmen. Du kan dra och släppa ett namnutrymme för att ändra deras respektive prioritetsordning. Du kan också välja **[!UICONTROL Unique Per Graph]** för att avgöra om ett namnutrymme är unikt.

![Algoritmkonfigurationen för verktyget Diagramsimulering.](../images/graph-simulation/algorithm-configuration.png)

>[!TAB Simulerat diagramvisningsprogram]

Simulerat diagramvisningsprogram: Det simulerade diagramvisningsprogrammet visar det resulterande diagrammet baserat på händelser som du har lagt till och den algoritm som du har konfigurerat. En rak linje mellan två identiteter innebär att en länk upprättas. En prickad linje anger att en länk har tagits bort.

![Den simulerade diagramvisningsprogrampanelen, med ett exempel på ett simulerat diagram.](../images/graph-simulation/simulated-graph.png)

>[!ENDTABS]

## Lägg till händelser {#add-events}

Börja genom att välja **[!UICONTROL Add events]**.

![Knappen Lägg till händelser har valts.](../images/graph-simulation/add-events.png)

Ett popup-fönster visas för [!UICONTROL Event #1]. Ange din kombination av identitetsnamn och identitetsvärde härifrån. Du kan använda listrutan för att välja ett identitetsnamnutrymme. Du kan också skriva de första bokstäverna i ett namnutrymme och sedan välja alternativen i listrutan. När du har valt namnutrymmet anger du ett identitetsvärde som motsvarar namnutrymmet.

![Fönstret Event #1 med ett tomt gränssnitt.](../images/graph-simulation/event-one.png)

>[!TIP]
>
>Det identitetsvärde som du anger under [!DNL Graph Simulation] övningar behöver inte vara verkliga identitetsvärden och kan vara enkla platshållare.

När din första identitet är klar väljer du ikonen Lägg till (**`+`**) för att lägga till en andra identitet.

![Den första fullständiga identiteten för {Email: tom@acme.com} finns i panelen Händelser i Graph Simulation.](../images/graph-simulation/event-one-added.png)

Upprepa sedan samma steg och lägg till en andra identitet. Två fullständigt kvalificerade identiteter krävs för att skapa ett identitetsdiagram. I exemplet nedan läggs ett ECID till som ett namnutrymme och anges med värdet `111`. När du är klar väljer du **[!UICONTROL Save]**.

![En andra identitet för {ECID: 111} läggs till i händelse nr 1.](../images/graph-simulation/first-event.png)

The [!UICONTROL Events] gränssnittsuppdateringar för att visa din första händelse, som i det här fallet är: `{Email: tom@acme.com, ECID: 111}`.

![Det uppdaterade händelsegränssnittet med {Email: tom@acme.com, ECID: 111}.](../images/graph-simulation/add-second-event.png)

Upprepa sedan samma steg för att lägga till en andra händelse. För händelse 2, lägg till `{Email: summer@acme.com}` som din första identitet och sedan lägga till samma `{ECID: 111}` som den andra identiteten, vilket skapar en andra händelse för `{Email: summer@acme.com}, {ECID: 111}`. När du är klar bör du ha två händelser, en för `{Email: tom@acme.com, ECID: 111}` och en för `{Email: summer@acme.com}, {ECID: 111}`.

![Det uppdaterade händelsegränssnittet med två händelser.](../images/graph-simulation/two-events.png)

### Läs in exempel {#load-example}

Välj **[!UICONTROL Load example]** för att skapa ett exempeldiagram med en förinställd algoritm och händelsekonfiguration.

![Alternativet Läs in exempel har valts.](../images/graph-simulation/load-example.png)

Ett popup-fönster visas med tillgängliga diagramscenarier som du kan välja mellan:

| Exempeldiagram | Beskrivning | Exempel |
| --- | --- | --- |
| Delad enhet | Delad enhet avser scenarier där två olika användare loggar in på samma enhet. | En man och fru delar en iPad för surfning och e-handel. |
| Ogiltig (icke-unik) telefon | Ogiltig eller icke-unik telefon hänvisar till scenarier där två olika användare använder samma telefonnummer för att skapa ett konto. | En mor och hennes dotter använder sitt delade hemtelefonnummer för att registrera sig för e-handelskonton. |
| Felaktiga identitetsvärden | &quot;Dåliga&quot; identitetsvärden hänvisar till scenarier där identitetstjänsten genererar icke-unika IDFA:er på grund av felaktig implementering. | WebSDK skickar felaktigt en `user_null` värdet för varje händelse på grund av problem med kodimplementering. |

![Ett fönster som visar tillgängliga förkonfigurerade exempel: delad enhet, ogiltig telefon och felaktiga identitetsvärden.](../images/graph-simulation/example-options.png)

Välj något av alternativen som ska läsas in [!DNL Graph Simulation] med förkonfigurerade händelser och algoritm. Du kan fortfarande göra ytterligare konfigurationer av alla förinlästa diagramscenarioexempel.

![Händelser och algoritm som konfigurerats för ogiltig telefon.](../images/graph-simulation/example-loaded.png)

När du är klar väljer du **[!UICONTROL Simulate]**.

![Ett exempeldiagram simulerat för en ogiltig telefon.](../images/graph-simulation/example-simulated.png)

### Använd textversion {#use-text-version}

Du kan också använda textläge för att konfigurera händelser. Om du vill använda textläget markerar du inställningsikonen och väljer **[!UICONTROL Text (Advanced users)]**.

![Inställningsikonen är markerad.](../images/graph-simulation/settings.png)

Du kan ange dina identiteter manuellt i textläge. Använda kolon (`:`) för att skilja identitetsvärdet som motsvarar det namnutrymme som du anger och sedan använda ett komma (`,`) för att separera dina identiteter. Om du vill skilja olika händelser från varandra använder du en ny rad för varje händelse.

![Händelsepanelen som använder textlägesversionen.](../images/graph-simulation/text-version.png)

### Redigera händelse {#edit-event}

Om du vill redigera en händelse markerar du ellipserna (`...`) bredvid en viss händelse och välj **[!UICONTROL Edit]**.

![Ikonen för redigeringshändelsen är markerad.](../images/graph-simulation/edit.png)

### Ta bort händelse {#delete-event}

Om du vill ta bort en händelse markerar du ellipserna (`...`) bredvid en viss händelse och välj **[!UICONTROL Delete]**.

![Ikonen Ta bort händelse har valts.](../images/graph-simulation/delete.png)

## Konfigurera algoritm {#configure-algorithm}

>[!IMPORTANT]
>
>Den algoritm som du konfigurerar styr hur identitetstjänsten hanterar de namnutrymmen som du anger i dina händelser. Alla konfigurationer som du sätter ihop i [!DNL Graph Simulation UI] sparas inte i identitetsinställningarna.

När du har lagt till dina händelser kan du nu konfigurera algoritmen som ska användas för att simulera diagrammet. Börja genom att välja **[!UICONTROL Add config]**.

![Konfigurationspanelen för algoritmen.](../images/graph-simulation/add-config.png)

En tom konfigurationsrad visas. Börja med att ange samma namnutrymme som du använde för händelserna. I det här fallet börjar du med att skriva e-post. När du anger namnutrymmet visas kolumnerna för [!UICONTROL Identity Symbol] och [!UICONTROL Identity Type] fylls i automatiskt.

![Den första konfigurationsposten.](../images/graph-simulation/add-namespace.png)

Upprepa sedan samma steg och lägg till ditt andra namnutrymme, som i det här fallet är ECID. När alla namnutrymmen har angetts kan du börja konfigurera deras prioriteringar och unika utseende.

* **Namnområdesprioritet**: Prioriteten för ett namnutrymme avgör dess relativa betydelse jämfört med andra namnutrymmen i ett givet identitetsdiagram. Om identitetsdiagrammet till exempel har fyra olika namnutrymmen: CRM ID, ECID, Email och Apple IDFA, kan du konfigurera prioriteter för att fastställa prioritetsordningen för det fyra namnutrymmet.
* **Unikt namnutrymme**: Om ett namnutrymme har angetts som unikt genereras diagram med identitetstjänsten som anger att endast en identitet med ett givet unikt namnutrymme kan finnas. Om namnutrymmet E-post till exempel har angetts som ett unikt namnutrymme kan ett diagram bara ha en identitet med E-post. Om det finns mer än en identitet med e-postnamnutrymmet tas den äldsta länken bort.

Om du vill konfigurera namnutrymmesprioritet markerar du och drar namnutrymmesraderna till önskad prioritetsordning, där den översta raden representerar högre prioritet och den nedersta raden motsvarar lägre prioritet. Om du vill ange ett namnutrymme som unikt väljer du **[!UICONTROL Unique Per Graph]** kryssrutan.

När du är klar väljer du **[!UICONTROL Simulate]**.

![Alla namnutrymmen har konfigurerats.](../images/graph-simulation/all-namespaces.png)

## Visa simulerat diagram

The [!UICONTROL Simulated Graph] I visas de identitetsdiagram som genereras baserat på händelser som du har lagt till och den algoritm som du har konfigurerat.

| Diagramikoner | Beskrivning |
| --- | --- |
| Heldragen linje | En heldragen linje representerar en etablerad länk mellan två identiteter. |
| Prickad linje | En prickad linje representerar en borttagen länk mellan två identiteter. |
| Nummer på rad | Ett nummer på en rad representerar tidsstämpeln som den angivna länken skapades för. Det lägsta talet (1) representerar den tidigaste etablerade länken. |

I exempeldiagrammet nedan finns det en prickad linje mellan `{Email: tom@acme.com}` och `{ECID: 111}` på grund av följande orsaker:

* E-postadressen angavs som unik under algoritmens konfigurationssteg. Därför kan det bara finnas en identitet med ett e-postnamnutrymme i ett diagram.
* Länken mellan `{Email: tom@acme.com}` och `{ECID: 111}` var den första etablerade identiteten (Event #1). Det är den äldsta länken och tas därför bort.

![Den simulerade diagramvisningsprogrampanelen, med ett exempel på ett simulerat diagram.](../images/graph-simulation/simulated-graph.png)

## Nästa steg

Genom att läsa det här dokumentet kan du nu använda [!DNL Graph Simulation] för att bättre förstå hur dina identitetsdata behandlas utifrån en viss uppsättning regler och konfigurationer. Mer information finns i följande dokument:

* [Länkningsregler för identitetsdiagram](overview.md)
* [Identitetsoptimeringsalgoritm](identity-optimization-algorithm.md)
* [Namnområdesprioritet](namespace-priority.md)
