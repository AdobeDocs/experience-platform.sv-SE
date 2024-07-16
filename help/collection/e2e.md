---
title: Översikt över datainsamling från början till slut
description: En översikt på hög nivå över hur du skickar händelsedata till Adobe Experience Cloud-lösningar med Adobe Experience Platform datainsamlingsfunktioner.
exl-id: 01ddbb19-40bb-4cb5-bfca-b272b88008b3
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '2534'
ht-degree: 0%

---

# Översikt över datainsamling från början till slut

Adobe Experience Platform samlar in och överför data till andra Adobe-produkter och tredjepartsdestinationer. För att kunna skicka händelsedata från ditt program till Experience Platform är det viktigt att förstå dessa kärntekniker och hur de konfigureras för att leverera data till de destinationer du behöver, när du behöver det.

Den här guiden innehåller en självstudiekurs på hög nivå om hur du skickar en händelse via Edge Network med hjälp av plattformens datainsamlingsfunktioner. Självstudiekursen går igenom stegen för att installera och konfigurera taggtillägget Adobe Experience Platform Web SDK i användargränssnittet för datainsamling (tidigare Adobe Experience Platform Launch).

>[!NOTE]
>
>Du kan också välja att installera och konfigurera SDK manuellt om du inte vill använda taggar, men de omgivande stegen måste ändå slutföras enligt nedan.
>
>Alla steg som omfattar användargränssnittet för datainsamling kan också utföras i användargränssnittet för Experience Platform.

## Förhandskrav

