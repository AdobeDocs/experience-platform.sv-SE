---
keywords: Experience Platform;användarhandbok;kundhandbok;populära ämnen;konfigurera instans;skapa instans;
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
feature: Customer AI
title: Konfigurera en AI-instans för kund
topic-legacy: Instance creation
description: Intelligenta tjänster ger kunden artificiell intelligens (AI) som en lättanvänd Adobe Sensei-tjänst som kan konfigureras för olika användningsområden. I följande avsnitt beskrivs hur du konfigurerar en instans av Kundens AI.
exl-id: 78353dab-ccb5-4692-81f6-3fb3f6eca886
source-git-commit: 52ab1527d3021500d934afe56cfc751116f784a4
workflow-type: tm+mt
source-wordcount: '2218'
ht-degree: 0%

---

# Konfigurera en AI-instans för kund

Tack vare kundens AI, som ingår i Intelligent Services, kan ni generera anpassade benägenhetspoäng utan att behöva bekymra er om maskininlärning.

Intelligenta tjänster ger kunden artificiell intelligens (AI) som en lättanvänd Adobe Sensei-tjänst som kan konfigureras för olika användningsområden. I följande avsnitt beskrivs hur du konfigurerar en instans av Kundens AI.

## Konfigurera din instans {#set-up-your-instance}

Välj **[!UICONTROL Services]** i den vänstra navigeringen. The **[!UICONTROL Services]** webbläsaren visas och alla tillgängliga tjänster visas. Välj **[!UICONTROL Open]**.

![](../images/user-guide/navigate-to-service.png)

The **Kund-AI** Gränssnittet visas och visar alla tjänstinstanser.

- Du hittar **[!UICONTROL Total profiles scored]** mätvärdena finns längst ned till höger på sidan **[!UICONTROL Create instance]** behållare. Det här måttet spårar det totala antalet profiler som kunden har bedömt för det aktuella kalenderåret, inklusive alla sandlådemiljöer och eventuella borttagna tjänstinstanser.

![](../images/user-guide/total-profiles.png)

Tjänstinstanser kan redigeras, klonas och tas bort med kontrollerna till höger i användargränssnittet. Om du vill visa dessa kontroller väljer du en instans från din befintliga **[!UICONTROL Service instances]**. Kontrollerna innehåller följande:

- **[!UICONTROL Edit]**: Markera **[!UICONTROL Edit]** gör att du kan ändra en befintlig tjänstinstans. Du kan redigera instansens namn, beskrivning och bedömningsfrekvens.
- **[!UICONTROL Clone]**: Markera **[!UICONTROL Clone]** kopierar den valda tjänstinstansinställningen. Du kan sedan ändra arbetsflödet för att göra mindre ändringar och byta namn på det som en ny instans.
- **[!UICONTROL Delete]**: Du kan ta bort en tjänstinstans, inklusive alla tidigare körningar.
- **[!UICONTROL Data source]**: En länk till den datauppsättning som används av den här instansen. Om du använder flera datauppsättningar och markerar hyperlänktexten, öppnas förhandsvisningsprogramvaran för datauppsättningen.
- **[!UICONTROL Last run details]**: Detta visas bara när en körning misslyckas. Här visas information om varför körningen misslyckades, t.ex. felkoder.
- **[!UICONTROL Score definition]**: En snabb översikt över målet som du konfigurerade för den här instansen.

![](../images/user-guide/service-instance-panel.png)

Om du vill skapa en ny instans väljer du **[!UICONTROL Create instance]**.

![](../images/user-guide/dashboard.png)

## Inställningar

Arbetsflödet där instansen skapas visas med början på **[!UICONTROL Setup]** steg.

Nedan finns viktig information om värden som du måste ge instansen:

- **[!UICONTROL Name]:** Instansens namn används på alla platser där AI-poäng för kunder visas. Därför bör namn beskriva vad förutsägelsepoängen representerar. Exempel:&quot;Sannolikhet för att avbryta tidskriftsprenumeration&quot;.

