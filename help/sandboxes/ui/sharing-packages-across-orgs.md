---
title: Dela paket mellan organisationer med hjälp av verktygslådan
description: Lär dig hur du använder sandlådeverktyg i Adobe Experience Platform för att dela paket mellan olika organisationer.
badge: Beta
source-git-commit: 0e280972feb990221272d272aa2a9e3852beb5e8
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---

# Dela paket mellan organisationer med hjälp av sandlådeverktyg

>[!NOTE]
>
>Paket som delas mellan olika organisationer är för närvarande i betaversion och endast tillgängliga för vissa betakunder.

Förbättra konfigurationsnoggrannheten i olika sandlådor och exportera och importera smidigt sandlådekonfigurationer mellan sandlådor i olika organisationer med sandlådeverktygen. Det här dokumentet beskriver hur du använder sandlådeverktyg i Adobe Experience Platform för att dela paket mellan olika organisationer. Det finns två typer av delade paket:

- **Privat paket**

[Privata paket](#private-packages) kan bara delas med organisationer som har godkänt delningsbegäran från källorganisationen via en tillåtelselista som väljer att delta.

- **Offentligt paket**

[Offentliga paket](./sandbox-tooling.md/#export-and-import-an-entire-sandbox) är tillgängliga för import utan ytterligare godkännande. Dessa paket kan delas på en partners webbplats, blogg eller plattform. Paketets nyttolast tillåter att paket kopieras och klistras in från dessa kanaler till målorganisationen.

## Privata paket {#private-packages}

>[!NOTE]
>
>Om du vill initiera och godkänna en delningsbegäran och dela paket mellan organisationer måste du ha rollbaserad behörighet för **package-share**.

Använd sandlådeverktygen för att skapa partnerskap, spåra status för partnerförfrågningar, hantera befintliga partnerskap och dela paket med partnerorganisationer.

### Skapa en förfrågan om organisationskoppling

Navigera till fliken **[!UICONTROL Sandboxes]** **[!UICONTROL Partner orgs]** om du vill skapa en förfrågan om organisationskoppling. Välj sedan **[!UICONTROL Manage partner orgs]**.

![Användargränssnittet för sandlådor, med fliken Partnerorgan och Hantera partnerorganisationer markerade.](../images/ui/sandbox-tooling/private-manage-partner-orgs.png)

I dialogrutan [!UICONTROL Package partner management] anger du organisations-ID i **[!UICONTROL Enter Org ID]** och trycker på Enter (Windows) eller Retur (Mac). Organisations-ID:t visas i avsnittet **[!UICONTROL Selected Org IDs]** nedan. När du har lagt till ID:n väljer du **[!UICONTROL Confirm]**.

>[!TIP]
>
>Du kan ange flera organisations-ID:n samtidigt med kommaseparerade listor eller genom att ange varje organisations-ID följt av enter.

![Dialogrutan för paketpartners med Ange Org ID, Valda Org ID:n och Bekräfta är markerad.](../images/ui/sandbox-tooling/private-enter-org-id.png)

Delningsbegäran har skickats till partnerorganisationen och du återgår till fliken [!UICONTROL Sandboxes] **[!UICONTROL Partner orgs]** som visar **[!UICONTROL Outgoing request]**.

![Fliken Partnerorganisation med utgående begäran markerad.](../images/ui/sandbox-tooling/private-outgoing-request.png)

### Auktorisera en partnerbegäran {#authorize-request}

Navigera till fliken [!UICONTROL Sandboxes] **[!UICONTROL Partner orgs]** om du vill godkänna en förfrågan om organisationskoppling. Välj sedan **[!UICONTROL Incoming request]**.

![Användargränssnittet för sandlådor med fliken Partnerorgan och fliken Inkommande begäran markerad.](../images/ui/sandbox-tooling/private-authorise-partner-org.png)

Aktuell **[!UICONTROL Status]** för begäran är **Väntar** i det här skedet. Om du vill godkänna begäran markerar du ellipsen (`...`) bredvid den valda begäran och väljer sedan **[!UICONTROL Approve]** i listrutan.

![Lista över inkommande begäranden som visar listrutan med Godkänn markerat.](../images/ui/sandbox-tooling/private-approve-partner-org.png)

Dialogrutan **[!UICONTROL Review partner org request]** innehåller information om förfrågan om organisationskoppling. Ange en [!UICONTROL Reason] för godkännande och välj sedan **[!UICONTROL Approve]**.

![Dialogrutan Granska partnerorganisationsförfrågan med orsak och godkännande markerad.](../images/ui/sandbox-tooling/private-approval-partner-org.png)

Du återgår till sidan [!UICONTROL Incoming request] och status för begäran har uppdaterats till **[!UICONTROL Approved]**.

![Listan över inkommande begäranden med Godkänt är markerad.](../images/ui/sandbox-tooling/private-approved-partner-org.png)

Använd det här arbetsflödet/den här processen för att dela paket mellan organisationen och källorganisationen.

### Dela paket med partnerorganisationer {#share-package}

>[!NOTE]
>
>Endast paket med statusen **Publicerad** kan delas.

Om du vill dela ett paket med en godkänd partnerorganisation går du till fliken [!UICONTROL Sandboxes] **[!UICONTROL Packages]**. Markera sedan ellipsen (`...`) bredvid paketet och välj **[!UICONTROL Share package]** i listrutan.

![Lista med paket som visar listrutemenyn med Dela-paketet markerat.](../images/ui/sandbox-tooling/private-share-package.png)

I dialogrutan **[!UICONTROL Share package]** väljer du det paket som ska delas i listrutan **[!UICONTROL Share settings]** och sedan **[!UICONTROL Confirm]**.

>[!TIP]
>
>Det går att välja flera organisationer. De valda organisationerna visas under listrutan [!UICONTROL Share settings].

![Dialogrutan Dela paket med Dela-inställningar och Bekräfta markerat.](../images/ui/sandbox-tooling/private-share-package-confirm.png)

## Nästa steg {#next-steps}

Det här dokumentet visar hur du använder sandlådeverktygen för att dela paket mellan olika organisationer. Mer information finns i [Verktygshandboken för sandlådan](../ui/sandbox-tooling.md).

Mer information om hur du utför olika åtgärder med sandbox-API:t finns i [utvecklarhandboken för sandlådan](../api/getting-started.md). En översikt över sandlådor i Experience Platform på hög nivå finns i [översiktsdokumentationen](../home.md).
