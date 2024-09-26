---
title: Dela paket mellan organisationer med hjälp av verktygslådan
description: Lär dig hur du använder sandlådeverktyg i Adobe Experience Platform för att dela paket mellan olika organisationer.
badge: Beta
source-git-commit: 492f1d9dc08965dba3f1c5b6e1d479ef645afd04
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---

# Dela paket mellan organisationer med hjälp av sandlådeverktyg

>[!NOTE]
>
>Paket som delas mellan olika organisationer är för närvarande i betaversion och endast tillgängliga för vissa betakunder.

Det här dokumentet beskriver hur du använder sandlådeverktyg i Adobe Experience Platform för att dela paket mellan olika organisationer.

Förbättra konfigurationsnoggrannheten i olika sandlådor och exportera och importera smidigt sandlådekonfigurationer mellan sandlådor i olika organisationer med sandlådeverktygen. Det finns två typer av delade paket:

**Privat paket**

Privata paket kan bara delas med organisationer som har godkänt delningsbegäran från källorganisationen via ett deltagande i tillåtelselista.

**Offentligt paket**

Offentliga paket kan importeras utan ytterligare godkännande. Dessa paket kan delas på en partners webbplats, blogg eller plattform. Paketets nyttolast tillåter att paket kopieras och klistras in från dessa kanaler till målorganisationen.

## Privata paket

>[!NOTE]
>
>Om du vill initiera och godkänna en delningsbegäran och dela paket mellan organisationer måste du ha rollbaserad behörighet för **package-share**.

Med sandlådeverktygen kan du skapa partnerskap, följa upp statusen för en partnerskapsförfrågan, hantera befintliga partnerskap och dela paket med partnerorganisationer.

### Skapa en förfrågan om organisationskoppling

Navigera till fliken [!UICONTROL Sandboxes] **[!UICONTROL Partner orgs]** om du vill skapa en förfrågan om organisationskoppling. Välj sedan **[!UICONTROL Manage partner orgs]**.

![Användargränssnittet för sandlådor, med fliken Partnerorgan och Hantera partnerorganisationer markerade.](../images/ui/sandbox-tooling/private-manage-partner-orgs.png)

Ange organisations-ID i **[!UICONTROL Enter Org ID]** i dialogrutan [!UICONTROL Package partner management] och tryck på Retur. Organisations-ID:t visas i avsnittet **[!UICONTROL Selected Org IDs]** nedan. När du har lagt till ID:n väljer du **[!UICONTROL Confirm]**.

>[!TIP]
>
>Du kan ange flera organisations-ID:n samtidigt med kommaseparerade listor eller genom att ange varje organisations-ID följt av enter.

![Dialogrutan för paketpartners med Ange Org ID, Valda Org ID:n och Bekräfta är markerad.](../images/ui/sandbox-tooling/private-enter-org-id.png)

Delningsbegäran har skickats till partnerorganisationen och du återgår till fliken [!UICONTROL Sandboxes] **[!UICONTROL Partner orgs]** som visar **[!UICONTROL Outgoing request]**.

![Fliken Partnerorganisation med utgående begäran markerad.](../images/ui/sandbox-tooling/private-outgoing-request.png)

### Auktorisera en partnerbegäran

Navigera till fliken [!UICONTROL Sandboxes] **[!UICONTROL Partner orgs]** om du vill godkänna en förfrågan om organisationskoppling. Välj sedan **[!UICONTROL Incoming request]**.

![Användargränssnittet för sandlådor med fliken Partnerorgan och fliken Inkommande begäran markerad.](../images/ui/sandbox-tooling/private-authorise-partner-org.png)

Aktuell **[!UICONTROL Status]** för begäran är **Väntande**. Om du vill godkänna begäran markerar du ellipsen (`...`) bredvid den valda begäran och väljer sedan **[!UICONTROL Approve]** i listrutan.

![Lista över inkommande begäranden som visar listrutan med Godkänn markerat.](../images/ui/sandbox-tooling/private-approve-partner-org.png)

Dialogrutan **[!UICONTROL Review partner org request]** innehåller information om förfrågan om organisationskoppling. Ange en [!UICONTROL Reason] för godkännande och välj sedan **[!UICONTROL Approve]**.

![Dialogrutan Granska partnerorganisationsförfrågan med orsak och godkännande markerad.](../images/ui/sandbox-tooling/private-approval-partner-org.png)

Du återgår till sidan [!UICONTROL Incoming request] och status för begäran har uppdaterats till **[!UICONTROL Approved]**.

![Listan över inkommande begäranden med Godkänt är markerad.](../images/ui/sandbox-tooling/private-approved-partner-org.png)

Nu kan du dela paket mellan din organisation och källorganisationen.

### Dela paket med partnerorganisationer

>[!NOTE]
>
>Endast paket med statusen **Publicerad** kan delas.

Om du vill dela ett paket med en godkänd partnerorganisation går du till fliken [!UICONTROL Sandboxes] **[!UICONTROL Packages]**. Markera sedan ellipsen (`...`) bredvid paketet och välj **[!UICONTROL Share package]** i listrutan.

![Lista med paket som visar listrutemenyn med Dela-paketet markerat.](../images/ui/sandbox-tooling/private-share-package.png)

I dialogrutan **[!UICONTROL Share package]** väljer du det paket som ska delas i listrutan **[!UICONTROL Share settings]** och sedan **[!UICONTROL Confirm]**.

![Dialogrutan Dela paket med Dela-inställningar och Bekräfta markerat.](../images/ui/sandbox-tooling/private-share-package-confirm.png)

>[!TIP]
>
>Det går att välja flera organisationer. De valda organisationerna visas under listrutan [!UICONTROL Share settings].

## Nästa steg

Det här dokumentet visar hur du använder sandlådeverktygen för att dela paket mellan olika organisationer. Mer information finns i [Verktygshandboken för sandlådan](../ui/sandbox-tooling.md).

Anvisningar om hur du utför olika åtgärder med sandbox-API:t finns i [utvecklarhandboken för sandlådan](../api/getting-started.md). En översikt över sandlådor i Experience Platform på hög nivå finns i [översiktsdokumentationen](../home.md).