- **[!UICONTROL Description]:** En beskrivning som anger vad du försöker förutse.

- **[!UICONTROL Propensity type]:** Propensitetstypen bestämmer poängsättets och den metriska polaritetens avsikt. Du kan antingen välja **[!UICONTROL Churn]** eller **[!UICONTROL Conversion]**. Se anteckningen under [poängsammanfattning](./discover-insights.md#scoring-summary) i dokumentet med insikter om du vill ha mer information om hur benägenhetstypen påverkar instansen.

![Installationsskärm](../images/user-guide/create-instance.png)

Ange önskade värden och välj sedan **[!UICONTROL Next]** för att fortsätta.

## Markera data {#select-data}

Kunds-AI använder designdata för Adobe Analytics, Adobe Audience Manager, Experience Event och Consumer Experience Event för att beräkna benägenhetspoängen. När du väljer en datauppsättning visas bara de som är kompatibla med kundens AI. Om du vill välja en datauppsättning väljer du (**+**) bredvid datauppsättningsnamnet eller markera kryssrutan för att lägga till flera datauppsättningar samtidigt. Använd sökalternativet för att snabbt hitta de datauppsättningar du är intresserad av.

![Välj och söka efter datauppsättning](../images/user-guide/configure-dataset-page.png)

När du har valt de datauppsättningar du vill använda väljer du **[!UICONTROL Add]** om du vill lägga till datauppsättningarna i förhandsgranskningsfönstret för datauppsättningar.

![Välj datauppsättningar](../images/user-guide/select-datasets.png)

Välja informationsikonen ![informationsikon](../images/user-guide/info-icon.png) bredvid datauppsättningen öppnar förhandsvisningsprogramdrivrutinen för datauppsättningen.

![Välj och söka efter datauppsättning](../images/user-guide/dataset-info-2.png)

Datauppsättningsförhandsvisningen innehåller data som senaste uppdateringstid, källschema och en förhandsgranskning av de första tio kolumnerna.

### Fullständighet för datauppsättning {#dataset-completeness}

Det finns ett procentvärde för datauppsättningens fullständighet i datauppsättningsförhandsvisningen. Det här värdet ger en snabb ögonblicksbild av hur många kolumner i datauppsättningen som är tomma/null. Om en datauppsättning innehåller många värden som saknas och dessa värden hämtas någon annanstans rekommenderar vi att du inkluderar datauppsättningen som innehåller de värden som saknas. I det här exemplet är person-ID tomt, men person-ID fångas in i en separat datauppsättning som kan inkluderas.

>[!NOTE]
>
>Datauppsättningens fullständighet beräknas med hjälp av det maximala utbildningsfönstret för kundens AI (ett år). Detta innebär att data som är mer än ett år gamla inte beaktas när datamängdens fullständighetsvärde visas.
<!-- training dataset completness needs to change -->
![Fullständighet för datauppsättning](../images/user-guide/dataset-info.png)

### Välj en identitet {#identity}

För att flera datauppsättningar ska kunna kopplas till varandra måste du välja en identitetstyp (kallas även&quot;id namespace&quot;) och ett identitetsvärde i det namnutrymmet. Om du har tilldelat mer än ett fält som en identitet i ditt schema under samma namnutrymme, visas alla tilldelade identitetsvärden i den listruta för identitet som föregås av namnutrymmet, till exempel `EMAIL (personalEmail.address)` eller `EMAIL (workEmail.address)`.

>[!IMPORTANT]
>
>Samma identitetstyp (namnutrymme) måste användas för varje datamängd som du väljer. En grön bock visas bredvid identitetstypen i identitetskolumnen som anger att datauppsättningarna är kompatibla. Om du till exempel använder namnutrymmet Telefon och `mobilePhone.number` som identifierare måste alla identifierare för de återstående datauppsättningarna innehålla och använda namnutrymmet Telefon.

Markera en identitet genom att markera det understrukna värdet i identitetskolumnen. Välj en identitetsleverantör.

![välj samma namnutrymme](../images/user-guide/identity-type.png)

Om fler än en identitet är tillgänglig i ett namnutrymme måste du välja rätt identitetsfält för ditt användningsfall. Det finns till exempel två e-postidentiteter tillgängliga i e-postnamnutrymmet, en arbets- och en personlig e-postadress. Beroende på användningsfallet är det troligare att ett personligt e-postmeddelande fylls i och är mer användbart i individuella prognoser. Detta innebär att `EMAIL (personalEmail.address)` väljs som identitet.

![Datauppsättningsnyckeln är inte markerad](../images/user-guide/select-identity.png)

>[!NOTE]
>
> Om det inte finns någon giltig identitetstyp (namnutrymme) för en datauppsättning måste du ange en primär identitet och tilldela den till ett identitetsnamnutrymme med hjälp av [schemaredigerare](../../../xdm/schema/composition.md#identity). Mer information om namnutrymmen och identiteter finns på [Namnutrymmen för identitetstjänst](../../../identity-service/namespaces.md) dokumentation.

## Definiera ett mål {#define-a-goal}

<!-- https://www.adobe.com/go/cai-define-a-goal -->

The **[!UICONTROL Define goal]** visas och innehåller en interaktiv miljö där du kan definiera ett förutsägelsemål visuellt. Ett mål består av en eller flera händelser, där varje händelses förekomst baseras på det villkor den innehåller. Målet för en kundens AI-instans är att fastställa sannolikheten för att uppnå dess mål inom en viss tidsram.

Om du vill skapa ett mål väljer du **[!UICONTROL Enter Field Name]** följt av ett fält från listrutan. Välj den andra inmatningen, en sats för händelsens villkor, och ange sedan eventuellt målvärdet för att slutföra händelsen. Ytterligare händelser kan konfigureras genom att välja **[!UICONTROL Add event]**. Slutför målet genom att tillämpa en tidsram för förutsägelse i antal dagar och sedan välja **[!UICONTROL Next]**.

![](../images/user-guide/define-a-goal.png)

### Kommer att inträffa och kommer inte att inträffa

När du definierar ditt mål kan du välja **[!UICONTROL Will occur]** eller **[!UICONTROL Will not occur]**. Markera **[!UICONTROL Will occur]** betyder att de händelsevillkor du definierar måste uppfyllas för att en kunds händelsedata ska inkluderas i insikterna-gränssnittet.

Om du till exempel vill konfigurera ett program för att förutsäga om en kund kommer att göra ett köp, kan du välja **[!UICONTROL Will occur]** följt av **[!UICONTROL All of]** och sedan ange **commerce.purchase.id** (eller ett liknande fält) och **[!UICONTROL exists]** som -operatorn.

![inträffar](../images/user-guide/occur.png)

Det kan dock finnas fall då du är intresserad av att förutsäga om en händelse inte kommer att inträffa inom en viss tidsperiod. Om du vill konfigurera ett mål med det här alternativet väljer du **[!UICONTROL Will not occur]** i listrutan på den översta nivån.

Om du till exempel är intresserad av att förutsäga vilka kunder som blir mindre engagerade och inte besöker inloggningssidan för ditt konto nästa månad. Välj **[!UICONTROL Will not occur]** följt av **[!UICONTROL All of]** och sedan ange **web.webInteraction.URL** (eller ett liknande fält) och **[!UICONTROL equals]** som operatorn med **konto-inloggning** som värdet.

![inträffar inte](../images/user-guide/not-occur.png)

### Alla och alla

I vissa fall kanske du vill förutsäga om en kombination av händelser kommer att inträffa och i andra fall kanske du vill förutsäga förekomsten av en händelse från en fördefinierad uppsättning. För att kunna förutsäga om en kund kommer att ha en kombination av händelser väljer du **[!UICONTROL All of]** i listrutan på den andra nivån **[!UICONTROL Define Goal]** sida.

Du kanske vill förutsäga om en kund köper en viss produkt. Detta förutsägelsemål definieras av två villkor: a `commerce.order.purchaseID` **exists** och `productListItems.SKU` **är lika med** något specifikt värde.

![Alla exempel](../images/user-guide/all-of.png)

För att kunna förutsäga om en kund kommer att ha någon händelse från en viss uppsättning kan du använda **[!UICONTROL Any of]** alternativ.

Du kanske vill förutsäga om en kund besöker en viss URL-adress eller en webbsida med ett visst namn. Detta förutsägelsemål definieras av två villkor: `web.webPageDetails.URL` **börjar med** ett särskilt värde och `web.webPageDetails.name` **börjar med** ett visst värde.

![Alla exempel](../images/user-guide/any-of.png)

### Berättigad population *(valfritt)*

Som standard genereras benägenhetspoäng för alla profiler såvida inte en stödberättigad population anges. Du kan ange en berättigad population genom att definiera villkor för att inkludera eller exkludera profiler baserat på händelser.

![berättigad population](../images/user-guide/eligible-population.png)

### Anpassade händelser (*valfri*) {#custom-events}

Om du har ytterligare information förutom [standardhändelsefält](../input-output.md#standard-events) som används av kundens AI för att generera benägenhetspoäng, finns ett anpassat händelsealternativ. Om du använder det här alternativet kan du lägga till ytterligare händelser som du anser vara inflytelserika, vilket kan förbättra modellens kvalitet och bidra till mer korrekta resultat. Om den datamängd du har valt innehåller anpassade händelser som har definierats i ditt schema, kan du lägga till dem i din instans.

![händelsefunktion](../images/user-guide/event-feature.png)

Om du vill lägga till en anpassad händelse väljer du **[!UICONTROL Add custom event]**. Därefter anger du ett anpassat händelsenamn och mappar det till händelsefältet i schemat. Anpassade händelsenamn visas i stället för fältvärdet när du tittar på inflytelserika faktorer och andra insikter. Detta innebär användar-ID:n, reservations-ID:n, enhetsinformation och andra anpassade värden listas med det anpassade händelsenamnet i stället för händelsens ID/värde. Dessa ytterligare anpassade händelser används av kundens AI för att förbättra modellens kvalitet och ge mer korrekta resultat.

![Eget händelsefält](../images/user-guide/custom-event.png)

Välj sedan den operator som du vill använda i listrutan med tillgängliga operatorer. Endast operatorer som är kompatibla med händelsen visas.

![Anpassad händelseoperator](../images/user-guide/custom-operator.png)

Ange fältvärdena om den markerade operatorn kräver ett. I det här exemplet behöver vi bara se om det finns ett hotell- eller restaurangbokningar. Men om vi vill vara mer exakta kan vi använda likhetsoperatorn och ange ett exakt värde i värdeprompten.

![Fältvärde för anpassad händelse](../images/user-guide/custom-value.png)

När du är klar väljer du **[!UICONTROL Next]** i det övre högra hörnet för att fortsätta.

### Egna profilattribut (*valfri*)

Du kan definiera viktiga profildatauppsättningsfält (med tidsstämplar) i dina data utöver de [standardhändelsefält](../input-output.md#standard-events) används av kundens AI för att generera benägenhetspoäng. Om du använder det här alternativet kan du lägga till ytterligare profilattribut som du anser vara inflytelserika, vilket kan förbättra modellens kvalitet och ge mer korrekta resultat. Om du dessutom lägger till anpassade profilattribut kan kundens AI bättre visa hur specifika profiler hamnar i en benägenhetsklocka.

>[!NOTE]
>
>När du lägger till ett anpassat profilattribut följer du samma arbetsflöde som när du lägger till en anpassad händelse.

![lägg till ett anpassat profilattribut](../images/user-guide/profile-attributes.png)

### Konfigurera ett schema *(valfritt)* {#configure-a-schedule}

The **[!UICONTROL Advanced]** visas. Med det här valfria steget kan du konfigurera ett schema för att automatisera förutsägelsekörningar, definiera undantag för förutsägelser för att filtrera vissa händelser eller välja **[!UICONTROL Finish]** om inget behövs.

Konfigurera ett poängschema genom att konfigurera **[!UICONTROL Scoring Frequency]**. Automatiserade prognoskörningar kan schemaläggas att köras antingen varje vecka eller varje månad.

![](../images/user-guide/schedule.png)

### Undantag för förutsägelse

Om datauppsättningen innehåller kolumner som lagts till som testdata kan du lägga till den kolumnen eller händelsen i en exkluderingslista genom att markera **Lägg till undantag** följt av att ange det fält som du vill utesluta. Detta förhindrar att händelser som uppfyller vissa villkor utvärderas när bakgrundsmusik genereras. Den här funktionen kan användas för att filtrera bort irrelevanta dataindata eller vissa kampanjer.

Om du vill exkludera en händelse väljer du **[!UICONTROL Add exclusion]** och definiera händelsen. Om du vill ta bort ett undantag markerar du ellipserna (**[!UICONTROL ...]**) till det övre högra hörnet i händelsebehållaren och välj sedan **[!UICONTROL Remove Container]**.

![](../images/user-guide/exclusion.png)

### Växla profil

Tack vare växlingsknappen Profil kan kundens artificiell intelligens (AI) exportera poängresultaten till kundprofilen i realtid. Om du inaktiverar den här växeln kan du inte lägga till modellens poängresultat i profilen. Resultat av AI-bedömning för kunder är fortfarande tillgängliga med den här funktionen inaktiverad.

När du använder AI för första gången bör du inaktivera den här funktionen tills du är nöjd med modellens utdataresultat. Detta förhindrar att du överför flera poängsättningsdatauppsättningar till kundprofilen i realtid samtidigt som du finjusterar modellen.

![Växla profil](../images/user-guide/advanced-workflow.png)

När du har angett poängschemat, inkluderar du undantag för förutsägelser och profilen växlar var du vill ha det väljer du **[!UICONTROL Finish]** i det övre högra hörnet för att skapa en AI-instans för kunden.

Om instansen skapas utan fel utlöses en förutsägelsekörning omedelbart och efterföljande körningar utförs enligt ditt definierade schema.

>[!NOTE]
>
>Beroende på storleken på indata kan det ta upp till 24 timmar att slutföra förutsägelser.

Genom att följa det här avsnittet har du konfigurerat en instans av Customer AI och utfört en förutsägelsekörning. När körningen är klar fyller poängsatta insikter automatiskt i profiler med förutbestämda poängvärden om profilväxlingen är aktiverad. Vänta i upp till 24 timmar innan du fortsätter till nästa avsnitt i den här självstudiekursen.

## Nästa steg {#next-steps}

Genom att följa den här självstudiekursen har du konfigurerat en instans av kundens AI och genererat benägenhetspoäng. Nu kan du välja att använda segmentverktyget för att [skapa kundsegment med förutbestämda poäng](./create-segment.md) eller [identifiera insikter med kundens AI](./discover-insights.md).

## Ytterligare resurser

Följande video är utformad för att ge dig en bättre förståelse för hur kundens AI kan konfigureras. Dessutom finns bästa praxis och exempel på användningsfall.

>[!IMPORTANT]
>
> Följande video är inaktuell. Den senaste informationen finns i dokumentationen.

>[!VIDEO](https://video.tv.adobe.com/v/32665?learn=on&quality=12)
