---
title: Push-felsökningsvy
description: Den här vägledningen innehåller information om vyn Push Debug (Push Debug) i Adobe Experience Platform Assurance.
exl-id: a9558ee2-2e80-4b0d-ab45-2020be85e634
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 0%

---

# Push-felsökningsvy

I push-felsökningsvyn i Adobe Experience Platform Assurance kan du validera push-konfigurationen för din app och skicka ett testmeddelande till din enhet.

## Klienter

![Push-klienter](./images/push-debug-view/clients.png)

Klientens listruta innehåller en lista över varje unik klient som har anslutit till denna Assurance-session. En klient är antingen en unik enhet eller en unik programinstallation för en enhet. Om till exempel en Android-enhet och en iOS-enhet har anslutits till sessionen, visas dessa klienter i listrutan Klienter.

När du har installerat om och återanslutit programmet på en enhet visas en annan klient. Om det redan finns en enhet med det namnet lägger den nya listrutan till en siffra 2 till namnet.

Den här vyn är bara aktiverad för en enskild klient, så om du väljer en annan klient ändras informationen på skärmen.

## Validera inställningar

The **[!UICONTROL Validate Setup]** validerar och ger mer information om programmets push-konfiguration. Det finns tre paneler som utför valideringar. De visar en grön bockmarkering om valideringarna lyckas. Om det finns tre gröna bockmarkeringar har appen konfigurerats korrekt för push-meddelanden, skriver push-tokens till användarprofilen och har en associerad appyta konfigurerad.

Om något inte fungerar som väntat visas ett varningsmeddelande med information om hur du åtgärdar problemet:

![Ogiltigt tillstånd](./images/push-debug-view/invalid-state.png)

### Klientinformation

Den här panelen kontrollerar om enheten är korrekt konfigurerad. Detta inkluderar konfiguration av tillägget i användargränssnittet för datainsamling, initiering av tillägget och dess förutsättningar i programmet samt hämtning av push-token från enheten.

Om det är giltigt visas enhetens ECID, push-token, Edge Sandbox-namn och -typ på panelen.

### Profilinformation

När klienten är korrekt konfigurerad kontrollerar den här panelen om enheten skriver till en profil. Den validerar också att push-token i profilen matchar den på enheten.

Om det är giltigt visas enhetens ECID, push-token, programmets program-ID, meddelandeplattformen och om push-token har nekats. Token kan nekas av olika anledningar som att användaren har avinstallerat appen eller att användaren har inaktiverat push-meddelanden för appen.

![Blockerad](./images/push-debug-view/deny-list-blocked.png)

Längst ned på panelen finns en länk som öppnar den här profilen på en ny flik.

### Autentiseringsuppgifter och konfiguration för AppStore

Den här panelen kontrollerar att program-ID:t och meddelandeplattformen som sparades i profilen har en matchande appyta. En appyta är den plats där push-autentiseringsuppgifter för programmet överförs.

Om profilen är giltig visas namnet på appytan, program-ID:t och namnet på meddelandetjänsten.

Längst ned på panelen finns en länk som öppnar den här specifika appytan på en ny flik.

## Skicka testpush

The **[!UICONTROL Send Test Push]** kan användas för att skicka ett testmeddelande till din enhet.

Det finns flera rutor som kan konfigureras för att testa olika push-funktioner för iOS och Android. När konfigurationen är klar väljer du **[!UICONTROL Send Test Push Notification]** för att skicka ditt meddelande.

![Skicka push](./images/push-debug-view/send.png)

### Meddelande

I **[!UICONTROL Message]** kan du ange en rubrik och brödtext för meddelandet. Funktionen för tyst meddelande kan även aktiveras här.

![Meddelanderuta](./images/push-debug-view/message-pane.png)

### Push-mål

The **[!UICONTROL Push Target]** kan du anpassa vilken push-token och appyta som ska användas när push-meddelandet skickas.

Den här informationen tillhandahålls som standard om **[!UICONTROL Validate Setup]** har tre gröna bockmarkeringar. Du kan dock ange en egen push-token och appyta, även om appen inte är helt konfigurerad.

![Målfönster](./images/push-debug-view/target-pane.png)

### Klickbeteende

Från **[!UICONTROL Click Behavior]** kan du välja vilket beteende som ska vara när användaren klickar på ett push-meddelande på enheten. Som standard öppnas programmet, men du kan öppna en länk eller en webbsida.

Om du väljer att använda en depålänk måste apputvecklaren skapa en åt dig.

![Beteendefönster](./images/push-debug-view/click-behavior.png)

### Multimedia

The **[!UICONTROL Rich Media]** I kan du lägga till extra media i ett meddelande, till exempel en bild, en video eller GIF. Apputvecklaren måste lägga till kod i appen för att den här funktionen ska kunna aktiveras.

![Rich Pane](./images/push-debug-view/rich-pane.png)

### Knapparna

The **[!UICONTROL Buttons]** kan du lägga till extra knappar i push-meddelandet. Varje knapp kan öppna programmet, öppna en länk till programmet eller öppna en webbsida.

Apputvecklaren måste lägga till kod i appen för att den här funktionen ska kunna aktiveras.

![Knappfönster](./images/push-debug-view/buttons-pane.png)

### Anpassade data

The **[!UICONTROL Custom Data]** kan du lägga till anpassade data i push-meddelandet. Varje nyckel/värde-par skickas som metadata tillsammans med meddelandet och kan användas av utvecklare för att skapa kraftfulla upplevelser och lägga till ytterligare spårning.

![Anpassat fönster](./images/push-debug-view/custom-pane.png)

## Testresultat

När du har skickat ett meddelande visas **[!UICONTROL Test Results]** -avsnittet tar emot data från push-tjänsterna för meddelandet. Här ser du om meddelandet har skickats till Google/iOS meddelandetjänster:

![Testresultat](./images/push-debug-view/test-results.png)

Om några problem uppstår visas de här:

![Testresultatfel](./images/push-debug-view/test-error.png)

## Avancerat

### Visa meddelandenyttolast

Intill **[!UICONTROL Send Test Push Notification]** är en uppsättning ellipser med en snabbmeny. Härifrån kan du visa meddelandets nyttolast. På så sätt kan du se exakt vilket meddelande som kommer att skickas till fjärrmeddelandetjänsten. Du kan granska den här nyttolasten eller kopiera och klistra in den i ett push-testverktyg.

![Anpassat fönster](./images/push-debug-view/message-payload.png)
