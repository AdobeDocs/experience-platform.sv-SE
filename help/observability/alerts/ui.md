---
keywords: Experience Platform;hem;populära ämnen;datumintervall
title: Användargränssnittshandbok för aviseringar
description: Lär dig hur du hanterar aviseringar i användargränssnittet i Experience Platform.
feature: Alerts
exl-id: 4ba3ef2b-7394-405e-979d-0e5e1fe676f3
source-git-commit: ed18ecea98497e0c20d44617436a013bf83b69d2
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Användargränssnittshandbok för aviseringar

Med Adobe Experience Platform användargränssnitt kan du visa historik över mottagna aviseringar baserat på mätvärden som visas av Adobe Experience Platform observability Insights. I användargränssnittet kan du även visa, aktivera, inaktivera och prenumerera på tillgängliga varningsregler.

>[!NOTE]
>
>En introduktion till varningar i Experience Platform finns i [varningsöversikt](./overview.md).

För att komma igång väljer du **[!UICONTROL Alerts]** i den vänstra navigeringen.

![](../images/alerts/ui/workspace.png)

## Hantera varningsregler

The **[!UICONTROL Browse]** På -fliken visas de regler som kan aktivera en varning.

![](../images/alerts/ui/rules.png)

Välj en regel i listan om du vill visa dess beskrivning och dess konfigurationsparametrar i den högra listen, inklusive tröskelvärde och allvarlighetsgrad.

![](../images/alerts/ui/rule-details.png)

Markera ellipsen (**...**) bredvid en regel namn, och i en listruta visas kontroller för att aktivera eller inaktivera varningen (beroende på dess aktuella status) och för att prenumerera eller avbryta prenumerationen på e-postmeddelanden för varningen.

![](../images/alerts/ui/disable-subscribe.png)

## Aktivera e-postaviseringar

Varningsmeddelanden kan skickas direkt till ditt e-postmeddelande.

Välj klockikonen (![klockikon](../images/alerts/ui/bell-icon.png)) som finns i det övre menyfliksområdet till höger för att visa meddelanden och meddelanden. I listrutan som visas väljer du kodikonen (![cog icon](../images/alerts/ui/cog-icon.png)) för att öppna inställningssidan för Experience Cloud.

![](../images/alerts/ui/edit-preferences.png)

The **Profil** visas. Välj **[!UICONTROL Notifications]** i den vänstra navigeringen för att komma åt inställningarna för e-postaviseringar.

![](../images/alerts/ui/profile.png)

Bläddra till **E-post** längst ned på sidan och markera **[!UICONTROL Instant notifications]**

![](../images/alerts/ui/notifications.png)

Alla aviseringar du prenumererar på levereras nu till den e-postadress som är ansluten till ditt Adobe ID-konto.

## Visa aviseringshistorik

The **[!UICONTROL History]** På -fliken visas historiken över mottagna aviseringar för din organisation, inklusive regeln som utlöste aviseringen, utlösande datum och löst datum (om tillämpligt).

![](../images/alerts/ui/history.png)

Välj en avisering och mer information visas i den högra listen, inklusive en kort sammanfattning av händelsen som utlöste aviseringen.

![](../images/alerts/ui/history-details.png)

## Nästa steg

Det här dokumentet innehåller en översikt över hur du visar och hanterar aviseringar i plattformsgränssnittet. Se översikten på [Insikter om observerbarhet](../home.md) för mer information om tjänstens funktioner.
