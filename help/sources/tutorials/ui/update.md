---
keywords: Experience Platform;home;popular topics;update accounts;
description: null
solution: Experience Platform
title: Uppdatera kontoinformation i användargränssnittet
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 413687a0d9e790ea3f61a858002e9510216d7c34
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 1%

---


# Uppdatera kontoinformation i användargränssnittet

Under vissa omständigheter kan det vara nödvändigt att uppdatera informationen för ett befintligt källkonto. På arbetsytan [!UICONTROL Sources] kan du redigera, lägga till och ta bort information om ett konto, inklusive värden för namn, beskrivning och autentiseringsuppgifter.

I den här självstudiekursen beskrivs hur du uppdaterar information och autentiseringsuppgifter för ett befintligt konto från [!UICONTROL Sources] arbetsytan.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] System](../../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata.
   - [Grundläggande om schemakomposition](../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

## Uppdatera konton

Logga in för att logga in på användargränssnittet [för](https://platform.adobe.com) Experience Platform och välj sedan **[!UICONTROL Sources]** från den vänstra navigeringen för att komma åt [!UICONTROL Sources] arbetsytan. Välj **[!UICONTROL Accounts]** i den övre rubriken om du vill visa befintliga konton.

![katalog](../../images/tutorials/update/catalog.png)

Sidan visas **[!UICONTROL Accounts]** . På den här sidan finns en lista med visningsbara konton, inklusive information om källa, användarnamn, antal dataflöden och datum när de skapades.

Välj ![filterikonfiltret](../../images/tutorials/update/filter.png) längst upp till vänster för att öppna sorteringspanelen.

![account-list](../../images/tutorials/update/accounts-list.png)

Sorteringspanelen innehåller en lista med alla källor. Du kan välja mer än en källa i listan för att komma åt ett filtrerat urval konton som är associerade med olika källor.

Välj den källa som du vill arbeta med för att visa en lista över dess befintliga konton. När du har identifierat det konto du vill uppdatera markerar du ellipserna (`...`) bredvid kontonamnet.

![account-sort](../../images/tutorials/update/accounts-sort.png)

En listruta visas med alternativ för **[!UICONTROL Add data]**, **[!UICONTROL Edit details]** och **[!UICONTROL Delete]**. Välj **[!UICONTROL Edit details]** på menyn för att uppdatera ditt konto.

![uppdatera](../../images/tutorials/update/update.png)

I **[!UICONTROL Edit account details]** dialogrutan kan du uppdatera ett kontos namn, beskrivning och autentiseringsuppgifter. När du har uppdaterat den önskade informationen väljer du **[!UICONTROL Save]**.

![edit-account-details](../../images/tutorials/update/edit-account-details.png)

Efter en stund visas en grön bekräftelseruta längst ned på skärmen som bekräftar att uppdateringen lyckades.

![uppdateringsbekräftad](../../images/tutorials/update/update-confirmed.png)

## Nästa steg

Genom att följa den här självstudiekursen har du använt arbetsytan för att uppdatera kontoinformationen [!UICONTROL Sources] .

Anvisningar om hur du utför dessa åtgärder programmatiskt med API:t finns i självstudiekursen om hur du [!DNL Flow Service] uppdaterar anslutningsinformation med API:t [](../../tutorials/api/update.md)för Flow Service.