---
title: Översikt över tillägget Algoliets händelsevidarebefordring
description: Lär dig hur du konfigurerar och använder tillägget för händelsevidarebefordran i Algolia i Adobe Experience Platform. Vidarebefordra användarbeteendedata via API:t för insikter, konfigurera regler, mappa XDM-fält och verifiera händelseleverans.
last-substantial-update: 2025-05-09T00:00:00Z
source-git-commit: d1b641ed0b48357a2f4b78d6829ccab52e4889ca
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 0%

---


# Översikt över tillägget [!DNL Algolia] för händelsevidarebefordring {#overview}

>[!NOTE]
>
>Adobe Experience Platform Launch ingår nu i Adobe Experience Platform datainsamlingstekniker. Därför har terminologisk uppdatering gjorts i produktdokumentationen. En omfattande lista över de här ändringarna finns i [handboken om terminologisk uppdatering](../../../../tags/term-updates.md).

Använd [!DNL Algolia] för att leverera snabba, relevanta och personaliserade sökupplevelser. Med AI-optimering kan ni förbättra sökresultaten och rekommendationerna så att användarna snabbt kan hitta de produkter, det innehåll eller den information de behöver.

Använd tillägget [!DNL Algolia] för vidarebefordran av händelser för att skicka användarbeteendehändelser till [!DNL Algolia] via [!DNL Insights API]. Dessa beteendedata möjliggör AI-baserade rekommendationer, personaliserade upplevelser och intelligenta sökfunktioner.

## Förhandskrav {#prerequisites}

