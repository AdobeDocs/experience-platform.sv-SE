---
title: Adobe Experience Manager Forms Extension - översikt
description: Läs om Adobe Experience Manager Forms-taggtillägget i Adobe Experience Platform.
source-git-commit: f31a1d2e84dee262e04f1db0415ffd76248ecb6c
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Översikt över Adobe Experience Manager Forms-tillägg

Det här dokumentet innehåller en översikt över Adobe Experience Manager Forms-taggtillägget i Adobe Experience Platform.

## Händelser

Följande händelsetyper tillhandahålls av tillägget:

1. **Återgivning**: Startar när användaren återger (öppnar) ett formulär.
1. **Fel**: Utlöses när användaren gör ett valideringsfel i ett formulär.
1. **Hjälp**: Utlöses när användaren klickar på hjälpikonen för ett fält.
1. **Skicka**: Utlösare när formulär skickas.
1. **Fältbesök**: Utlöses när ett fält besöks.
1. **Övergiven**: Startar när användaren stänger fliken eller navigerar till en annan URL.
1. **Spara**: Startar när ett formulär sparas i portalen.

>[!IMPORTANT]
>
>Händelsen Spara är för närvarande inte tillgänglig för formulär som en molntjänst. Anpassade händelser som skickas av regelredigeraren i Adaptive Forms kan fångas in med händelsen Capture custom.

## Dataelement

Tillägget innehåller flera dataelement som kan användas för att skicka egenskaper i analysanrop.

## Komma igång

Följ stegen nedan för att komma igång med tillägget.

1. Installera Adobe Experience Manager Forms-tillägget från tilläggskatalogen. Ingen ytterligare konfiguration krävs efter installationen.
2. Installera och konfigurera [Adobe Analytics-tillägget](../analytics/overview.md#Configure-the-Adobe-Analytics-extension).

## Skapa en regel

En regel som använder tillägget Experience Manager Forms ser ut så här:

![Åtgärdskonfiguration](./images/rule.png)

Följ stegen nedan för att skapa en liknande regel för implementeringen.

### Lägg till en händelse

1. Välj **Adobe Experience Manager Forms** i listrutan Tillägg.
2. Välj händelsen som ska hämtas.

![Åtgärdskonfiguration](./images/AEM-forms-event.png)

### Lägga till en åtgärd

1. Välj&quot;Adobe Analytics&quot; i listrutan för tillägg.
2. Välj &quot;set variable&quot; i listrutan Åtgärdstyp.
3. I konfigurationsvyn väljer du de egenskaper och händelser som ska skickas.
4. Lägg till en sändningsbeacon-åtgärd för att skicka analysanropet med händelser och egenskaper som anges i steg 3
   ![Åtgärdskonfiguration](./images/AEM-forms-sendBeacon.png)
5. Lägg till en åtgärd av typen&quot;clear variable&quot;.

![Åtgärdskonfiguration](./images/AEM-forms-action.png)