I den här självstudien används användargränssnittet för datainsamling för att skapa ett schema, konfigurera ett datastream och installera Web SDK. För att kunna utföra de här åtgärderna i användargränssnittet måste du ha tillgång till minst en webbegenskap tillsammans med följande [egenskapsrättigheter](../tags/ui/administration/user-permissions.md#property-rights):

* Utveckla
* Hantera tillägg

Se guiden [Hantera behörigheter för datainsamling](./permissions.md) för att lära dig hur du beviljar åtkomst till egenskaper och egenskapsrättigheter.

Om du vill använda de olika datainsamlingsprodukterna som nämns i den här guiden måste du även ha tillgång till datastreams och möjlighet att skapa och hantera scheman. Om du behöver tillgång till någon av dessa funktioner kontaktar du ditt Adobe-kontoteam för att få den åtkomst du behöver. Observera att om du inte har köpt Adobe Experience Platform ger Adobe dig tillgång till SDK utan extra kostnad.

Om du redan har åtkomst till Platform måste du se till att du har aktiverat alla [behörigheter](../access-control/home.md#permissions) under följande kategorier:

* Datamodellering
* Identiteter

Mer information om hur du tilldelar behörigheter för plattformsfunktioner till användare finns i [användargränssnittsöversikten för åtkomstkontroll](../access-control/ui/overview.md).

## Processsammanfattning

Processen med att konfigurera datainsamling för webbplatsen kan sammanfattas på följande sätt:

1. [Skapa ett schema](#schema) för att bestämma hur dina data ska struktureras när de skickas till Edge Network.
1. [Skapa en datastream](#datastream) för att konfigurera vilka mål du vill att dina data ska skickas till.
1. [Installera och konfigurera Web SDK](#sdk) för att skicka data till dataströmmen när vissa händelser inträffar på webbplatsen.

När du kan skicka data till Edge Network kan du även [konfigurera vidarebefordran av händelser](#event-forwarding) om din organisation har en licens för det.

## Skapa ett schema {#schema}

[Experience Data Model (XDM)](../xdm/home.md) är en öppen källkodsspecifikation som innehåller gemensamma strukturer och definitioner för data i form av scheman. Med andra ord är XDM ett sätt att strukturera och formatera data på ett sätt som kan användas av Edge Network och andra Adobe Experience Cloud-program.

Det första steget i att konfigurera datainsamlingsåtgärderna är att skapa ett XDM-schema som representerar dina data. I ett senare steg i den här självstudiekursen mappas de data som du vill skicka till strukturen för det här schemat.

>[!NOTE]
>
>XDM-scheman är mycket anpassningsbara. I stället för att vara alltför prediktiv fokuserar stegen nedan specifikt på schemakraven för Web SDK. Utanför dessa parametrar kan du definiera den återstående strukturen för dina data.

Välj **[!UICONTROL Schemas]** i den vänstra navigeringen i användargränssnittet. Här visas en lista med tidigare skapade scheman som tillhör din organisation. Om du vill fortsätta väljer du **[!UICONTROL Create schema]** och sedan **[!UICONTROL XDM ExperienceEvent]** i listrutan.

![Arbetsytan Scheman](./images/e2e/schemas.png)

En dialogruta visas där du uppmanas att börja lägga till fältgrupper i schemat. Om du vill skicka händelser med Web SDK måste du lägga till fältgruppen **[!UICONTROL AEP Web SDK ExperienceEvent Mixin]**. Den här fältgruppen innehåller definitioner för dataattribut som samlas in automatiskt av Web SDK-biblioteket.

Använd sökfältet för att begränsa listan så att det blir enklare att hitta fältgruppen. När du har hittat den markerar du den i listan innan du väljer **[!UICONTROL Add field groups]**.

![Arbetsytan Scheman](./images/e2e/add-field-group.png)

Schemaarbetsytan visas med en trädstruktur i XDM-schemat som innehåller fälten från Web SDK-fältgruppen.

![Schemastruktur](./images/e2e/schema-structure.png)

Markera rotfältet i trädet för att öppna **[!UICONTROL Schema properties]** i den högra listen, där du kan ange ett namn och en valfri beskrivning för schemat.

![Namnge schemat](./images/e2e/name-schema.png)

Om du vill lägga till fler fält i schemat kan du göra det genom att välja **[!UICONTROL Add]** under avsnittet **[!UICONTROL Field groups]** i den vänstra listen.

![Lägg till fältgrupper](./images/e2e/add-field-groups.png)

>[!NOTE]
>
>I guiden om att [lägga till fältgrupper](../xdm/ui/resources/schemas.md#add-field-groups) i XDM-dokumentationen finns mer information om hur du söker efter olika fältgrupper så att de passar dina användningsexempel.
>
>Det bästa sättet är att bara lägga till fält för data som du planerar att skicka via Edge Network. När du har lagt till fält i ett schema och sparat det, kan endast additiva ändringar göras i schemat därefter. Mer information finns i avsnittet [regler för schemautveckling](../xdm/schema/composition.md#evolution).

När du har lagt till de fält du behöver väljer du **[!UICONTROL Save]** för att spara schemat.

![Spara schemat](./images/e2e/save-schema.png)

## Skapa ett datastream {#datastream}

En datastream är en konfiguration som talar om för Edge Network var du vill att dina data ska skickas. En datastream anger vilka Experience Cloud-produkter du vill skicka data till och hur du vill att data ska hanteras och lagras i respektive produkt.

>[!NOTE]
>
>Om du vill använda [händelsevidarebefordran](../tags/ui/event-forwarding/overview.md) (förutsatt att din organisation har licens för funktionen) måste du aktivera den för ett datastream på samma sätt som du aktiverar Adobe-produkter. Information om den här processen beskrivs i ett [senare avsnitt](#event-forwarding).

Välj **[!UICONTROL Datastreams]** i den vänstra navigeringen. Härifrån kan du välja ett befintligt datastam från listan som ska redigeras, eller så kan du skapa en ny konfiguration genom att välja **[!UICONTROL New Datastream]**.

![Datastreams](./images/e2e/datastreams.png)

Konfigurationskraven för en datastream beror på vilka produkter och funktioner du skickar data till. Mer information om konfigurationsalternativen för varje produkt finns i [datastreams-översikten](../datastreams/overview.md).

## Installera och konfigurera Web SDK {#install}

När du har skapat ett schema och ett datastream är nästa steg att installera och konfigurera Platform Web SDK för att börja skicka data till Edge Network.

>[!NOTE]
>
>I det här avsnittet används användargränssnittet för datainsamling för att konfigurera Web SDK-taggtillägget, men du kan även installera och konfigurera det med Raw-kod i stället. Mer information finns i följande handböcker:
>
>* [Installera SDK](/help/web-sdk/install/overview.md)
>* [Konfigurera SDK](/help/web-sdk/commands/configure/overview.md)
>
>Observera också att även om du bara vill använda händelsevidarebefordran måste du fortfarande installera och konfigurera SDK enligt beskrivningen innan du konfigurerar händelsevidarebefordran i ett [senare steg](#event-forwarding).

Processen kan sammanfattas enligt följande:

1. [Installera Adobe Experience Platform Web SDK på en taggegenskap](#install-sdk) för att få tillgång till dess funktioner.
1. [Skapa ett XDM-objektdataelement](#data-element) om du vill mappa variabler på webbplatsen till strukturen i XDM-schemat som du skapade tidigare.
1. [Skapa en regel](#rule) som talar om för SDK när data ska skickas till Edge Network.
1. [Skapa och installera ett bibliotek](#library) för att implementera regeln på din webbplats.

### Installera SDK på en taggegenskap {#install-sdk}

Välj **[!UICONTROL Tags]** i den vänstra navigeringen om du vill visa en lista med taggegenskaper. Du kan välja en befintlig egenskap som ska redigeras om du vill, eller så kan du markera **[!UICONTROL New Property]** i stället.

![Egenskaper](./images/e2e/properties.png)

Om du skapar en ny egenskap anger du ett beskrivande namn och anger [!UICONTROL Platform] till **[!UICONTROL Web]**. Ange den fullständiga domänen för webbegenskapen och välj sedan **[!UICONTROL Save]**.

![Skapa egenskap](./images/e2e/create-property.png)

Översiktssidan för egenskapen visas. Här väljer du **[!UICONTROL Extensions]** i den vänstra navigeringen och sedan **[!UICONTROL Catalog]**. Sök efter listan för Platform Web SDK (eventuellt med sökfältet för att begränsa resultaten) och välj **[!UICONTROL Install]**.

![Installera Web SDK](./images/e2e/install-sdk.png)

Konfigurationssidan för SDK visas. De flesta obligatoriska värden fylls i automatiskt med standardvärden som du kan ändra om du vill.

![Konfigurera Web SDK](./images/e2e/configure-sdk.png)

Innan du kan installera SDK måste du dock välja en datastream så att den vet var data ska skickas till. Under **[!UICONTROL Datastreams]** använder du listrutemenyn för att välja den datastream som du konfigurerade i ett [tidigare steg](#datastream). När du har angett datastream väljer du **[!UICONTROL Save]** för att slutföra installationen av SDK till egenskapen.

![Ange dataström och spara](./images/e2e/set-datastream.png)

### Skapa ett XDM-dataelement {#data-element}

För att SDK ska kunna skicka data till Edge Network måste dessa data mappas till XDM-schemat som du skapade i ett [föregående steg](#schema). Mappningen görs med hjälp av ett dataelement.

I användargränssnittet väljer du **[!UICONTROL Data Elements]** och sedan **[!UICONTROL Create New Data Element]**.

![Skapa nytt dataelement](./images/e2e/data-elements.png)

På nästa skärm väljer du **[!UICONTROL Adobe Experience Platform Web SDK]** under listrutan [!UICONTROL Extension] och sedan **[!UICONTROL XDM object]** som dataelementtyp.

![XDM-objekttyp](./images/e2e/xdm-object.png)

Konfigurationsdialogrutan visas för XDM-objekttypen. Dialogrutan väljer automatiskt din plattformssandlåda, och härifrån kan du se alla scheman som har skapats i den sandlådan. Välj XDM-schemat som du skapade tidigare från listan.

![XDM-objekttyp](./images/e2e/select-schema.png)

Schemats struktur visas. Alla fält med en asterisk (**\***) anger fält som fylls i automatiskt när händelser utlöses. För alla andra fält kan du utforska schemats struktur och fylla i resten av data.

![Mappa data till XDM-fält](./images/e2e/map-schema.png)

>[!NOTE]
>
>Skärmbilden ovan visar hur du mappar en globalt tillgänglig variabel från klientsidan på webbplatsen (`cartAbandonsTotal`) till ett XDM-fält genom att referera till dess namn i fältet [!UICONTROL Value], omgivet av procenttecken (`%`).
>
>Du kan också använda andra dataelement som du redan har skapat för att fylla i dessa fält. Mer information finns i referensen för [dataelement](../tags/ui/managing-resources/data-elements.md) i taggdokumentationen.

När du har mappat dina data till schemat anger du ett namn för dataelementet innan du väljer **[!UICONTROL Save]**.

![Namnge och spara dataelement](./images/e2e/name-and-save.png)

### Skapa en regel

När du har sparat dataelementet är nästa steg att skapa en regel som skickar den till Edge Network när en viss händelse inträffar på webbplatsen (till exempel när en kund lägger till en produkt i en kundvagn).

Du kan ange regler för praktiskt taget alla händelser som kan inträffa på webbplatsen. I det här avsnittet visas hur du skapar en regel som utlöses när en kund skickar in ett formulär. Följande HTML representerar en enkel webbsida med formuläret&quot;Lägg till i kundvagnen&quot;, som kommer att vara regelns ämne:

```html
<!DOCTYPE html>
<html>
<body>

  <form id="add-to-cart-form">
    <label for="item">Product:</label><br>
    <input type="text" id="item" name="item"><br>
    <label for="amount">Amount:</label><br>
    <input type="number" id="amount" name="amount" value="1"><br><br>
    <input type="submit" value="Add to Cart">
  </form> 

</body>
</html>
```

I användargränssnittet för datainsamling väljer du **[!UICONTROL Rules]** i den vänstra navigeringen och sedan **[!UICONTROL Create New Rule]**.

![Regler](./images/e2e/rules.png)

Ange ett namn för regeln på nästa skärm. Härifrån är nästa steg att bestämma händelsen för regeln (med andra ord när regeln ska aktiveras). Välj **[!UICONTROL Add]** under [!UICONTROL Events].

![Namnregel](./images/e2e/name-rule.png)

Händelsekonfigurationssidan visas. Om du vill konfigurera en händelse måste du först välja händelsetyp. Händelsetyper tillhandahålls av tillägg. Om du vill ställa in en händelse av typen&quot;skicka formulär&quot;, till exempel, väljer du tillägget **[!UICONTROL Core]** och sedan händelsetypen **[!UICONTROL Submit]** under kategorin **[!UICONTROL Form]**.

>[!NOTE]
>
>Mer information om de olika händelsetyperna i webbtilläggen för Adobe, inklusive hur du konfigurerar dem, finns i [Adobe-tilläggsreferensen](../tags/extensions/client/overview.md) i taggdokumentationen.

Med formulärsändningshändelsen kan du använda en [CSS-väljare](https://www.w3schools.com/css/css_selectors.asp) för att referera till ett specifikt element som regeln ska starta på. I exemplet nedan används ID:t `add-to-cart-form` så att den här regeln bara aktiveras för formuläret&quot;Lägg till i kundvagnen&quot;. Välj **[!UICONTROL Keep Changes]** om du vill lägga till händelsen i regeln.

![Händelsekonfiguration](./images/e2e/event-config.png)

Regelkonfigurationssidan visas igen och visar att händelsen har lagts till. Du kan begränsa [!UICONTROL If] genom att lägga till ytterligare villkor till regeln.

I annat fall är nästa steg att lägga till en åtgärd som regeln ska utföra när den aktiveras. Välj **[!UICONTROL Add]** under **[!UICONTROL Actions]** för att fortsätta.

![Lägg till åtgärd](./images/e2e/add-action.png)

Sidan för åtgärdskonfiguration visas. Om du vill hämta regeln för att skicka data till Edge Network väljer du **[!UICONTROL Adobe Experience Platform Web SDK]** som tillägg och **[!UICONTROL Send event]** som åtgärdstyp.

![Åtgärdstyp](./images/e2e/action-type.png)

Skärmen uppdateras och visar ytterligare alternativ för att konfigurera åtgärden skicka händelse. Under **[!UICONTROL Type]** kan du ange ett anpassat typvärde för att fylla i `eventType` XDM-fältet. Under **[!UICONTROL XDM data]** anger du namnet på XDM-datatypen som du skapade tidigare (omges av procenttecken), eller väljer databasikonen (![Databasikonen](./images/e2e/database-symbol.png)) för att välja den från en lista. Detta är de data som slutligen kommer att skickas till Edge Network.

Välj **[!UICONTROL Keep Changes]** när du är klar.

![Åtgärdskonfiguration](./images/e2e/action-config.png)

När du har konfigurerat regeln väljer du **[!UICONTROL Save]** för att slutföra processen.

![Spara regel](./images/e2e/save-rule.png)

### Skapa och installera ett bibliotek {#library}

När regeln har konfigurerats kan du lägga till den i ett taggbibliotek, skapa biblioteket i en miljö och installera det bygget på webbplatsen.

>[!NOTE]
>
>Om du inte har konfigurerat någon miljö i användargränssnittet för datainsamling än måste du göra det innan du kan skapa en version. Mer information finns i avsnittet [Konfigurera en miljö för en webbegenskap](../tags/ui/publishing/environments.md#web-configuration) i taggdokumentationen.

Mer information om hur du skapar ett bibliotek, lägger till tillägg och regler i biblioteket och skapar biblioteket i en miljö finns i guiden om [hantering av bibliotek](../tags/ui/publishing/libraries.md) i taggdokumentationen. När du skapar biblioteket måste du ta med tillägget Platform Web SDK och de datainsamlingsregler som du skapade tidigare.

När du har skapat biblioteket och dess bygge har tilldelats en miljö kan du installera den miljön på klientsidan av webbplatsen. Mer information finns i avsnittet [Installera miljöer](../tags/ui/publishing/environments.md#installation).

När du har installerat miljön på webbplatsen kan du [testa implementeringen](../tags/ui/publishing/embed-code-testing.md) med Adobe Experience Platform Debugger.

## Konfigurera händelsevidarebefordran (valfritt) {#event-forwarding}

>[!NOTE]
>
>Vidarebefordran av händelser är bara tillgängligt för organisationer som har licensierats för det.

När du har konfigurerat SDK för att skicka data till Edge Network kan du konfigurera vidarebefordran av händelser för att tala om för Edge Network var du vill att dessa data ska levereras.

Om du vill använda händelsevidarebefordran måste du först skapa en egenskap för händelsevidarebefordran. Välj **[!UICONTROL Event Forwarding]** i den vänstra navigeringen och välj sedan **[!UICONTROL New Property]**. Ange ett namn för egenskapen innan du väljer **[!UICONTROL Save]**.

När du har skapat en egenskap för vidarebefordring av händelser är nästa steg att skapa en regel som bestämmer var data ska skickas. Regler för egenskaper för vidarebefordran av händelser skapas på ungefär samma sätt som taggegenskaper, med undantag för att inga händelser kan anges (eftersom vidarebefordran endast hanterar händelser som tas emot direkt från datastream). För regelns åtgärd kan du använda ett av de tillgängliga tilläggen för vidarebefordran av händelser eller använda anpassad kod för att leverera händelsen i stället.

![Regel för vidarebefordran av händelse](./images/e2e/event-forwarding-rule.png)

På liknande sätt som tidigare måste du, när du har konfigurerat regeln, lägga till den i ett bibliotek och skapa biblioteket i en miljö.

När bygget är klart är det sista steget att uppdatera datastream som du [tidigare konfigurerat](#datastream) och aktivera händelsevidarebefordran. Börja med att navigera till **[!UICONTROL Datastreams]** och välj det aktuella dataflödet i listan. Härifrån aktiverar du växlingen för att vidarebefordra händelser och anger namnen på den egenskap och miljö som du just konfigurerade.

![Dataström för vidarebefordran av händelser](./images/e2e/event-forwarding-datastream.png)

## Nästa steg

Den här guiden ger en heltäckande översikt över hur du skickar data till Edge Network med hjälp av Platform Web SDK. Mer information om de olika komponenterna och tjänsterna finns i dokumentationen som är länkad till i den här handboken.