Innan du installerar tillägget bör du kontrollera att du har ett [!DNL Algolia]-konto med åtkomst till [!DNL Insights API]. Om du inte har något konto [registrerar du dig](https://dashboard.algolia.com/users/sign_up) och aktiverar åtkomst till API:t.

Se även till att du förstår hur du använder [!DNL Algolia] [!DNL Insights API]. En översikt över hur du skickar händelser finns i [skicka händelser med Insights API](https://www.algolia.com/doc/guides/sending-events/getting-started/).

Samla följande värden från din [!DNL Algolia]-kontokontrollpanel:
- **[!UICONTROL Application ID]**
- **[!UICONTROL Search API Key]**
- **[!UICONTROL Index Name]**

## Installera tillägget {#install}

Så här installerar du tillägget [!DNL Algolia]:

Navigera till **[!UICONTROL Data Collection]** i [!DNL Adobe Experience Platform]. Klicka på fliken **[!UICONTROL Extensions]**.  

Öppna **[!UICONTROL Catalog]** och leta upp tillägget **[!UICONTROL Algolia Event Forwarding]** och välj sedan **[!UICONTROL Install]**.

![Installationsprocessen för tillägget Algolia Event Forwarding i Adobe Experience Platform](../../../images/extensions/server/algolia/install-extension.png)

### Konfigurera tillägget {#configure-extension}

Om du vill konfigurera tillägget [!DNL Algolia] för vidarebefordran av händelser går du till fliken **[!UICONTROL Extensions]**, markerar tillägget **[!UICONTROL Algolia]** och väljer sedan **[!UICONTROL Configure]**.

![Konfigurationsskärmen för tillägget för vidarebefordran av Algoliska händelser i Adobe Experience Platform](../../../images/extensions/server/algolia/configure.png)

| Egenskap | Beskrivning |
|----------|-------------|
| **[!UICONTROL Application ID]** | Ange [!UICONTROL Application ID] som finns i Algoliet Dashboard under avsnittet [ API-nycklar ](https://www.algolia.com/account/api-keys/all). |
| **[!UICONTROL Search API Key]** | Ange [!UICONTROL Search API Key] som finns i Algoliet Dashboard under avsnittet [ API-nycklar ](https://www.algolia.com/account/api-keys/all). |
| **[!UICONTROL Index Name]** | Ange [!UICONTROL Index Name] som innehåller dina produkter eller ditt innehåll. Detta index används som standardvärde. |

{style="table-layout:auto"}

## Tilläggsåtgärdstyper för händelsevidarebefordran av [!DNL Algolia] {#action-types}

Tillägget [!DNL Algolia] för vidarebefordran av händelser erbjuder en enda åtgärdstyp som kan användas i avsnittet **[!UICONTROL Then]** i en regel:

### Skicka händelse {#send-event}

Konfigurera åtgärden **[!UICONTROL Send event]** för att vidarebefordra händelser till [!DNL Algolia]:

Välj **[!UICONTROL Rules]** > **[!UICONTROL Add Rule]** eller välj en befintlig regel. Lägg till en åtgärd i delen **[!UICONTROL Then]** av regeln och välj **[!UICONTROL Extension]**: [!DNL Algolia] Vidarebefordra händelser > **[!UICONTROL Action Type]**: **[!UICONTROL Send Events]**.

![Konfiguration av åtgärden Skicka händelse i tillägget Vidarebefordra händelse i Algolia.](../../../images/extensions/server/algolia/send-event.png)

## Implementera händelsefältgruppen [!DNL Algolia] {#algolia-field-group}

Se till att du lägger till händelsefältgruppen [!DNL Algolia] i schemat innan du använder tillägget [!DNL Algolia] för händelsevidarebefordran. Det är en av standardfältgrupperna som tillhandahålls via Experience Platform.

![Konfiguration av händelsefältgrupp i Algolia](../../../images/extensions/server/algolia/algolia-field-groups.png)

### Lägg till fältgruppen [!DNL Algolia] i ditt schema {#add-algolia-field-group}

Så här lägger du till händelsefältgruppen [!DNL Algolia]:

Navigera till **[!UICONTROL Schemas]** och välj **[!UICONTROL Browse]**.

Lägg till ett nytt schema eller uppdatera ett befintligt schema som du använder för att skicka webbhändelser och hovra över ikonen **[!UICONTROL Add]**. Ange *[!DNL Algolia]* i sökrutan om du vill begränsa resultaten.

Välj fältgruppen **[!DNL Algolia]Händelseinformation** > **[!UICONTROL Add field group]** > **[!UICONTROL Save]**.

![Konfiguration av fältgrupp för Algoliprofil i Experience Platform](../../../images/extensions/server/algolia/algolia-profile-field-group.png)

### Mappa och skicka data med taggen [!UICONTROL Data Collection]

Tillägget [!DNL Algolia] för vidarebefordran av händelser kan användas med **[!DNL Adobe Experience Platform Web SDK]** för att skicka data från din webbplats till [!DNL Algolia]. Detta görs genom att skapa en taggegenskap, mappa data till objektet [!DNL XDM] och konfigurera regler för att skicka händelser.

#### Steg 1: Skapa en taggegenskap med SDK på webben

1. Skapa en taggegenskap.
2. Installera tillägget [!DNL Adobe Experience Platform Web SDK].
3. Använd det här tillägget om du vill mappa data från HTML till fältgruppen **[!DNL Algolia]Event**.

![Exempel på en HTML-datauppsättning som mappas till händelsefältgruppen Algolia](../../../images/extensions/server/algolia/html-dataset.png)

#### Steg 2: Skapa ett dataelement för mappning av [!DNL XDM]

1. Skapa en [!UICONTROL Data Element] med **[!DNL Adobe Experience Platform Web SDK]**.
2. Välj **[!UICONTROL XDM object]** som dataelementtyp.
3. Mappa dina data till rätt [!DNL XDM]-fält och se till att [!DNL Algolia]-specifika fält fylls i.

![](../../../images/extensions/server/algolia/xdm-mapping.png)

#### Steg 3: Skapa en regel för att skicka händelser

1. Skapa en ny regel i taggegenskapen.
2. Lägg till nödvändiga händelseutlösare, till exempel sidinläsning eller klickningshändelser.
3. Lägg till en åtgärd med **[!DNL Adobe Experience Platform Web SDK]**.
4. Välj **[!UICONTROL Send event]** som åtgärdstyp.
5. Konfigurera åtgärden så att dataelementet [!DNL XDM] används.

![Exempel på konfiguration av en regelåtgärd i tillägget för vidarebefordran av Algoliska händelser](../../../images/extensions/server/algolia/rule-action.png)

#### Steg 4: Publicera och testa

1. Publicera reglerna och tilläggsändringarna i målmiljön.
2. Använd [!DNL Adobe Experience Platform Debugger] för att verifiera att data skickas till Adobe Experience Platform och vidarebefordras till [!DNL Algolia].

![Konfigurera en regel för att skicka händelser med tillägget Algolia](../../../images/extensions/server/algolia/adobe-debugger.png)

### Verifiera händelser i [!DNL Algolia]

När du har konfigurerat tillägget [!DNL Algolia] för vidarebefordring av händelser kan du verifiera att händelser skickas och tas emot korrekt genom att följa dessa steg:

Navigera till din [!DNL Algolia]-instrumentpanel och gå till **[!UICONTROL Data Sources > Events > Debugger]**.

Välj händelsen som matchar händelsen som skickades från [!DNL Algolia]-händelsevidarebefordringstillägget och verifiera att det finns förväntade data i händelsen.

![Verifiera händelser i Algoliet-felsökaren](../../../images/extensions/server/algolia/algolia-debugger.png)

## Vanliga implementeringsscenarier

Använd tillägget [!DNL Algolia] för händelsevidarebefordran för att samla in och skicka användarinteraktionsdata för olika användningsfall, vilket förbättrar sökrelevansen och personaliseringen.

### Spåra produkt- eller innehållsvyer

Använd tillägget för att spåra när användare visar produkt- eller innehållssidor, vilket hjälper [!DNL Algolia] förstå användarintressen.

### Spåra konverteringshändelser

Spåra tilläggshändelser, köp och andra konverteringshändelser för att optimera [!DNL Algolia]s AI-baserade rekommendationer.

## Felsökning

Om du stöter på problem när du implementerar tillägget för att vidarebefordra [!DNL Algolia]-händelser bör du överväga följande felsökningssteg:

### Händelser visas inte i [!DNL Algolia]

Om händelser inte visas i [!DNL Algolia] kontrollerar du följande:

- **Verifiera API-autentiseringsuppgifter**: Kontrollera att **[!UICONTROL Application ID]** och **[!UICONTROL API Key]** matchar värdena på kontrollpanelen i [!DNL Algolia].
- **Kontrollera händelsefelsökning**: Använd [!DNL Algolia]-händelsefelsökaren för att bekräfta om händelser tas emot. Om inte, kontrollerar du konfigurationen för regeln för vidarebefordran av händelse.
- **Inspektera XDM-mappning**: Kontrollera att alla obligatoriska fält i schemat [!DNL Algolia] är korrekt mappade i objektet [!DNL XDM].

### Felaktiga händelsedata

- Kontrollera att [!DNL XDM]-objektdataelementet är korrekt mappat till [!DNL Algolia]-schemat, med alla obligatoriska fält.
- Bekräfta att händelseparametrarna matchar det förväntade format och den struktur som beskrivs i [!DNL Algolia]s API-dokumentation för insikter.

## Nästa steg

I den här guiden beskrivs hur du skickar data till [!DNL Algolia] med [!DNL Algolia Event Forwarding Extension]. Mer information om funktioner för vidarebefordran av händelser i [!DNL Adobe Experience Platform] finns i [översikten över vidarebefordran av händelser](../../../ui/event-forwarding/overview.md).

Mer information om hur du felsöker implementeringen med verktyget för felsökning och övervakning av händelsevidarebefordran finns i [Adobe Experience Platform Debugger-översikten](../../../../debugger/home.md) och [Övervaka aktiviteter i händelsevidarebefordran](../../../ui/event-forwarding/monitoring.md).

## Ytterligare resurser

- [[!DNL Algolia] API-dokumentation för insikter](https://www.algolia.com/doc/rest-api/insights/)
- [[!DNL Algolia] Händelsedokumentation](https://www.algolia.com/doc/guides/sending-events/getting-started/)
- [[!DNL Adobe Experience Platform] Dokumentation för vidarebefordran av händelser](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=sv-SE)
- [[!DNL Algolia] Översikt över AI-funktioner](https://www.algolia.com/products/ai-search/)
