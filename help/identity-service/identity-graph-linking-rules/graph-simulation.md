---
title: Diagramsimulering
description: Lär dig hur du använder Graph Simulation i gränssnittet för identitetstjänsten.
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 2afdfd54b420bcf59423ea64048d928422ea61c9
workflow-type: tm+mt
source-wordcount: '1555'
ht-degree: 1%

---

# Diagramsimulering

Diagramsimulering är ett verktyg i identitetstjänstens gränssnitt som du kan använda för att simulera hur ett identitetsdiagram beter sig när en viss kombination av identiteter anges och hur du konfigurerar [algoritm för identitetsoptimering](./identity-optimization-algorithm.md).

Läs det här dokumentet för att lära dig hur du kan använda diagramsimulering för att bättre förstå identitetsgrafens beteende och hur diagramalgoritmen fungerar.

## Bekanta dig med gränssnittet Graph Simulation

Du kan komma åt Graph Simulation i Adobe Experience Platform-gränssnittet. Välj **[!UICONTROL Identities]** i den vänstra navigeringen och sedan väljer **[!UICONTROL Graph Simulation]** i det övre sidhuvudet.

![Gränssnittet Graph Simulation i Adobe Experience Platform-gränssnittet.](../images/graph-simulation/graph-simulation.png)

Gränssnittet för diagramsimulering kan delas in i tre avsnitt:

* Händelser: Använd **[!UICONTROL Events]** för att lägga till identiteter för att simulera ett diagram. En fullständigt kvalificerad identitet måste ha ett ID-namnutrymme och dess motsvarande identitetsvärde. Du måste lägga till minst två identiteter för att simulera ett diagram. Du kan också välja **[!UICONTROL Load Example]** för att ange en förkonfigurerad händelse- och algoritminställning.

![Händelsepanelen i verktyget Diagramsimulering.](../images/graph-simulation/events.png)

* Algoritmkonfiguration: Använd **[!UICONTROL Algorithm Configuration]** för att lägga till och konfigurera optimeringsalgoritmen för dina namnutrymmen. Du kan dra och släppa ett namnutrymme för att ändra deras respektive prioritetsordning. Du kan också välja **[!UICONTROL Unique Per Graph]** för att avgöra om ett namnutrymme är unikt.

![Algoritmkonfigurationen för verktyget Diagramsimulering.](../images/graph-simulation/algorithm-configuration.png)

* Simulerad diagramvisning: Det simulerade diagramvisningsprogrammet visar det resulterande diagrammet baserat på händelser som du har lagt till och den algoritm som du har konfigurerat. En rak linje mellan två noder innebär att en länk upprättas. En prickad linje anger att en länk har tagits bort.


![Den simulerade diagramvisningsprogrampanelen, med ett exempel på ett simulerat diagram.](../images/graph-simulation/simulated-graph.png)

## Lägg till händelser

Börja genom att välja **[!UICONTROL Add Events]**.

![Knappen Lägg till händelser är markerad.](../images/graph-simulation/add-events.png)

