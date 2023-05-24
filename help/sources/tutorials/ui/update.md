---
keywords: Experience Platform;hem;populära ämnen;uppdatera konton
description: Under vissa omständigheter kan det vara nödvändigt att uppdatera informationen för ett befintligt källkonto. På arbetsytan Källor kan du lägga till, redigera och ta bort information om en befintlig batch- eller direktuppspelningsanslutning, inklusive namn, beskrivning och autentiseringsuppgifter.
solution: Experience Platform
title: Uppdatera kontoinformation för källanslutning i användargränssnittet
type: Tutorial
exl-id: de264bd4-fe3d-4622-9f24-f1612d8334c9
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 1%

---

# Uppdatera kontoinformation i användargränssnittet

Under vissa omständigheter kan det vara nödvändigt att uppdatera informationen för ett befintligt källkonto. The [!UICONTROL Sources] Med arbetsytan kan du lägga till, redigera och ta bort information om en befintlig batch- eller direktuppspelningsanslutning, inklusive namn, beskrivning och autentiseringsuppgifter.

I den här självstudiekursen beskrivs hur du uppdaterar information och autentiseringsuppgifter för ett befintligt konto från [!UICONTROL Sources] arbetsyta.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Källor](../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
- [Sandlådor](../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

## Uppdatera konton

Logga in på [Experience Platform UI](https://platform.adobe.com) och sedan markera **[!UICONTROL Sources]** från vänster navigering för att komma åt [!UICONTROL Sources] arbetsyta. Välj **[!UICONTROL Accounts]** från den övre rubriken för att visa befintliga konton.

![katalog](../../images/tutorials/update/catalog.png)

The **[!UICONTROL Accounts]** visas. På den här sidan finns en lista med visningsbara konton, inklusive information om källa, användarnamn, antal dataflöden och datum när de skapades.

Markera filterikonen ![filter](../../images/tutorials/update/filter.png) längst upp till vänster för att öppna sorteringspanelen.

![account-list](../../images/tutorials/update/accounts-list.png)

Sorteringspanelen innehåller en lista med alla källor. Du kan välja mer än en källa i listan för att komma åt ett filtrerat urval konton som är associerade med olika källor.

Välj den källa som du vill arbeta med för att visa en lista över dess befintliga konton. När du har identifierat det konto du vill uppdatera väljer du ellipserna (`...`) bredvid kontonamnet.

![account-sort](../../images/tutorials/update/accounts-sort.png)

En nedrullningsbar meny visas med alternativ för att **[!UICONTROL Add data]**, **[!UICONTROL Edit details]** och **[!UICONTROL Delete]**. Välj **[!UICONTROL Edit details]** på menyn för att uppdatera ditt konto.

![update](../../images/tutorials/update/update.png)

The **[!UICONTROL Edit account details]** kan du uppdatera ett kontos namn, beskrivning och inloggningsuppgifter. När du har uppdaterat den önskade informationen väljer du **[!UICONTROL Save]**.

![edit-account-details](../../images/tutorials/update/edit-account-details.png)

Efter en stund visas en bekräftelseruta längst ned på skärmen som bekräftar att uppdateringen lyckades.

![uppdateringsbekräftad](../../images/tutorials/update/update-confirmed.png)

## Nästa steg

Genom att följa den här självstudiekursen har du använt [!UICONTROL Sources] för att uppdatera information om ett befintligt källkonto.

För steg om hur du utför dessa åtgärder programmatiskt med [!DNL Flow Service] API, se självstudiekursen om [uppdatera anslutningsinformation med API:t för Flow Service](../../tutorials/api/update.md).
