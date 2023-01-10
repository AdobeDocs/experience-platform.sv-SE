---
keywords: Experience Platform;hemmabruk;populära ämnen; ta bort konton
description: Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. I den här självstudiekursen beskrivs hur du tar bort konton från arbetsytan Källor.
solution: Experience Platform
title: Ta bort konton för källanslutning i användargränssnittet
type: Tutorial
exl-id: 7cb65d17-d99d-46ff-b28f-7469d0b57d07
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# Ta bort källanslutningskonton

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. I den här självstudiekursen beskrivs hur du tar bort konton från **[!UICONTROL Sources]** arbetsyta.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] System](../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
   - [Grunderna för schemakomposition](../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

## Ta bort konton med användargränssnittet

>[!TIP]
>
>Innan du tar bort källkontot måste du först ta bort alla befintliga dataflöden som är kopplade till källkontot. Om du vill ta bort befintliga dataflöden kan du läsa självstudiekursen om [ta bort källans dataflöden i användargränssnittet](./delete.md).

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och sedan markera **[!UICONTROL Sources]** från det vänstra navigeringsfältet för att komma åt **[!UICONTROL Sources]** arbetsyta. The **[!UICONTROL Catalog]** I visas en mängd olika källor som du kan skapa konton och dataflöden med. Varje källa visar antalet befintliga konton och dataflöden som är kopplade till dem.

Välj **[!UICONTROL Accounts]** för att komma åt **[!UICONTROL Accounts]** sida.

![catalog-accounts](../../images/tutorials/delete-accounts/catalog.png)

En lista över befintliga konton visas. På den här sidan finns en lista med sorterbar information för befintliga konton, t.ex. källa, användarnamn, associerade dataflöden och skapat datum. Välj **trattikon** längst upp till vänster för att sortera.

![dataflows-list](../../images/tutorials/delete-accounts/accounts.png)

Sorteringspanelen visas till vänster på skärmen och innehåller en lista med tillgängliga källor. Du kan välja mer än en källa med sorteringsfunktionen.

Välj den källa som du vill komma åt och leta reda på kontot som du vill ta bort från listan med konton i huvudgränssnittet. I exemplet är den valda källan **[!DNL Azure Blob Storage]** och kontonamnet är **[!UICONTROL blobTestConnector]**. När du väljer flera källor från sorteringspanelen visas dina senast skapade konton först eftersom listan sorteras efter skapad den.

Välj det konto du vill ta bort.

![dataflows-sort](../../images/tutorials/delete-accounts/sort.png)

The **[!UICONTROL Properties]** visas till höger på skärmen och innehåller information om det valda kontot.

Markera ellipserna (`...`) bredvid namnet på det konto du vill ta bort. En popup-panel visas med alternativ för att **[!UICONTROL Add data]**, **[!UICONTROL Edit details]** och **[!UICONTROL Delete]**. Välj **[!UICONTROL Delete]** för att ta bort kontot.

![dataflows-sort](../../images/tutorials/delete-accounts/delete.png)

En slutgiltig bekräftelsedialogruta visas. Välj **[!UICONTROL Delete]** för att slutföra processen.

![delete](../../images/tutorials/delete-accounts/confirm.png)

## Nästa steg

Genom att följa den här självstudiekursen har du använt **[!UICONTROL Sources]** arbetsyta för att ta bort befintliga konton.

För steg om hur du utför dessa åtgärder programmatiskt med [!DNL Flow Service] API, se självstudiekursen om [ta bort anslutningar med API:t för Flow Service](../../tutorials/api/delete.md)