Ett popup-fönster visas för [!UICONTROL Event #1]. Ange din kombination av identitetsnamn och identitetsvärde härifrån. Du kan använda listrutan för att välja ett identitetsnamnutrymme. Du kan också skriva de första bokstäverna i ett namnutrymme och sedan välja alternativen i listrutan. När du har valt namnutrymmet anger du ett identitetsvärde som motsvarar namnutrymmet.

![](../images/graph-simulation/event-one.png)

>[!TIP]
>
>Det identitetsvärde som du anger under diagramsimuleringsövningar behöver inte vara verkliga identitetsvärden och kan vara enkla platshållare.

När din första identitet är klar väljer du ikonen Lägg till (**`+`**) för att lägga till en andra identitet.

![Den första fullständiga identiteten för {Email: tom@acme.com} finns i panelen Händelser i Graph Simulation.](../images/graph-simulation/event-one-added.png)

Upprepa sedan samma steg och lägg till en andra identitet. Två fullständigt kvalificerade identiteter krävs för att skapa ett identitetsdiagram. I exemplet nedan läggs ett ECID till som ett namnutrymme och anges med värdet `111`. När du är klar väljer du **[!UICONTROL Save]**.

![En andra identitet för {ECID: 111} läggs till i händelse nr 1.](../images/graph-simulation/first-event.png)

The [!UICONTROL Events] gränssnittsuppdateringar för att visa din första händelse, som i det här fallet är: `{Email: tom@acme.com, ECID: 111}`.

![Det uppdaterade händelsegränssnittet med {Email: tom@acme.com, ECID: 111}.](../images/graph-simulation/add-second-event.png)

Upprepa sedan samma steg för att lägga till en andra händelse. För händelse 2, lägg till `{Email: summer@acme.com}` som din första identitet och sedan lägga till samma `{ECID: 111}` som den andra identiteten, vilket skapar en andra händelse för `{Email: summer@acme.com}, {ECID: 111}`. När du är klar bör du ha två händelser, en för `{Email: tom@acme.com, ECID: 111}` och en för `{Email: summer@acme.com}, {ECID: 111}`.

![Det uppdaterade händelsegränssnittet med två händelser.](../images/graph-simulation/two-events.png)

### Läs in exempel

+++Markera om du vill visa steg för hur du använder förinlästa diagramexempel

Om du vill skapa ett exempeldiagram med en förkonfigurerad algoritm väljer du **[!UICONTROL Load example]**. Ett popup-fönster visas med tillgängliga diagramscenarier som du kan välja mellan:

| Exempeldiagram | Beskrivning | Exempel |
| --- | --- | --- |
| Delad enhet | Delad enhet avser scenarier där två olika användare loggar in på samma enhet. | En man och fru delar en iPad för surfning och e-handel. |
| Ogiltig (icke-unik) telefon | Ogiltig eller icke-unik telefon hänvisar till scenarier där två olika användare använder samma telefonnummer för att skapa ett konto. | En mor och hennes dotter använder sitt delade hemtelefonnummer för att registrera sig för e-handelskonton. |
| Felaktiga identitetsvärden | &quot;Dåliga&quot; identitetsvärden hänvisar till scenarier där identitetstjänsten genererar icke-unika IDFA:er på grund av felaktig implementering. | WebSDK skickar felaktigt en `user_null` värdet för varje händelse på grund av problem med kodimplementeringen. |

Välj något av alternativen för att läsa in diagramsimulering med förkonfigurerade händelser och algoritm. Du kan fortfarande göra ytterligare konfigurationer av alla förinlästa diagramscenarioexempel.

När du är klar väljer du **[!UICONTROL Simulate]**.

+++

### Använd textversion

+++Välj för att visa steg för hur du använder textversion

Du kan också använda textläge för att konfigurera händelser. Om du vill använda textläge väljer du verktyget (?) och sedan markera **[!UICONTROL Text (Advanced users)]**.

Du kan ange dina identiteter manuellt i textläge. Använda kolon (`:`) för att skilja identitetsvärdet som motsvarar det namnutrymme som du anger och sedan använda ett komma (`,`) för att separera dina identiteter. Om du vill skilja olika händelser från varandra använder du en ny rad för varje händelse.

+++

### Redigera händelse

Om du vill redigera en händelse markerar du ellipserna (`...`) bredvid en viss händelse och välj **[!UICONTROL Edit]**.

### Ta bort händelse

Om du vill ta bort en händelse markerar du ellipserna (`...`) bredvid en viss händelse och välj **[!UICONTROL Delete]**.

## Konfigurera algoritm

Den algoritm som du konfigurerar styr hur identitetstjänsten hanterar de namnutrymmen som du anger i dina händelser. Konfigurationer som du har satt ihop i användargränssnittet för diagramsimulering sparas inte i identitetsinställningarna.

Börja med att välja Lägg till (`+`) i det nedre hörnet av algoritmkonfigurationspanelen.



En tom konfigurationsrad visas. Börja med att ange samma namnutrymme som du använde för händelserna. I det här fallet börjar du med att ange CRM-ID:t. När du anger namnutrymmet visas kolumnerna för [!UICONTROL Identity Symbol] och [!UICONTROL Identity Type] fylls i automatiskt.



Upprepa sedan samma steg och lägg till ditt andra namnutrymme, som i det här fallet är ECID. När alla namnutrymmen har angetts kan du börja konfigurera deras prioriteringar och unika utseende.

* **Namnområdesprioritet**: Prioriteten för ett namnutrymme avgör dess relativa betydelse jämfört med andra namnutrymmen i ett givet identitetsdiagram. Om identitetsdiagrammet till exempel har fyra olika namnutrymmen: CRM ID, ECID, Email och Apple IDFA, kan du konfigurera prioriteter för att fastställa prioritetsordningen för det fyra namnutrymmet. (LÄGG TILL VARFÖR)
* **Unikt namnutrymme**: Om ett namnutrymme har angetts som unikt genereras diagram med identitetstjänsten som anger att endast en identitet med ett givet unikt namnutrymme kan finnas. Om CRM-ID till exempel har angetts som ett unikt namnutrymme kan ett diagram bara ha en identitet med CRM-ID. Om det finns mer än en identitet med CRM ID-namnutrymmet tas den äldsta länken bort.

Om du vill konfigurera namnutrymmesprioritet markerar du och drar namnutrymmesraderna till önskad prioritetsordning, där den översta raden representerar högre prioritet och den nedersta raden motsvarar lägre prioritet. Om du vill ange ett namnutrymme som unikt väljer du **[!UICONTROL Unique Per Graph]** kryssrutan.



När du är klar väljer du **[!UICONTROL Simulate]**.

## Visa simulerat diagram

The [!UICONTROL Simulated Graph] I visas de identitetsdiagram som genereras baserat på händelser som du har lagt till och den algoritm som du har konfigurerat.

| Diagramikoner | Beskrivning |
| --- | --- |
| Heldragen linje | En heldragen linje representerar en etablerad länk mellan två identiteter. |
| Prickad linje | En prickad linje representerar en borttagen länk mellan två identiteter. |
| Nummer på rad | Ett nummer på en rad representerar tidsstämpeln som den angivna länken skapades för. Det lägsta talet (1) representerar den tidigaste etablerade länken. |

I exempeldiagrammet nedan finns det en prickad linje mellan `{CRM ID: Tom}` och `{ECID: 111}` på grund av följande orsaker:

* CRM-ID angavs som unikt under algoritmens konfigurationssteg. Därför finns det bara en identitet med ett CRM ID-namnutrymme i ett diagram.
* Länken mellan `{CRM ID: Tom}` och `{ECID: 111}` var den första etablerade identiteten (Event #1). Det är den äldsta länken och tas därför bort.

## Exempel på diagramscenarier

>[!NOTE]
>
>CRM ID är ett anpassat namnutrymme. Därför kräver exemplen nedan att du skapar ett anpassat namnutrymme med ett visningsnamn och en identitetssymbol som är &quot;CRM ID&quot;.

I följande avsnitt visas exempel på diagramscenarier som du kan stöta på vid diagramsimulering.

### Endast CRM-ID

Händelser:

* CRM-ID: Tom, ECID: 111

Algoritmkonfiguration:

| Prioritet | Visningsnamn | Identitetssymbol | Identitetstyp | Unikt per diagram |
| ---| --- | --- | --- | --- |
| 1 | CRM-ID | CRM-ID | CROSS_DEVICE | Ja |
| 2 | ECID | ECID | COOKIE | NEJ |

+++Markera för att visa det simulerade diagrammet

+++

### CRM-ID med hashad e-post

I det här scenariot är ett CRM-ID inkapslat och representerar både online- (upplevelsehändelse) och offlinedata (profilpost). Det här scenariot innebär även att ett hashade e-postmeddelande, som representerar ett annat namnområde som skickas i CRM-postens datauppsättning tillsammans med CRM-ID, matas in.

Händelser:

* CRM-ID: Tom, Email_LC_SHA256: Tom<span>@acme.com
* CRM-ID: Tom, ECID: 111
* CRM ID: Sommar, Email_LC_SHA256: Sommar<span>@acme.com
* CRM-ID: Sommar, ECID: 222

Algoritmkonfiguration:

| Prioritet | Visningsnamn | Identitetssymbol | Identitetstyp | Unikt per diagram |
| ---| --- | --- | --- | --- |
| 1 | CRM-ID | CRM-ID | CROSS_DEVICE | Ja |
| 2 | E-post (SHA256, nedsänkt) | Email_LC_SHA256 | E-post | NEJ |
| 3 | ECID | ECID | COOKIE | NEJ |

+++Markera för att visa det simulerade diagrammet

+++

### CRM-ID med hashad e-post, hashad telefon, GAID och IDFA

Händelser:

* CRM ID: Tom, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
* CRM-ID: Tom, ECID: 111
* CRM-ID: Tom, ECID: 222, IDFA: A-A-A
* CRM ID: Sommar, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
* CRM-ID: Sommar, ECID: 333
* CRM ID: Sommar, ECID: 444, GAID:B-B-B

Algoritmkonfiguration:

| Prioritet | Visningsnamn | Identitetssymbol | Identitetstyp | Unikt per diagram |
| ---| --- | --- | --- | --- |
| 1 | CRM-ID | CRM-ID | CROSS_DEVICE | Ja |
| 2 | E-post (SHA256, nedsänkt) | Email_LC_SHA256 | E-post | NEJ |
| 3 | Telefon (SHA256) | Phone_SHA256 | Telefon | NEJ |
| 4 | Google Ad ID (GAID) | GAID | ENHET | NEJ |
| 5 | Apple IDFA (ID för Apple) | IDFA | ENHET | NEJ |
| 6 | ECID | ECID | COOKIE | NEJ |

+++Markera för att visa det simulerade diagrammet

+++