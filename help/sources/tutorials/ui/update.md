---
keywords: Experience Platform;hem;populära ämnen;uppdatera konton
description: Under vissa omständigheter kan det vara nödvändigt att uppdatera informationen för ett befintligt källkonto. På arbetsytan Källor kan du lägga till, redigera och ta bort information om en befintlig batch- eller direktuppspelningsanslutning, inklusive namn, beskrivning och autentiseringsuppgifter.
solution: Experience Platform
title: Uppdatera kontoinformation för Source Connection i användargränssnittet
type: Tutorial
exl-id: de264bd4-fe3d-4622-9f24-f1612d8334c9
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# Uppdatera kontoinformation i användargränssnittet

Under vissa omständigheter kan det vara nödvändigt att uppdatera informationen för ett befintligt källkonto. På arbetsytan [!UICONTROL Sources] kan du lägga till, redigera och ta bort information om en befintlig batch- eller direktuppspelningsanslutning, inklusive namn, beskrivning och autentiseringsuppgifter.

I den här självstudiekursen beskrivs hur du uppdaterar information och autentiseringsuppgifter för ett befintligt konto från arbetsytan [!UICONTROL Sources].

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Källor](../../home.md): Experience Platform tillåter data att hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av plattformstjänster.
- [Sandlådor](../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

## Uppdatera konton

Logga in på [Experience Platform-gränssnittet](https://platform.adobe.com) och välj sedan **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i [!UICONTROL Sources]. Välj **[!UICONTROL Accounts]** i den övre rubriken om du vill visa befintliga konton.

![katalog](../../images/tutorials/update/catalog.png)

Sidan **[!UICONTROL Accounts]** visas. På den här sidan finns en lista med visningsbara konton, inklusive information om källa, användarnamn, antal dataflöden och datum när de skapades.

Välj filterikonen ![filter](../../images/tutorials/update/filter.png) längst upp till vänster för att öppna sorteringspanelen.

![accounts-list](../../images/tutorials/update/accounts-list.png)

Sorteringspanelen innehåller en lista med alla källor. Du kan välja mer än en källa i listan för att komma åt ett filtrerat urval konton som är associerade med olika källor.

Välj den källa som du vill arbeta med för att visa en lista över dess befintliga konton. När du har identifierat det konto du vill uppdatera markerar du ellipserna (`...`) bredvid kontonamnet.

![accounts-sort](../../images/tutorials/update/accounts-sort.png)

En listruta visas med alternativ för **[!UICONTROL Add data]**, **[!UICONTROL Edit details]** och **[!UICONTROL Delete]**. Välj **[!UICONTROL Edit details]** på menyn för att uppdatera ditt konto.

![uppdatering](../../images/tutorials/update/update.png)

I dialogrutan **[!UICONTROL Edit account details]** kan du uppdatera ett kontos namn, beskrivning och autentiseringsuppgifter. När du har uppdaterat den önskade informationen väljer du **[!UICONTROL Save]**.

![edit-account-details](../../images/tutorials/update/edit-account-details.png)

Efter en stund visas en bekräftelseruta längst ned på skärmen som bekräftar att uppdateringen lyckades.

![update-confirm](../../images/tutorials/update/update-confirmed.png)

## Nästa steg

Genom att följa den här självstudiekursen har du använt arbetsytan [!UICONTROL Sources] för att uppdatera informationen för ett befintligt källkonto.

Anvisningar om hur du utför dessa åtgärder programmatiskt med API:t [!DNL Flow Service] finns i självstudiekursen [Uppdatera anslutningsinformation med API:t för Flow Service ](../../tutorials/api/update.md).
